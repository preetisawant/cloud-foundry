---

copyright:
  years: 2017, 2019
lastupdated: "2019-07-03"

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:hide-in-docs: .hide-in-docs}

# Start coding with Node-RED
{: #startNodeRed}

<!-- This file is reused in the CF Public subcollection. -->

Before you can start coding with Node-RED, you must first configure the editor.
{:shortdesc}

## Open the Node-RED flow editor
{: #openEditor}

1. After your application starts, click **Routes URL** or enter the following URL in a browser to display the Node-RED landing page.
```
    http://<varname>&lt;yourhost></varname>.mybluemix.net
```
2. Click **Go to your Node-RED flow editor** to open the browser-based flow editor. The editor makes it easy to connect devices, APIs, and online services by using the wide range of nodes that are included in the palette.

##Customizing your Node-RED instance
{: #customize_instance}

Before you begin, install the [Cloud Foundry command-line interface](https://github.com/cloudfoundry/cli/releases).

  ![Cloud Foundry command line interface](images/btn_cf_commandline.svg "Download Cloud Foundry command-line interface"){: hide-in-docs}

1. {: hide-in-docs}[Download and extract your starter code](http://bluemix.net) to set up your development environment.

   ![Download Starter Code](images/btn_starter-code.svg "Download Starter Code"){: hide-in-docs}

2. Change to your new directory.
```
$ cd <varname>directory_name</varname></codeblock>
```
3. Connect to {{site.data.keyword.cloud}}.
```
$ cf api https://api.{DomainName}/
```
4. Log in to {{site.data.keyword.cloud_notm}}.
```
$ cf login -u <varname props="keyref(user_ID)">user_name</varname>
$ cf target -o <varname props="keyref(org_name)">org_name</varname> -s <varname props="keyref(space_name)">space_name</varname>
```
5. Deploy your app to {{site.data.keyword.cloud_notm}}.
```
<codeblock>$ cf push <varname props="keyref(app_name)">app_name</varname></codeblock>
```
6. Access your app to see your changes.
```
<varname props="keyref(host)">host</varname>.<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/Appdomainname"/>
```
