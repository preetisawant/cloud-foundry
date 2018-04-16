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

# Determine your spaces
{: #determinespaces}

Within an organization, spaces provide an extra level of boundary enforcement and abstraction.

A space is a reserved area in the organization where users can develop and run apps and services. You can create any number of spaces in an organization, and you can control the users that have access to a space. See [Spaces](/docs/account/orgs_spaces.html#orgsspacesusers) for more details.

If you plan to define many spaces, you might want to create an application to help manage the spaces. When the number of spaces exceeds sixty, you might want to consider defining another organization.

## Spaces for single-organization versus multi-organization
{: #spaceconsiderations}

When you adopt a single-organization architecture, the level of segregation and abstraction is provided by the spaces that you define within the organization. Consider the following guidance when you define spaces:

* Define a space to host a service that requires provisioning and configuring only once in the organization.
* Define spaces based on the delivery lifecycle.
  For example, you can define one or more spaces for apps that are being developed, one or more spaces for apps that are in the test phase, and one or more
  spaces for apps that are in production.
* If the delivery lifecycle boundary is not sufficient, you can achieve more segregation by defining one or more spaces per LOB and delivery phase.
* Identify if you need to enforce boundaries for different users groups.
  For example, your developers cannot develop the application and test it. You require a different set of users to test the application. In this scenario, you create two spaces, one for
  developers of the application and one for testers of the application. Then, grant each set of users access to the correct space.

When you implement a multi-organization architecture, you can segregate each organization by the LOB, the delivery lifecycle, or both. You can then define multiple spaces, which are based on the number of apps or projects that are delivered by the same department in the company. Consider the following guidance when you plan the spaces in an organization:

* Define a space to host a service that requires provisioning and configuring only once in the organization.
* Define a space per application, per group of related apps, or for a specific project.
* If you need to enforce boundaries for different users, define a space for each set of users. When a user is granted a developer role in a space, that user has full access to any resources and {{site.data.keyword.Bluemix_notm}} services) that are provisioned and running in that space. When you need to enforce tighter security to prevent users controlling every resource, consider defining different spaces. Within any of these spaces, you can provision {{site.data.keyword.Bluemix_notm}} services that are used by the apps running in that space.

## Space naming, restrictions, and management
{: #spaceadmin}

To define the different spaces for your cloud organization, consider the following guidance:

* Define and enforce a naming convention. For example, define a naming convention where the space name includes information about where the organization is located and the type of cloud. You can change the name of a space after it is created. If a space name is altered, notify all of the space team members about the change.
* Define the restrictions that apply to the space. For example, define the type of apps that can be developed, managed, and deployed in each space.
* Identify the manager of the space. You might want to delegate the space administration to more than one person.
