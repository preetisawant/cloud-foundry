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

# What's New in {{site.data.keyword.cfee_full_notm}}

This document describes what's new in the various versions of {{site.data.keyword.cfee_full_notm}} released so far.

## Version 1.1.0
{: #v101}

_Release Date:_

The following changes were released in version 1.1.0 of the {{site.data.keyword.cfee_full_notm}} service:

* New capabilities:
   * Updating a CFEE instance to a new version.
   * Scaling the capacity of a CFEE instance by adding or deleting Cloud Foundry cells.
   * New capability to audit Cloud Foundry activities through the integration with an automatically configured IBM Cloud Activity Tracker service instance.
   * New capability to persist Cloud Foundry log events through an automatically configured IBM Cloud Log Analysis service instance.
   * New `ibmcloud cfee` commands to retrieve and set permissions to create CFEE instances. The commands aggregate and simplify the setting of permissions for the CFEE service and for the required supporting services.
   * New `ibmcloud catalog blacklist` command to simplify visibility control of IBM Cloud services for users in an IBM Cloud account.

* Resolved problems:
   *  Resolved Problem: Intermittent error accessing cell metrics
