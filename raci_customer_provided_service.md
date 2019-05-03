---

copyright:
  years: 2019
lastupdated: "2019-04-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Managing a customer-provided service
{: #managing-customer-provided-service}

Customer-provided services can be managed with respect to individual {{site.data.keyword.cfee_full_notm}} ({{site.data.keyword.cfee_short}}) instances. This includes adding, modifying and deleting these services. 

Within the [Open Service Broker specification](https://github.com/openservicebrokerapi/servicebroker), a type of service is more-properly known as a `service offering`. The term `service offering` will be used within this document.

## Common setup
{: #common-setup}

Whether you are adding, modifying or deleting custom service offerings, you need to perform the following steps:

1. Go to the {{site.data.keyword.cfee_short}} Overview page and locate the environment's API endpoint.

2. In the command line interface, set the API endpoint to your {{site.data.keyword.cfee_short}} environment's endpoint:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

3. Log into the {{site.data.keyword.cfee_short}} environment:

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  If you're using a federated ID, use the `-sso` option:

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
4. Ensure your currently-logged-in user has cf cloud_controller.admin authority in that {{site.data.keyword.cfee_short}} instance. This authority is automatically granted for users which are assigned the administrator or editor roles to a {{site.data.keyword.cfee_short}} instance.

## Adding a custom service offering
{: #add-custom-service-offering}

In addition to the common steps above, do the following to add a custom service offering:

1. Create an Open Service Broker compliant service broker that comforms to the [specification](https://github.com/openservicebrokerapi/servicebroker).

2. Ensure the service broker implementation is available to your {{site.data.keyword.cfee_short}} instance.

3. Create your service broker: 

  ```
  cf create-service-broker <service broker name> <service broker user> <service broker password> <service broker URL>
  ```
  {: pre}
  
4. Enable access to the service offering within your service broker: 

  ```
  cf enable-service-access <service offering name> <service plan name>
  ```
  {: pre}
  
5. Ensure your service offering is available. You can verify from either the command line or Stratos: 

  ```
  cf marketplace -s <service offering name>
  ```
  {: pre}
  
6. Create an instance of your service offering:

  ```
  cf create-service <service offering name> <service plan name> <service instance name>
  ```
  {: pre}


## Modifying a custom service offering
{: #modify-custom-service-offering}

In addition to the common steps above, do the following to modify a custom service offering:

1. Change your Open Service Broker compliant service broker that comforms to the [specification](https://github.com/openservicebrokerapi/servicebroker) to include your modified behavior.

2. Ensure the service broker implementation is available to your {{site.data.keyword.cfee_short}} instance.

3. Update your service broker: 

  ```
  cf update-service-broker <service broker name> <service broker user> <service broker password> <service broker URL>
  ```
  {: pre}
  
4. If you have added service offerings or service plans to your service broker, you will have to enable access to these new items within your service broker: 

  ```
  cf enable-service-access <service offering name> <service plan name>
  ```
  {: pre}
  
5. Ensure your service offering is available. You can verify from either the command line or Stratos: 

  ```
  cf marketplace -s <service offering name>
  ```
  {: pre}
  
6. Create an instance of your service offering:

  ```
  cf create-service <service offering name> <service plan name> <service instance name>
  ```
  {: pre}


## Deleting a custom service offering
{: #delete-custom-service-offering}

In addition to the common steps above, do the following to delete a custom service offering:

1. All related service instances of all service offerings provided by the service broker have to be previously deleted.

2. Delete your service broker: 

  ```
  cf delete-service-broker <service broker name>
  ```
  {: pre}
  
3. Ensure your service offering is no longer available. You can verify from either the command line or Stratos: 

  ```
  cf marketplace -s <service offering name>
  ```
  {: pre}
  
