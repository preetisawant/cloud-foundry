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

# Creating an environment
{: #create-environment}

## Prerequisites
* Ensure that you are in the {{site.data.keyword.Bluemix_notm}} account where you want to create the environment.
* Ensure that you have the correct [permissions](https://https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html) before creating instances of the {{site.data.keyword.cfee_full_notm}}. 
* [Prepare your IBM Cloud account](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html) to ensure that it can create the infrastructure resources necessary for a CFEE instance (CFEE instances are deployed into Kubernetes worker nodes from the Kubernetes Service).  

## Creating a CFEE instance
1.  Open the {{site.data.keyword.Bluemix_notm}} [catalog](https://cloud.ibm.com/catalog).

2.  Locate the {{site.data.keyword.cfee_full_notm}} service in the catalog and click it to open the overview page for the service.  That first page provides an overview of the main features of the service. Click **Continue**.

3.  Configure the CFEE instance to be created:
    * Select a plan. See the [Eirini technical preview](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) section for a description of the limitations of tis plan.
    * Enter a **Name** for the CFEE instance.
    * Select a **Resource group** under which the environment is grouped. Only those resource groups to which you have access in the current IBM Cloud account will be listed in the _Resourouce groups_ dropdown, which means that you need to have permission to access at least one resource group in the account to be able to create an CFEE.
    * Select the **Geography** and **Location** where the service instance is to be provisioned. See the list of [available provisioning locations and data centers](https://https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") by geography for CFEE and supporting services. 

4. CFEE instances are provisioned on a Kubernetes cluster. Cloud Foundry cells are provisoned within worker zones in the Kuberentes cluster. You can configure the location, hardware and encryption of the cluster:
    * Select the hardware isolation for the Kubernetes cluster:   
      * _Virtual-shared_: Infrastructure resources in the cluster, such as the hypervisor and physical hardware, are distributed between you and other IBM customers, but each worker node is single-tenant to you.
      * _Virtual-dedicated_: The worker nodes in the cluster are hosted on infrastructure that is devoted to your account.
    * Data in the cluster are encrypted by default. You have the option of turning off _Encrypt local disk_.
    * Select the **Geography** and **Region** where the Kubernetes cluster willl be provisioned.
    * Select the **Zones** where the Kubernetes worker nodes will be deployed. You have the option of provision the worker nodes in the same zone (**Single Zone**) or in multiple zones (**Multizone**).  
    Available VLANs are automatically retrieved for the selected zones. If no available VLANs are available, they will be created automatically.
    
    **Note: Provisioning on an isolated network:** You can target VLANs in an isolated network. When the CFEE instance is created in an isolated network, the policies in the isolated network (e.g., calico policies or VRA rules) must allow ALL outbound access from the CFEE instance for the CFEE to be provisioned successfully. Once the CFEE is created, the outbound access restrictions can be reinstated, except for outbound access to certain services and micro-services in the IBM Cloud.  See the [Operating in an isolated network](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network) documentation for more information.
    
    Once the CFEE is crated, the Kubernetes cluster into which the environment is provisioned will appear (like any other resource in your IBM Cloud account) in the {{site.data.keyword.Bluemix_notm}} [dashboard](https://https://cloud.ibm.com/catalog/dashboard/apps/). For more information, see [Kubernetes Service documentation](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov).

5.  Configure the capacity of the CFEE:
    * Select the **Number of cells** for the CFEE. These are the application cells that will host the applications deployed into the CFEE.  
    * Select the **Node size**, which determines the capacity of the Cloud Foundry cells (CPU and memory) .
    
    In addition to the application cells that you specify above, additional _Control Plane cells_ are created and reserved for the operation and control of the Cloud Foundry platform in your CFEE. 

    **Note:** We recommend that VLAN spanning be enabled if the worker nodes in the Kubernetes cluster are provisioned on different subnets.  Worker nodes on different subnets may prevent connectivity among them if VLAN spanning is disabled.  See [VLAN spanning](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning) documentation for more information.

6.  In the **Compose for PostgreSQL** fields, select one of the public organizations, then select one of the spaces available in that organization. The instance of the Compose for PostgreSQL instance will be provisioned in the selected space. The Compose for PostgreSQL service is a required dependency of the CFEE service.

    **Note:** Under _Compose for PostgreSQL_ only organizations in the location where you intend to provision the CFEE instance (step 4 above) and to which you have access, are available for selection.  Within a specific organization, only spaces to which you have _developer_ access are available for selection. 

7.  The **Order Summary** in the right-hand side of the page reflects the cost of the CFEE instance and the ancillary services along with the estimated monthly total.

8.  Click **Create**, which opens the environment dashboard and indicates the creation progress and status.

**Note:** Once the creation process has started, a table row for the CFEE is shown in the {{site.data.keyword.Bluemix_notm}} dashboard, in the _Resource List_, and in the [Cloud Foundry Environments dashboard](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments).  The status in the table row indicates when creation is completed.

The automated process that creates the environment deploys the infrastructure into a Kubernetes cluster and configures it to make it ready for use. The process takes 90 - 120 minutes.

Once CFEE is created you will receive multiple emails confirming the provisioning of the CFEE and supporting services, as well as emails notifying you of the status of the corresponding orders.

When you create a CFEE instance, there are three additional supporting service instances created in the same IBM Cloud account. Those supporting service instances are named after the CFEE instance name. Hence, creating a CFEE results in a total of four service instances created in the IBM Cloud account:
* CFEE instance ("_cfeename_").
* Kubernetes cluster ("_cfeename_-cluster"). The cluster provides the infrastructure into which the CFEE instance is provisioned.
* Cloud Object Storage instance ("_cfeename_-cos"). The instance is used to store data generated during the creation of the CFEE application containers (e.g. uploaded application packages, buildpacks, and compiled executables).
* Compose for PosgreSQL instance ("_cfeename_-postgres"). The instance is used to store Cloud Foundry data on the CFEE instance (e.g., auditing application deployment, start and stop events; keeping records of CFEE user membership, organizations, spaces, applications and service connections). 

## The Eirini technical preview plan
{: #eirini}

 The Eirini Technical Preview plan allows you to explore a CFEE using native Kubernetes as the container scheduler (instead of Diego). The Kubernetes scheduler is used in the CFEE to deploy and run apps in the Cloud Foundry application runtime, add users, create an organization and spaces, deploy apps, and bind those apps to services. See the [Eirini project](https://www.cloudfoundry.org/project-eirini/) documentation for more information about the Eirini incubator project from the Cloud Foundry Foundation.
 The following limitations apply to CFEE instances created from the Eirini Technical preview plan:
 
* Kubernetes with `containerd` is not supported. Only Kuberetes versions are supported that use Docker instead of `containerd`. The latest version of the IBM Container Service (IKS) that supports Docker is v1.10.
* Cloud Foundry SSH is not supported.
* `cf push` of Docker images is not supported.
* Kubernetes native Eirini staging is not supported. CFEE instances created from the Eirini technical preview plan use Eirini for running apps, but not for staging them. Diego cells are still used for staging apps.
* Restart of specific app instances (`cf restart-app-instance`) is not supported.

 
