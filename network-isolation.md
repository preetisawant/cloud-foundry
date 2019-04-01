---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Operating in an isolated network
{: #isolated-network}


Starting with version 2.2.0, {{site.data.keyword.cfee_full}} (CFEE) instances can operate inside an isolated networks that protects and secures the environment from external threats. You create an isolated network through private VLANs and a set of control mechanisms to route, filter, and protect traffic into and out of the resources inside the network perimeter. Isolated networks are setup using technologies like Virtual Router Appliances ([VRAs](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)). 

**Note:** CFEE instances operating in an isolated network required that the CFEE kubernetes cluster be update to v1.13. Updating the Kubernetes cluster v1.13 is independent of the CFEE update.

A CFEE instance is provisioned into a cluster from the IBM Kubernetes Service. The CFEE's Cloud Foundry cells (where applications are hosted) are provisioned into the Cluster's worker nodes. This means that access to the CFEE cells and applications implies accessing the cluster worker nodes. 

The worker nodes contain Application Loads Balancers (ALBs) that distribute the applications' workload among the worker nodes. CFEE v2.2.0 enables the Kubernetes ALBs in both, private and public networks.  This means that CFEE v2.2.0 can be accessed from both, public or private networks.

## CFEE management in an isolated network
{: #control-plan-access}

In v2.2.0 the CFEE management plane (the sub-system used for provisioning, updates and other lifecycle activities) does not rely on the ALBs or worker nodes directly to manage a CFEE instance. Instead, the CFEE management plane uses the _VPN connection between the Kubernetes master and worker nodes_ to access the CFEE instance and its resources. This enables the management plane to control the CFEE instance.

After you create your CFEE instance, the management plane creates an [IAM service ID](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) in your account that it gives to the IKS master node. The CFEE management plane uses this service ID to access the CFEE host workers through the master node and its VPN access for subsequent provisioning and management operations, including deploying the main Cloud Foundry component of CFEE.

The diagram below depicts a CFEE installed behind a VRA network perimeter.   
![Network isolation](img/CFEE_IsolatedNetwork.png  "Diagram describing how a CFEE works in an isolated network.")

## Controlling access to CFEE instances in an isolated network
{: #oppening-access-points}

CF apps running in a CFEE instance frequently need to reach outside the isolated network for various reasons. For example, an application may need to access a public RESTful service, or download packages from public registries, like a Docker image, NPM packages, Python modules, etc. Hence, you need to configure your firewall rules to enable your specific network access needs.

You can control inbound/outbound connectivity to/from an isolated network by configuring the rules for specific protocols, sources or target endpoints. You can create and configure these by using control mechanisms in the specific technology used to setup the network perimeter (e.g. VRA). However, the simplest way to control this is by creating [Calico network policies](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy) that define network rules specifically for the host Kubernetes cluster. Please see [creating and applying Calico network policies](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies) for step-by-step guidance.

Network access rules related to a network isolated CFEE can be of the following types:

* **Inbound traffic access:** When a Kubernetes cluster is installed, it automatically sets and configures a [default Calico policy](https://console.bluemix.net/docs/containers/cs_network_policy.html#default_policy) that allows management access to the worker nodes (hosting your CFEE instance in this case).

<br>
**Default** Calico rules for accessing the **Kubernetes cluster** worker nodes:

    ```
    allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
    allow-vrrp                      1600    ibm.role == 'worker_public'                        
    allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
    allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
    allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
    ```
    {: codeblock}
<br />
If you are using an alternative network perimeter implementation, you'll need to setup the same policies using the corresponding control mechanisms.
  
* **Outbound traffic access:** CFEE relies on a number of services in IBM Cloud with public endpoints. Your isolated network needs to allow your CFEE instance to reach these endpoints. These are listed below along with their respective Calico policies.

| Rule   | Description | Endpoint |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | Enable the CFEE's Kubernetes cluster to access the CFEE management plane | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Enable Docker registries access | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | Access the CFEE Kubernetes cluster management plane | [Learn more](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | Enable outbound and routing to the CFEE's Kubernetes cluster portable IP addresses | You can find your cluster portable addresses using: `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | Access the CFEE's Compose for PostgreSQL database | You can find the endpoint from the Compose instace `<cfee-name>-postgress`'s dashboard page and in the CFEE's _Private Access_ page. |
| cfee-egress-allow-rc | Access the IBM Cloud platform to enable service syndication | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | Access the IBM Cloud Container Registry | [Learn more](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (optional) Allow outgoing network traffic from the CFEE worker nodes to IBM Cloud Monitoring and IBM Cloud Log Analysis services | [Learn more](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | Allow outgoing network traffic from the CFEE worker nodes to the helm image retistry| [Learn more](https://github.ibm.com/Bluemix/cfee-network-isolation/blob/master/outbound/cfee-egress-allow-helm-tiller.md) |


<br>  
The final network security rule (the most **important** one) is the one that denies all access to network traffic that don't match the previous policies.
<br>
Calico rule for **denying all outbound access** (`cfee-egress-deny-all`):

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-egress-deny-all
spec:
  applyOnForward: true
  egress:
  - action: Deny
    destination: {}
    source: {}
  order: 3000
  selector: ibm.role in { 'worker_public' }
  types:
- Egress
```
{: codeblock}

<br>
Calico rule for **denying all inbound access** (`cfee-ingress-deny-all')
`):

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-ingress-deny-all
spec:
  applyOnForward: true
  ingress:
  - action: Deny
    destination: {}
    source: {}
  order: 4000
  selector: ibm.role=='worker_public'
  types:
- Ingress
```
{: codeblock}
<br>  
One complexity with outbound access from isolated networks is that some of the target endpoints are behind a _public edge_ network, like Cloudflare or Akamai. In this case you may need to potentially allow access to hundreds of IP addresses that change often. You can optionally avoid this situation by **allowing all outbound access** by using the following Calico rule (`cfee-egress-allow-all`):

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
   name: cfee-egress-allow-http
    spec:
   egress:
   - action: Allow
     destination:
       ports:
       - 443
       - 80
     protocol: TCP
     source: {}
   order: 1611
   selector: ibm.role in { 'worker_public' }
   applyOnForward: true
   types:
   - Egress
```
{: codeblock}
  
In the above example, all HTTP and HTTPS calls (all TCP traffic on ports 443 and 80) coming from the CFEE cluster worker nodes (“worker_public”) are allowed outbound (“egress”) access to the public network.

# Private access from the management control plane
{: #priate-access}

Management of a CFEE instance in an isolated network requires private access to the CFEE instance by the CFEE management control plane. Private access to the CFEE instance by the CFEE management control plane is enabled by default. 

Users with an _Administration_ role can disable private access by the CFEE management control plane. Note that disabling private access will disable the CFEE control plane from retrieving data and from managing the CFEE instance (neither through the user interface, the CLI nor the API). CFEE administrators can disable private access in the **Private Access** page (visible only to administrators), located in the CFEE user interface. Once in the page press **Disable**.  

Access to the isolated network takes place through an API key.  An API key is provided by default. A CFEE administrator can replace the default API key with a custom key. Enabling private access after it has been disable requires an API key that needs to be generated in the *_IBM Cloud API keys_* (In the IBM Cloud user interface header, go to _Manage > Acess (IAM) > IBM Cloud API keys_ ).

