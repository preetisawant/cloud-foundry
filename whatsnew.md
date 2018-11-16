---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# What's New in IBM Cloud Foundry Enterprise Environment

This document describes what's new in each version released up to this date of the {{site.data.keyword.cfee_full_notm}} service.

## Version 1.1.0
{: #v101}

_Release Date:_ 2018-11-16

The following changes were released in version 1.1.0 of the {{site.data.keyword.cfee_full_notm}} service:

* New capabilities:
   * [Updating](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) a CFEE instance to a new version.
   * [Scaling](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) the capacity of a CFEE instance by adding or deleting Cloud Foundry cells.
   * [Auditing](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) Cloud Foundry activities through integration with an automatically configured IBM Cloud Activity Tracker service instance.
   * Persisting Cloud Foundry [log events](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) through an automatically configured IBM Cloud Log Analysis service instance.
   * New `ibmcloud cfee` [commands](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) to retrieve and set permissions to create CFEE instances. The commands aggregate and simplify the setting of permissions for the CFEE service and for the required supporting services.
   * New `ibmcloud catalog blacklist` command to simplify [visibility control](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) of IBM Cloud services for users in an IBM Cloud account.

* Resolved problems:
   *  Resolved Problem: Intermittent error accessing cell metrics
   
See a demonstration of what's new in CFEE v1.1.0 in this [brief video](https://ibm.biz/CFEE-V110){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

You can find other videos on various CFEE topics in the [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").
