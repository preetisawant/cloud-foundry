---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Permissions
{: #permissions}

Before you begin creating and working with instances of the IBM Cloud Foundry Enterprise Environment service, the permissions of the administrator and the rest of the team must be set correctly.

## Permissions required to create a new environment
{: #perm-creating}

To create new instances of the IBM Cloud Foundry Enterprise Environment service, users must be granted access policies by the administrator of the account where the instance is to be created:

* Access to at least one resource group in the IBM Cloud account. Resource groups allow organizing resources into customized groupings to facilitate access control to those resources. You are prompted for a resource group when you create a new environment instance.
* Administrator or editor role to the IBM Cloud Foundry Enterprise Environment service in the resource group to which the environment is assigned. Users with either administrator or editor roles in the IBM Cloud Foundry Enterprise environment service can create and delete environments. But only users with an administration role can assign users to an IBM Cloud Foundry Enterprise Environment instance or change the roles that are assigned to users in that instance.
* Administrator or editor role to the IBM Cloud Container service in the resource group to which the environment is assigned. Instances of the IBM Cloud Foundry Enterprise Environment are deployed on container cluster infrastructure, which is provided by the IBM Cloud Container service. When you create an instance of the IBM Cloud Foundry Enterprise Environment service, the service automatically creates a Kubernetes cluster where the IBM Cloud Foundry Enterprise Environment is deployed. Access to the IBM Container service, specifically in the resource group to which the environment is assigned, is required for creating that cluster infrastructure.

To confirm that you have the required access policies to create an IBM Cloud Foundry Enterprise Environment instance:
1. Go to the **Manage > Users** menu in the IBM Cloud header to open the **Identity & Access** page.
2. In the Access policies tab, click the user who is creating the environment.
3. Confirm that access policies for the user who is creating the environment are consistent with the policies described previously.

The following screen illustrates access policies as they would appear in the Identity & Access page of the IBM Cloud that allow a user to create an IBM Cloud Foundry Enterprise Environment instance.

![Access policies](img/AccessPolicies_Creator.png)

## Permissions required to work with an environment
{: #perm-working}

To work with a instance of the IBM Cloud Foundry Enterprise Environment, users must be:
1. Members of the IBM Cloud account where the IBM Cloud Foundry Enterprise Environment instance was created.
2. Granted the following _Access Policies_ by the account administrator (see the _Identity & Access_ page under the **Manage > Users** menu in the IBM Cloud header to check your current account access policies):
  - Access to at least one resource group in the IBM Cloud account. Resource groups allow organizing resources into customized groupings to facilitate access control to those resources. You are prompted for a resource group when you create a new environment instance.
  - Users must be assigned access to the IBM Cloud Foundry Enterprise Environment service in the resource group under which the environment instance was created. The level of access and control that users have in an IBM Cloud Foundry Enterprise Environment instance depends on the role that is granted in the access policy:
     - Users assigned administrator or editor roles can create organizations, assign managers to organizations and spaces, have full permissions to all organizations and spaces within the environment, and perform operational actions by using the Cloud Controller API. These users are automatically granted _cloud_controller.admin scope_ in the Cloud Foundry _User Account and Authentication scope_.
     - Users assigned a viewer role can see that environment in the main IBM Cloud dashboard and can open its user interface. Users access to specific organizations and spaces within the environment is governed by the specific organization and spaces roles that are assigned by the managers of those organizations and spaces. For more information, see [Adding users to organizations](add_users.html).

The image illustrates the minimum access policies (as they would appear in the IBM Cloud _Identity & Access_ page) required to access an IBM Cloud Foundry Enterprise Environment.

![Access policies](img/AccessPolicies_User.png)

