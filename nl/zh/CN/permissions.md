---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 许可权
{: #permissions}

开始创建和使用 {{site.data.keyword.cfee_full}} 服务的实例之前，必须正确设置管理员和团队其余人员的许可权。

## 创建新环境所需的许可权
{: #perm-creating}

要创建 {{site.data.keyword.cfee_full_notm}} 服务的新实例，必须由要创建实例的帐户的管理员向用户授予访问策略：

* 对 {{site.data.keyword.Bluemix}} 帐户中至少一个资源组的访问权。通过资源组，可以将资源组织成定制的分组，以便于对这些资源进行访问控制。创建新的环境实例时，系统将提示创建资源组。

* 对分配给环境的资源组中 {{site.data.keyword.cfee_full_notm}} 服务的“管理员”或“编辑者”角色。在 {{site.data.keyword.cfee_full_notm}} 服务中具有“管理员”或“编辑者”角色的用户可以创建和删除环境。但是，只有具有管理角色的用户才能将用户分配给 {{site.data.keyword.cfee_full_notm}} 实例，或更改分配给该实例中用户的角色。

* 对 IBM Cloud Object Storage 服务的“管理员”或“编辑者”角色，此服务是 CFEE 服务必需的依赖项。IBM Cloud Object Storage 服务的实例用于存储在创建 ICFEE 应用程序容器期间生成的数据（例如，上传的应用程序包、buildpack 和已编译的可执行文件）。

* Compose for PostgreSQL 服务的实例是 CFEE 服务必需的依赖项。Compose for PostgreSQL 用于在 CFEE 实例上存储 Cloud Foundry 数据（例如，审计应用程序部署，启动和停止事件；保留 CFEE 用户成员资格、组织、空间、应用程序和服务连接的记录）。Compose for PostgreSQL 服务的实例部署在公共 Cloud Foundry 组织（与 CFEE 组织不相关）中。部署了 Compose for PostgresSQL 实例的公共 Cloud Foundry 组织具有特定名称：**_cfee-`<accountId>`_**，其中“accountId”是要供应 CFEE（以及 Compose for PostgreSQL 服务实例）的 IBM Cloud 帐户的标识。帐户所有者创建 CFEE 实例时，将自动创建公共 Cloud Foundry 组织。如果非帐户所有者的用户尝试创建 CFEE 实例，那么不会自动创建组织（所以尝试创建 CFEE 将失败）。因此，必须将 IBM Cloud 帐户中要创建 CFEE 实例但并不是帐户所有者的任何用户添加到 **_cfee-`<accountId>`_** 公共 Cloud Foundry 组织中，并向其授予**管理者角色**。   

   要将 IBM Cloud 帐户中的用户添加到 _cfee-`<accountId>`_ 公共组织，请执行以下操作：
    * 转至[**管理 > 帐户 > Cloud Foundry 组织**](https://console.bluemix.net/account/organizations)。
    * 单击 **_cfee-`<accountId>`_** 组织。
    * 转至页面顶部的**用户**选项卡。
    * 查找需要创建 CFEE 实例的用户，然后单击该用户的**管理者**复选框。如果需要有能力创建 CFEE 实例的用户不在列表中，请单击表上方的**添加或邀请用户**以将用户添加到 **_cfee-`<accountId>`_** 组织或邀请用户加入该组织。

   **注**：虽然在 IBM Cloud 帐户所有者创建 CFEE 实例时，会隐式自动创建 **_cfee-`<accountId>`_** 公共组织，但帐户所有者（并且只有帐户所有者）可以改为手动创建公共 Cloud Foundry 组织，而无需创建 CFEE 实例。IBM Cloud 帐户所有者可以在**管理 > 帐户 > Cloud Foundry 组织**页面中手动创建公共 _cfee-`<accountId>`_ 组织。如果您是帐户所有者并创建了公共 _cfee-`<accountId>`_ 组织，请确保将其准确命名为 _cfee-`<accountId>`_。要查找 IBM Cloud 帐户标识，请转至[**管理 > 帐户 > Cloud Foundry 组织**](https://console.bluemix.net/account/organizations)页面，并查看浏览器中提供的页面 URL。IBM Cloud 帐户标识是页面 URL 中 `=` 后面的一组字母数字值。或者，可以转至__管理 > 帐户 > 用户__，并将鼠标悬停在位于页面右上角的_帐户_名称左侧的工具提示上。
   
* 对分配给环境的资源组中 {{site.data.keyword.Bluemix_notm}} Container Service 的“管理员”或“编辑者”角色。{{site.data.keyword.cfee_full_notm}} 的实例部署在 {{site.data.keyword.Bluemix_notm}} Container Service 提供的容器集群基础架构上。创建 {{site.data.keyword.cfee_full_notm}} 服务的实例时，该服务会自动创建部署了 {{site.data.keyword.cfee_full_notm}} 的 Kubernetes 集群。需要对 IBM Container Service（尤其是分配给环境的资源组中的 IBM Container Service）的访问权，才可创建该集群基础架构。

要确认您是否具有创建 {{site.data.keyword.cfee_full_notm}} 实例所需的访问策略，请执行以下操作：
1. 转至 {{site.data.keyword.Bluemix_notm}} 标题中的[**管理 > 帐户 > 用户**](https://console.bluemix.net/iam/#/users)菜单，以打开**身份和访问权**页面。
2. 在“访问策略”选项卡中，单击要创建环境的用户。
3. 确认要创建环境的用户的访问策略是否与先前描述的策略一致。

以下屏幕说明了允许用户创建 {{site.data.keyword.cfee_full_notm}} 实例的 {{site.data.keyword.Bluemix_notm}} 的“身份和访问权”页面中显示的访问策略。

![访问策略](img/AccessPolicies_Creator.png)

## 使用环境所需的许可权
{: #perm-working}

要使用 {{site.data.keyword.cfee_full_notm}} 的实例，用户必须满足以下要求：
1. 是在其中创建了 {{site.data.keyword.cfee_full_notm}} 实例的 {{site.data.keyword.Bluemix_notm}} 帐户的成员。
2. 由帐户管理员授予了以下_访问策略_（请查看 {{site.data.keyword.Bluemix_notm}} 标题中[**管理 > 帐户 > 用户**](https://console.bluemix.net/iam/#/users)菜单下的_身份和访问权_页面，以检查当前帐户访问策略）：
  - 对 {{site.data.keyword.Bluemix_notm}} 帐户中至少一个资源组的访问权。通过资源组，可以将资源组织成定制的分组，以便于对这些资源进行访问控制。创建新的环境实例时，系统将提示创建资源组。
  - 用户必须分配有对在其中创建了环境实例的资源组中 {{site.data.keyword.cfee_full_notm}} 服务的访问权。用户在 {{site.data.keyword.cfee_full_notm}} 实例中具有的访问和控制级别取决于访问策略中授予的角色：
     - 分配有“管理员”或“编辑者”角色的用户可以创建组织，为组织和空间分配管理者，对环境中的所有组织和空间具有完全许可权，并可使用云控制器 API 执行业务操作。在 Cloud Foundry _用户帐户和认证作用域_中，会自动授予这些用户 _cloud_controller.admin 作用域_。
     - 分配有“查看者”角色的用户可以在主 {{site.data.keyword.Bluemix_notm}} 仪表板中看到该环境，并可以打开其用户界面。用户对环境中特定组织和空间的访问权由这些组织和空间的管理者所分配的特定组织和空间角色进行管理。有关更多信息，请参阅[向组织添加用户](add-users.html)。

下图说明了访问 {{site.data.keyword.cfee_full_notm}} 所需的最低访问策略（访问策略将显示在 {{site.data.keyword.Bluemix_notm}} 的_身份和访问权_页面中）。

![访问策略](img/AccessPolicies_User.png)

