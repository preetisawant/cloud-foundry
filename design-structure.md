---

copyright:

  years: 2018
lastupdated: "2018-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Design the structure of your IBM Cloud Foundry Enterprise Environment
{: #bpimplementation}

Instead of the traditional, strictly defined development, test, and production methodology, you can implement an environment where developers and testers can collaborate along with other team members. If you design the way you want to develop and deliver your apps, create spaces to fulfill that methodology. Instead of designing your environment from the organization level down, consider designing your {{site.data.keyword.cfee_full}} (CFEE) from the space level up.

Consider the scale and scope of the apps you plan to develop and deploy. A Cloud Foundry space can be used as a development environment for one or more apps that are tightly connected or defined. Apart from a development space, for example, you can create spaces for unit testing, performance testing, and integration testing. Spaces can also be defined for build, staging, and production. Each of the spaces that you create can be shared with different team members within the same organization.

Create separate Cloud Foundry organizations when you have people working on different business areas and where their activities do not overlap. If there are two independent groups, then creating an organization for each defines clear boundaries for the delivery and management of team players and resources. You can define an API to communicate between the organizations.

Cloud Foundry organizations can be created to match how you want to work rather than the structure within a company. Typically, company organizations can change but the development and maintenance of an application continues regardless. Design your {{site.data.keyword.cfee_full}} instance for the lifetime of the apps and not on your company organization structure.

Iterative development and deployment can result in apps that expand quickly. Your delivery process design must be able to scale up quickly and easily. You want continuous development with a fast deployment rate. Having your development and production spaces in the same CFEE organization provides access to the same resources. Managing different spaces within a single organization reduces the administration workload. The development, test, and operations personnel can collaborate easily if they are working within the same CFEE organization.

Implement a naming standard to clearly identify the organization and space usage. For example, you might include the type of cloud, the geographical region, the usage type (such as dev, test, prod), the application name, and the version or revision number. The organizations and spaces can then be easily identified for administration and access purposes.  

The number of spaces can multiply rapidly because of iterative development. You can define as many spaces as you need within an organization. If you plan to define many spaces, you might want to create an application to help manage the spaces. When the number of spaces exceeds sixty, you might want to consider defining another organization.

Have one person create and manage an organization, define the spaces, and grant team member access. A second person can be given the same access to maintain the environment when the organization manager is disabled.  

Identify all of the people who need access to each space and organization. Determine their role. The job role of a team member determines their authority. For example, a senior developer needs the authority to view and update the whole {{site.data.keyword.cfee_full}} development environment. However, a junior developer is limited as to what they can view and update.
