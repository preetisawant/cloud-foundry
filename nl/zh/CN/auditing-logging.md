---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 审计和日志记录
{: #auditing-logging}

通过 {{site.data.keyword.cfee_full}} (CFEE) 中的审计和日志记录功能，管理员可以审计在 CFEE 实例中执行的事件，而开发者可以跟踪从其 Cloud Foundry 应用程序生成的日志事件。

CFEE 中的审计和日志记录功能通过与 IBM Cloud 的 Log Analysis 和 Activity Tracker 服务的集成予以支持。

## 审计
{: #auditing}

通过审计，CFEE 管理员可以跟踪在 CFEE 实例中执行的 Cloud Foundry 可审计活动。这些活动包括登录、创建组织和空间、用户成员资格和角色分配、应用程序部署、服务绑定以及域配置。审计通过与 IBM Cloud 中的 Activity Tracker 服务的集成予以支持。由 CFEE 管理员选择的 Activity Tracker 服务实例将自动配置为接收表示在 Cloud Foundry 内和 CFEE 控制平面上执行的操作的事件。用户可以在 Activity Tracker 服务实例的用户界面中查看和管理这些事件。

要对 CFEE 实例启用审计，请执行以下操作：

1. 打开 CFEE 用户界面，然后在左侧导航窗格中打开到**操作 > 审计**条目以打开“审计”页面。
2. 单击**启用审计**，然后选择 IBM Cloud 帐户中可用的其中一个 **Activity Tracker 实例**。如果没有可用的实例，用户将在 IBM Cloud“目录”中看到用于创建新 Activity Tracker 实例的选项。
3.  启用审计后，页面中将显示配置详细信息。详细信息包括配置的状态以及 Activity Tracker 服务实例本身的链接，用户可以通过此链接查看和管理审计事件。

可以通过单击**禁用审计**来禁用审计，这将除去先前添加和配置的 Activity Tracker 服务实例。此操作不会删除 Activity Tracker 服务实例。

## 日志记录持久存储
{: #logging}

Cloud Foundry 事件的日志记录功能通过与 IBM Cloud 中的 Log Analysis 服务的集成予以支持。由 CFEE 管理员选择的 Log Analysis 服务实例将自动配置为接收并持久存储从 CFEE 实例生成的 Cloud Foundry 日志记录事件。用户可以在 Log Analysis 服务实例的用户界面中查看和管理这些日志记录事件。

要对 CFEE 实例启用日志记录，请执行以下操作：

1. 确保您具有 [IAM 访问策略](https://console.bluemix.net/iam/#/users)，用于为您分配针对打算在其中持久存储日志记录事件的 Log Analysis 服务实例的“编辑者”、“操作员”或“管理员”角色。
2. 打开 CFEE 用户界面，然后在左侧导航窗格中打开到**操作 > 日志记录**条目以打开“日志记录”页面。
3. 单击**启用持久存储**，然后选择 IBM Cloud 帐户中其中一个可用的 **Log Analysis 实例**。如果没有可用的实例，用户将在 IBM Cloud“目录”中看到用于创建实例的选项。
4. 启用日志记录持久存储后，页面中将显示配置详细信息。详细信息包括配置的状态以及 Log Analysis 服务实例本身的链接，用户可以通过此链接查看和管理日志记录事件。

**警告：**启用“日志记录持久存储”需要中断性重新启动 CFEE 控制平面和单元。在重新启动期间，所有管理功能都可用，但在此 CFEE 实例中运行的某些应用程序和服务可能不可用。在重新启动期间，CFEE 组件的状态将反映在“运行状况检查”页面中。重新启动大约需要 20 分钟。

可以通过单击**禁用日志持久存储**来禁用日志持久存储，这将除去先前添加和配置的服务实例。此操作不会删除 Log Analysis 服务实例。

**注：**禁用日志持久存储后，仍将生成 Cloud Foundry 日志记录事件，只是这些事件不会在 CFEE 实例外部持久存储。
