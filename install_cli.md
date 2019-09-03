---

copyright:

  years: 2015，2019

lastupdated: "2019-09-03"

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

Before you begin, download and install the {{site.data.keyword.Bluemix_notm}} CLI.

<p>
<a class="xref" href="https://clis.ng.bluemix.net" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_bx_commandline.svg" alt="Download {{site.data.keyword.Bluemix_notm}} CLI" /> </a>
</p>
{: hide-in-docs}

The CLI is not supported by Cygwin. Use the tool in a command-line window other than the Cygwin command-line window.
{: important}


After you install the CLI, you can get started:

  1. {: hide-in-docs}Download the code for your app to a new directory to set up your development environment.
    
    <p> 
    <a class="xref" href="https://cloud.ibm.com" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/btn_starter-code.svg" alt="Download application code" /> </a>
    </p>{: hide-in-docs}

  2. Change to the directory where your code is located.

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">your_new_directory</var></code></pre>

  3.  Make changes to your app code as you see fit. For example, if you are using a {{site.data.keyword.Bluemix_notm}} sample application and your app contains the `src/main/webapp/index.html` file, you can modify it and edit "Thanks for creating ..." to say something new. Ensure the app runs locally before you deploy it back to {{site.data.keyword.Bluemix_notm}}.

    Take note of the `manifest.yml` file. When deploying your app back to {{site.data.keyword.Bluemix_notm}}, this file is used to determine your application’s URL, memory allocation, number of instances, and other crucial parameters. You can [read more about the manifest file ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} in the Cloud Foundry documentation.

    Also pay attention to the `README.md` file, which contains details such as build instructions if applicable.

    Note: If your application is a Liberty app, you must build it before redeploying.

  4. Connect and log in to {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

  If you are using a federated ID, use the `-sso` option.

  <pre class="pre"><code class="hljs">bluemix login  -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</code></pre>

  You must add single or double quotes around `username`, `org_name`, and  `space_name` if the value contains a space, for example, `-o "my org"`.
  {: note}

  5. From <var class="keyword varname">your_new_directory</var>, redeploy your app to {{site.data.keyword.Bluemix_notm}} by using the **`ibmcloud app push`** command. For more information, see [**`ibmcloud app push`**](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_commands_apps#ibmcloud_app_push).

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></code></pre>

  6. Access your app by browsing to https://<var class="keyword varname" data-hd-keyref="app_url">app_url</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>.
