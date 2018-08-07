---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Getting started tutorial
{: #getting-started}

{{site.data.keyword.cfee_full}} (Experimental) is a cloud platform for hosting apps and services in the cloud. {{site.data.keyword.cfee_full_notm}} makes it easy to scale apps as consumption grows, simplifying the runtime, middleware, and infrastructure so that you can focus on developing apps.
{: shortdesc}

This getting started tutorial shows how to create an {{site.data.keyword.cfee_full_notm}}, add users, create an organization and spaces, deploy apps, and bind those apps to services.

## Understanding permissions
{: #permissions}

To work with instances of the {{site.data.keyword.cfee_full_notm}}, service users must have the correct permissions. For more information, see [Permissions](/docs/cloud-foundry/permissions.html).

## Step 1: Ensuring that the {{site.data.keyword.Bluemix_notm}} account can create infrastructure resources
{: #accountprep-environment}

ICFEE instances are deployed on infrastructure resources, which are Kubernetes worker nodes from the IBM Container service.  [Prepare your IBM Cloud account](/docs/cloud-foundry/prepare-account.html) to ensure that it can create the infrastructure resources necessary for an ICFEE instance.

## Step 2: Creating your ICFEE instance
{: #creating-environment}

Before you create your ICFEE, make sure that you are in the {{site.data.keyword.Bluemix_notm}} IBM Cloud account where you want to create the environment and that you have the required access policies (per step 1 above).

1. Open the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.bluemix.net/catalog).
2. Locate the {{site.data.keyword.cfee_full_notm}} service in the catalog and click it to open the overview page for the service.
3. The first page of the creation page provides an overview of the main features of the service. Click **Continue**.
4. Configure the instance to be created by providing the following:
    * Select a plan (plan availability may be restricted during the service's _experimental_ phase).
    * Enter a **Name** for the service instance.
    * Select a **Location** where the service instance is to be provisioned.
    * Select the **Number of cells** for the Cloud Foundry environment.
    * Select the **Machine type**, which determines the size of the Cloud Foundry cells (CPU and memory). The availability of machine types may be restricted during the service's _experimental_ phase.
    * Select a **Resource group** under which the environment is grouped. Only those resource groups to which you have access in the current IBM Cloud account will be listed in the _Resourouce groups_ dropdown, which means that you need to have permission to access at least one resource group in the account to be able to create an ICFEE. 
5. Optionally, open the **Infrastructure** section to see the properties of the Kubernetes cluster supporting the ICFEE instance. Note that the **Number of worker nodes** equals the number of cells plus 2 (two of the provisioned Kubernetes worker nodes support the ICFEE control plane).
5. The **Order Summary** in the right-hand side of the page reflects the cost of the ICFEE instance and the estimated total.
6. Click **Create**, which opens the environment dashboard and indicates the creation progress and status. The environment's creation status is also indicated in the {{site.data.keyword.Bluemix_notm}} dashboard, where the environment is listed.

The automated process that creates the environment deploys the hardware infrastructure on a container cluster, deploys the Cloud Foundry components into that cluster, and configures the environment to make it ready to use. The process takes 45 - 60 minutes.

**Note:** The Kubernetes cluster on which the environment is deployed appears in the {{site.data.keyword.Bluemix_notm}} [dashboard](https://console.bluemix.net/dashboard/apps/). For more information, see [{{site.data.keyword.Bluemix_notm}} Container Service documentation](/docs/containers/cs_why.html#cs_ov).

## Step 3: Creating organizations and spaces

After you create the {{site.data.keyword.cfee_full_notm}}, see [Creating organizations and spaces](/docs/cloud-foundry/orgs-spaces.html) for information on how to structure the environment by creating organizations and spaces. Apps in an {{site.data.keyword.cfee_full_notm}} are scoped within specific spaces. In turn, a space exists within a specific organization. Members of an organization share a quota plan, apps, services instances, and custom domains.

## Step 4: Adding users to organizations and spaces

Then, [add users](/docs/cloud-foundry/add-users.html) to those organizations and spaces under specific role assignments. You can control the level of access available to users in those organizations and spaces.

## Step 5: Deploying applications

When you're ready, you can [deploy the app](/docs/cloud-foundry/deploy-apps.html) with the {{site.data.keyword.Bluemix_notm}} command line interface.

## Step 6: Creating service instances

Create [service instances](/docs/cloud-foundry/add-serv-inst.html) to start service functions and make them available to your applications.

## Step 7: Binding applications to service instances

[Bind your app](/docs/cloud-foundry/binding.html) to a service instance to use the service's functions.

## Step 8: Installing the Stratos Console to manage applications (optional)

The Stratos Console is an open source web-based application to manage Cloud Foundry. The Stratos Console application can be optionally installed and used in a specific ICFEE environment to manage its organizations, spaces, and applications.

Users with IBM Cloud administrator or editor roles in the ICFEE instance can install the Stratos Console application in that ICFEE instance. To install the Stratos Console application:

1. Open the ICFEE instance where you want to install the Stratos console.
2. Click **Install Stratos Console** on the overview page. The button is visible only to users with administrator or editor permissions to that ICFEE instance.
3. In the Install Stratos Console dialog, select an installation option. You can install the Stratos console application either on the ICFEE control plane or in one of the cells. Select a version of the Stratos console and the number of instances of the application to install. If you install the Stratos console app in a cell, you're prompted for the organization and space where to deploy the application.
4. Click **Install**.

The app takes about 5 minutes to install. Once the installation is complete, a **Stratos Console** button appears in place of the **Install Stratos Console** button on the overview page to start the application. The **Stratos Console** button is available to all users with access to the ICFEE instance. However, the organization and space membership assignments limit what a user can see in manage in the Stratos console.

Start the Stratos console:

1. Open the ICFEE instance where the Stratos console was installed.
2. Click **Stratos Console** on the overview page.
3. The Stratos console is opened in a separate browser tab. When you open the console for the first time, you're prompted to accept two consecutive warnings because of self-signed certificates.
4. Click **Login** to open the console. No credentials are required since the application uses your {{site.data.keyword.Bluemix_notm}} credentials.

What you can see and manage is limited by your organizations and space membership and roles.
