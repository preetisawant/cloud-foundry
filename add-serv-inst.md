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

# Creating and viewing service instances
{: #creating-services}

Applications deployed in an {{site.data.keyword.cfee_full_notm}} can be bound to two types of service instances:
1. Service instances managed by a local Cloud Foundry service broker (local to the CFEE). These in turn can be of two types:
   *  1a. An instance of a service offering created from the Cloud Foundry marketplace of the current {{site.data.keyword.cfee_full_notm}} instance. This type of service instance requires a registered service broker available in the environment. A service broker shows a catalog of service offerings and plans, as well as enables the creation, removal, binding and unbinding of instances from those service offerings. See the [Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html) in the Cloud Foundry documentation for more information.
   * 1b. A user-provided service instance. Creation of this type is supported through the CLI, but not through the user interface. Nonetheless, user-provided service instances will be listed in the user interface.
2. Public service instances created from the {{site.data.keyword.Bluemix}} catalog and available in the {{site.data.keyword.Bluemix}} account.
Public service instances available in the {{site.data.keyword.Bluemix}} account cannot be available, by themselves, to CFEE environments.  In order for a public service instance (available in the {{site.data.keyword.Bluemix}} account) to become available to spaces in an CFEE environment, an alias to the service instance must be created in the target CFEE space. The alias functions as a reference to the actual public service instance.  Once the service alias is created in an CFEE space, it can be bound to applications in that CFEE.  Service aliasing allows developers to leverage the vast catalog of {{site.data.keyword.Bluemix}} services in their applications deployed in CFEE environments.


## Creating and viewing service aliases in an CFEE space
{: #creating-services_inspace}

An alias to an existing public service instance available in your IBM Cloud account allows you to bind that service instance to applications deployed in an CFEE space. Creating an alias to an existing {{site.data.keyword.Bluemix_notm}} service instance requires user access to the instance itself. For more information, see the Identity & Access page under the **Manage > Users** menu in the {{site.data.keyword.Bluemix_notm}} header to check your current account access policies.

To create a service instance alias within a space in an CFEE:

1. In your {{site.data.keyword.Bluemix_notm}} dashboard, find the Cloud Foundry Enterprise environment that hosts your application.
2. Go to **Organizations** in the navigation pane and open the organization and space where the application is located.
3. Go to the **Spaces** tab and locate the space that contains the application.
4. In the target space page, go to the **Services** tab and click **Create service**.  This will open the **Catalog** page for the {{site.data.keyword.cfee_full_notm}}.  The page lists services offerings from two sources (See _Source_ column):
   * Offerings from the IBM Cloud catalog .
   * Offerings from the local {{site.data.keyword.cfee_full_notm}} marketplace.
5. Find and select an available service offering that you want to instantiate.
6. Depending on the source of the service offering (IBM Cloud or local CFEE) proceed to one of the following:
   * **Continue** to the IBM Cloud service offering creation page to provide the name of the new service instance, region, plan and other properties required to create the service in the IBM Cloud.  Once you click *Create* the service instance will be created in the IBM Cloud.  In addition, an alias of that service instance will be created in the {{site.data.keyword.cfee_full_notm}}.  The alias will be available for binding with applications in the {{site.data.keyword.cfee_full_notm}}.
   **Note:** When creating an {{site.data.keyword.Bluemix_notm}} in this fasion, in addition to creating a public instance available to users in the IBM Cloud account, an alias to that service instance is created in the {{site.data.keyword.cfee_full_notm}} from which it was created.
   * **Create** the service instance in the local Cloud Foundry marketplace. This will open a dialog where you provide the name of the new service instance and the plan. Once you click *Create* the service instance will be created in the {{site.data.keyword.cfee_full_notm}} and will be available for binding with applications in the {{site.data.keyword.cfee_full_notm}}.

After the service instance is created, the service instance (if it's created in the local Cloud Foundry marketplace) or alias (if the service instance was created from the IBM Cloud catalog) is listed under the **Services** tab.


## Creating and viewing service aliases across all CFEE environments in the global Cloud Foundry dashboard
{: #creating-services_across}

You can see a consolidated view of all service instance aliases (across all CFEE instances) in the global Cloud Foundry dashboard.

1. Click the Menu icon ![Account Checking](img/HamburgerMenu.png  "Screen cap that shows the menu icon") > **Cloud Foundry** to open the Cloud Foundry dashboard.
2. Click **Enterprise > Services** in the left navigation pane.
The table in the view shows the following information:

| Element   | Description |
|-----------|---------------|
| Service Alias | The name of the service instance alias. |
| Service instance | The public IBM Cloud service instance from which the alias is created. |
| Offering | The service offering from the IBM Cloud catalog from where the service instance was created. |
| CFEE | The {{site.data.keyword.cfee_full}} where the alias resides. |
| Organization | The organization in the CFEE instance where the alias resides. |
| Space | The space within the organization in the CFEE instance where the alias resides. |
{:caption="Table 1. Description of key elements" caption-side="top"}

You can perform the following actions in this view:
* Sort the items in the table by any of the properties displays as table columns.
* Bind applications to a specific alias by accessing the alias overflow menu of the alias located at the row's far right.
* Expand an alias (row) to see all the applications bound that alias.
* Start, stop applications by accessing the application overflow menu of the alias located at the row's far right.
* Navigate to an CFEE, CFEE organization or CFEE space by clicking on the link with the corresponding CFEE, organization, or space.

To create a service alias from the global Cloud Foundry dashboard:
1. Click **Create service alias** button at the top of the page. This will open the _Create Service Alias_ dialog.  The dialog lists all the public service instances available in the current IBM Cloud account.
2. Select one of the public service instances.
3. Click **Create**. Once created, the new service instance alias will be added to the list.
The service alias will also appear in the list of services in the CFEE space, where it can be bound to applications in that space (CFEE > Organizations > Space > Services).


