---

copyright:
  years: 2019
lastupdated: "2019-04-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Auditing accounts
{: #auditing-accounts}

## Auditing events
{: #auditing-events}
Customers can retrieve audit events for the various activities that occur within their individual {{site.data.keyword.cfee_full_notm}} ({{site.data.keyword.cfee_short}}) instances.  
These events can be retrieved from Activity Tracker.

First set up your Activity Tracker instance, following the [detailed documented steps](https://cloud.ibm.com/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla#getting-started-with-cla). 

Then [enable auditing](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-auditing-logging#auditing-logging) of the specific {{site.data.keyword.cfee_short}} instance.

Reference the Activity Tracker [documentation](https://cloud.ibm.com/docs/services/cloud-activity-tracker/index.html) for event fields, types of audit events, configuration and event retrieval. 
Events can be downloaded using the Activity Tracker [API](https://cloud.ibm.com/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-downloading_events_api#downloading_events_api) and [CLI](https://cloud.ibm.com/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-downloading_events#downloading_events).  
These events can also be viewed through [user interfaces](https://cloud.ibm.com/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-view_acc_events#view_acc_events).

## Alerting on audit events
{: #altering-on-audit-events}
If customers desire to receive alerts for audit events, they can use external tools like QRadar to extract audit events from Activity Tracker and configure to receive alerts accordingly.

