---

copyright:
  years: 2019
lastupdated: "2019-09-01"
---

# CFEE on IBM Virtual Private Cloud (VPC)
{: #cfee-on-vpc}

You can provision an IBM Cloud Foundry Enterprise Environment into an existing IBM Virtual Private Cloud (VPC).

VPC allows you to create your own space in the IBM Cloud, to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud. IBM Cloud Foundry Enterprise Environment fully utilizes this capability, and allows you to host your applications with the highest level of network security and isolation possible. Full information about VPC, how this technology works, and how it is enabled, can be found in the [VPC documentation](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-about)

Follow the instructions [here to create your VPC](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-getting-started).

## Prerequisites
{: #prereq}
Before provisioning CFEE into your VPC, ensure that you have the following:
1. You must have the same permissions to [provision on classic infrastructure](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions) (excluding permissions for VLANS or datacenters).
1. The IKS resource group and region must be associated with a user that has Kubernetes Administrator and VPC viewer access. The access can be reset using the command `ibmcloud ks api-key reset`. [See documentation here.](https://cloud.ibm.com/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#api_key-commands)
1. To provision a CFEE in an isolated environment you must enable the [private service endpoints](https://cloud.ibm.com/docs/resources?topic=resources-private-network-endpoints#cs_cli_install_steps).

## Limitations
{: #limitations}
Before provisioning a CFEE into your VPC, please keep in mind:
1. The VPC limitations listed [here](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-known-limitations).
1. You must have sufficient [quota available for your VPC](https://cloud.ibm.com/docs/infrastructure/vpc-on-classic?topic=vpc-on-classic-quotas).
1. You must have sufficient [load balancer resource quotas available for your VPC](https://cloud.ibm.com/docs/infrastructure/vpc-on-classic?topic=vpc-on-classic-quotas#load-balancer-quotas).
1. If the subnets do not have a public gateway attached, you must configure your VPC in a way that [allows outbound access to certain ip addresses for your CFEE.](cloud-foundry-isolated-network)
1. You must have enough unallocated IPs in a VPC subnet before you provision a CFEE. The minimum number required is the number of cells per zone plus control plane nodes plus 10. E.g., **2 cells per zone + 2 control plane nodes + 10 = 14 IPs**.
   
   **Note:** A VPC subnet will typically have a small number of IPs allocated prior to any use. Check the available number of IPs in the subnet to be sure there are more than the number of IPs required for a VPC CFEE.

1. If a worker node deployment fails due to an IBM Kubernetes Service issue, you must redeploy the CFEE instance. This cannot be fixed without redeploying because CFEE instances are dependant on the IBM Kubernetes Service. 

## Creating a VPC CFEE
{: #creating-vpc-cfee}
1. Create your VPC as [detailed here](https://cloud.ibm.com/docs/vpc-on-classic?topic=vpc-on-classic-getting-started).
1. Go to the CFEE [creation page](https://dev.console.cloud.ibm.com/cfadmin/create).
1. Select VPC environment.
1. Choose your recently created VPC from the dropdown.
1. Choose the Worker Zones and Subnets you plan to use.
1. Continue to follow the instructions for creating a regular CFEE [here](cloud-foundry-create-environment).

## Limitations
{: #limitations}
There are several limitations detailed in the [release notes for v5.0.0](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-what-s-new-in-ibm-cloud-foundry-enterprise-environment#v500)

## Managing VPC CFEE Worker Nodes
{: #worker-nodes}
In the VPC Kubernetes cluster hosting your CFEE, managing the worker nodes is done differently from classic CFEE. [See VPC cluster limitations](https://cloud.ibm.com/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#vpc_ks_limits). In the event that one of the worker nodes goes down, you must replace the worker node:
1. Log into the IBM Cloud CLI.
1. Find the cluster associated with your CFEE. The name of the cluster is `<CFEE name>-cluster`. 

        ibmcloud ks clusters

1. Identify the worker node that is failing:

        ibmcloud ks workers --cluster <cluster name>

1. Execute a worker replace on the failing worker node:

        ibmcloud ks worker replace --cluster <cluster name> --worker <worker IP>

    Please note the worker ID (attribute "id"). You will need provide this to CFEE support so they can accurately update your cluster metadata in the management plane

When the worker node is finished provisioning, the pods running the Cloud Foundry components will use the new worker node.

        ibmcloud ks cluster config <cluster name>
        kubectl -n cf get pods


## Disabling Kubernetes public-service-endpoint on a VPC CFEE

1. Log into the IBM Cloud CLI.
2. Find the cluster associated with your VPC CFEE. The format of the name of the cluster is `<CFEE name>-cluster`. 

        ibmcloud ks clusters

3. Disable kubernetes public-service-endpoint:
 
          ibmcloud ks cluster feature disable public-service-endpoint --cluster <CFEE name>-cluster

4. Identify all worker node in the CFEE:

        ibmcloud ks workers --cluster <cluster name>

5. Execute a worker replace on the all worker nodes:

        ibmcloud ks worker replace --cluster <cluster name> --worker <worker IP>

    Please note the worker ID (attribute "id") for each worker.

6. After all workers have been replaced. You will need to provide the worker IDs to CFEE support so they can accurately update your cluster metadata in the management plane.
  
    When the worker nodes are finished provisioning, the pods running the Cloud Foundry components will use the new worker nodes.

        ibmcloud ks cluster config <cluster name>
        kubectl -n cf get pods
        
    If you have any issues with your CFEE instance, contact CFEE support. 
