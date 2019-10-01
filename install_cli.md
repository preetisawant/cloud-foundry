---

copyright:

  years: 2015，2019

lastupdated: "2019-10-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
{:hide-in-docs: .hide-in-docs}
{:pre: .pre}
{:note: .note}
{:important: .important}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Download, modify, and redeploy your Cloud Foundry app with the command-line interface
{: #cf-deploy-cli}

<!-- This file is reused in the CF Public subcollection. -->

Use the {{site.data.keyword.Bluemix}} command-line interface (CLI) to download, modify, and redeploy your Cloud Foundry applications and service instances.
{:shortdesc}

Before you begin, [download and install the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started).


After you install the CLI, you can get started:

  1. {: hide-in-docs}[Download the code for your app](https://cloud.ibm.com) to a new directory to set up your development environment.

  2. Change to the directory where your code is located.

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">your_new_directory</var></code></pre>

  3.  Make changes to your app code as you see fit. For example, if you are using a {{site.data.keyword.Bluemix_notm}} sample application and your app contains the `src/main/webapp/index.html` file, you can modify it and edit "Thanks for creating ..." to say something new. Ensure the app runs locally before you deploy it back to {{site.data.keyword.Bluemix_notm}}.

    Take note of the `manifest.yml` file. When deploying your app back to {{site.data.keyword.Bluemix_notm}}, this file is used to determine your application’s URL, memory allocation, number of instances, and other crucial parameters. You can [read more about the manifest file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} in the Cloud Foundry documentation.

    Also pay attention to the `README.md` file, which contains details such as build instructions if applicable.

    Note: If your application is a Liberty app, you must build it before redeploying.

  4. Log in to {{site.data.keyword.cloud_notm}} with your IBMid. If you have multiple accounts, you are prompted to select which account to use. If you do not specify a region with the `-r` flag, you must also select a region.
  ```
  ibmcloud login
  ```
  {: codeblock}
  
  If your credentials are rejected, you might be using a federated ID. To log in with a federated ID, use the `--sso` flag. See [Logging in with a federated ID](/docs/iam/federated_id?topic=iam-federated_id#federated_id) for more details.
  {: tip}

  5. To access Cloud Foundry services, you must specify a Cloud Foundry org and space. You can run the following command to interactively identify the org and space:
  ```
  ibmcloud target --cf
  ```
  {: codeblock}

  Or, if you know which org and space that the service belongs to, you can use the following command:
  ```
  ibmcloud target -o <value> -s <value>
  ```
  {: codeblock}

   6. From `your_new_directory`, redeploy your app to {{site.data.keyword.Bluemix_notm}} by using the **`ibmcloud cf push`** command. For more information, see [**`ibmcloud cf push`**](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_apps#ibmcloud_app_push).

  7. Access your app by browsing to the app URL.
