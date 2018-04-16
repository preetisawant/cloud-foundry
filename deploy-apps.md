---

copyright:
  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Deploying apps
{: #deploy_apps}

Download and install the IBM Cloud command line interface. [Download the IBM Cloud CLI](https://clis.ng.bluemix.net){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

After you install the command line interface, follow these steps:

1. Change to the directory where your code is located. `cd <your_directory>`
2. Go to the IBM Cloud Foundry Enterprise environment _Overview_ page and locate the environment's _API endpoint_.
3. In the command line interface, set the API endpoint to your environment's endpoint:
 ```
cf api <api_enpoint>
 ```
4. Log in to the environment
  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  If you're using a federated ID, use the `-sso` option.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **Note**: You must add single or double quotation marks around `username`, `org_name`, and  `space_name` if the value contains a space, for example, `-o "my org"`.

5.  From `<your_new_directory>`, redeploy your app to {{site.data.keyword.Bluemix_notm}} by using the `bluemix app push` command. For more information about the `cf app push` command, see [Uploading your application](/docs/starters/upload_app.html).

  ```
  cf push <app_name>
  ```
  {: pre}

6.  Access your app by browsing to `https://<app_url>.<AppDomainName>`.
