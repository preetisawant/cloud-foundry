---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 入门教程
{: #getting-started}

{{site.data.keyword.cfee_full}} 是一种云平台，用于在云中托管应用程序和服务。通过 {{site.data.keyword.cfee_full_notm}}，可以在使用量增长时轻松扩展应用程序，这简化了运行时、中间件和基础架构，使您能够专注于开发应用程序。
{: shortdesc}

本入门教程说明了如何创建 {{site.data.keyword.cfee_full_notm}}，添加用户，创建组织和空间，部署应用程序以及将这些应用程序绑定到服务。

## 了解许可权
{: #permissions}

要使用 {{site.data.keyword.cfee_full_notm}} 的实例，服务用户必须具有正确的许可权。有关更多信息，请参阅[许可权](https://console.bluemix.net/docs/cloud-foundry/permissions.html)。

## 步骤 1：确保 {{site.data.keyword.Bluemix_notm}} 帐户可以创建基础架构资源
{: #accountprep-environment}

CFEE 实例会部署在基础架构资源上，即部署在 Kubernetes 服务中的 Kubernetes 工作程序节点上。[准备 IBM Cloud 帐户](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html)，以确保该帐户可以为 CFEE 实例创建必需的基础架构资源。

## 步骤 2：创建 CFEE 实例
{: #creating-environment}

创建 CFEE 之前，请确保您已登录到要在其中创建环境的 {{site.data.keyword.Bluemix_notm}} 帐户中，并且具有所需的访问策略（根据上面的步骤 1）。

1.  打开 {{site.data.keyword.Bluemix_notm}} [目录](https://console.bluemix.net/catalog)。

2.  在目录中找到 {{site.data.keyword.cfee_full_notm}} 服务，然后单击该服务以打开服务的概述页面。

3.  创建页面的第一个页面会提供服务主要功能的概述。单击**继续**。

4.  提供以下内容，以配置要创建的 CFEE 实例：
    * 选择套餐（在 Beta 期间，套餐可用性可能会受到限制）。
    * 输入服务实例的**名称**。
    * 选择要在其中供应服务实例的**位置**。对于 CFEE 和配套服务，可按地理位置查看其[可用供应位置和数据中心](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 的列表。 
    * 选择用于 Cloud Foundry 环境的**单元数**。
    * 选择**机器类型**，这将确定 Cloud Foundry 单元的大小（CPU 和内存）。
    * 选择要将环境分组到其下的**资源组**。只有在当前 IBM Cloud 帐户中您有权访问的资源组才会列在_资源组_下拉列表中，这意味着您需要有权访问帐户中至少一个资源组，才能创建 CFEE。

5.  在 **Compose for PostgreSQL** 字段中，选择某个公共组织，然后选择该组织中某个可用的空间。在所选空间中，将会供应 Compose for PostgreSQL 实例。Compose for PostgreSQL 服务是 CFEE 服务必需的依赖项。

**注：**只有您要在其中供应 CFEE 实例（上面步骤 4）并且有权访问的位置中的组织才可供选择。在特定的组织内，只有您对其拥有 _developer_ 访问权的空间才可供选择。 

6.  （可选）打开**基础架构**部分，以查看支持 CFEE 实例的 Kubernetes 集群的属性。请注意，**工作程序节点数**等于单元数加 2（这两个供应的 Kubernetes 工作程序节点支持 CFEE 控制平面）。{{site.data.keyword.Bluemix_notm}} [仪表板](https://console.bluemix.net/dashboard/apps/)上会显示在哪个 Kubernetes 集群上部署了环境。有关更多信息，请参阅 [Kubernetes 服务文档](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov)。

**注：**如果在不同的子网上供应 Kubernetes 集群中的工作程序节点，那么建议您启用 VLAN Spanning。如果禁用 VLAN Spanning，那么系统可能会阻止不同子网上工作程序节点之间的连接。有关更多信息，请参阅 [VLAN Spanning](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning) 文档。

7.  页面右侧的**订单摘要**反映了 CFEE 实例和辅助服务的成本以及每月估算总计。

8.  单击**创建**，这将打开环境仪表板并指示创建进度和状态。

9.  启动供应后，该环境会显示在 {{site.data.keyword.Bluemix_notm}}“仪表板”以及 [Cloud Foundry 环境仪表板](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments)中。供应完成时，状态会予以指示。

创建环境的自动化过程会将基础架构部署到 Kubernetes 集群中，并对其进行配置，使其可供随时使用。此过程需要 90 到 120 分钟。

成功创建环境后，您会收到多封确认供应 CFEE 和配套服务的电子邮件，还会收到通知您对应订单状态的电子邮件。

## 步骤 3：创建组织和空间

创建 {{site.data.keyword.cfee_full_notm}} 后，请参阅[创建组织和空间](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html)，以获取有关如何通过创建组织和空间来构造环境的信息。{{site.data.keyword.cfee_full_notm}} 中的应用程序的作用域限定在特定空间内，而空间存在于特定组织内。组织的成员共享配额套餐、应用程序、服务实例和定制域。

**注：**位于顶部 IBM Cloud 标题中的**_管理 > 帐户 > Cloud Foundry 组织_**菜单中提供的 _Cloud Foundry 组织_页面专用于公共 IBM Cloud 组织，**不适用于 CFEE 组织**。CFEE 组织在 CFEE 实例的_组织_页面中进行管理。打开 CFEE 用户界面，然后单击**_组织_**页面以创建和管理该 CFEE 的组织。

## 步骤 4：向组织和空间添加用户

向用于控制用户访问级别的特定角色分配下的组织和空间[添加用户](https://console.bluemix.net/docs/cloud-foundry/add-users.html)。用户必须事先具有对 CFEE 实例的访问权，才能将这些用户添加为该 CFEE 中的组织和空间的成员。请参阅[许可权](https://console.bluemix.net/docs/cloud-foundry/permissions.html)。

## 步骤 5：部署和查看应用程序

准备就绪后，可以使用 {{site.data.keyword.Bluemix_notm}} 命令行界面来[部署应用程序](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)。在用户界面中查看特定 CFEE 空间上下文中的已部署应用程序的列表，或以全局方式查看所有 CFEE 实例中已部署应用程序的列表。您还可以在这些视图中启动、停止或删除应用程序。

## 步骤 6：使用服务

[创建服务](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#creating-services_inspace)或[添加 IBM Cloud 帐户中可用的现有服务](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#adding-services_inspace)。CFEE 空间中有可用的服务实例后，您可以将其绑定到在该空间中部署的 CFEE 应用程序。

## 步骤 7：将应用程序绑定到服务实例

[绑定应用程序](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#bind_services)到服务实例别名，以便使用服务的功能。

您了解 [Cloud Foundry 仪表板](https://console.bluemix.net/dashboard/cloudfoundry/overview)吗？在该仪表板中，您可以查看一个包含 {{site.data.keyword.Bluemix_notm}}（_Public_ 和 _Enterprise_ (CFEE)）中所有应用程序和服务的统一视图。在 Cloud Foundry 仪表板中，单击左侧导航窗格中的 _Public_ 后，可以查看 IBM Cloud 帐户中可用的公共应用程序和服务。单击 _Enterprise_ 后，可以查看所有 CFEE 环境、部署到 CFEE 空间中的应用程序，以及可用于 CFEE 空间的服务。
{:tip}

## 步骤 8：安装 Stratos Console 来管理应用程序（可选）

Stratos Console 是用于使用 Cloud Foundry 的基于 Web 的开放式源代码工具。可以选择在特定 CFEE 环境中安装并使用 Stratos Console 应用程序，以用于管理该环境的组织、空间和应用程序。

在 CFEE 实例中具有 IBM Cloud“管理员”或“编辑者”角色的用户可以在该 CFEE 实例中安装 Stratos Console 应用程序。

要安装 Strateos Console 应用程序，请执行以下操作：

1. 打开要安装 Stratos Console 的 CFEE 实例。
2. 单击概述页面上的**安装 Stratos Console**。该按钮仅对具有对该 CFEE 实例的管理员或编辑者许可权的用户显示。
3. 在“安装 Stratos Console”对话框中，选择安装选项。您可以在 CFEE 控制平面上或其中一个单元中安装 Stratos Console 应用程序。选择 Stratos Console 的版本以及要安装的应用程序实例数。如果是在单元中安装 Stratos Console 应用程序，那么系统将提示您提供部署应用程序的组织和空间。
4. 单击**安装**。

安装该应用程序需要大约 5 分钟时间。安装完成后，概述页面上原先显示的_安装 Stratos Console_ 按钮将改为 **Stratos Console** 按钮。_Stratos Console_ 按钮用于启动该控制台，并且可供所有具有 CFEE 实例访问权的用户使用。组织和空间成员资格分配可能会限制用户在 Stratos Console 中可以查看和管理的内容。

要启动 Stratos Console，请执行以下操作：

1. 打开安装了 Stratos Console 的 CFEE 实例。
2. 单击概述页面上的 **Stratos Console**。
3. Stratos Console 会在单独的浏览器选项卡中打开。首次打开该控制台时，由于使用的是自签名证书，系统会提示您接受两个连续警告。
4. 单击**登录**以打开该控制台。不需要任何凭证，因为应用程序使用的是您的 {{site.data.keyword.Bluemix_notm}} 凭证。

有关 CFEE API 的信息，请参阅 CFEE [API 文档](https://console.bluemix.net/apidocs/cfaas){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。
{:tip}
