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

# Creating service instances
You can create three types of service instances:

* An alias to an {{site.data.keyword.Bluemix}} service instance outside the {{site.data.keyword.cfee_full_notm}}. Creating an alias to an {{site.data.keyword.Bluemix_notm}} service instance requires user access to the instance itself. For more information, see the Identity & Access page under the **Manage > Users** menu in the {{site.data.keyword.Bluemix_notm}} header to check your current account access policies.
* An instance of a service offering available in the catalog of the current {{site.data.keyword.cfee_full_notm}}.
* A user-provided service instance. Creation of this type is supported through the CLI, but not through the user interface.

**Note:** Aliases to {{site.data.keyword.Bluemix_notm}} service instances are not supported in the experimental plan. With the experimental plan, service instances can be created from service offerings available in the target {{site.data.keyword.cfee_full_notm}}.

To create a service instance:

1. In your {{site.data.keyword.Bluemix_notm}} dashboard, find the Cloud Foundry Enterprise environment that hosts your application.
2. Go to **Organizations** in the navigation pane and open the organization and space where the application is located.
3. Go to the **Spaces** tab and locate the space that contains the application.
4. In the target space page, go to the **Services** tab and click **Create**.
5. In the _Create_ window, select a **Service instance type**.
6. Find and select an available service offering, and enter a **Service instance name** for it.
7. Click **Create**.

After the service instance is created, the service instance or alias is listed under the **Services** tab.