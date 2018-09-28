---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Working with services
{: #workingwith-services}

Applications deployed in an {{site.data.keyword.cfee_full_notm}} can be bound to two types of service instances:
1. Public service instances created from the {{site.data.keyword.Bluemix}} catalog and available in the {{site.data.keyword.Bluemix}} account.  
Public service instances available in the {{site.data.keyword.Bluemix}} account cannot be available, by themselves, to CFEE environments.  In order for a public service instance (available in the {{site.data.keyword.Bluemix}} account) to become available to spaces in an CFEE environment, they have to be specifically added to the target CFEE space. Once the {{site.data.keyword.Bluemix}} service instance is added to the CFEE space, it can be bound to applications in that CFEE space.  This allows developers to leverage the vast catalog of {{site.data.keyword.Bluemix}} services in their applications deployed in CFEE environments, while allowing access control to those {{site.data.keyword.Bluemix}} services.

   In addition to adding existing {{site.data.keyword.Bluemix}} service instances to a CFEE space you can create a new {{site.data.keyword.Bluemix}} service instance from within a CFEE space, which also adds it automatically to that CFEE space.

2. Service instances managed by a local Cloud Foundry service broker (local to the CFEE). These in turn can be of two types:
   *  2a. An instance of a service offering created from the Cloud Foundry marketplace of the current {{site.data.keyword.cfee_full_notm}} instance. This type of service instance requires a registered service broker available in the environment. A service broker shows a catalog of service offerings and plans, as well as enables the creation, removal, binding and unbinding of instances from those service offerings. See the [Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html) in the Cloud Foundry documentation for more information.
   * 2b. A user-provided service instance. Creation of this type is supported through the CLI, but not through the user interface. Nonetheless, user-provided service instances will be listed in the user interface.
   

## Viewing {{site.data.keyword.Bluemix_notm}} service instances across all CFEE environments
{: #viewing-services_across}

Go to the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) to see a consolidated view of all the {{site.data.keyword.Bluemix_notm}} service instances (to which you have access) in the {{site.data.keyword.Bluemix_notm}} account and see which ones have been added to which CFEE spaces.

This view shows all the {{site.data.keyword.Bluemix_notm}} available in the account and indicates which ones have been added (aliased) to which CFEE spaces. Expand a service instance to show the CFEE spaces where it has been added.  You can further expand those to see the applications in those CFEE spaces to which those service instances have been bound.  

From this view you can also bind applications deployed into the CFEE spaces to which those service instances have been added by. Go to the menu located at the far right of the table row for the corresponding service (available to a specific CFEE space) and select **Bind to applications**.

## Adding existing {{site.data.keyword.Bluemix_notm}} service instances to a CFEE space
{: #adding-services_inspace}

You can bind an {{site.data.keyword.Bluemix_notm}} service instances to applications deployed into a CFEE space.  Before an IBM Cloud service instance can be bound to appplication deployed in CFEE it has to be added to the CFEE space in which the application is deployed. The following is required before you can add an {{site.data.keyword.Bluemix_notm}} service instance to a CFEE Space:
* The {{site.data.keyword.Bluemix_notm}} service must be available in the same {{site.data.keyword.Bluemix_notm}} account where the CFEE instance resides.
* You must have access to the {{site.data.keyword.Bluemix_notm}} service instance itself. For more information, see the Identity & Access page under the **Manage > Users** menu in the {{site.data.keyword.Bluemix_notm}} header to check your current account access policies.

To Add an existing {{site.data.keyword.Bluemix_notm}} service instance to a CFEE space:
1. Go to the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services).  
2. Locate the {{site.data.keyword.Bluemix_notm}} service instance from the list and invoke the menu at the far right of the corresponding table row.
3. Select **Add service**.
4. In the _Add service_ dialog, select the CFEE, org and space where you want to add the service, and click **Add**.
5. Expand the target {{site.data.keyword.Bluemix_notm}} service to find the new CFEE where the service has been added.


Alternatively, you can add {{site.data.keyword.Bluemix_notm}} service instance from within the CFEE space where you want to add it:
1. In your {{site.data.keyword.Bluemix_notm}} [dashboard](https://console.bluemix.net/dashboard) or [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services), find the Cloud Foundry Enterprise environment that hosts your application.
2. Go to **Organizations** in the navigation pane and open the organization and space where the application is located.
3. Go to the **Spaces** tab and locate the space that contains the application.
4. In the target space page, go to the **Services** tab and click **Add service**.  This will open the __Add service__ dialog.  The page lists services service instances available in the {{site.data.keyword.Bluemix_notm}} account.
5. Find and select an available service instance you want to add to the CFEE space. 
6. The service instance will be added to the list of services available in the CFEE space.

   **Note:** When you add an {{site.data.keyword.Bluemix_notm}} service to a CFEE space, an alias to that service instance is created in that space. When you **Remove** the service instance from a CFEE space (from the menu located in the far right of the corresponding service instance row in the table), the service is not deleted from the public account.  The action simmply removes it from the specific CFEE account and is no longer available for binding to applications in that CFEE space.  Also, when you delete the service instance itself from the {{site.data.keyword.Bluemix_notm}} account, the service is no longer available to any CFEE spaces. 

## Creating {{site.data.keyword.Bluemix_notm}} service instances from a CFEE space UI
{: #creating-services_inspace}
You can create {{site.data.keyword.Bluemix_notm}} service instances from within a CFEE space.  Creating an {{site.data.keyword.Bluemix_notm}} service instance results in the following:
* The {{site.data.keyword.Bluemix_notm}} service instance is created in the IBM Cloud.  This is equivalent to creating the service instance from the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.bluemix.net/catalog).
* The {{site.data.keyword.Bluemix_notm}} service instance is added (aliased) into the CFEE space from which the creation action was initiated.


To create a service instance from within a CFEE space:
1. In the target space page, go to the **Services** tab and click **Create service**.  This will open the **Marketplace** view for the {{site.data.keyword.cfee_full_notm}}.  The view lists services offerings from two sources (See __Source__ column):
   * Offerings from the {{site.data.keyword.Bluemix_notm}} catalog .
   * Offerings from the local {{site.data.keyword.cfee_full_notm}} marketplace.
5. Find and select an available service offering that you want to instantiate. 
6. Depending on the source of the service offering (IBM Cloud catalog or local CFEE marketplace) proceed to one of the following:
   * If the selected service offering is an {{site.data.keyword.Bluemix_notm}} catalog offering, you will see a button to **Continue** to the IBM Cloud service offering creation page.  The is the same page available from the {{site.data.keyword.Bluemix_notm}} catalog.  In this page you provide the name of the new service instance, region, plan and other properties required to create the service in the IBM Cloud.  Once you create the service instance will be created in the IBM Cloud and automatically added to the current CFEE space.
   * If the the selected service offering comes from the local CFEE catalog,  you will see a button to **Create** the service instance. You will be prompted for an organization and space in the current CFEE where the service instance will be created.

## Creating {{site.data.keyword.Bluemix_notm}} service instances from a CFEE space using the CLI
{: #creating-services_cli}

You can create a service instance from the CLI from a space in a CFEE.  Creating a service from the CLI in a CFEE space is equivalent to creating it from the UI in that space. That is, creating a service has the following double result:
* The {{site.data.keyword.Bluemix_notm}} service instance is created in the IBM Cloud.  This is equivalent to creating the service instance from the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.bluemix.net/catalog).
* The {{site.data.keyword.Bluemix_notm}} service instance is added (alised) into the CFEE space from which the creation action was initiated.

The difference between creating a service instance from a CFEE space vs. crating it from the CLI is in the lifecycle of the created service instance.  When you create the service instance in the CFEE space UI the lifecycle of the created service instance is controlled from the service instance itself in the {{site.data.keyword.Bluemix_notm}} account.  This means that updates to the service plan is control from the instance in the {{site.data.keyword.Bluemix_notm}} acount, not from the CFEE space.  Alternative, if the service instance is created from the CLI, the service's lifecycle is controlled from the CFEE space (the service is updated from the CFEE space).

Service instances created from the CLI are also displayed in the UI, and are indicated by an ` * ` nexts to the service instance name.

To create service instances using the CLI follow the following steps:

1. Download and install the {{site.data.keyword.Bluemix}} command line interface (if you haven't. [Download the Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

2. Go to the {{site.data.keyword.cfee_full}} Overview page and locate the environment's API endpoint.

3. In the command line interface, set the API endpoint to your CFEE environment's endpoint:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Log into the CFEE environment:

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  If you're using a federated ID, use the `-sso` option:

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. Create the service:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  Optionally, you can provide a file containing parameters in a valid JSON object required for creating a specific service.
  The path to the parameters file can be an absolute or relative path to a file:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  Following is an example of a valid JSON object:
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   For help creating a service from the CLI, issue the following:
  
  ```
  cf cs -help
  ```
  See [Managing Service Instances with the cf CLI](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") in the Cloud Foundry documentation for more information.
  
## Binding services to applications
{: #bind_services}

You can bind a service instance to an application deployed in a CFEE either from the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) or from the Services tab of a CFEE space page.  

To bind a service instance to an application from the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services):
1. Go to the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) to see a consolidated view of all the {{site.data.keyword.Bluemix_notm}} service instances available to you in the {{site.data.keyword.Bluemix_notm}} account.  The view is also intended to show which {{site.data.keyword.Bluemix_notm}} services instances are available (aliased into) in which CFEE spaces. You can expand a service instance to show the CFEE spaces where it has been added.  You can further expand those to see the applications in those CFEE spaces to which those service instances have been bound. 
2. Locate the {{site.data.keyword.Bluemix_notm}} service instance you want to bind.
3. Expand the corresponding view to see all the CFEE spaces where that service instance has been added. If that service instance has not been added to the CFEE space where the application is deployed, select **Add** from the menu at the row's far right to make the service instance available in the target CFEE space.
4. Go to the menu located in the far right of the row corresponding to the CFEE/space where the service instance is available, and select **Bind application**.
5. In the __Bind application__ dialog select the application you want to bind.
6. The application is now bound to the service instance in the CFEE space where the application is deployed.  You can expand the row to corresponding row in the table to see the bound applications in the CFEE space.


To bind an application to a service instance from the __Services__ page of a CFEE space:

1. Open the CFEE user interface where the application is deployed.
2. Go to **Organizations** in the left navigation pane and open the organization and space where the application is deployed.
3. Go to the **Spaces** tab and locate the space that contains the application.
4. In the target space page, go to the **Services** tab.
5. In the table of **Service instances**, go to the __Actions__ menu in the far right of the row corresponding to the service instance you want to bind, and select **Bind**.
6. Select the application that you want to bind to the service instance.

To unbind an application from a service instance:

1. In the **Services** tab of the space, expand the target service instance to show the apps that are bound to it.
2. Go the Actions menu in an application's row and select **Unbind service**.

See [Bind a Service Instance](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") in the Cloud Foundry documentation for more information about binding applications using the CLI.


