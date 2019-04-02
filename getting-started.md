---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Getting started tutorial
{: #getting-started}

{{site.data.keyword.cfee_full}} (CFEE) is a cloud platform for hosting apps and services in the cloud. {{site.data.keyword.cfee_full_notm}} makes it easy to scale apps as consumption grows, simplifying the runtime, middleware, and infrastructure so that you can focus on developing apps.
{: shortdesc}

This getting started tutorial shows how to create an {{site.data.keyword.cfee_full_notm}}, add users, create an organization and spaces, deploy apps, and bind those apps to services.

**Note:** The steps that follow are applicable to CFEEs created from the **Standard** plan.  If this CFEE was created from the **Eirini Technical Preview** plan, follow **only steps 1 through 6**, and step **11**. The capabilities described in steps 8 through 11 are not supported in the _Eirini Technical Preview_ plan.  See [Getting started with the Eirini technical preview](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).
The _Eirini Technical Preview_ plan allows you to explore a CFEE using native Kubernetes as the container scheduler (instead of Diego).  The Kubernetes scheduler is used in the CFEE to deploy and run apps in the Cloud Foundry application runtime, add users, create an organization and spaces, deploy apps, and bind those apps to services. 

## Step 1: Create your CFEE instance
{: #create-environment}

You can create an instance of the {{site.data.keyword.cfee_full_notm}} (CFEE) from the {{site.data.keyword.Bluemix_notm}} catalog. Before creating the CFEE instance visit the [Create environment](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment) documentation for guidance on preparing your {{site.data.keyword.Bluemix_notm}} account, ensuring the right permissions, and steps for creating the CFEE instance.


## Step 2: Create organizations and spaces
{: #create-orgsandspaces}

After you create the {{site.data.keyword.cfee_full_notm}}, see [Creating organizations and spaces](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html) for information on how to structure the environment by creating organizations and spaces. Apps in an {{site.data.keyword.cfee_full_notm}} are scoped within specific spaces. In turn, a space exists within a specific organization. Members of an organization share a quota plan, apps, services instances, and custom domains.

When you create an organization you assign a quota to it.  The quota sets limits on the resources (memory, cpu, etc.) available for that organization. You can assign a different quota at a later time. There is a set of pre-configured quotas available in every CFEE, but you can also create your own custom quotas in the **Quotas** page of the CFEE user interface.  You can make a custom quota the _Default_ quota by invoking the _Copy to default_ action from the quota's menu, which copies the values of the custom quota into the default quota.

**Note:** The _Cloud Foundry organizations_ page available from the **_Manage > Account > Cloud Foundry orgs_** menu located in the top IBM Cloud header is intended exclusively for public IBM Cloud organizations, **not for CFEE organizations**. CFEE organizations are managed within the _Organizations_ page of an CFEE instance.  Open the CFEE user interface and click  the **_Organizations_** page to create and manage organizations for that CFEE.

## Step 3: Add users to organizations and spaces
{: #add-users}

[Add users](https://console.bluemix.net/docs/cloud-foundry/add-users.html) to those organizations and spaces under specific role assignments controlling their level of access.  Before users can be added as members of organizations and spaces in an CFEE, those users must have prior access to the CFEE instance. See [Permissions](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Step 4: Deploy and view applications
{: #deploy-apps}

When you're ready, you can [deploy the app](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) with the {{site.data.keyword.Bluemix_notm}} command line interface.  View the list of deployed applications in the user interface, either in the context of a specific CFEE space, or globally across all CFEE instances.  You can also start, stop, or delete applications from those views.

## Step 5: Create or add IBM Cloud service instances to CFEE spaces
{: #service-instances}

[Create services](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) or [Add existing services](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) available in the IBM Cloud account.  Once a service instance is available in a CFEE space, you can bind it to CFEE applications deployed in that space.

## Step 6: Bind applications to service instances
{: #bind-apps}

[Bind your app](https://console.bluemix.net/docs/cloud-foundry/binding.html) to a service instance alias in order to use the service's functions.

In the [Cloud Foundry dashboard](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") you can see a consolidated view of all the applications and services, both *public* and *enterprise*.  Once in the Cloud Foundry dashboard, click *Public* in the left navigation pane to see the public applications and services available in the IBM Cloud account.  Click on *Enterprise* to see all the CFEE environments, applications deployed into CFEE spaces, and services available to CFEE spaces.
{:tip}

## Step 7: Enable auditing and logging persistance (optional)
{: #enable-auditingandlogging}

Enable the environment for [auditing events](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) and [logging persistence](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#logging).

## Step 8: Enable Monitoring tools (optional)
{: #enable-monitoring}

Monitoring tools are not automatically provisioned on CFEE instances v2.2.0 or later. CFEE administrators can [enable monitoring tools](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring) once the CFEE instance is created. The monitoring toolset includes Prometheus, Grafana and Alertmanager.

## Step 9: Create and secure Cloud Foundry domains (optional)
{: #create-domains}

Create [domains](https://console.bluemix.net/docs/cloud-foundry/domains.html#domains) for all applications in the CFEE (shared domains) or for a specific organization (private domains), and secure them with SSL certificates.

## Step 10: Configure the prioritization order of the Cloud Foundry buildbacks
{: #create-buildpacks}

Buildpacks provide the runtime support for applications deployed in a Cloud Foundry environment, automatically configuring the runtime for an application and handling its dependencies.  Cloud Foundry includes a set of buildpacks for common languages and frameworks.  [Learn more](https://docs.cloudfoundry.org/buildpacks/) about Cloud Foundry buildpacks.  

You can create and upload custom buildpacks in the **Buildpacks** page of the CFEE user interface. Buildpacks have an ordipnal position in the priority list.  During the staging of an application, Cloud Foundry checks the compatibility of the application against the set of buildpacks, starting with position 1. The compatibility checks proceeds down the priority list until it finds a compatible buildpack. Ensure that the priority sequence of the buildpack set meets the needs of your development teams.  You can change the position of a buildpack in the priority sequence by dragging and dropping the buildpack name into a different position.  You can also manage buildpacks through the [Cloud Foundry CLI](https://docs.cloudfoundry.org/adminguide/buildpacks.html).

## Step 11: Install the Stratos Console to manage applications (optional)
{: #install-stratos}

The Stratos Console is an open source web-based tool for working with Cloud Foundry. The Stratos Console application can be optionally installed and used in a specific CFEE environment to manage its organizations, spaces, and applications.

Users with IBM Cloud administrator or editor roles in the CFEE instance can install the Stratos Console application in that CFEE instance.

To install the Stratos Console application:

1. Open the CFEE instance where you want to install the Stratos console.
2. Click **Install Stratos Console** on the overview page. The button is visible only to users with administrator or editor permissions to that CFEE instance.
3. In the Install Stratos Console dialog, select an installation option. You can install the Stratos application either in a Cloud Foundry cell or in the Kubernetes cluster. Select a version of the Stratos console and the number of instances of the application to install. If you install the Stratos console app in a Cloud Foundry cell, you are prompted for the organization and space where to deploy the application.
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
