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

# Auditing and logging
{: #auditing-logging}

The auditing and logging capabilities in {{site.data.keyword.cfee_full}} (CFEE) allow administrators to audit any event taking place in a CFEE instance, and developers to track log events generated from their applications.

Auditing and logging in CFEE are suppoted through integration with the Log Analysis and Activity Tracker IBM Cloud services.

## Auditing
{: #auditing}

Auditing of activities taking place on a CFEE instance, including.... Auditing is supported through integration with the Activity Tracker service in the IBM Cloud. An instance of the Activity Tracker service selected by the CFEE administrator is configured automatically to receive events representing actions performed in the CFEE.  The user can see and manage those events in the user interface of the Activity Tracker service instance.

To enable auditing for a CFEE instance:

1. Open a CFEE's user interface and to **Operations > Auditing** entry in the left navigation pane to open the Logging page.
2. Click **Enable auditing** and select one of the **Activity Tracker instances** available in the IBM Cloud account.  If no instances are available, the user will see an option to create a new Activity Tracker instance in the IBM Cloud atalog.
3.  Once logging persistance is enabled, configuration details are displayed in the page. Details include the status of the configuration, and a link to the Activity Tracker service instance itself, where they user can go to see and manage auditing events.

You can disable Auditing by clicking **Disable auditing**, which will remove the Activity tracker service instance previously added and configured.

## Logging persistence
{: #logging-auditing}

Logging of Cloud Foundry events is supported through integration with the Log Analysis service in the IBM Cloud. An instance of the Log Analysis service selected by the CFEE administrator is configured automatically to receive and persist Cloud Foundry logging events generated from the CFEE.  The user can see and manage those logging events in the user interface of the Log Analysis service instance.

To enable logging for a CFEE instance:

1. Open a CFEE's user interface and to **Operations > Logging** entry in the left navigation pane to open the Logging page.
2. Click **Enable persistence** and select one of the **Log Analysis instances** available in the IBM Cloud account.  If no instances are available, the user will see an option to create an instance in the IBM Cloud catalog.
3. Once logging persistance is enabled, configuration details are displayed in the page. Details include the status of the configuration, and a link to the Log Analysis service instance itself, where they user can go to see and manage logging events.

**Warning:** Enabling Logging Persistence requires a disruptive restart of the CFEE control plane and cells.  During the restart, all administrative functionality will be available, but some applications and services running in this CFEE instance may be unavailable.  The status of the CFEE components will be reflected in the Health Check page during the restart.  The restart takes approximately 20 minutes.

You can disable Log persistence by clicking **Disable log persistence**, which will remove the service instance previously added and configured.

**Note:** When you disable log persistance, the Cloud Foundry logging events are still being generated, they are just not persisted.

