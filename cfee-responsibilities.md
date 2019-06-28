---

copyright:
  years: 2019
lastupdated: "2019-06-24"

keywords: Cloud Foundry Enterprise Environment, responsibilities, ha, high availability, disaster recovery

subcollection: cloud-foundry

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}


# Your responsibilities by using {{site.data.keyword.cfee_full_notm}}
{: #responsibilities-cfee}

Learn about management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cfee_full}}.
{:shortdesc}

## Management responsibilities
{: #responsibilities}

IBM provides you with an enterprise cloud platform to deploy your workload. You choose how to set up, integrate, backup, and operate your workloads in the cloud.


## Cloud infrastructure

**IBM responsibilities**

- Deploy an instance of {{site.data.keyword.containerlong_notm}} Postgres and {{site.data.keyword.cos_full}} for each Cloud Foundry environment.
- Deploy a Cloud Foundry environment consisting of all standard {{site.data.keyword.cfee_short}} components.
- Fulfill requests for more infrastructure, such as adding and removing cells.

**Your responsibilities**  
- Use the provided API, CLI, or console tools to [scale the environment](/docs/cloud-foundry?topic=cloud-foundry-update-scale#scale) to meet the needs of your workload.
  
## Managing {{site.data.keyword.cfee_full_notm}}

**IBM responsibilities**  
- Provide a suite of tools to automate {{site.data.keyword.cfee_short}} management, such as the {{site.data.keyword.cfee_short}} API, CLI plug-in, and console.
- Perform continuous review and service improvements, and notify you when there are changes (with and without customer impact) to {{site.data.keyword.cfee_short}}. Make major and minor updates available for you to apply.
- Provide high availability capabilities such as multizone region deployment for {{site.data.keyword.cfee_short}}.
- Provide capabilities to view utilization, capacity and performance data. For example, provide pre-configured alerts to notify when usage thresholds are exceeded.
- Provide rolling changes to ensure there's no impact to the entire environment by applications or services.
- Provide tools, such as the autoscaler, to create additional instances of your applications.

**Your responsibilities**  

- [Manage changes](/docs/cloud-foundry?topic=cloud-foundry-management-enablement#managing-change) such as updating versions.
- [Monitor and act on alerts](/docs/cloud-foundry?topic=cloud-foundry-monitoring) for platform issues using runbooks provided by IBM.
- [Open incidents for IBM Support](https://cloud.ibm.com/unifiedsupport/cases/manage).
- [Manage customer-provided services](/docs/cloud-foundry?topic=cloud-foundry-managing-customer-provided-service#managing-customer-provided-service).
- Optional: Generate [utilization, capacity and performance reports](/docs/cloud-foundry?topic=cloud-foundry-monitoring#grafana) across {{site.data.keyword.cfee_short}} instances.

## Security-rich environment

**IBM responsibilities**
- Maintain controls commensurate to various industry compliance standards.
- [Provide security and access control service](/docs/cloud-foundry?topic=cloud-foundry-permissions#permissions)
with IBM Cloud Identity and Access Management (IAM).


**Your responsibilities**
- Use the API, CLI, or console tools [to apply the provided security patch updates to your Cloud Foundry environment](/docs/cloud-foundry?topic=cloud-foundry-update-scale#update).
- [Manage access and users](https://cloud.ibm.com/iam#/users) for {{site.data.keyword.cfee_short}}.
- [Create an isolated network and deploy your Cloud Foundry environment in isolation](/docs/cloud-foundry?topic=cloud-foundry-isolated-network).
- [Provide information to allow for account audits and alerts in the services and {{site.data.keyword.cfee_short}} platform](/docs/cloud-foundry?topic=cloud-foundry-auditing-logging#auditing).
- [Protect external services](/docs/account?topic=account-find-access#find-access) (for example, databases) with access controls.

## App orchestration

**IBM responsibilities** 

- Provision the Cloud Foundry environment so that you can access the {{site.data.keyword.cfee_short}} API.
- Provide Cloud Foundry integrations with select third-party partnership technologies, such as Log Analysis with LogDNA.
- Provide the capability for service binding to other IBM Cloud services.

**Your responsibilities**

- Use the provided tools and features to [manage the lifecycle of customer-owned applications](/docs/cloud-foundry?topic=cloud-foundry-getting-started#deploy-apps), [integrate with other services](/docs/cloud-foundry?topic=cloud-foundry-getting-started#bind-apps), and monitor the health of the application (for example, [Availability Monitoring](https://cloud.ibm.com/catalog/services/availability-monitoring)).

## Abuse of {{site.data.keyword.cfee_full_notm}}
{: #terms}

Clients cannot misuse {{site.data.keyword.cfee_full}}.

Misuse includes:
- Any illegal activity
- Distribution or execution of malware
- Harming or interfering with the use of {{site.data.keyword.cfee_full}}
- Harming or interfering with the use of any other service or system
- Unauthorized access to any service or system
- Unauthorized modification of any service or system
- Violation of the personal rights of others

See [Cloud Services terms](/docs/overview/terms-of-use?topic=overview-terms) for overall terms of use.
