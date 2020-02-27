---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-12"

keywords: IBM Cloud, Cloud Foundry Enterprise Environment

subcollection: cloud-foundry

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Open Source Tools for Managing Cloud Foundry

## The Stratos Console
{: #stratos}

The Stratos Console is an open source web-based tool for working with Cloud Foundry. The Stratos Console application can be installed and used in a specific CFEE environment to manage its organizations, spaces, and applications.

## Installing the Stratos Console
{: #install-stratos}

Users with IBM Cloud administrator or editor roles in the CFEE instance can install the Stratos Console application in that CFEE instance.

To install the Stratos Console application:

1. Open the CFEE instance where you want to install the Stratos console.
2. Click **Install Stratos Console** on the overview page. The button is visible only to users with administrator or editor permissions to that CFEE instance.
3. In the Install Stratos Console dialog, select an installation option. You install Stratos  as a Cloud Foundry application. Select the number of instances of the application to install. Since Stratos is installed as a Cloud Foundry application, you are also prompted for the organization and space in which to deploy the application.
4. Click **Install**.

The application takes about 5 minutes to install. Once installation is complete, a **Stratos Console** button appears in place of the _Install Stratos Console_ button on the overview page. The _Stratos Console_ button launches the console and is available to all users with access to the CFEE instance. Organization and space membership assignments may limit what a user can see and manage in the Stratos console.

## Starting the Stratos Console

To start the Stratos console:

1. Open the CFEE instance where the Stratos console was installed.
2. Click **Stratos Console** on the overview page.
3. The Stratos console is opened in a separate browser tab. When you open the console for the first time, you're prompted to accept two consecutive warnings because of self-signed certificates.
4. Click **Login** to open the console. No credentials are required since the application uses your {{site.data.keyword.Bluemix_notm}} credentials.

## Uninstalling the Stratos Console

To uninstall the Stratos console:

1. Login with the `cf` CLI.
2. Target the org and space into which you deployed Stratos.
3. You can verify that you have targeted the correct space by running `cf apps` - the Stratos console is deployed as an application named `stratos-console`.
4. Remove Stratos by running `cf delete stratos-console` and responding to the prompts which follow.
