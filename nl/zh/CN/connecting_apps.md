---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# 管理连接
{: #connect_app}

可以在服务仪表板的**连接**选项卡中，将服务连接到现有或新的 {{site.data.keyword.Bluemix}} 应用程序。将 Cloud Foundry 服务连接到 Cloud Foundry 应用程序会在它们之间创建绑定，您可以在**连接**选项卡中，取消绑定、添加其他连接或删除连接。

但是，将 {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) 管理的服务实例连接到 Cloud Foundry 应用程序时，将在相应的 Cloud Foundry 空间中使用指定的绑定信息，自动创建 IAM 管理的服务的别名。此别名表示为 IAM 管理的服务的 Cloud Foundry 服务实例。
{:shortdesc}

## 什么是别名？
{: #what_is_alias}

别名是资源组中 IAM 管理的服务与组织或空间内的 Cloud Foundry 应用程序之间的连接。在 {{site.data.keyword.Bluemix_notm}} 控制台中，连接（别名）表示为 Cloud Foundry 服务实例。可以通过修改表示连接的服务实例来管理别名。

别名类似于保存远程资源引用的符号链接，支持在整个平台上对实例进行互操作和复用。例如，可以在资源组中创建服务的实例，然后通过在任何可用 Cloud Foundry 区域的组织或空间中创建别名，从而在这些区域中复用该实例。

以下规则适用于别名：

* 别名没有额外费用，但每个别名都会计入 Cloud Foundry 组织中的配额。
* 在 {{site.data.keyword.Bluemix_notm}} 控制台中，每个 Cloud Foundry 空间只能创建一个别名。但是，可以使用 {{site.data.keyword.Bluemix_notm}} CLI 为每个空间创建多个别名。有关更多信息，请参阅[用于管理资源组和资源的命令](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources)。
* 如果您具有相应许可权，那么可以在同一帐户的任何空间、组织和区域中，创建 IAM 管理的服务与任何 Cloud Foundry 应用程序之间的多个连接。
* 在同一空间中建立 IAM 管理的一个服务实例与不同 Cloud Foundry 应用程序之间的多个连接时，这些连接将使用相同的别名。
* 取消绑定 IAM 管理的服务实例*不会*删除用于表示别名的 Cloud Foundry 服务实例。
* 删除 IAM 管理的服务实例连接到的 Cloud Foundry 应用程序*不会*删除用于表示别名的 Cloud Foundry 实例。
* 删除 IAM 管理的服务实例*将会*删除用于表示别名的 Cloud Foundry 服务实例。

## 创建 IAM 管理的服务与 Cloud Foundry 应用程序之间的连接（别名）
{: #creating_alias}

要将 IAM 管理的服务实例连接到 Cloud Foundry 应用程序，请执行以下操作：

1. 转至仪表板。

2. 单击应用程序的名称以打开应用程序详细信息视图。

3. 单击**连接现有项**，然后从现有 Cloud Foundry 应用程序中进行选择。或者，单击**创建连接**以创建要连接到的 Cloud Foundry 应用程序。

4. 指定**用于连接的访问角色**。此值会设置 IAM 服务访问角色。有关更多信息，请参阅 [IAM 访问权](/docs/iam/users_roles.html#userroles)。

5. （可选）可以通过允许 IAM 生成唯一值来提供**连接的服务标识**，或者提供现有服务标识。有关更多信息，请参阅[创建和管理服务标识](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids)。

6. 单击**创建**。

## 查看别名

创建 IAM 管理的服务与 Cloud Foundry 应用程序之间的连接后，别名会显示在已连接 Cloud Foundry 应用程序的**连接**选项卡上。此外，别名还会在仪表板上显示为正在运行的 Cloud Foundry 服务实例，并且仅在您将其打开时才包含**连接**选项卡。

1. 转至仪表板。
2. 在 **Cloud Foundry 服务**表中，单击服务实例的名称以打开服务详细信息视图。如果其中仅有**连接**选项卡，说明这是别名。

## 删除别名

删除别名最简单的方法是删除 IAM 管理的服务实例。但是，也可以保留 IAM 管理的服务实例，而改为直接删除别名。

1. 转至仪表板。
2. 在 **Cloud Foundry 服务**表中，单击服务实例的名称以打开服务详细信息视图。如果其中仅有**连接**选项卡，说明这是别名。
3. 删除实例。

## 创建多个 Cloud Foundry 服务之间的连接
{: #cf}

有关将 Cloud Foundry 服务绑定到其他 Cloud Foundry 服务的更多详细信息，请参阅[在其他服务中使用服务](../apps/reqnsi.html#add_service)。
