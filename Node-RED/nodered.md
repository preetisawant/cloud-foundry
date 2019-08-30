---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Creating apps with the Node-RED Starter
{: #gettingstarted-nodered}

<!-- This file is reused in the CF Public subcollection. -->

Node-RED provides a browser-based flow editor that makes it easy to connect devices, APIs, and online services by using the wide range of nodes in the palette. You can deploy the flows to the Node.js runtime environment with a single click. This starter application provides a version of Node-RED that is customized to run in {{site.data.keyword.cloud}}.   
{:shortdesc}

Use the editor to create flows right away. You can also customize Node-RED itself. For more information, see the [Node-RED site ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://nodered.org/){: new_window}{: new_window}.

## Using Node-RED
{: #usingNodeRed}

Complete the following steps to use the Node-RED starter application from the {{site.data.keyword.cloud_notm}} console.

1. Create a Node-RED starter application and download the starter code:
  1. Click **Create App** to deploy a Node-RED starter application.
  2. Provide the app name and host in the prompt.
2. After your application starts, click **Routes URL** or enter the following URL in a browser to display the Node-RED landing page.
  ```
    http://<varname>&lt;yourhost></varname>.mybluemix.net
  ```
3. Click **Go to your Node-RED flow editor** to open the browser-based flow editor. The editor makes it easy to connect devices, APIs, and online services by using the wide range of nodes that are included in the palette.

## Customizing your Node-RED instance
{: #customizingNodeRed}

You can customize your Node-RED instance for your needs. For example, you can replace the landing page with your own page, add http authentication to the flow editor, or add new nodes to the palette.

1. Download the application code by clicking **Start Coding > Download Starter Code** on the application's overview page.
2. Ensure that the Cloud Foundry command-line interface (CLI) is installed. See [the instructions for installing the command line interface](/docs/starters/?topic=starters-download-modify-and-redeploy-your-cloud-foundry-app-with-the-command-line-interface) for more information.
3. Log in to the {{site.data.keyword.cloud_notm}} environment.
  ```
  $ cf login -a https://api.<ph conref="cloudoeconrefs.dita#cloudoeconrefs/domainname"></ph> -u <varname props="keyref(user_ID)">&lt;your user ID></varname> -p <varname>*****</varname> -o <varname props="keyref(org_name)">&lt;your org name></varname> -s <varname
  props="keyref(space_name)">&lt;your space name></varname>
  ```
4. Modify the application, and deploy it again. The default application landing page describes some of the customization. Nodes and packages can be added to your instance of NodeRED by adding them to the list of dependencies.  After you complete your changes, use the CLI to deploy the application to {{site.data.keyword.cloud_notm}} again.

  For example, run the following command in the root directory of the application:
  ```
  $ cf push <varname>&lt;yourappname></varname>
  ```

## Access the VCAP_SERVICES environment
{: #VCAP}

To access the VCAP_SERVICES environment from a Node-RED flow, you must add the environment variable to the Function node's global context.

1. Edit your "bluemix-settings.js" and add an entry to the *functionGlobalContext* property to parse VCAP_SERVICES.
2. Redeploy your Node-RED application.

  ```
  functionGlobalContext: { VCAP_SERVICES: JSON.parse(process.env.VCAP_SERVICES)}
  ```

After you redeploy Node-RED, you can  access VCAP_SERVICES in a Function node as the *context.global.VCAP_SERVICES* variable.
