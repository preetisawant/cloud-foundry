---

copyright:
  years: 2018
lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}    


# Managing domains
{: #domains}

[Learn about domains](https://docs.cloudfoundry.org/devguide/deploy-apps/routes-domains.html){: new_window} ![External link icon](../icons/launch-glyph.svg "External link icon") and how they work in Cloud Foundry.

There are two types of Cloud Foundry domains:
* Shared domains available to any application in any space within the {{site.data.keyword.cfee_full_notm}}.  To access the shared domains go to the **Domains** page in the left navigation pane of the UI (under *Operations*).
* Private domains available only to applications and spaces within a specific organization.  To access the domains within an organization, go to the **Organizations** page in the left navigation pane of the UI, open the organization, and go to the **Domains** tab.

## Creating and deleting domains
{: #create-domains}

To create a shared domains, go to **Domains** in the left navigation pane of the {{site.data.keyword.cfee_full_notm}}.  

To create a private domain, go to the **Organizations** page in the left navigation pane of the UI, open the organization, and go to the **Domains** tab.

Once in the _Domains_ page (for shared domains) or in the _Domains_ tab of a specific organization (for private domains) click **Create domain** to create a domain, and enter a unique name.

**Note:** Domain names must be unique accross the entire scope of the {{site.data.keyword.cfee_full_notm}}.  That is, a private domain cannot take the name of any shared or private domain within a given {{site.data.keyword.cfee_full_notm}}

You can also create a shared domain from the Cloud Foundry CLI by issuing the following command:
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
You can create a private domain from the Cloud Foundry CLI by issuing the following command:
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**Note:** Domains created from the Cloud Foundry CLI will be reflected in UI immediately but may take up to 1 hour to become effective.

To delete a domain, go to the menu located at the far right of the table row corresponding to the domain you want to delete, and select **Delete domain**.
  
You can also delete a shared domain from the CLoud Foundry CLI by issuing the following command:
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## Uploading SSL certificates
 {: #upload-certificates}
 
You can upload an SSL certificate for a domain (shared or private). Click **Upload** in the table row corresponding to the domain to which the certificate is being added, select the file containing the certificate and the file containing the private key.

Starting in CFEE v3.1.0, you can whitelist a bundle of client certificates along with the Certificate Authority (CA) certificates required to authenticate those client certificates.  This provides customers a convenient way to create mutual Transport Layer Security (TLS) authentication, scoping the authentication to specific custom domains. This enables customers more granular control over client access to their Cloud Foundry applications.
In the _Upload certificate_ dialog, click **Load leaf certificates**" to upload a file containing one or more client certificates. Click **Load certificate signing tree** to upload a file containing one or more CA certificates used to authenticate the client certificates. The list of whitelisted users will be shown below.
{: important}

 ## Setting up a custom domain for app routes
 {: #custom-domains}
  
Perform the following to setup a custom domain for the app routes in a CFEE:

1. Configure DNS for the custom domain to point to the CFEE default domain (see the _Domains_ page in CFEE user interface).
2. In the CFEE _Domains_ page, register the custom domain's URL.
3. Optionally, add SSL certificate.
3. Add a route to the app through either the _Stratos console_ or the `cf` CLI.
