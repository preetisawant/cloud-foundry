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

帐户管理员必须为用户设置正确的许可权，用户才能在帐户中创建和使用 {{site.data.keyword.cfee_full}} 服务实例。 

## 创建新环境所需的许可权
{: #perm-creating}

要创建新的 CFEE 服务实例，帐户管理员必须向用户授予访问策略，这些策略不仅要针对 CFEE 服务本身，而且还要针对在创建 CFEE 后自动创建的配套服务。

用户必须拥有以下“身份和访问权管理”(IAM) 访问策略，才能创建 {{site.data.keyword.cfee_full_notm}} 实例：

* 针对 {{site.data.keyword.Bluemix}} 帐户中**_缺省_****资源组**的_查看者_（或更高级别的）访问权。通过资源组，可以将资源组织成定制的分组，以便于对这些资源进行访问控制。创建新的环境实例时，系统将提示创建资源组。用户必须拥有对_缺省_资源组的访问权，因为系统会始终将 Kubernetes 集群供应到该资源组中。用户可以在不同的资源组中供应 CFEE 实例，但系统仍会将 Kuberetes 集群供应到_缺省_资源组中。如果用户在不同的资源组中供应 CFEE，那么用户必须拥有该资源组的查看者访问权。

* 针对分配给环境的资源组中 **{{site.data.keyword.cfee_full_notm}} 服务**资源的“管理员”或“编辑者”角色。在 {{site.data.keyword.cfee_full_notm}} 服务中具有“管理员”或“编辑者”角色的用户可以创建和删除环境。但是，只有具有管理角色的用户才能将用户分配给 {{site.data.keyword.cfee_full_notm}} 实例，或更改分配给该实例中用户的角色。
   
* 针对 **Kubernetes 服务**资源的“管理员”角色。{{site.data.keyword.cfee_full_notm}} 实例会部署在 Kubernetes 服务提供的容器集群基础架构上。当您创建 {{site.data.keyword.cfee_full_notm}} 服务的实例时，该服务会自动创建 Kubernetes 集群。要创建该集群基础架构，需要拥有对 Kubernetes 服务的访问权。您可以将 Kubernetes 服务策略的访问权范围限定为您要在其中供应 CFEE 实例的特定区域，或者限定为所有区域。

* 针对 **IBM Cloud Object Storage 服务**的“管理员”或“编辑者”角色。此服务是 CFEE 服务必需的依赖项。IBM Cloud Object Storage 服务的实例用于存储在创建 ICFEE 应用程序容器期间生成的数据（例如，上传的应用程序包、buildpack 和已编译的可执行文件）。

* Compose for PostgreSQL 服务的实例是 CFEE 服务必需的依赖项。Compose for PostgreSQL 用于在 CFEE 实例上存储 Cloud Foundry 数据（例如，审计应用程序部署，启动和停止事件；保留 CFEE 用户成员资格、组织、空间、应用程序和服务连接的记录）。**Compose for PostgreSQL 服务**的实例会部署在您在创建 {{site.data.keyword.cfee_full_notm}} 实例时所选的公共 Cloud Foundry 组织（与 CFEE 组织无关）内的空间中。这意味着，在创建 {{site.data.keyword.cfee_full_notm}} 实例时，您需要对要在其中供应 CFEE 实例的位置中的至少一个组织拥有管理员访问权。此外，还需要对该组织中的至少一个空间拥有开发者访问权。 

  如果您不是要在其中创建 CFEE 实例的位置中的至少一个公共组织的成员，请让 IBM Cloud 管理员邀请您成为其中一员。如果您的角色为帐户管理员，那么可以将用户添加到帐户中的公共组织和空间内，具体步骤如下：

     * 转至[**管理 > 帐户 > Cloud Foundry 组织**](https://console.bluemix.net/account/organizations)，然后单击**添加组织**，或选择现有组织。
     * 转至组织页面顶部的**用户**选项卡。
     * 找到需要创建 CFEE 实例的用户。如果您希望某个用户能够创建 CFEE 实例，但该用户不在列表中，请单击表上方的**添加或邀请用户**，以将该用户添加或邀请到组织中。
     * 转至组织页面顶部的**空间**选项卡。
     * 找到要在其中供应 Compose for PostgreSQL 服务实例的空间，然后选中**开发者**角色复选框。

以下屏幕说明了允许用户创建 {{site.data.keyword.cfee_full_notm}} 实例的 {{site.data.keyword.Bluemix_notm}} 的“身份和访问权”页面中显示的访问策略。

![访问策略](img/AccessPolicies_Creator.png)

要确认您是否具有创建 {{site.data.keyword.cfee_full_notm}} 实例所需的访问策略，请执行以下操作：
1. 转至 {{site.data.keyword.Bluemix_notm}} 标题中的[**管理 > 帐户 > 用户**](https://console.bluemix.net/iam/#/users)菜单，以打开**身份和访问权**页面。
2. 在“访问策略”选项卡中，单击要创建环境的用户，以便为其分配访问策略或查看其访问策略。

## 使用环境所需的许可权
{: #perm-working}

要使用 {{site.data.keyword.cfee_full_notm}} 的实例，用户必须满足以下要求：
1. 是在其中创建了 {{site.data.keyword.cfee_full_notm}} 实例的 {{site.data.keyword.Bluemix_notm}} 帐户的成员。
2. 拥有帐户管理员授予的以下 IAM _访问策略_（要查看当前帐户访问策略，请参阅 {{site.data.keyword.Bluemix_notm}} 标题中[**管理 > 帐户 > 用户**](https://console.bluemix.net/iam/#/users)菜单下的_身份和访问权_页面）：

  - 针对特定资源组中 {{site.data.keyword.cfee_full_notm}} 服务的访问权（在该资源组下创建了环境实例）。用户在 {{site.data.keyword.cfee_full_notm}} 实例中具有的访问和控制级别取决于访问策略中授予的角色：
     - 分配有“管理员”或“编辑者”角色的用户可以创建组织，为组织和空间分配管理者，对环境中的所有组织和空间具有完全许可权，并可使用云控制器 API 执行业务操作。在 Cloud Foundry _用户帐户和认证作用域_中，会自动授予这些用户 _cloud_controller.admin 作用域_。
     - 分配有“查看者”角色的用户可以在主 {{site.data.keyword.Bluemix_notm}} 仪表板中看到该环境，并可以打开其用户界面。用户对环境中特定组织和空间的访问权由这些组织和空间的管理者所分配的特定组织和空间角色进行管理。有关更多信息，请参阅[向组织添加用户](add-users.html)。

下图说明了访问 {{site.data.keyword.cfee_full_notm}} 所需的最低访问策略（访问策略将显示在 {{site.data.keyword.Bluemix_notm}} 的_身份和访问权_页面中）。

![访问策略](img/AccessPolicies_User.png)

