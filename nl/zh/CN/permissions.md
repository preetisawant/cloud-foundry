---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2019-02-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 许可权
{: #permissions}

对于要创建 {{site.data.keyword.cfee_full}} (CFEE) 实例的帐户，该帐户的管理员必须为用户设置正确的许可权后，用户才能创建和使用 CFEE 服务。 

## 许可权概述
{: #perm-summary}

下面是在 CFEE 实例中执行各种任务至少需要的 [IAM](https://cloud.ibm.com/iam#/users) 和 [Cloud Foundry 角色分配](https://cloud.ibm.com/account/cloud-foundry)的摘要。剩余部分将更详细地描述这些许可权。

|**任务**&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|**IAM 访问角色**&nbsp; &nbsp; &nbsp; |**Cloud Foundry 角色**&nbsp; &nbsp; &nbsp;|
|----------------------------------------|-------------------|-------------------|
|创建 CFEE|  <ul><li>要在其中创建 CFEE 的资源组中的“查看者”角色。</li> <li>CFEE 服务中的“编辑者”角色。</li> <li>Kubernetes 服务中的“管理员”角色。</li> <li>IBM Cloud Object Storage 服务中的编辑者平台角色和管理者服务访问角色。</li> </ul> | <ul><li>公共组织中的“用户”角色。</li> <li>该公共组织的空间中的“开发者”角色。</li></ul>|
|更新 CFEE 版本|  <ul><li>CFEE 资源组中的“查看者”角色。</li> <li>CFEE 服务中的“编辑者”平台角色。</li></li> <li>Kubernetes 服务中的“操作员”角色。</li> <li>Cloud Object Storage 服务中的“编辑者”角色。</li> </ul> | <ul><li>公共组织中的“用户”角色。</li> <li>该公共组织的空间中的“开发者”角色。</li></ul>|
|扩展 CFEE 容量（添加/除去单元）|  <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“管理员”角色。</li> <li>Kubernetes 服务中的“操作员”角色。</li> <li>Cloud Object Storage 服务中的“编辑者”角色。</li> </ul> | |
|监视 CFEE|  <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“编辑者”角色。</li> <li>CFEE 的 Kubernetes 集群中的“操作员”角色。</li></ul> |  |
|查看 CFEE 资源使用情况|  <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“查看者”角色。</li></ul> |  |
|启用 CFEE 审计| <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“编辑者”角色。</li></ul> | <ul><li>部署 Activity Tracker 服务实例的公共 Cloud Foundry 空间中的“审计员”角色。</li></ul>  |
|查看 CFEE 审计事件| <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“编辑者”角色。</li></ul> | <ul><li>部署 Activity Tracker 服务实例的公共 Cloud Foundry 空间中的“审计员”角色。</li></ul>  |
|启用 CFEE 日志持久存储| <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“编辑者”角色。</li></ul> |<ul><li>部署 Log Analysis 服务实例的公共 Cloud Foundry 空间中的“审计员”角色。</li></ul>  |
|查看 CFEE 持久存储的日志| <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“编辑者”角色。</li></ul> | <ul><li>部署 Log Analysis 服务实例的公共 Cloud Foundry 空间中的“审计员”角色。</li></ul> |
|创建 CFEE 组织| <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“编辑者”角色。</li></ul> |  |
|创建 CFEE 空间| <ul><li>CFEE 实例资源组中的“查看者”角色。</li> <li>CFEE 实例中的“查看者”角色。</li></ul> | <ul><li>要在其中创建空间的组织中的“管理者”角色。</li></ul> |
|管理共享域|<ul><li>CFEE 实例资源组中的“查看者”角色。</li><li>CFEE 实例中的“编辑者”角色。</li></ul>|  |
|查看共享域|<ul><li>CFEE 实例资源组中的“查看者”角色。</li><li>CFEE 实例中的“查看者”角色。</li></ul>|  |
|管理专用域|<ul> <li>CFEE 实例资源组中的“查看者”角色。</li><li>CFEE 实例中的“查看者”角色。</li></ul>| <ul><li>拥有域的组织中的“管理者”角色。</li></ul>|
|查看专用域|<ul> <li>CFEE 实例资源组中的“查看者”角色。</li><li>CFEE 实例中的“查看者”角色。</li></ul>|<ul><li>拥有域的组织中的“查看者”角色。</li></ul>|
|在 CFEE 空间中创建/删除 IBM Cloud 服务实例| <ul><li>要在其中创建 CFEE 的资源组中的“查看者”角色。</li> <li>CFEE 实例中的“查看者”角色。</li> <li>要在其中创建服务实例的资源组中的“编辑者”角色，或针对要实例化的受 IAM 管理的服务的“编辑者”角色。</li> </ul>| <ul><li>在其中创建服务实例（以及将自动添加服务实例/创建服务实例别名）的 CFEE 空间中的“开发者”角色。</li></ul> |
|在 CFEE 空间中添加/除去 IBM Cloud 服务实例（即，在 CFEE 空间中创建/删除 IBM Cloud 服务的别名）| <ul><li>CFEE 实例资源组中的“查看者”角色。</li><li>CFEE 实例中的“查看者”角色。</li><li>针对要添加的服务实例的“操作员”平台角色和“读取者”服务角色。</li></ul>|<ul><li>要添加（创建别名）服务实例的 CFEE 空间中的“开发者”角色。</li></ul> |
|在 CFEE 空间中绑定或取消绑定 IBM Cloud 服务实例|<ul> <li>要绑定或取消绑定的服务实例的资源组中的“编辑者”角色。</li><li>CFEE 实例中的“查看者”角色。</li><li>针对要绑定的服务实例的“操作员”平台角色和“写入者”服务角色。</li></ul> | <ul><li>要绑定服务实例的 CFEE 空间中的“开发者”角色。</li></ul> |
|发出 `cf` CLI 命令|<ul> <li>CFEE 实例资源组中的“查看者”角色。</li><li>CFEE 实例中的“查看者”角色。</li></ul> | <ul><li>执行命令所需的组织/空间中的 Cloud Foundry 角色。</li></ul> |
{: caption="表 1. 在 CFEE 中执行任务所需的许可权" caption-side="top"}

## 创建新环境所需的许可权
{: #perm-creating}

要创建新的 CFEE 服务实例，帐户管理员必须向用户授予访问策略，这些策略不仅要针对 CFEE 服务本身，而且还要针对在创建 CFEE 时同时自动创建的支持服务。

用户必须拥有以下“身份和访问权管理”(IAM) 访问策略，才能创建 {{site.data.keyword.cfee_full_notm}} 实例：

* 针对 {{site.data.keyword.Bluemix}} 帐户中**_缺省_****资源组**的_查看者_（或更高级别的）访问权。通过资源组，可以将资源组织成定制的分组，以便于对这些资源进行访问控制。创建新的环境实例时，系统将提示创建资源组。用户必须拥有对_缺省_资源组的访问权，因为系统会始终将 Kubernetes 集群供应到该资源组中。用户可以在不同的资源组中供应 CFEE 实例，但系统仍会将 Kuberetes 集群供应到_缺省_资源组中。如果用户在不同的资源组中供应 CFEE，那么用户必须拥有该资源组的查看者访问权。

* 针对环境分配到的资源组中 **{{site.data.keyword.cfee_full_notm}} 服务**资源的_管理员_或_编辑者_角色。在 {{site.data.keyword.cfee_full_notm}} 服务中具有“管理员”或“编辑者”角色的用户可以创建和删除环境。但是，只有具有管理角色的用户才能将用户分配给 {{site.data.keyword.cfee_full_notm}} 实例，或更改分配给该实例中用户的角色。
   
* 针对 **Kubernetes 服务**资源的_管理员_角色。{{site.data.keyword.cfee_full_notm}} 实例会部署在 Kubernetes 服务提供的容器集群基础架构上。当您创建 {{site.data.keyword.cfee_full_notm}} 服务的实例时，该服务会自动创建 Kubernetes 集群。要创建该集群基础架构，需要拥有对 Kubernetes 服务的访问权。您可以将 Kubernetes 服务策略的访问权范围限定为您要在其中供应 CFEE 实例的特定区域，或者限定为所有区域。

* 针对 **IBM Cloud Object Storage 服务**的_管理者_或_编辑者_平台角色以及管理者服务访问角色。此服务是 CFEE 服务必需的依赖项。IBM Cloud Object Storage 服务的实例用于存储在创建 ICFEE 应用程序容器期间生成的数据（例如，上传的应用程序包、buildpack 和已编译的可执行文件）。

* Compose for PostgreSQL 服务的实例是 CFEE 服务必需的依赖项。Compose for PostgreSQL 用于在 CFEE 实例上存储 Cloud Foundry 数据（例如，审计应用程序部署，启动和停止事件；保留 CFEE 用户成员资格、组织、空间、应用程序和服务连接的记录）。**Compose for PostgreSQL 服务**的实例会部署在您在创建 {{site.data.keyword.cfee_full_notm}} 实例时所选的公共 Cloud Foundry 组织（与 CFEE 组织无关）内的空间中。这意味着在创建 {{site.data.keyword.cfee_full_notm}} 实例时，您需要对打算在其中供应 CFEE 实例的位置中的至少一个组织具有_管理者_访问权。此外，还需要对该组织中的至少一个空间具有_开发者_访问权。 

  如果您不是要在其中创建 CFEE 实例的位置中的至少一个公共组织的成员，请让 IBM Cloud 管理员邀请您成为其中一员。如果您的角色为帐户管理员，那么可以将用户添加到帐户中的公共组织和空间内，具体步骤如下：

     * 转至[**管理 > 帐户 > Cloud Foundry 组织**](https://console.bluemix.net/account/organizations)，然后单击**添加组织**，或选择现有组织。
     * 转至组织页面顶部的**用户**选项卡。
     * 找到需要创建 CFEE 实例的用户。如果您希望某个用户能够创建 CFEE 实例，但该用户不在列表中，请单击表上方的**添加或邀请用户**，以将该用户添加或邀请到组织中。
     * 转至组织页面顶部的**空间**选项卡。
     * 找到要在其中供应 Compose for PostgreSQL 服务实例的空间，然后选中**开发者**角色复选框。

以下屏幕说明了允许用户创建 {{site.data.keyword.cfee_full_notm}} 实例的 {{site.data.keyword.Bluemix_notm}} 的“身份和访问权”页面中显示的访问策略。

![访问策略](img/AccessPolicies_Creator.png)

您可以使用 {{site.data.keyword.Bluemix}} 命令行授予用户许可权。还可以通过在 JSON 格式的文件中指定由策略创建命令调用的策略的参数（即，服务、角色、区域等），从而为用户定义访问策略。请参阅[使用命令行分配 IAM 策略](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline)以获取更多信息，或在命令行中发出 `ibmcloud iam -help`。请注意，这需要安装 [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use)。
{:tip}

要确认您是否具有创建 {{site.data.keyword.cfee_full_notm}} 实例所需的访问策略，请执行以下操作：
1. 转至 {{site.data.keyword.Bluemix_notm}} 标题中的[**管理 > 访问权 (IAM) > 用户**](https://console.bluemix.net/iam/#/users)菜单，以打开**身份和访问权**页面。
2. 在“访问策略”选项卡中，单击要创建环境的用户，以便为其分配访问策略或查看其访问策略。

有关管理 {{site.data.keyword.Bluemix}} 中的用户和访问权（包括如何组织一组用户和服务标识以便一次为多个用户分配访问权）的更多信息，请参阅[管理用户和访问权](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage)。

### 使用 CLI 加快用于创建环境的许可权设置
{: #permcli-creating}

可以通过 `ibmcloud cfee create-permission-set` 来加速用于创建 CFEE 实例的许可权设置。通过该命令，CFEE 管理员可以在单个命令中设置用于创建 CFEE 实例及其所有辅助服务的必需访问策略。 

该命令将许可权设置为 IAM _访问组_，并将用户添加到该_访问组_。发出该命令的管理员可以在命令中包含现有_访问组_。如果未提供_访问组_，那么会自动创建缺省 _cfee-provision-access-group_。

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

该命令为目标用户设置以下访问策略：

*  针对当前 IBM Cloud 帐户中 Cloud Object Storage 和 CFEE 服务的“编辑者”角色。
*  针对当前 IBM Cloud 帐户中 Kubernetes 服务的“管理员”角色。
*  针对供应 Compose for PostgreSQL 的当前组织中当前空间的“开发者”角色。

有关该命令的更多详细信息，请发出以下命令：

```
cfee create-permission-set -help
```
{: pre}

可以使用 `ibmcloud cfee create-permission-get` 来查找或验证用户的已实施访问策略：

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## 使用环境所需的许可权
{: #perm-working}

要使用 {{site.data.keyword.cfee_full_notm}} 的实例，用户必须满足以下要求：
1. 是在其中创建了 {{site.data.keyword.cfee_full_notm}} 实例的 {{site.data.keyword.Bluemix_notm}} 帐户的成员。
2. 拥有帐户管理员授予的以下 IAM _访问策略_（要查看当前帐户访问策略，请参阅 {{site.data.keyword.Bluemix_notm}} 标题中[**管理 > 访问权 (IAM) > 用户**](https://console.bluemix.net/iam/#/users)菜单下的_身份和访问权_页面）：

    在 CFEE 实例中工作的任何用户都需要针对以下项的_查看者_平台角色（或更高角色）：
  - 在其下创建 CFEE 实例的资源组。
  - CFEE 实例本身。 
  
   用户在 CFEE 实例中具有的访问和控制级别取决于其访问策略中授予的角色：

  - 具有针对 CFEE 实例的_查看者_角色的用户可以在主 {{site.data.keyword.Bluemix_notm}}“仪表板”中看到列出了该 CFEE 实例，并可打开其用户界面。用户对环境中特定组织和空间的访问权由这些组织和空间的管理者所分配的特定组织和空间角色进行管理。有关更多信息，请参阅[向组织添加用户](add-users.html)。
  
  - 分配有针对 CFEE 实例的_管理者_或_编辑者_角色的用户可以创建组织，为组织和空间分配管理者，对环境中的所有组织和空间具有完全许可权，并可通过云控制器 API 执行业务操作。在 Cloud Foundry _用户帐户和认证作用域_中，会自动授予这些用户 _cloud_controller.admin 作用域_。

  - 用户需要针对 CFEE 实例的_编辑者_平台角色或更高角色以及针对在其中供应 CFEE 的 Kubernetes 集群的_操作员_角色或更高角色，才能**将 CFEE 更新为新版本**。

  - 用户需要针对 CFEE 实例的_管理员_平台角色以及针对在其中供应 CFEE 的 Kubernetes 集群的_操作员_角色或更高角色，才能对 CFEE **更改容量**（添加或除去单元）。
 
  - 用户需要针对 IBM Cloud 服务实例的_操作员_平台角色（或更高角色），才能向 CFEE 空间**添加**该*服务实例*（即，在 CFEE 空间中创建服务实例别名）。
 
  - 用户需要针对 IBM Cloud 服务实例的_操作员_平台角色（或更高角色）和_写入者_服务角色（或更高角色），才能将该服务实例**绑定**到部署在 CFEE 空间中的应用程序。


## 最佳实践：访问组
{: #access-groups}

请考虑使用访问组来管理和简化 CFEE 的访问控制。通过访问组，可以定义可为其分配访问策略的任意组。添加到访问组的任何用户都会自动分配有该组的访问策略。 

可以在 IBM Cloud 用户界面中或通过 `ibmcloud` CLI 来创建和管理访问组。 

在用户界面中，转至菜单栏，单击**管理 > 访问权 (IAM)**，然后选择[访问组](https://cloud.ibm.com/iam#/groups)。

或者，可以使用 `ibmcloud` CLI：

1. 创建访问组：

  ```
  ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
  {: pre}

2. 为该访问组创建访问策略：

  ```
  ibmcloud iam access-group-policy-create GROUP_NAME
  ```
  {: pre}

3. 向该访问组添加用户：

  ```
  ibmcloud iam access-group-user-add <user-name> [<user-name2...]
  ```
  {: pre}

<br>
有关更多信息，请参阅[设置访问组](https://cloud.ibm.com/docs/iam/groups.html#groups)。
