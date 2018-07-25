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
You can create three types of service instances from a {{site.data.keyword.cfee_full_notm}}:

* An {{site.data.keyword.Bluemix}} service instance.  When you create an {{site.data.keyword.cfee_full_notm}} from an {{site.data.keyword.cfee_full_notm}}, in addition to creating a public instance available to users in the IBM Cloud account, an alias to that service instance is created in the {{site.data.keyword.cfee_full_notm}} from which it was created. 
* An alias to an existing {{site.data.keyword.Bluemix}} service instance existing outside the {{site.data.keyword.cfee_full_notm}}. Creating an alias to an existing {{site.data.keyword.Bluemix_notm}} service instance requires user access to the instance itself. For more information, see the Identity & Access page under the **Manage > Users** menu in the {{site.data.keyword.Bluemix_notm}} header to check your current account access policies.
* An instance of a service offering available in the Cloud Foundry marketplace catalog of the current {{site.data.keyword.cfee_full_notm}} instance. This type of service instance requires a registered service broker available in the environment. A service broker shows a catalog of service offerings and plans, as well as enables the creation, removal, binding and unbinding of instances from those service offerings. See the [Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html) in the Cloud Foundry documentation for more information.
* A user-provided service instance. Creation of this type is supported through the CLI, but not through the user interface. Nonetheless, user-provided service instances will be listed in the user interface.

To create a service instance:

1. In your {{site.data.keyword.Bluemix_notm}} dashboard, find the Cloud Foundry Enterprise environment that hosts your application.
2. Go to **Organizations** in the navigation pane and open the organization and space where the application is located.
3. Go to the **Spaces** tab and locate the space that contains the application.
4. In the target space page, go to the **Services** tab and click **Create service**.  This will open the **Catalog** page for the {{site.data.keyword.cfee_full_notm}}.  The page lists services offerings from two sources (See _Source_ column):
   * Offerings from the IBM Cloud catalog .
   * Offerings from the local {{site.data.keyword.cfee_full_notm}} marketplace.
5. Find and select an available service offering that you want to instantiate. 
6. Depending on the source of the service offering (IBM Cloud or local CFEE) proceed to one of the following:
   * **Continue** to the IBM Cloud service offering creation page to provide the name of the new service instance, region, plan and other properties required to create the service in the IBM Cloud.  Once you click *Create* the service instance will be created in the IBM Cloud.  In addition, an alias of that service instance will be created in the {{site.data.keyword.cfee_full_notm}}.  The alias will be available for binding with applications in the {{site.data.keyword.cfee_full_notm}}.
   * **Create** the service instance in the local Cloud Foundry marketplace. This will open a dialog where you provide the name of the new service instance and the plan. Once Once you click *Create* the service instance will be created in the {{site.data.keyword.cfee_full_notm}} and will be available for binding with applications in the {{site.data.keyword.cfee_full_notm}}.

The newly created service instance (or alias) will be listed in the **Services** tab.
