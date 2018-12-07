---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# What's New in IBM Cloud Foundry Enterprise Environment

This document describes what's new in each version released up to this date of the {{site.data.keyword.cfee_full_notm}} service.

## Version 1.1.2
{: #v112}

_Release Date:_ 2018-12-07

The following changes were released in version 1.1.2 of the {{site.data.keyword.cfee_full_notm}} service:
* New data centers in Chennai (che01) and Milan (mil01) are now available for provisioning CFEE instances.
* Security patches.

## Version 1.1.1
{: #v111}

_Release Date:_ 2018-11-28

The following changes were released in version 1.1.1 of the {{site.data.keyword.cfee_full_notm}} service:
* Resolved potential exposure to sensitive information in internal update logs.
   
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
