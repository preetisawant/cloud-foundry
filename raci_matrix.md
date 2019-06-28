---

copyright:
  years: 2019
lastupdated: "2019-04-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Use Cases and Responsibilities Table
{: #usecases-and-responsibilities-table}

A responsibility assignment matrix, also known as RACI matrix, describes the participation by various roles in completing tasks or deliverables for a project or business process. It is especially useful in clarifying roles and responsibilities in cross- functional/departmental projects and processes.  

( **R** ) Responsible - Those who do the work to achieve the task. There is at least one role with a participation type of responsible, although others can be delegated to assist in the work required.  
( **A** ) Accountable (also Approver or final approving authority) - The one ultimately answerable for the correct and thorough completion of the deliverable or task, and the one who delegates the work to those responsible. In other words, an accountable must sign off (approve) work that responsible provides. There must be only one accountable specified for each task or deliverable.  
( **C** ) Consulted - Those whose opinions are sought, typically subject matter experts; and with whom there is two-way communication.  
( **I** ) Informed - Those who are kept up-to-date on progress, often only on completion of the task or deliverable; and with whom there is just one-way communication.  

| **ID**  | **Use Case**                                                                                                                    | Customer | IBM Cloud |
|---------|---------------------------------------------------------------------------------------------------------------------------------|----------|-----------|
| **1**   | **Service Catalog Management**                                                                                                  |          |           |
| 1_0_0   | Add service catalog item (e.g. IBM Cloud offers a new DBaaS)                                                                    |          | R         |
| 1_0_1   | Change service catalog item (e.g. change the version of a DB in a DBaaS)                                                        |          | R         |
| 1_0_3   | [Managing a customer-provided service](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-managing-customer-provided-service#managing-customer-provided-service)                                                                                           | R        |           |
| 1_0_4   | [Request a change for {{site.data.keyword.cfee_short}}](http://ibm.biz/cloudideas)                                                                               | R        |           |
| **2**   | **Availability Management**                                                                                                     |          |           |
| 2_0_0   | Perform continuous review and service improvement                                                                               |          | R         |
| **3**   | **IT Service Continuity Management**                                                                                            |          |           |
| 3_0_0   | Provide HA/DR capabilities for {{site.data.keyword.cfee_short}}                                                                 |          | R         |
| **4**   | **Demand Management**                                                                                                           |          |           |
| 4_0_0a  | Provide capabilities to view utilization, capacity and performance data                                                         |          | R         |
| 4_0_0b  | [Generate utilization, capacity and performance reports](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring#grafana)                                                                          | R        |           |
| **5**   | **Service Level Management**                                                                                                    |          |           |
| 5_0_0   | Publish all SLAs for {{site.data.keyword.cfee_short}}                                                                           |          | R         |
| **6**   | **Capacity Management**                                                                                                         |          |           |
| 6_0_0   | [Provide utilization capacity and performance reports across {{site.data.keyword.cfee_short}} instances](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring#grafana)                          | R        |           |
| 6_0_1a  | Provide pre-configured alerts to alert when usage thresholds are exceeded                                                       |          | R         |
| 6_0_1b  | [Receive alerts when defined usage thresholds are exceeded](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring#customizing-the-alertmanager-configuration)                                                                        | R        |           |
| 6_0_2   | [Provide additional capacity within a reasonable time](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-update-scale#scale)                                                                            | R        |           |
| **7**   | **Information Security Management**                                                                                             |          |           |
| 7_0_0   | [Provide security and access control service](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-permissions#permissions)                                                                                     | R        |          |
| 7_0_1   | [Protect external services (e.g. DB) with access controls](https://cloud.ibm.com/docs/account?topic=account-find-access#find-access)                                                                        | R        |          |
| 7_0_3   | [Provide information to allow for account audits and alerts in the services and {{site.data.keyword.cfee_short}} platform](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-auditing-accounts#auditing-accounts)                                                   | R        |           | 
| **8**   | **Transition Planning and Support**                                                                                             |          |           |
| 8_0_0   | Plan and execute on major change                                                                                                |          | R         |
| **9**   | **Change Management**                                                                                                           |          |           |
| 9_0_0   | Notification of a change to {{site.data.keyword.cfee_short}} with customer impact                                    |          | R         |
| 9_0_1   | Notification of a change to {{site.data.keyword.cfee_short}} with non customer impact                                |          | R         |
| 9_0_2   | [Applying changes](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-managing-change#managing-change)                                                   | R        |           |
| 9_0_3   | Provide rolling change to ensure changes do not impact entire environment (by application or service)                           |          | R         |
| **10**  | **Change Evaluation**                                                                                                           |          |           |
| 10_0_0  | Release and test new platform (on IBM environments)                                                                             |          | R         |
| 10_0_2  | Develop and prepare detailed change documentation (including prerequisites and impact)                                           |          | R         |
| 10_0_4  | Release platform to customer environments                                                                                       |          | R         |
| **11**  | **Knowledge Management**                                                                                                        |          |           |
| 11_0_0  | Publish all run books and information                                                                                           |          | R         |
| **12**  | **Operations Management**                                                                                                       |          |           |
| 12_0_0  | [Monitor and alert on platform issues](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)                                                                                            | R        |          |
| **15**  | **Event Management**                                                                                                            |          |           |
| 15_0_0a | Provide pre-defined monitors and alerts on platform issues                                                                      |          | R         |
| 15_0_0b | [Receive and act on alerts for platform issues](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)                                                                                   | R        |           |
| **16**  | **Incident Management**                                                                                                         |          |           |
| 16_0_0a | [Manage platform incidents to closure](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-debug_overview)                                                                                                                              | R        |           |
| 16_0_0b | Support on platform incidents until closure                                                                                     |          | R         |
| **17**  | **Problem Management**                                                                                                          |          |           |
| 17_0_0  | Perform and provide RCA for customer impacting events or those events which continue to occur and require customer notification |          | R         |
| **18**  | **Service Reporting (Enables Access Management)**                                                                               |          |           |
| 18_0_0  | [Users defined in {{site.data.keyword.cfee_short}}](https://cloud.ibm.com/iam#/users)                                                                                                 | R        |           |
| 18_0_6  | [Open/Closed incidents visibility and reports](https://cloud.ibm.com/unifiedsupport/cases/manage)                                                                                   | R        |           |
| 18_0_7  | [Request for specific feature (e.g. services) ](http://ibm.biz/cloudideas)                                                                           | R        |           |
