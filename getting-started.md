---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Getting started tutorial
{: #getting-started}

{{site.data.keyword.cfee_full}} is a cloud platform for hosting apps and services in the cloud. {{site.data.keyword.cfee_full_notm}} makes it easy to scale apps as consumption grows, simplifying the runtime, middleware, and infrastructure so that you can focus on developing apps.
{: shortdesc}

This getting started tutorial shows how to create an {{site.data.keyword.cfee_full_notm}}, add users, create an organization and spaces, deploy apps, and bind those apps to services.

## Understanding permissions
{: #permissions}

To work with instances of the {{site.data.keyword.cfee_full_notm}}, service users must have the correct permissions. For more information, see [Permissions](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Step 1: Ensure that the {{site.data.keyword.Bluemix_notm}} account can create infrastructure resources
{: #accountprep-environment}

CFEE instances are deployed on infrastructure resources, which are Kubernetes worker nodes from the Kubernetes Service.  [Prepare your IBM Cloud account](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html) to ensure that it can create the infrastructure resources necessary for an CFEE instance.

## Step 2: Create your CFEE instance
{: #create-environment}

Before you create your CFEE, make sure that you are in the {{site.data.keyword.Bluemix_notm}} IBM Cloud account where you want to create the environment and that you have the required access policies (per step 1 above).

1.  Open the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.bluemix.net/catalog).

2.  Locate the {{site.data.keyword.cfee_full_notm}} service in the catalog and click it to open the overview page for the service.

3.  The first page of the creation page provides an overview of the main features of the service. Click **Continue**.

4.  Configure the CFEE instance to be created by providing the following:
    * Select a plan (plan availability may be restricted during Beta).
    * Enter a **Name** for the service instance.
    * Select a **Location** where the service instance is to be provisioned. See the list of [available provisioning locations and data centers](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") by geography for CFEE and supporting services. 
    * Select the **Number of cells** for the Cloud Foundry environment.
    * Select the **Machine type**, which determines the size of the Cloud Foundry cells (CPU and memory) .
    * Select a **Resource group** under which the environment is grouped. Only those resource groups to which you have access in the current IBM Cloud account will be listed in the _Resourouce groups_ dropdown, which means that you need to have permission to access at least one resource group in the account to be able to create an CFEE.

5.  In the **Compose for PostgreSQL** fields, select one of the public organizations, then select one of the spaces available in that organization. The instance of the Compose for PostgreSQL instance will be provisioned in the selected space. The Compose for PostgreSQL service is a required dependency of the CFEE service

**Note:** Only organizations in the location where you intend to provision the CFEE instance (step 4 above) and to which you have access are available for selection.  Within a specific organization, only spaces to which you have _developer_ access are available for selection. 

6.  Optionally, open the **Infrastructure** section to see the properties of the Kubernetes cluster supporting the CFEE instance. Note that the **Number of worker nodes** equals the number of cells plus 2 (two of the provisioned Kubernetes worker nodes support the CFEE control plane).
The Kubernetes cluster on which the environment is deployed appears in the {{site.data.keyword.Bluemix_notm}} [dashboard](https://console.bluemix.net/dashboard/apps/). For more information, see [Kubernetes Service documentation](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov).

**Note:** We recommend that VLAN spanning be enabled if the worker nodes in the Kubernetes cluster are provisioned on different subnets.  Worker nodes on different subnets may prevent connectivity among them if VLAN spanning is disabled.  See [VLAN spanning](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning) documentation for more information.

7.  The **Order Summary** in the right-hand side of the page reflects the cost of the CFEE instance and the ancillary services along with the estimated monthly total.

8.  Click **Create**, which opens the environment dashboard and indicates the creation progress and status.

9.  Once provisioning has started the environment is shown in the {{site.data.keyword.Bluemix_notm}} dashboard, as well as in the [Cloud Foundry Environments dashboard](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments).  The status indicates when provisioning is completed.

The automated process that creates the environment deploys the infrastructure into a Kubernetes cluster and configures it to make it ready for use. The process takes 90 - 120 minutes.

Once you successfully create the environment you will receive multiple emails confirming the provisioning of the CFEE and supporting services, as well as emails notifying you of the status of the corresponding orders.

**Note** that when you create a CFEE instance, there are three additional supporting service instances created in the same IBM Cloud account. Those supporting service instances are named after the CFEE instance name. Hence, creating a CFEE results in a total of four service instances created in the IBM Cloud account:
* CFEE instance ("_cfeename_").
* Kubernetes cluster ("_cfeename_-cluster"). The cluster provides the infrastructure into which the CFEE instance is provisioned.
* Cloud Object Storage instance ("_cfeename_-cos"). The instance is used to store data generated during the creation of the CFEE application containers (e.g. uploaded application packages, buildpacks, and compiled executables).
* Compose for PosgreSQL instance ("_cfeename_-postgres"). The instance is used to store Cloud Foundry data on the CFEE instance (e.g., auditing application deployment, start and stop events; keeping records of CFEE user membership, organizations, spaces, applications and service connections). 

## Step 3: Create organizations and spaces
{: #create-orgsandspaces}

After you create the {{site.data.keyword.cfee_full_notm}}, see [Creating organizations and spaces](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html) for information on how to structure the environment by creating organizations and spaces. Apps in an {{site.data.keyword.cfee_full_notm}} are scoped within specific spaces. In turn, a space exists within a specific organization. Members of an organization share a quota plan, apps, services instances, and custom domains.

**Note:** The _Cloud Foundry organizations_ page available from the **_Manage > Account > Cloud Foundry orgs_** menu located in the top IBM Cloud header is intended exclusively for public IBM Cloud organizations, **not for CFEE organizations**. CFEE organizations are managed within the _Organizations_ page of an CFEE instance.  Open the CFEE user interface and click  the **_Organizations_** page to create and manage organizations for that CFEE.

## Step 4: Add users to organizations and spaces
{: #add-users}

[Add users](https://console.bluemix.net/docs/cloud-foundry/add-users.html) to those organizations and spaces under specific role assignments controlling their level of access.  Before users can be added as members of organizations and spaces in an CFEE, those users must have prior access to the CFEE instance. See [Permissions](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Step 5: Deploy and view applications
{: #deploy-apps}

When you're ready, you can [deploy the app](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) with the {{site.data.keyword.Bluemix_notm}} command line interface.  View the list of deployed applications in the user interface, either in the context of a specific CFEE space, or globally across all CFEE instances.  You can also start, stop, or delete applications from those views.

## Step 6: Create or Add IBM Cloud service instances to CFEE spaces
{: #service-instances}

[Create services](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) or [Add existing services](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) available in the IBM Cloud account.  Once a service instance is available in a CFEE space, you can bind it to CFEE applications deployed in that space.

## Step 7: Bind applications to service instances
{: #bind-apps}

[Bind your app](https://console.bluemix.net/docs/cloud-foundry/binding.html) to a service instance alias in order to use the service's functions.

In the [Cloud Foundry dashboard](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") you can see a consolidated view of all the applications and services, both *public* and *enterprise*.  Once in the Cloud Foundry dashboard, click *Public* in the left navigation pane to see the public applications and services available in the IBM Cloud account.  Click on *Enterprise* to see all the CFEE environments, applications deployed into CFEE spaces, and services available to CFEE spaces.
{:tip}

## Step 8: Enable auditing and logging persistance (optional)
{: #enable-auditingandlogging}

Enable the environment for [auditing events](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) and [logging persistence](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#logging).

## Step 9: Create and secure Cloud Foundry domains (optional)
{: #create-domains}

Create [domains](https://console.bluemix.net/docs/cloud-foundry/domains.html#domains) for all applications in the CFEE (shared domains) or for a specific organization (private domains), and secure them with SSL certificates.


## Step 10: Install the Stratos Console to manage applications (optional)
{: #install-stratos}

The Stratos Console is an open source web-based tool for working with Cloud Foundry. The Stratos Console application can be optionally installed and used in a specific CFEE environment to manage its organizations, spaces, and applications.

Users with IBM Cloud administrator or editor roles in the CFEE instance can install the Stratos Console application in that CFEE instance.

To install the Stratos Console application:

1. Open the CFEE instance where you want to install the Stratos console.
2. Click **Install Stratos Console** on the overview page. The button is visible only to users with administrator or editor permissions to that CFEE instance.
3. In the Install Stratos Console dialog, select an installation option. You can install the Stratos console application either on the CFEE control plane or in one of the cells. Select a version of the Stratos console and the number of instances of the application to install. If you install the Stratos console app in a cell, you're prompted for the organization and space where to deploy the application.
4. Click **Install**.

The application takes about 5 minutes to install. Once installation is complete, a **Stratos Console** button appears in place of the _Install Stratos Console_ button on the overview page. The _Stratos Console_ button launches the console and is available to all users with access to the CFEE instance. Organization and space membership assignments may limit what a user can see and manage in the Stratos console.

To start the Stratos console:

1. Open the CFEE instance where the Stratos console was installed.
2. Click **Stratos Console** on the overview page.
3. The Stratos console is opened in a separate browser tab. When you open the console for the first time, you're prompted to accept two consecutive warnings because of self-signed certificates.
4. Click **Login** to open the console. No credentials are required since the application uses your {{site.data.keyword.Bluemix_notm}} credentials.


## Additional resources
{: #additional-resources}

You can perform some administrations tasks in a CFEE usig `ibmcloud CFEE` CLI commands. The commands allow you to get information about a CFEE instance, as well as to manage its organizations and spaces. See [IBM Cloud CLI CFEE command reference](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

You can find videos with in-depth discussions and demonstrations on various CFEE topics in the [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

Information on the CFEE API's in the CFEE [API documentation](https://console.bluemix.net/apidocs/cfaas){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").
