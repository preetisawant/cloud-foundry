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
* Administrator or editor role to the {{site.data.keyword.Bluemix_notm}} Container service in the resource group to which the environment is assigned. Instances of the {{site.data.keyword.cfee_full_notm}} are deployed on container cluster infrastructure, which is provided by the {{site.data.keyword.Bluemix_notm}} Container service. When you create an instance of the {{site.data.keyword.cfee_full_notm}} service, the service automatically creates a Kubernetes cluster where the {{site.data.keyword.cfee_full_notm}} is deployed. Access to the IBM Container service, specifically in the resource group to which the environment is assigned, is required for creating that cluster infrastructure.

To confirm that you have the required access policies to create an {{site.data.keyword.cfee_full_notm}} instance:
1. Go to the **Manage > Users** menu in the {{site.data.keyword.Bluemix_notm}} header to open the **Identity & Access** page.
2. In the Access policies tab, click the user who is creating the environment.
3. Confirm that access policies for the user who is creating the environment are consistent with the policies described previously.

The following screen illustrates access policies as they would appear in the Identity & Access page of the {{site.data.keyword.Bluemix_notm}} that allow a user to create an {{site.data.keyword.cfee_full_notm}} instance.

![Access policies](img/AccessPolicies_Creator.png)

## Permissions required to work with an environment
{: #perm-working}

To work with a instance of the {{site.data.keyword.cfee_full_notm}}, users must be:
1. Members of the {{site.data.keyword.Bluemix_notm}} account where the {{site.data.keyword.cfee_full_notm}} instance was created.
2. Granted the following _Access Policies_ by the account administrator (see the _Identity & Access_ page under the **Manage > Users** menu in the {{site.data.keyword.Bluemix_notm}} header to check your current account access policies):
  - Access to at least one resource group in the {{site.data.keyword.Bluemix_notm}} account. Resource groups allow organizing resources into customized groupings to facilitate access control to those resources. You are prompted for a resource group when you create a new environment instance.
  - Users must be assigned access to the {{site.data.keyword.cfee_full_notm}} service in the resource group under which the environment instance was created. The level of access and control that users have in an {{site.data.keyword.cfee_full_notm}} instance depends on the role that is granted in the access policy:
     - Users assigned administrator or editor roles can create organizations, assign managers to organizations and spaces, have full permissions to all organizations and spaces within the environment, and perform operational actions by using the Cloud Controller API. These users are automatically granted _cloud_controller.admin scope_ in the Cloud Foundry _User Account and Authentication scope_.
     - Users assigned a viewer role can see that environment in the main {{site.data.keyword.Bluemix_notm}} dashboard and can open its user interface. Users access to specific organizations and spaces within the environment is governed by the specific organization and spaces roles that are assigned by the managers of those organizations and spaces. For more information, see [Adding users to organizations](add-users.html).

The image illustrates the minimum access policies (as they would appear in the {{site.data.keyword.Bluemix_notm}} _Identity & Access_ page) required to access an {{site.data.keyword.cfee_full_notm}}.

![Access policies](img/AccessPolicies_User.png)

