---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-29-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Auditing and logging
{: #logging-auditing}

The logging and auditing capabilities in {{site.data.keyword.cfee_full}} (CFEE) allow administrators audit any event taking place in a CFEE instance, and developers to track log events generated from their applications.

Logging and auditing in a CFEE are suppoted through integration with the IBM Cloud Services: Log Analysis and Activity Tracker services respectively.

## Logging persistence
{: #logging-auditing}

The CFEE logging of Cloud Foundry events is supported through integration with the Log Analysis service in the IBM Cloud account. Once a target instance of the Log Analysis service is selected, the instance is configured automatically to send and persist logging events from the CFEE instance to that Log Analysis instance.  The user can go to the UI of that service instance to see and manage logging events.

To enable logging for a CFEE instance:

1. Open a CFEE's user interface and to **Operations > Logging** entry in the left navigation pane to open the Logging page.
2. Click **Enable persistence** and select one of the **Log Analysis instances** available in the IBM Cloud account.  If no instances are available, the user will see an option to create an instance in the catalog.
3. The page is refresh with details about the configured Log Analysis service instance, including the status of the configuration, and a link to the Log Analysis service instance itself.

You can disable Log persistence by clicking on **Disable log persistence**, which will remove the service instance previously added and automatically configured.

**Note:** When you disable log persistance, the Cloud Foundry logging events are still being generated, they are just not persisted.

## Auditing
{: #auditing}

Auditing of activities taking place on a CFEE instance, including.... The capability is supported through integration with the Activity Tracker service in the IBM Cloud account. Once a target instance of the Log Analysis service is selected, the instance is configured automatically to send activity events from the CFEE instance to that Log Analysis instance.  The user can go to the UI of that service instance to see and manage auditing events.

To enable auditing for a CFEE instance:

1. Open a CFEE's user interface and to **Operations > Auditing** entry in the left navigation pane to open the Logging page.
2. Click **Enable persistence** and select one of the **Activity Tracker instances** available in the IBM Cloud account.  If no instances are available, the user will see an option to create an instance in the catalog.
3. The page is refresh with details about the configured Activity Tracker service instance, including the status of the configuration, and a link to the Activity Tracker service instance itself.

You can disable Auditing by clicking on **Disable auditing**, which will remove the Activity tracker service instance previously added and automatically configured.
