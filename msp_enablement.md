---

copyright:
  years: 2019
lastupdated: "2019-06-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Management enablement
{: #management-enablement}

This document is an introduction to administrative and operational aspects of an {{site.data.keyword.cfee_full_notm}} ({{site.data.keyword.cfee_short}}).

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
| Account Owner                      | Customer        | Manage on-boarding and support of users to his account in IBM Cloud   |
| Application Developer and Operator | Customer        | Manage lifecycle of customer-owned applications                       |
| Cloud Foundry Administrator        | Customer        | Manage day-to-day requirements of development teams and Cloud Foundry |
| **Environment Administrator**      | Customer        | Manage all elements of Cloud Foundry, IaaS, databases, etc          |
| IBM Cloud                          | IBM             | Provide means for deployment, scaling, upgrading, and operating       |

The following picture is a visual representation of the roles and responsibilities:

![{{site.data.keyword.cfee_full_notm}}](img/ICFEE_HighLevelRoles.png  "High level roles in an {{site.data.keyword.cfee_full_notm}}")

## Customer Management
{: #management-msp-engagement}

The customers choice to use {{site.data.keyword.cfee_short}} includes how to handle the Environment Administrator role.
The customer can fulfill the responsibilities of the Environment Administrator on their own, or may engage a management offering provider to fulfill that role for them.

The customer decides {{site.data.keyword.cfee_short}} management based on the following:
- Understand there are layers of “shared management responsibilities” – Customer & IBM Cloud roles
- Deploy a {{site.data.keyword.cfee_short}} instance (with or without the assistance of management offering provider)
- Decide who should fulfill the Environment Administrator role – the customer or a management offering provider)
- If desired, engage with that management offering provider for environment management services

## Managing change
{: #managing-change}

During the life-cycle of a {{site.data.keyword.cfee_full_notm}} ({{site.data.keyword.cfee_short}}) instance there is a shared responsibility between 
the customer and IBM to apply changes.

The customer will notice available updates in the IBM Cloud console. The customer can implement the changes as described
[here](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-update-scale#update-scale).

Various considerations need to be taken into account based on the customers procedures for change management.
For instance:

- determination of appropriate change windows
- installation of prerequisites 
- installation of changes
- verification of successful changes
- customer-specific considerations

## Management Offering Provider
{: #management-service-provider}

During the life-cycle of a {{site.data.keyword.cfee_short}} instance there is a shared responsibility between the customer and IBM
to perform administrative and operational tasks: monitoring health, handling alerts, executing upgrades,
scaling up and down the environment, etc. These tasks are typically done by the Environment Administrator role.

If the customer decides to not manage this role themselves, but instead engage a management offering provider to fulfill the responsibilities of the Environment Administrator role, the following steps are recommended with regard to that provider:
1. You should check the terms and conditions, capabilities, operations practices, roles and responsibilities, rules, SLA offered, cost, and all other relavent information before signing a management offering contract <br> (outside of and not related to the digital purchase of {{site.data.keyword.cfee_short}} instances)
1. You would then add the management offering provider to have access tp the IBM Cloud Account that contains the {{site.data.keyword.cfee_short}} instances, and any other set up steps with which you have agreed upon
1. The management offering provider would then access your environment and would set up steps, processes and tooling as it was agreed upon
1. The management offering provider would then fulfill the responsibilities of the Environment Administrator for proper availability, health and performance of {{site.data.keyword.cfee_short}} instances, along with any other agreed upon tasks.

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
