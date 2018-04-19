---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-18"

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

This getting started tutorial shows how to create an {{site.data.keyword.cfee_full_notm}}, onboard users, create an organization and spaces, deploy apps, and bind those apps to services.

## Permissions
{: #permissions}

To work with instances of the {{site.data.keyword.cfee_full_notm}}, service users must have the correct permissions. For more information, see [Permissions](permissions.html).

## Step 1: Creating your environment
{: #creating-environment}

The {{site.data.keyword.cfee_full_notm}} service is available in the {{site.data.keyword.Bluemix_notm}} catalog:
* Make sure that you are in the {{site.data.keyword.Bluemix_notm}} account where you want to create the environment and that you have the required access policies as described previously.
* Visit the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.stage1.bluemix.net/catalog).
* Locate the {{site.data.keyword.cfee_full_notm}} service in the catalog and click it to open the creation pages.

On the creation page:
* Provide a Name for the environment.
* Select the **Location** where the environment is to be deployed and the **Resource group** under which the environment is grouped.

Proceed to the second creation page, which includes the configuration fields for the container cluster where the {{site.data.keyword.cfee_full_notm}} is deployed:

This page includes fields for the Kubernetes cluster configuration. The name of the Kubernetes cluster is synchronized with the CFEE name you entered earlier.

Click **Create**, which opens the user interface for the environment and indicates the creation progress and status. The environment's creation status is also indicated in the {{site.data.keyword.Bluemix_notm}} dashboard, where the environment is listed.

The automated process that creates the environment deploys the hardware infrastructure on a container cluster, deploys the Cloud Foundry components into that cluster, and configures the environment to make it ready to use. The process takes between 45-60 minutes.

**Note:** The Kubernetes cluster on which the environment is deployed appears in the {{site.data.keyword.Bluemix_notm}} [dashboard](https://console.bluemix.net/dashboard/apps/). See more information about the [{{site.data.keyword.Bluemix_notm}} Container Service documentation](/docs/containers/cs_why.html#cs_ov).

## Step 2: Creating organizations and spaces

After you create the {{site.data.keyword.cfee_full_notm}}, see [Creating organizations and spaces](orgs-spaces.html) for information on how to structure the environment by creating organizations and spaces. Apps in an {{site.data.keyword.cfee_full_notm}} are scoped within specific spaces. In turn, a space exists within a specific organization. Members of an organization share a quota plan, apps, services instances, and custom domains.

## Step 3: Adding users to organizations and spaces

Then [add users](add-users.html) to those organizations and spaces under specific role assignments.  This allows you to control the level of access available to users in those organizations and spaces.

## Step 4: Deploying apps

When you're ready, you can [deploy the app](deploy-apps.html) with the {{site.data.keyword.Bluemix_notm}} command line interface.

## Step 5: Creating service instances

Create [service instances](add-serv-inst.html) to start service capabilities and make them available to your applications.

## Step 6: Binding and unbinding apps to service instances

[Bind your app](binding.html) to a service instance to use the service's functions.
