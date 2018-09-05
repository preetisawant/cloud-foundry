---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Permissions
{: #permissions}

Before you begin creating and working with instances of the {{site.data.keyword.cfee_full}} service, the permissions of the administrator and the rest of the team must be set correctly.

## Permissions required to create a new environment
{: #perm-creating}

To create new instances of the {{site.data.keyword.cfee_full_notm}} service, users must be granted access policies by the administrator of the account where the instance is to be created:

* Access to at least one resource group in the {{site.data.keyword.Bluemix}} account. Resource groups allow organizing resources into customized groupings to facilitate access control to those resources. You are prompted for a resource group when you create a new environment instance.

* Administrator or editor role to the {{site.data.keyword.cfee_full_notm}} service in the resource group to which the environment is assigned. Users with either administrator or editor roles in the {{site.data.keyword.cfee_full_notm}} service can create and delete environments. But only users with an administration role can assign users to an {{site.data.keyword.cfee_full_notm}} instance or change the roles that are assigned to users in that instance.

* Administrator or editor role to the IBM Cloud Object Storage service.  An instance of IBM Cloud Object Storage service is used to store data generated during the creation of your ICFEE application containers (e.g. uploaded application packages, buildpacks, and compiled executables).

* An instance of Compose for PostgreSQL service is created and used to store data related to your CFEE instance (e.g., auditing application deployment, start and stop events; keeping records of CFEE user membership, organizations, spaces, applications and service connections).  That instance of the Compose for PostgreSQL service is deployed in a public Cloud Foundry organization (unrelated to CFEE organizations). The public Cloud Foundry organization where the Compose for PostgresSQL instance is deployed has a specific name: **_cfee-`<accountId>`_**, where "accountId" is the id of the IBM Cloud account where the CFEE (along with the Compose for PostgreSQL service instance) is to be provisioned.  The public Cloud Foundry organization is created automatically when the account owner creates a CFEE instance.  However, any user of the IBM Cloud account who creates CFEE instances but is not the account owner needs to be added to that public Cloud Foundry organization with a **manager role**.   

   To add a user from the IBM Cloud account to the _cfee-`<accountId>`_ public organization:
    * Go to [**Manage > Account > Cloud Foundry Orgs**](https://console.bluemix.net/account/organizations).
    * Click the **_cfee-`<accountId>`_** organization.
    * Go to the **Users** tab at the top of the page.
    * Find the user who needs to create CFEE instances and click the **Manager** checkbox for that user. If the user you want to be able to create CFEE instances is not in the list, click **Add or invite user** above the table to add or invite users to the **_cfee-`<accountId>`_** organization.

   **Note**: Although the _cfee-<accountId>_ public organization is implicitely and automatically created when the IBM Cloud account owner creates a CFEE instance, the account owner could instead create the public Cloud Foundry organization manually, without the need to create a CFEE instance. The IBM Cloud account owner can create the public _cfee-`<accountId>`_ in the **Manage > Account > Cloud Foundry Orgs** page. If you create the public organization, make sure that you name it exactly as _cfee-`<accountId>`_. To  find the IBM Cloud account ID, go to the [**Manage > Account > Cloud Foundry Orgs**](https://console.bluemix.net/account/organizations) page and look at the page URL available in your browser.  The IBM Cloud account ID is the set of alphanumeric values following the `=` in the page URL. Alternatively, you can go to the __Manage > Account > Users__ and hover over the tooltip to the left of the _Account_ name located at page's top-right corner.
   
* Administrator or editor role to the {{site.data.keyword.Bluemix_notm}} Container service in the resource group to which the environment is assigned. Instances of the {{site.data.keyword.cfee_full_notm}} are deployed on container cluster infrastructure, which is provided by the {{site.data.keyword.Bluemix_notm}} Container service. When you create an instance of the {{site.data.keyword.cfee_full_notm}} service, the service automatically creates a Kubernetes cluster where the {{site.data.keyword.cfee_full_notm}} is deployed. Access to the IBM Container service, specifically in the resource group to which the environment is assigned, is required for creating that cluster infrastructure.

To confirm that you have the required access policies to create an {{site.data.keyword.cfee_full_notm}} instance:
1. Go to the [**Manage > Account > Users**](https://console.bluemix.net/iam/#/users) menu in the {{site.data.keyword.Bluemix_notm}} header to open the **Identity & Access** page.
2. In the Access policies tab, click the user who is creating the environment.
3. Confirm that access policies for the user who is creating the environment are consistent with the policies described previously.

The following screen illustrates access policies as they would appear in the Identity & Access page of the {{site.data.keyword.Bluemix_notm}} that allow a user to create an {{site.data.keyword.cfee_full_notm}} instance.

![Access policies](img/AccessPolicies_Creator.png)

## Permissions required to work with an environment
{: #perm-working}

To work with a instance of the {{site.data.keyword.cfee_full_notm}}, users must be:
1. Members of the {{site.data.keyword.Bluemix_notm}} account where the {{site.data.keyword.cfee_full_notm}} instance was created.
2. Granted the following _Access Policies_ by the account administrator (see the _Identity & Access_ page under the [**Manage > Account > Users**](https://console.bluemix.net/iam/#/users) menu in the {{site.data.keyword.Bluemix_notm}} header to check your current account access policies):
  - Access to at least one resource group in the {{site.data.keyword.Bluemix_notm}} account. Resource groups allow organizing resources into customized groupings to facilitate access control to those resources. You are prompted for a resource group when you create a new environment instance.
  - Users must be assigned access to the {{site.data.keyword.cfee_full_notm}} service in the resource group under which the environment instance was created. The level of access and control that users have in an {{site.data.keyword.cfee_full_notm}} instance depends on the role that is granted in the access policy:
     - Users assigned administrator or editor roles can create organizations, assign managers to organizations and spaces, have full permissions to all organizations and spaces within the environment, and perform operational actions by using the Cloud Controller API. These users are automatically granted _cloud_controller.admin scope_ in the Cloud Foundry _User Account and Authentication scope_.
     - Users assigned a viewer role can see that environment in the main {{site.data.keyword.Bluemix_notm}} dashboard and can open its user interface. Users access to specific organizations and spaces within the environment is governed by the specific organization and spaces roles that are assigned by the managers of those organizations and spaces. For more information, see [Adding users to organizations](add-users.html).

The image illustrates the minimum access policies (as they would appear in the {{site.data.keyword.Bluemix_notm}} _Identity & Access_ page) required to access an {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_User.png)

