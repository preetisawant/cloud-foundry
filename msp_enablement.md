---

copyright:
  years: 2019
lastupdated: "2019-05-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Management Enablement
{: #management-enablement}

This document is an introduction into administrative and operational aspects of an {{site.data.keyword.cfee_full_notm}} ({{site.data.keyword.cfee_short}}).

## Overview of Management
{: #management-overview}

During the lifecycle of a {{site.data.keyword.cfee_short}} instance there is a shared responsibility between the customer and IBM to handle administrative and operational tasks. 

Operating and managing a {{site.data.keyword.cfee_short}} instance has two sets of responsibilities:
- Customer-managed responsibilities
- IBM Cloud-managed responsibilities


## Roles and Responsibilities
{: #management-roles-responsibilities}

Responsibilities are associated with roles. The customer can decide to fulfill all roles
on his own or to engage with a **Managed Service Provider** (MSP) as shown in the table below:

| Role                               | Responsibility  | Description                                                           |
|------------------------------------|-----------------|-----------------------------------------------------------------------|
| Application Developer and Operator | Customer        | Manage lifecycle of customer-owned applications                       |
| Cloud Foundry Administrator        | Customer        | Manage day-to-day requirements of development teams and Cloud Foundry |
| **Environment Administrator**      | Customer or MSP | Manage all elements of Cloud Foundry, IaaS, databases, etc.           |
| Account Owner                      | Customer        | Manage on-boarding and support of users to his account in IBM Cloud   |
| IBM Cloud                          | IBM             | Provide means for deployment, scaling, upgrading, and operating       |

<!--
1. Application Developer and Operator (Customer)
1. Cloud Foundry Administrator (Customer)
1. Environment Administrator (**Customer or Vendor**)
1. IBM Cloud Account Owner (Customer).

The table below shows the management and operational responsibilities for a {{site.data.keyword.cfee_short}} instance:

| Responsibility                                                | Description                                                                                                                    |
|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| **Customer**                                                  | Application development, operations and user management<br> (the same steps as any application management in any public cloud) |
| **Management Service Provider (MSP)** <br> customer or vendor | Manage the Cloud Foundry environment – <br> monitoring, scaling, upgrading, and operating                                      |
| **IBM Cloud**                                                 | Provide means for deployment, scaling, upgrading, and operating                                                                |

<haberc>: I believe this was not intended to go on public IBM Docs, but it's just a list of talking points
### Important Notes
- These three responsibilities are the set of steps it takes to "manage and operate" a {{site.data.keyword.cfee_short}} instance for application delivery
- The "Customer" responsibility can be met in several ways
    - The customer can do all the levels of management effort (Customer and MSP)
    - The customer can do the "Customer" activities and hire someone to do the MSP role for them using the MSP Engagement process
- The MSP Engagement process can be handled by a customer, or the customer can engage third-party technical vendors who are experts in the cloud, Cloud Foundry, and Kubernetes container spaces to fulfill that MSP role
- IBM Cloud will create an MSP Engagement full set of information and processes to allow an MSP to execute that environment responsibility
- IBM Global Technology Services (GTS) will offer an MSP paid offering to deliver the MSP role for customers
- IBM Cloud will maintain a list of IBM and third-party management partners that can fulfill that MSP role and will present them to users during {{site.data.keyword.cfee_short}} creation time and through documentation.


The roles for managing and operating a {{site.data.keyword.cfee_short}} instance are shown in the following table:

| Responsibility         | Role                                                                                                                                                                                                                                                                                                               |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Customer**           | 1. Application Developer and Operator - manage lifecycle of customer-owned applications<br>2. Cloud Foundry Administrator - manage day-to-day requirements of development teams and Cloud Foundry <br>4. IBM Cloud Account Owner - manage on-boarding and support of users to his account in IBM Cloud |
| **Customer or Vendor** | 3. Environment Administrator - manage all elements of Cloud Foundry, IaaS, databases, etc.                                                                                                                                                                                                                         |
| **IBM Cloud**          | 5. IBM Cloud - provide the means for deploying, scaling, upgrading, and operating                                                                                                                                                                                                                                  |

1. Application Developer and Operator - lifecycle management of customer-owned applications
1. Cloud Foundry Administrator - manage the day-to-day requirements of development teams and Cloud Foundry 
1. Environment Administrator - manage all elements of Cloud Foundry, IaaS, databases, etc.
1. IBM Cloud Account Owner - manage the on-boarding and support of users to his account in IBM Cloud
1. IBM Cloud - provide the means for deploying, scaling, upgrading, and operating
-->

The following picture is a visual representation of the roles and responsibilities:

![{{site.data.keyword.cfee_full_notm}}](img/ICFEE_HighLevelRoles.png  "High level roles in an {{site.data.keyword.cfee_full_notm}}")


## Use Cases and Responsibilities Table
{: #usecases-and-responsibilities-table}

The table below describes responsibilities in a {{site.data.keyword.cfee_short}} instance.

( **R** ) Responsible - who does the work to achieve the use case.
<!--
( **A** ) Accountable (also Approver or final approving authority) - The one ultimately answerable for the correct and thorough completion of the deliverable or task, and the one who delegates the work to those responsible. In other words, an accountable must sign off (approve) work that responsible provides. There must be only one accountable specified for each task or deliverable.
( **C** ) Consulted - Those whose opinions are sought, typically subject matter experts; and with whom there is two-way communication.
( **I** ) Informed - Those who are kept up-to-date on progress, often only on completion of the task or deliverable; and with whom there is just one-way communication.
-->

| **Use Case**                                                                                                                                                                                                                 | Customer | IBM Cloud |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|-----------|
| **Service Catalog Management**                                                                                                                                                                                               |          |           |
| Add service catalog item (e.g. IBM Cloud offers a new DBaaS)                                                                                                                                                                 |          | R         |
| Change service catalog item (e.g. change the version of a DB in a DBaaS)                                                                                                                                                     |          | R         |
| [Managing a customer-provided service](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-managing-customer-provided-service#managing-customer-provided-service)                                                   | R        |           |
| [Request a change for {{site.data.keyword.cfee_short}}](http://ibm.biz/cloudideas)                                                                                                                                           | R        |           |
| **Availability Management**                                                                                                                                                                                                  |          |           |
| Perform continuous review and service improvement                                                                                                                                                                            |          | R         |
| **IT Service Continuity Management**                                                                                                                                                                                         |          |           |
| Provide HA/DR capabilities for {{site.data.keyword.cfee_short}}                                                                                                                                                              |          | R         |
| **Demand Management**                                                                                                                                                                                                        |          |           |
| Provide capabilities to view utilization, capacity and performance data                                                                                                                                                      |          | R         |
| [Generate utilization, capacity and performance reports](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring#grafana)                                                                                    | R        |           |
| **Service Level Management**                                                                                                                                                                                                 |          |           |
| Publish all SLAs for {{site.data.keyword.cfee_short}}                                                                                                                                                                        |          | R         |
| **Capacity Management**                                                                                                                                                                                                      |          |           |
| [Provide utilization capacity and performance reports across {{site.data.keyword.cfee_short}} instances](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring#grafana)                                    | R        |           |
| Provide pre-configured alerts to alert when usage thresholds are exceeded                                                                                                                                                    |          | R         |
| [Receive alerts when defined usage thresholds are exceeded](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring#customizing-the-alertmanager-configuration)                                              | R        |           |
| [Provide additional capacity within a reasonable time](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-update-scale#scale)                                                                                      | R        |           |
| **Information Security Management**                                                                                                                                                                                          |          |           |
| [Provide security and access control service](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions#permissions)                                                                                          | R        |           |
| [Protect external services (e.g. DB) with access controls](https://cloud.ibm.com/docs/account?topic=account-find-access#find-access)                                                                                         | R        |           |
| [Provide information to allow for account audits and alerts in the services and {{site.data.keyword.cfee_short}} platform](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-auditing-accounts#auditing-accounts) | R        |           |
| **Transition Planning and Support**                                                                                                                                                                                          |          |           |
| Plan and execute on major change                                                                                                                                                                                             |          | R         |
| **Change Management**                                                                                                                                                                                                        |          |           |
| Notification of a change to {{site.data.keyword.cfee_short}} with customer impact                                                                                                                                            |          | R         |
| Notification of a change to {{site.data.keyword.cfee_short}} with non customer impact                                                                                                                                        |          | R         |
| [Applying changes](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-managing-change#managing-change)                                                                                                             | R        |           |
| Provide rolling change to ensure changes do not impact entire environment (by application or service)                                                                                                                        |          | R         |
| **Change Evaluation**                                                                                                                                                                                                        |          |           |
| Release and test new platform (on IBM environments)                                                                                                                                                                          |          | R         |
| Develop and prepare detailed change documentation (including prerequisites and impact)                                                                                                                                       |          | R         |
| Release platform to customer environments                                                                                                                                                                                    |          | R         |
| **Knowledge Management**                                                                                                                                                                                                     |          |           |
| Publish all run books and information                                                                                                                                                                                        |          | R         |
| **Operations Management**                                                                                                                                                                                                    |          |           |
| [Monitor and alert on platform issues](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)                                                                                                              | R        |           |
| **Event Management**                                                                                                                                                                                                         |          |           |
| Provide pre-defined monitors and alerts on platform issues                                                                                                                                                                   |          | R         |
| [Receive and act on alerts for platform issues](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)                                                                                                     | R        |           |
| **Incident Management**                                                                                                                                                                                                      |          |           |
| [Manage platform incidents to closure](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-debug_overview)                                                                                                          | R        |           |
| Support on platform incidents until closure                                                                                                                                                                                  |          | R         |
| **Problem Management**                                                                                                                                                                                                       |          |           |
| Perform and provide RCA for customer impacting events or those events which continue to occur and require customer notification                                                                                              |          | R         |
| **Service Reporting (Enables Access Management)**                                                                                                                                                                            |          |           |
| [Users defined in {{site.data.keyword.cfee_short}}](https://cloud.ibm.com/iam#/users)                                                                                                                                        | R        |           |
| [Open/Closed incidents visibility and reports](https://cloud.ibm.com/unifiedsupport/cases/manage)                                                                                                                            | R        |           |
| [Request for specific feature (e.g. services)](http://ibm.biz/cloudideas)                                                                                                                                                   | R        |           |


## Customer MSP Engagement
{: #management-msp-engagement}

The customers choice to use {{site.data.keyword.cfee_short}} includes how to handle the Environment Administrator role.
The customer can fulfill the responsibilities of the Environment Administrator on his own or engage with a **Managed Service Provider** (MSP)
to fulfill that role for him. A customer that decides to do the full management himself is acting as his own MSP.

The customer decides {{site.data.keyword.cfee_short}} management based on the following:
- Understand there are layers of “shared management responsibilities” – Customer, MSP, IBM Cloud
- Deploy a {{site.data.keyword.cfee_short}} instance (with or without assistance of an MSP)
- Decide who should fulfill the Environment Administrator role – the customer or an MSP (IBM's or a third party)
- Engage with that MSP.

## Management Service Provider
{: #management-service-provider}

During the life-cycle of a {{site.data.keyword.cfee_short}} instance there is a shared responsibility between the customer and IBM
to perform administrative and operational tasks: monitoring health, handling alerts, executing upgrades,
scaling up and down the environment, etc. These tasks are typically done by the Environment Administrator role
based on updates and user interfaces provided by IBM Cloud.

If the customer decides to engage a Managed Service Provider (MSP) to fulfill the responsibilities of the
Environment Administrator role, the following steps are recommended:
1. The customer checks the terms and conditions of an MSP and signs a management contract with the MSP <br> (outside of and not related to the digital purchase of {{site.data.keyword.cfee_short}} instances)
1. The customer and the MSP sync on expectations, rules, roles and operations
1. The customer adds the MSP to the IBM Cloud Account that contains the {{site.data.keyword.cfee_short}} instances
1. The MSP accesses the environment and sets up steps, processes and tooling as it was agreed upon between the customer and the MSP
1. The MSP fulfills the responsibilities of the Environment Administrator for proper availability, health and performance of  {{site.data.keyword.cfee_short}} instances.

<!--
### MSP Enabled Methods

This enablement by IBM Cloud to an MSP lists the recommended methodologies and operations strategies for managing the Cloud Foundry
environment, allowing for a flexible and complete management solution.

It is enabled by a "management operations" concept that attaches tools to levels of the management capability.
IBM defines the management operations and includes various information about possible tooling,
connecting methods, and examples. Some management tooling IBM Cloud offers with the Cloud Foundry environment stand-up, others are added by the MSP.
MSPs can easily expand operational tools into this management concept. This allows a flexible delivery of management with low operational overhead and known starting point capabilities,
and allows MSPs to expand with unique offerings.
-->
