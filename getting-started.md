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

This getting started tutorial shows how to create an {{site.data.keyword.cfee_full_notm}}, add users, create an organization and spaces, deploy apps, and bind those apps to services.

## Understanding permissions
{: #permissions}

To work with instances of the {{site.data.keyword.cfee_full_notm}}, service users must have the correct permissions. For more information, see [Permissions](permissions.html).

## Step 1: Ensuring that the {{site.data.keyword.Bluemix_notm}} account can create infrastructure resources
{: #accountprep-environment}

ICFEE instances are deployed on infrastructure resources, which are Kubernetes worker nodes from the IBM Container service. The IBM Cloud account under which the ICFEE instance is created must allow creation of infrastructure resources, such as a Pay-As-You-Go or Subscription account. For more information, see [Account types](https://console.bluemix.net/docs/account/index.html#accounts). The cost of those infrastructure resources shows up in your IBM Cloud invoice.

If you have a SoftLayer account, you can link that SoftLayer account with the IBM Cloud account. To link the IBM Cloud and SoftLayer accounts:

1. Get the SofLayer account's user name and API Key by accessing the [SoftLayer console](https://control.softlayer.com). Once you log in to SoftLayer, select the account you want to link to the {{site.data.keyword.Bluemix_notm}} account. Selecting the account opens the account's profile page. Scroll down to the end of the page to find the account's user name and API key. If you don't have an API key, you can generate it if you're the account owner. If you're not the account owner, ask the account owner to generate it.
2. Log in to {{site.data.keyword.Bluemix_notm}} from the command line. If your organization uses a federated login, you might need to use the `-sso` option.

  ```
  ibmcloud login
  ```

3. In the command line interface, initialize the container service:

  ```
  ibmcloud cs init
  ```

4. Set your SoftLayer credentials in the IBM Container Service registry:

  ```
  ibmcloud cs credentials-set --infrastructure-username <SofLayer_username> --infrastructure-api-key <SoftLayer_api_key>
  ```

**Note:** You must have sufficient permissions in the SoftLayer account to create a regular Kubernetes cluster from the IBM Container service. If you don't, ask the SoftLayer account administrator, or the user who gave you access to the SoftLayer account to grant you those additional permissions.

## Step 2: Creating your ICFEE instance
{: #creating-environment}

Before you create your ICFEE, make sure that you're in the {{site.data.keyword.Bluemix_notm}} account where you want to create the environment and that you have the access policies that you need.

1. Open the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.bluemix.net/catalog).
2. Locate the {{site.data.keyword.cfee_full_notm}} service in the catalog and click it to open the creation page.
3. On the creation page, provide a name for the environment.
4. Then, select the **Location** where the environment is to be deployed and the **Resource group** under which the environment is grouped.
5. On the second creation page, which includes the configuration fields for the container cluster where the {{site.data.keyword.cfee_full_notm}} is deployed. Add information to the fields for the Kubernetes cluster configuration. The name of the Kubernetes cluster is synchronized with the ICFEE name you entered earlier.
6. Click **Create**, which opens the environment dashboard and indicates the creation progress and status. The environment's creation status is also indicated in the {{site.data.keyword.Bluemix_notm}} dashboard, where the environment is listed.

The automated process that creates the environment deploys the hardware infrastructure on a container cluster, deploys the Cloud Foundry components into that cluster, and configures the environment to make it ready to use. The process takes 45 - 60 minutes.

**Note:** The Kubernetes cluster on which the environment is deployed appears in the {{site.data.keyword.Bluemix_notm}} [dashboard](https://console.bluemix.net/dashboard/apps/). For more information, see [{{site.data.keyword.Bluemix_notm}} Container Service documentation](/docs/containers/cs_why.html#cs_ov).

## Step 3: Creating organizations and spaces

After you create the {{site.data.keyword.cfee_full_notm}}, see [Creating organizations and spaces](orgs-spaces.html) for information on how to structure the environment by creating organizations and spaces. Apps in an {{site.data.keyword.cfee_full_notm}} are scoped within specific spaces. In turn, a space exists within a specific organization. Members of an organization share a quota plan, apps, services instances, and custom domains.

## Step 4: Adding users to organizations and spaces

Then, [add users](add-users.html) to those organizations and spaces under specific role assignments. You can control the level of access available to users in those organizations and spaces.

## Step 5: Deploying applications

When you're ready, you can [deploy the app](deploy-apps.html) with the {{site.data.keyword.Bluemix_notm}} command line interface.

## Step 6: Creating service instances

Create [service instances](add-serv-inst.html) to start service functions and make them available to your applications.

## Step 7: Binding applications to service instances

[Bind your app](binding.html) to a service instance to use the service's functions.

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
