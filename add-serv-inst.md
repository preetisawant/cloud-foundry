---

copyright:
  years: 2018
lastupdated: "2018-11-16"

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
   * 2b. A user-provided service instance. Creation of this type is supported through the Command Line Interface (CLI), but not through the user interface. Nonetheless, user-provided service instances will be listed in the user interface.
   

## Viewing {{site.data.keyword.Bluemix_notm}} service instances across all CFEE environments
{: #viewing-services_across}

Go to the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) to see a consolidated view of all the {{site.data.keyword.Bluemix_notm}} service instances (to which you have access) in the {{site.data.keyword.Bluemix_notm}} account and see which ones have been added to which CFEE spaces.

This view shows all the {{site.data.keyword.Bluemix_notm}} service instances available in the account and indicates which ones have been added (aliased) to which CFEE spaces. Expand a service instance to show the CFEE spaces where it has been added.  You can further expand those to see the applications in those CFEE spaces to which those service instances have been bound.  

From this view you can also bind applications deployed into the CFEE spaces to which those service instances have been added. Go to the menu located at the far right of the table row for the corresponding service (available to a specific CFEE space) and select **Bind to applications**.

## Adding existing {{site.data.keyword.Bluemix_notm}} service instances to a CFEE space
{: #adding-services-inspace}

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
4. In the target space page, go to the **Services** tab and click **Add service**.  This will open the __Add service__ dialog.  The page lists service instances available in the {{site.data.keyword.Bluemix_notm}} account.
5. Find and select an available service instance you want to add to the CFEE space. 
6. The service instance will be added to the list of services available in the CFEE space.

   **Note:** When you add an {{site.data.keyword.Bluemix_notm}} service to a CFEE space, an alias to that service instance is created in that space. When you **Remove** the service instance from a CFEE space (from the menu located in the far right of the corresponding service instance row in the table), the service is not deleted from the public account.  The action simmply removes it from the specific CFEE account and is no longer available for binding to applications in that CFEE space.  Also, when you delete the service instance itself from the {{site.data.keyword.Bluemix_notm}} account, the service is no longer available to any CFEE spaces. 

## Creating {{site.data.keyword.Bluemix_notm}} service instances from a CFEE space's user interface
{: #creating-services_inspace}
You can create {{site.data.keyword.Bluemix_notm}} service instances from within a CFEE space.  Creating an {{site.data.keyword.Bluemix_notm}} service instance results in the following:
* The {{site.data.keyword.Bluemix_notm}} service instance is created in the IBM Cloud.  This is equivalent to creating the service instance from the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.bluemix.net/catalog).
* An alias to the {{site.data.keyword.Bluemix_notm}} service instance is added (aliased) to the CFEE space from which the creation action was initiated. An alias service instance (in a CFEE space) is a reference to the actual service instance (in the IBM Cloud account). The service instance alias allows developers to interact with the service instance (e.g., binding to applications) by handling all the credentials automatically for interacting with the service instance. .

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

The difference between creating a service instance from a CFEE space vs. creating it from the CLI is in the lifecycle of the created service instance.  When you create the service instance in the CFEE space UI the lifecycle of the created service instance is controlled from the service instance itself in the {{site.data.keyword.Bluemix_notm}} account.  This means that updates to the service plan is controlled from the instance in the {{site.data.keyword.Bluemix_notm}} acount, not from the CFEE space.  Alternatively, if the service instance is created from the CLI, the service's lifecycle is controlled from the CFEE space (the service is updated from the CFEE space).

Service instances created from the CLI are also displayed in the UI, and are indicated by an ` * ` next to the service instance name.

To create service instances using the CLI follow the following steps:

1. Download and install the {{site.data.keyword.Bluemix}} command line interface (if you haven't done it already). [Download the Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

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

Users with _editor_ role or higher to a {{site.data.keyword.Bluemix_notm}} service instance can bind that instance to an application deployed in a CFEE space,  either from the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) or from the Services tab of a CFEE space's user interface.   

To bind a service instance to an application from the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services):
1. Go to the [Cloud Foundry services dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) to see a consolidated view of all the {{site.data.keyword.Bluemix_notm}} service instances available to you in the {{site.data.keyword.Bluemix_notm}} account.  The view is also intended to show which {{site.data.keyword.Bluemix_notm}} services instances are available (aliased into) in which CFEE spaces. You can expand a service instance to show the CFEE spaces where it has been added.  You can further expand those to see the applications in those CFEE spaces to which those service instances have been bound. 
2. Locate the {{site.data.keyword.Bluemix_notm}} service instance you want to bind.
3. Expand the corresponding view to see all the CFEE spaces where that service instance has been added. If that service instance has not been added to the CFEE space where the application is deployed, select **Add** from the menu at the row's far right to make the service instance available in the target CFEE space.
4. Go to the menu located in the far right of the row corresponding to the CFEE/space where the service instance is available, and select **Bind application**.
5. In the __Bind application__ dialog select the application you want to bind.
6. The application is now bound to the service instance.  You can expand a service instance in the table to see the applications bound to it (in a specific CFEE space).


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

## Service visibility
{: #service_visibility}

Customers can control who can create new IBM Cloud services from a CFEE environment.  They can also control who can add existing IBM Cloud services to a CFEE space.  This control is exerted by controlling the visibility of service offerings (and/or instances of those service offerings) to users.

### Controlling the creation of service instances
{: #control_servicecreation}

Controlling the creation of services can be accomplished by controlling the visibility of service offerings in the IBM Cloud Catalog for either all users in the IBM Cloud account or for users in specific Cloud Foundry organizations.

#### Controlling visibility to users in an IBM Cloud account to the IBM Cloud catalog
{: #creation_accountvisibility}

IBM Cloud account administrators (users with _Administrator_ role to all IAM enabled services) can prevent a service or service plan from showing int the catalog for all users in a given **IBM Cloud account**.  Account administrators can prevent all account users from using a service by blacklisting a service or service plan for all the users in an account. Blacklisting a service will prevent users in that account from even seeing that service (or service plan) in the IBM Cloud catalog.  This is done through an `ibmcloud catalog blacklist` command which has the following syntax:

  ```
  ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]
  ```

In its simoplest form, you can backlist you can make a service offering (all its plans) invisibile for users in the current account by issueing the following command:

  ```
  Ibmcloud catalog blacklist <thisService>
  ```
  {: pre}

You could blacklist visibility not just generally for the entire service offering, but for a specific plan in a specific region.  For this, though you need to use the ID for the corresponding entry in the global catalog, not the name.   If you want to prevent users from seeing a specific plan in a specific region you can issue the following:

  ```
  Ibmcloud catalog blacklist -add <catalogEntryID>
  ```
  {: pre}
  
 To remove services from the blacklist:
 ```
  Ibmcloud catalog blacklist -remove <catalogEntryID>
  ```
  {: pre}
 
You can find the ID of a given catalog entry (e.g., a service's plan and its deployment region) through the following command. The command returns all the plans and their deployment regions for a given service:

  ```
  ibmcloud catalog service <thisService>
  ```
  {: pre}

You can find more details for the `ibmcloud catalog blacklist` by issuing the following:

  ```
  Ibmcloud catalog blacklist -help
  ```
  {: pre}


#### Controlling visibility to users in a Cloud Foundry organization
{: #creation_orgvisibility}

You can use the `cf enable-service-access` and `cf disable-service-access` commands to control access to services for specific **Cloud Foundry organizations**.  Here the control point for access is Cloud Foundry (not the IBM Cloud Account).  Note that this is a native `cf` command (not an `ibmcloud` command). 

Consider the following when setting service visibility through the `cf` CLI:

*  `cf` commands enable and/or disable service offerings (optionally, specific service offering plans) for all users of specific Cloud Foundry organizations
* Enablement works by building an organization “whitelist”. That is, an inclusion list of Cloud Foundry organizations that do have access to a service (as opposed to the "blacklist" approach in the `ibmcloud` command described earlier, which works by defining a list of services excluded from visibility to account users). This means that access control to a catalog service with this approach works, not by defining which organizations cannot see a service (blacklisting), but by defining which organizations can see it (whitelisting).
*  When you give an organization access to a service (or service plan) by adding that organization to a whitelist, you are de facto disabling (excluding) all other organization from accessing it.  That is, once you whitelist an organization, you are disabling all other organization from access to that service (or service plan)
*  Before you add organizations to the "can see" list, you have to disable visibility for all the organizations.  You cannot disable access to a service plan if the plan is currently available to all organizations.

In accordance to the general behavior described above, we recommend to control organization access to services by issuing the following commands:
1. **Disable** access to a service plan for all orgs:
  ```
  cf disable-service-access <service name> -p <plan name>
  ```
  {: pre}
  
2. **Enable** access to the service plan for specific CFEE organizations.  This will disable the service plan for all other organizations not specifically enabled in the command. 
  ```
  cf enable-service-access <service name> -p <plan name> -o <org name>
  ```
  {: pre}
  
**Note:** We recommend to execute the Cloud Foundry enable and disable service commands for the entire service, not for specific plans.


### Controlling access to existing service instances
{: #control_serviceaddition}

Developers in a CFEE space can use existing service instances available in the IBM Cloud account.  Within a specific space of a CFEE, users can **Add** a service instance to that space (See [Adding existing service instances](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)above). Adding a service instance to a CFEE space creates an alias (a reference) to the service instance, which allows a developer to bind the service instance to an application deployed into that CFEE space as if it were the actual service instance.

Account administrators can control the use of service instances through [IAM access policies](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage).  From either the UI or the ibmcloud CLI they can assign roles to either the service instances themselves or to the resource groups in which those instances resided.  A developer would need _Viewer_ role or higher to a service instance (or its resource group) before they can add that instance to a space.

You can find videos with in-depth discussions and demonstrations on CFEE services in the [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").
{:tip}
