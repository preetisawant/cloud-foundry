----

copyright:
  years: 2018, 2019
lastupdated: "2019-06-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}

# Monitoring
{: #monitoring}

Monitoring an {{site.data.keyword.cfee_full}} instance and its supported infrastructure is supported by an open-source toolset consisting of Prometheus and Grafana.  The solution enables you to analyze, visualize and manage alerts for metrics in the Cloud Foundry environment.  There are three web consoles from which monitoring takes place: A Grafana console, a Prometheus console, and a Prometheus Alert Manager console.

Starting with CFEE v2.2.0, monitoring tools are not enabled by default when an environment is created.  Administrators can enable monitoring after the environment is created.  In the CFEE user interface, go to the _Monitoring_ page in the left navigation pane and click **Enable**. Enabling monitoring automatically provisions additional Kubernetes worker nodes (in the same IBM Cloud account) and installs the monitoring tools into those worker nodes.

**Note:** Access to the monitoring capability in an {{site.data.keyword.cfee_full}} instance requires an _Administrator_ or _Editor_ role in the CFEE (in additon to _Viewer_ role in the resource group under which the CFEE is grouped).  The default name of the Kubernetes cluster supporting a CFEE instance is _`<CFEEname>`-cluster_.

## Prometheus
{: #prometheus}

Prometheus is an open-source systems monitoring and alerting toolkit. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community.
It is a standalone open source project and maintained independently of any company. To emphasize this, and to clarify the project's governance structure, Prometheus joined the Cloud Native Computing Foundation in 2016 as the second hosted project, after Kubernetes. See the [Prometheus documentation](https://prometheus.io/docs/introduction/overview/) for more information.

The Prometheus ecosystem consists of multiple components, many of which are optional:

* The main Prometheus server which scrapes and stores time series data.</li>
* [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) to handle alerts.</li>
* Various special-purpose exporters like node exporter, blackbox exporter, etc.</li>
* A push gateway for supporting short-lived jobs.</li>

Prometheus gatheres metrics from instrumented jobs, either directly or via an intermediary push gateway for short-lived jobs. It stores all gathered samples locally and runs rules over this data to either aggregate and record new time series from existing data, or to generate alerts.

### Customizing the Prometheus Alertmanager configuration (optional)

Alertmanager has a default configuration file that defines the policies for handling, grouping, and notification routing of Alertmanager alerts. You can download the default configuration file and upload a custom configuration in the **Configuration** tab of the _Monitoring_ page.

You can refer to the [Alertmanager configuration](https://prometheus.io/docs/alerting/configuration/) documentation for details on how to configure notification for email, Slack, PagerDuty, etc.

<!--
### Federation of the Prometheus server

Prometheus provides a concept of
[federation](https://prometheus.io/docs/prometheus/latest/federation/)
which allows one Prometheus server to scrape metrics data from an other Prometheus server.
This concept allows you to integreate the Prometheus monitoring server in your
{{site.data.keyword.cfee_full}} instance with a Prometheus server you operate by yourself.

By default, the `/federate` endpoint of the built-in server is only reachable
withih the cluster. Any access from the extern using the hyperlinks on the
_Monitoring_ page of the CFEE user interface will result in a
`404 Unauthorized` response. To make it accessible from the outside, a simple
solution is to create a separate Kubernetes Service and an Ingress object.

In order to do so, you need to have access to your Kubernetes cluster (see
steps 1. to 4. in
[Access the Kubernetes Cluster](/docs/cloud-foundry?topic=cloud-foundry-monitoring#access-the-kubernetes-cluster)).
On your workstation, create a configuration file for the Service and the Ingress
object. Take the following as an example how to do that.

For the Service object, you can create a file `service.yaml` with content
similar to the following:
```
apiVersion: v1
kind: Service
metadata:
  annotations:
  labels:
    app: prometheus
    component: server
  name: prometheus-federation
  namespace: monitoring
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 9090
  selector:
    app: prometheus
    component: server
  type: ClusterIP
status:
  loadBalancer: {}
```
{: screen}

And for the Ingress object, use a file `ingress.yaml`, like the following.
You will need to adopt your CFEE instance's
domainname in the appropriate place:
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  labels:
    app: prometheus-federation
  name: prometheus-federation
  namespace: monitoringNote: These files provide a very simple, basic example, only. For example, you

spec:
  rules:
  - host: federation.<domainname>
    http:
      paths:
      - backend:
          serviceName: prometheus-federation
          servicePort: 80
        path: /federate
```
{: screen}
Once you are satisfied with the configurations, you can have Kubernetes create
respective object by executing:
```
$ kubectl apply -f service.yaml
```
{: pre}
```
$ kubectl apply -f ingress.yaml
```
{: pre}

**Note:** These files provide a very simple, basic example, only. For example, you
may want to add TLS configuration to the Ingress to support the `https` scheme.
Please refer to the [Kubernetes documentation](https://kubernetes.io/docs/home/)
for detailed information on Kubernetes objects, and how to manage them.
-->
## Grafana
{: #grafana}

Grafana is an open-source analytics platform for all metrics collected by Prometheus. The deployed Grafana version on your cluster is already configured to use the underlying Prometheus database. It also contains some valuable Grafana dashboards.  See the [Grafana documentation](http://docs.grafana.org/guides/getting_started/) for more information.

Data from individual panels can be exported from Grafana in CSV format. See the [Grafana Export Panel Data documentation](https://grafana.com/docs/reference/sharing/#export-panel-data) for more information.

## Accessing the Kubernetes cluster: Port forwarding

The Prometheus and Grafana components comprising the monitoring solution are pre-installed in the Kubernetes infrastructure supporting the CFEE instance.  Accessing the monitoring tools requires to **forward the ports** of the Prometheus, Prometheus AlertManager, and Grafana serverers.  This is done through the Kubernetes CLI.
The following guides you through the steps for installing the required CLI's, forwarding the server ports, and launching the consoles.

**Note:** The following instrutions are also available in the {{site.data.keyword.cfee_full}} user interface.  Open the CFEE instance user interface, click **Monitoring** in the left navigation pane, and go to the **Access** tab to see the instructions displayed.

1. Prequistes

* Check your [Access Policies](https://cloud.ibm.com/iam/#/users) to ensure that you have at least a Viewer role on the Kubernetes cluster supporting the environment.
*  Install the [IBM Cloud CLI](https://cloud.ibm.com/docs/cli/reference/ibmcloud/download_cli.html#install_use).
*  Install the [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  If you have an existing Kubernetes CLI, we recommend that you install the latest version.
*  Install the container service plug-in:
```
    ibmcloud plugin install container-service
```

2. Log into your IBM Cloud account:

  ```
  ibmcloud login -a https://cloud.ibm.com
  ```
  {: pre}

  If you have a federated ID, use __ibmcloud login -sso__ to log into the IBM Cloud CLI.

3. Target the IBM Cloud Container Service region in which you want to work (e.g., us-south):

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}

4. Set the context of the cluster in your cli:

  a. Get the command to set the environment variable and download the Kubernetes configuraton files:

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}

  b. Set the KUBECONFIG environment variable. Copy the output from the previous command and paste it in your terminal. The command output should look similar to the following:
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

5. Forward server ports. Set up port-forwarding in the Kubernetes cluster for the pods running Prometheus, AlertManager and Grafana. This will enable you to host the monitoring metrics by proxy on your local machine (localhost):

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000 &''
  ```
  {: pre}


## Launching the monitoring consoles
{: #launching-consoles}

You can launch the **Grafana**, **Prometheus** and **Prometheus Alertmanager** consoles, go to the _Monitoring_ page of the CFEE user interface and click on the corresponding hyperlink.  Each console is opened in a separate browser tab.

### Grafana dashboards

There is a default set of Grafana dashboards included in the CFEE instance. Those default dashboards are interactive and give you a view of the infrastructure used to host your CFEE instance. (Kubernetes cluster). Once you launch the Grafana console, click the **Home** button at the top of the Grafana console to select one of the pre-deployed dashboards (see list below), which will graph the corresponding metrics:

   For CFEE v2.1.0 or earlier there is a default `admin` user in Grafana, with the default password set to `admin`. We recommend to login with Userd/Password `admin/admin`, and change them to new credentials.  For CFEE v2.2.0 or later users are authenticated automatically with their IBM ID credentials.

   The following default dashboards are provided with the CFEE instance and are available from the _Home_ dropdown.

    Cloud Foundry dashboards:
   - _CF: Cells Capacity_
        - Shows the general status of the Cloud Foundry cells where the Cloud Foundry applications are deployed.
   - _CF: Diego Cell dashboard_
        - Shows the status of the Cloud Foundry cells and Diego components.
   - _CF: Router_
        - Shows the Cloud Foundry router status running on your CFEE environment.

   Dashboards for the Kubernetes infrastructure supporting your CFEE environment:
   - _Deployment_
        - Shows the status of your Kubernetes deployments.
   - _Kubernetes Cluster Health_
        - Shows the health of the Kubernetes cluster.
   - _Kubernetes Cluster Status_
        - Shows the status of the Kubernetes cluster.
   - _Kubernetes Resource Requests_
        - Shows the used CPU, memory and other parameters of the Kubernetes cluster.
   - _Pods_
        - Shows details for each pod running on the Kubernetes cluster.
   - _Replica Set_
        - Shows the status of the Kubernetes replica sets.       
   - _Worker Nodes_
        - Shows details for each worker node of the Kubernetes cluster.
   - _Worker Nodes Overview_
        - Shows the CPU and memory usage of the kubernetes infrastructure, along with its network traffic.
