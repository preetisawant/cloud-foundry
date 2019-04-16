---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# What's New in IBM Cloud Foundry Enterprise Environment

This document describes what's new in each version released up to this date of the {{site.data.keyword.cfee_full_notm}} service.

## Version 2.2.2
{: #v222}

_Release Date:_ 2019-04-16

The following changes were released in version 2.2.2 of the {{site.data.keyword.cfee_full_notm}} service (CFEE):

* Resolved v2.2.1 update problems. Version 2.2.2 di facto replaces version 2.2.1. 
* Resolved problem affecting specific use cases of `cf login`.
* Resolved minor problem with deployment of monitoring tools.
     
To update your CFEE's version, go to the _Updates and Scaling_ page in the CFEE's user interface. 

**Note** that this version does not pre-require version 2.2.0. You can update directly to version 2.2.2. However, if you bypass version 2.2.0, we still recommend that you update the CFEE Kubernetes cluster to v1.13 before the CFEE update (recommended also before a v2.2.0 update). 

## Version 2.2.1
{: #v221}

_Release Date:_ 2019-04-04

The following changes were released in version 2.2.1 of the {{site.data.keyword.cfee_full_notm}} service (CFEE):

* Resolved a number of minor problems interfering with routine operations of a CFEE:
     * Misattributed error messages. 
     * Incorrect buildpack upload timeout.
     * Unintended events on doble click delete icon.
     * Incorrect cluster version display.
     * Incorrect getting started page display.

To update your CFEE's version, go to the _Updates and Scaling_ page in the CFEE's user interface. 

**Note** that this version does not pre-require version 2.2.0. You can update directly to version 2.2.1. However, if you bypass version 2.2.0, we still recommend that you update the CFEE Kubernetes cluster to v1.13 before the CFEE update (recommended also before a v2.2.0 update).
 

## Version 2.2.0
{: #v220}

_Release Date:_ 2019-04-01

CFEE v2.2.0 includes the following versions of its constituent components:
* Cloud Foundry: v2.7.1.15.5
* Cloud Foundry API: v2.115.0
* CFEE Buildpacks: v0.1.5
* IBM Kubernetes service: No version update provided.  **Important:** We recomment that you update the CFEE Kubernetes cluster to v1.13 before updating to CFEE v2.2.0 (required when the CFEE instance operates in an isolated network).

The following changes were released in version 2.2.0 of the {{site.data.keyword.cfee_full_notm}} service (CFEE). To update your CFEE's version, go to the **Updates and Scaling** page in the CFEE's user interface and click **Update**:

* New option to **create** a CFEE instance in a **multi-zone** Kubernetes cluster. CFEE instances created on a multi-zone cluster distribute application instances, not only across worker nodes within a data center, but also across data centers, making your applications more resilient against infrastructure outages. Furthermore, multi-zone CFEEs can be **scaled** by  adding additional cells, or by removing existing ones from the current zones.  Note that you cannot add or remove zones from a multi-zone CFEE once the CFEE instance is created.
* CFEE v2.2.0 instances can now [operate within an **isolated network**](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). Note that if the CFEE instance is deployed in VLANs from an isolated network, some endpoints (IP addresses) [must be identified and routed properly](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points) for the CFEE instance to become operational. A CFEE instance requires a Kubernetes cluster v1.13 to operate in an isolated network.
* New capability to bind applications (deployed into a CFEE space) to service instances through the internal IBM network. The capability allows services supporting the IBM Cloud Service Endpoint to be consumed without accessing the public internet.
* **Monitoring** tools:
    * The monitoring tools (Prometheus, Grafana and Alertmanager) are no longer provisioned by default when you create a CFEE.  In CFEE v2.2.0 monitoring tools are provisioned only when explictely enabled by CFEE administrators.  Furthermore, when enabled, the monitoring tools are no longer provisioned into the CFEE control plane worker nodes. They are provisioned on their own worker nodes, outside the control plane. To enable and provision monitoring tools, go to the CFEE _Monitoring_ page (in the left-nav pane) and click **Enable monitoring**. 
    * When you update an existing CFEE to version 2.2.0, the existing monitoring tools are deleted from the control plane. Any existing custom configuration of the monitoring tools will be lost. 
    *  New capability to replace the default [Alertmanager configuration](https://prometheus.io/docs/alerting/configuration/) with a custom configuration that allows you to customize the handling, grouping, and notification routing of alerts. In the _Monitoring_ page you will be able to _Download_ the default configuration file, and _Upload_ a configuration file from your local file system.  See for an [example](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml) of a configuration file.
* New capability to tag CFEE instances in the {{site.data.keyword.Bluemix_notm}} [_Resource List_](https://cloud.ibm.com/resources) and in the CFEE user interface.
* General improvements to the user experience of the {{site.data.keyword.Bluemix_notm}} [**Cloud Foundry dashboard**](https://cloud.ibm.com/dashboard/cloudfoundry/overview). The _Cloud Foundry dashboard_ shows global views of CFEE instances, applications and public services aliased into CFEE spaces. 

**Note:** A new **Eirini technical preview** plan is available when creating a new CFEE instance. The plan is independent  of the v2.2.0 described above, which applies only to the _Standard_ plan.  The The Eirini Technical Preview plan allows you to explore a CFEE using native Kubernetes as the container scheduler (instead of Diego). See [Getting Started with the Eirini technical preview](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini) for more information.

See a demonstration of what's new in CFEE v2.1.0 in this [brief video](https://ibm.biz/CFEE-V220){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").


## Version 2.1.1
{: #v211}

_Release Date:_ 2019-03-20

The following changes were released in version 2.1.1 of the {{site.data.keyword.cfee_full_notm}} service (CFEE). To update your CFEE's version, go to the _Updates and Scaling_ page in the CFEE's user interface:

* Resolved problems preventing successful provisioning. 


## Version 2.1.0
{: #v210}

_Release Date:_ 2019-02-20

**Note:** You can only update to this version from version **2.0.2**. Update to version 2.0.2 before updating to version v2.1.0.

The following changes were released in version 2.1.0 of the {{site.data.keyword.cfee_full_notm}} service (CFEE). To update your CFEE's version, go to the **Updates and Scaling** page in the CFEE's user interface and click **Update**:

* New autoscaling capability that automatically scales Cloud Foundry application instances based on custom rules. Autoscaling is accessible from the CLI and from the Stratos console. The Stratos console can be optionally installed and launched from the _Overview_ page in the CFEE user interface. In the _Applications_ page of the Stratos console, select an  application and look for the **Auto Scaling** tab. Click *Create Policy* to launch the autoscaling editor to define the scaling policy for the target application.
  See the [autoscaling documentation](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps) for more information.
* New capability to manage buildapcks from the CFEE user interface, including drag-and-drop positioning of a buildpack in the priority list. The capability is available in the new **Buildpacks** page of the CFEE user interface (not the Stratos console). In the release, only buildpack zip files 1 MB in size (or smaller) can be added or updated through the user interface. You can upload buildpack zip files larger than 1 MB using the `cf create-buildpack` and `cf update-buildpack` commands. 
* New capability to manage organization quotas from the user interface, including visualizing which organizations are using a specific quota. The capability is available in the new **Quotas** page of the CFEE user interface (not the Stratos console). You can create new quotas and edit existing ones. You can also update the values of the default quota with the values from any existing quota by invoking the **Copy to Default** from the quota's menu.
* A new **Getting Started** page in the user interface guides users to the most important tasks to setup and use the environment.
* **Tags** can be added to a CFEE instance in the IBM Cloud resource list.  Tags added in the resource list will also appear in the header of the CFEE overview page.
* **Cloud Foundry** version 2.7.21.
* **Stratos** console version 2.3.0, which includes a security patch. Note that simply updating the CFEE version will not update the Stratos console version. You need to delete and re-install the Stratos console (in the CFEE Overview page), which automatically picks the latest Stratos console version.
* Users can navigate to the CFEE's Kubernetes **cluster** page from the overflow menu in the CFEE's overview page.

**Note:** If you update to CFEE v2.1.0 from a v2.0.x version, the update takes place with a single _Update_ action that automatically updates both, the control plane and the cells in sequence. If you update from a v1.x.x version, the update requires two separate _Update_ actions, one for updating the control plane (first), and one for updatting the cells.

See a demonstration of what's new in CFEE v2.1.0 in this [brief video](https://ibm.biz/CFEE-V210){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").


## Version 2.0.2
{: #v202}

_Release Date:_ 2019-02-08

The following changes were released in version 2.0.2 of the {{site.data.keyword.cfee_full_notm}} service (CFEE). To update your CFEE's version, go to the _Updates and Scaling_ page in the CFEE's user interface:

* Resolved problems preventing successful version updates. This version is a pre-req for updating to version **2.1.0**.


## Version 2.0.1
{: #v201}

_Release Date:_ 2019-01-10

The following changes were released in version 2.0.1 of the {{site.data.keyword.cfee_full_notm}} service (CFEE). To update your CFEE's version, go to the _Updates and Scaling_ page in the CFEE's user interface:

* Resolved problem that prevents custom domains from working properly.
* Resolved problem whereby organization metrics are not available while new metrics are retrieved.


## Version 2.0.0
{: #v200}

_Release Date:_ 2018-12-13

The following changes were released in version 2.0.0 of the {{site.data.keyword.cfee_full_notm}} service (CFEE). To update your CFEE's version, go to the _Updates and Scaling_ page in the CFEE's user interface:

* Improved CFEE version update resiliency.
* Improvements to the operational availability and resiliency of CFEE instances.
* Client side certificates for more secured access to applications, allowing the server to grant application access only to certified clients.
* When a CFEE instance is created, the supporting Kubernetes cluster and Cloud Object Storage service instance are now created in the same Resource Group as the CFEE service instance (instead of under the "Default" resource group).
* Security patch.
* Improvements to the `ibmcloud cfee` CLI:
    * New commands for creating an IBM Cloud service instance from a CFEE space and adding it to that CFEE space (`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`).
    * New commands for scaling the capacity of a CFEE (`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`).
    * Improvements to the command for managing CFEE instances (`ibmcloud cfee environments`).
    
      Update the ibmcloud CLI (`ibmcloud update`) to access these command enhancements, and issue `ibmcloud cfee -help` for more details.
      
**Note**: Updating a CFEE instance to version 2.0.0 only requires a single _update_ action that updates both, the control plane and the cells. No separate updates are required for the CFEE control plane and cells.


## Version 1.1.2
{: #v112}

_Release Date:_ 2018-12-07

The following changes were released in version 1.1.2 of the {{site.data.keyword.cfee_full_notm}} service:
* New data centers in Chennai (che01) and Milan (mil01) are now available for provisioning CFEE instances.
* Security patch.

## Version 1.1.1
{: #v111}

_Release Date:_ 2018-11-28

The following changes were released in version 1.1.1 of the {{site.data.keyword.cfee_full_notm}} service:
* Security patch.
   
## Version 1.1.0
{: #v110}

_Release Date:_ 2018-11-16

The following changes were released in version 1.1.0 of the {{site.data.keyword.cfee_full_notm}} service:

* New capabilities:
   * CFEE instances can be provisioned on [virtual-dedicated](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) Kubernetes worker nodes hosted on infrastructure that is devoted to your IBM Cloud account.
   * A new data center in Tokyo (tok05) is available for provisionng CFEE instances.
   * [Updating](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) a CFEE instance to a new version.
   * [Scaling](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) the capacity of a CFEE instance by adding or deleting Cloud Foundry cells.
   * [Auditing](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) Cloud Foundry activities through integration with an automatically configured IBM Cloud Activity Tracker service instance.
   * Persisting Cloud Foundry [log events](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) through an automatically configured IBM Cloud Log Analysis service instance.
   * Health Check view that indicates the operational status of CFEE components.
   * New commands to perform CFEE related actions on the command line interface (CLI):
     * `ibmcloud cfee create`, `ibmcloud cfee create-locations`, and `ibmcloud cfee create-status` commands to create CFEE instances from the command line interface, get a list of available data centers where a CFEE can be provisioned, and check the provisioning status of a CFEE being created.
     * `ibmcloud cfee create-permission-get` and `ibmcloud cfee create-permission-set`  [commands](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) to retrieve and set the permissions required to create CFEE instances. The commands aggregate and simplify the setting of permissions for the CFEE service and for the required supporting services.
     * `ibmcloud catalog blacklist` command to simplify [visibility control](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) of IBM Cloud services for users in an IBM Cloud account.

* Resolved problems:
   *  Resolved Problem: Intermittent error accessing cell metrics
<br/>   
See a demonstration of what's new in CFEE v1.1.0 in this [brief video](https://ibm.biz/CFEE-V110){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").  You can also find other videos on various CFEE topics in the [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").
