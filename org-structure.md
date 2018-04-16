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

# Determine your organization architecture
{: #orgstructure}

To design an environment that uses {{site.data.keyword.Bluemix_notm}} Public, {{site.data.keyword.Bluemix_dedicated_notm}}, {{site.data.keyword.Bluemix_local_notm}}, or any combination, you can use the following organization architectures:

* Single-organization: Consider this architecture if you require the same set of users to access resources that are available anywhere in the organization.
* Multi-organization: Consider this architecture if you require isolation between different environments.

## Single-organization versus multi-organization
{: #singleormulti}

In a single-organization environment, the infrastructure resources are shared by different areas of the company. Whereas, in a multi-organization environment the infrastructure resources are not shared.

Both organization architectures support the following principles:

* Boundary enforcement for apps, projects, or both.
* Authorization to manage resources that are granted by user role.

You can then define multiple spaces that are based on different lines of business (LOB), the delivery phases, specific projects, apps, user permissions, or a combination of these components.

To implement a multi-organization architecture you can define organizations that correspond to different LOBs, delivery phases, specific projects, user permissions, or a combination of these components. You can then define multiple spaces that are based on apps or projects that are delivered by the same department in the company.

{: tip}

## Organization considerations
{: #orgconsiderations}

When you implement a single-organization architecture, the organization includes all of the cloud resources, services, and apps that you use to develop, manage, and deploy cloud apps. In {{site.data.keyword.Bluemix_notm}} Public, the organization provides segregation between accounts and is available across all regions.

 ![Figure that shows the single-organization architecture](img/singleorg_example.svg "Figure that shows the single-organization architecture in {{site.data.keyword.Bluemix_notm}}")

 Figure 1. Example of a single-organization architecture.
{: #bpfigure1}

When you implement a multi-organization architecture, organizations provide the first level of boundary enforcement and abstraction that you can use to control and define what can be done and by whom. Design each organization around the different LOBs, the delivery phases, the roles of the users, specific projects, or a combination of these components.  

The number of organizations that you require depends on multiple factors:

* The level of granularity that you require within your organization to manage quotas and control costs.
* The level of security that you must enforce in your different environments. For example, if you are using containers, you might want to segregate container images that are used for development from the container images that are used for production.
* The location of the organizations due to corporate, country, and industry requirements. For example, you might want to run all of your apps in an environment that is located in a specific region in your geography (geo).

When you are defining the different organizations for your cloud structure, consider the following guidance:

* Define and then enforce a naming convention. For example, define a naming convention where the name of the organization includes information about the business area, the type of cloud, and the process phase (development, testing, or production). For organizations that are located in {{site.data.keyword.Bluemix_notm}} Public, you might want to add information about the region too.
* Define the restrictions that apply to the organization. For example, define the role of the team members that are going to work in that organization.
* Identify the manager of the organization.
* Identify the area of the business that is allocated to this organization.

The following scenarios show different approaches that you can adopt when you define the number of Cloud Foundry organizations in an environment:

### Scenario 1: Segregation of user groups by business application delivery

 Description: Corporate rules require that the apps of each LOB must be developed, managed, and deployed by users from each LOB. Security must be enforced so that users can access only the apps that are relevant to their part of the business. So, the users work in different business areas, the apps they are working on require access to different {{site.data.keyword.Bluemix_notm}} resources, and there is no activity overlap.

  Solution: You can create an organization for each business application delivery process. For example, one organization for retail banking, and one for investment banking.

  ![Figure that shows segregation of users by business application delivery](img/bank_example.svg "Figure that shows segregation of users by business application delivery")

  Figure 2. Example of a multi-organization architecture that is aligned to LOB delivery
{: #bpfigure2}

### Scenario 2: Segregation based on type of users (internal users, external users)

  Description: Your company works with different partners and you require clear boundaries between internal and external users.

  Solution: You can create an organization to deliver apps that are used internally. In addition, you can create one organization for each external partner.

### Scenario 3: Isolation by project

  Description: Your company runs hackathons to identify new services.  

  Solution: You can define one organization per hackathon and use the organization as a sandbox. After the hackathon, you can promote the sandbox organization into an extra organization in your account.

### Scenario 4: Isolation of users by delivery phase

  Description: A company wants development, test, and production users to collaborate across a delivery, but their access is controlled by user role and job experience.

  Solution: You can create a single-organization and define a space for each delivery phase. Then, depending on the user role and job experience, grant the read and write access that they require to complete their work and also collaborate within the organization.

  ![Figure that shows isolation of users by delivery phase](img/user_groups_example.svg "Figure that shows isolation of users by delivery phase")

   Figure 3. Example of a single-organization architecture that is aligned by delivery phase
{: #bpfigure3}

## Organization naming, restrictions, and management
{: #orgadmin}   

Consider the following organization guidance:

* Define and enforce a naming convention. For example, define a naming convention where the name of the organization includes information about the business area, the type of cloud, and the IT role (development, testing, or production). For organizations that are located in {{site.data.keyword.Bluemix_notm}} Public, you might want to add information about the region too. You can change the name of an organization after it is created. If an organization name is altered, notify all of the organization team members about the change.
* Define the restrictions that apply to the organization. For example, define the role of each of the team members and the permissions they need to work in that organization.
* Identify the manager of the organization. You might want to delegate the organization administration to more that one person.
* Identify the area of the business that is allocated to this organization. The application usage that is generated in each of the spaces, within the organization, is accumulated and reported at the organization level.
