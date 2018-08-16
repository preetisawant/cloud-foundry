---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Binding apps to services instances
{: #bind_services}

To bind an application to a service instance:

1. In your {{site.data.keyword.Bluemix}} dashboard, find the Cloud Foundry Enterprise Environment hosting your application.
2. Go to **Organizations** in the navigation pane and open the organization and space where the application is located.
3. Go to the **Spaces** tab and locate the space that contains the application.
4. In the target space page, go to the **Services** tab.
5. In the table of **Service instances**, go to the Actions menu in the far right of the row corresponding to the service instance you want to bind, and select **Bind**.
6. Select the application that you want to bind to the service instance.

To unbind an application from a service instance:

1. In the **Services** tab of the space, expand the target service instance to show the apps that are bound to it.
2. Go the Actions menu in an application's row and select **Unbind service**.

For more information, see [{{site.data.keyword.cfee_full_notm}}](index.html) and [Cloud Foundry documentation](https://docs.cloudfoundry.org/adminguide/).
