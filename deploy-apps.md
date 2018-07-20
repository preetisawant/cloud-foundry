---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Deploying apps
{: #deploy_apps}

You can deploy applications to {{site.data.keyword.Bluemix}} with the command line interface or the integrated development environments (IDEs). You can also use application manifests to deploy applications. When you use an application manifest, you reduce the number of deployment details that you must specify every time that you deploy an application to {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Deploying applications with the Cloud Foundry command
{: #dep_apps}

Download and install the {{site.data.keyword.Bluemix}} command line interface. [Download the {{site.data.keyword.Bluemix_notm}} CLI](https://clis.ng.bluemix.net){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon").

After you install the command line interface, follow these steps:

1. Change to the directory where your code is located. `cd <your_directory>`
2. Go to the {{site.data.keyword.cfee_full}} Overview page and locate the environment's API endpoint.
3. In the command line interface, set the API endpoint to your environment's endpoint:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

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

  **Note**: You must add single or double quotation marks around `username`, `org_name`, and  `space_name` if the value includes a space, for example, `-o "my org"`.

5.  From `<your_new_directory>`, redeploy your app to {{site.data.keyword.Bluemix_notm}} by using the `bluemix app push` command. For more information about the `cf app push` command, see [Uploading your application](/docs/starters/upload_app.html).

  ```
  cf push <app_name>
  ```
  {: pre}

6.  Access your app by browsing to `https://<app_url>.<AppDomainName>`.

## Application manifest
{: #appmanifest}

Application manifests include options that are applied to the `cf push` command. You can use an application manifest to reduce the number of deployment details that you must specify every time that you push an application to {{site.data.keyword.Bluemix_notm}}.

In application manifests, you can specify options such as the number of application instances to create, the amount of memory and disk quota to allocate, and other environment variables. You can also use application manifests to automate application deployments. The default name of a manifest file is `manifest.yml`.

### Supported options in the manifest file

The following table shows the supported options that you can use in an application manifest file. If you choose to use a different file name other than `manifest.yml`, you must use the **-f** option with the `cf push` command. In the following example, `appManifest.yml` is the file name:

```
cf push -f appManifest.yml
```

| Options | Description | Usage or example |
|:----------|:--------------|:---------------|
| **buildpack** | The URL or name of the custom buildpack. | `buildpack:` *buildpack_URL* |
| **disk_quota** | The disk quota that is allocated for an application. The default value is 1 G. | `disk_quota: 500M` |
| **domain** | The domain name of the application in {{site.data.keyword.Bluemix_notm}}. | `domain:` ng.bluemix.net |
| **host** | The host name of the application in {{site.data.keyword.Bluemix_notm}}. This value must be unique in the {{site.data.keyword.Bluemix_notm}} environment. | `host:` *host_name* |
| **name** | The application name in {{site.data.keyword.Bluemix_notm}}. This value must be unique in the {{site.data.keyword.Bluemix_notm}} environment. | `name:` *appname* |
| **path** | The location of your application. This value can be a relative path or absolute path. | `path:` *path_to_application* |
| **command** | The custom start command for your application, or the command to run script files. | `command:` *custom_command* `command:` *bash ./run.sh* |
| **memory** | The amount of memory to allocate for the application. The default value is 1G. | `memory: 512M` |
| **instances** | The number of instances to be created for your application. | `instances: 2` |
| **timeout** | The maximum amount of time in seconds that is used to start the application. The default value is 60 seconds. | `timeout: 80` |
| **no-route** | A Boolean value to prevent a route from being assigned to the application if the application is just running background. The default value is **false**. | `no-route: true` |
| **random-route** | A Boolean value to assign a random route to the application. The default value is **false**. | `random-route: true` |
| **services** | The services to bind to the application. | `services: - mysql_maptest` |
| **env** | The custom environment variables for the application. | `env: DEV_ENV: production` |
{: caption="Table 1. Supported options in the manifest YAML file" caption-side="top"}

### A sample manifest.yml file
{: #sample}

The following example shows a manifest file for a Node.js application that uses the built-in community Node.js buildpack in {{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}