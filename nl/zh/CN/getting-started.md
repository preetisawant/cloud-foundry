---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 入门教程
{: #getting-started}

{{site.data.keyword.cfee_full}} (CFEE) 是一种云平台，用于在云中托管应用程序和服务。通过 {{site.data.keyword.cfee_full_notm}}，可以在使用量增长时轻松扩展应用程序，这简化了运行时、中间件和基础架构，使您能够专注于开发应用程序。
{: shortdesc}

本入门教程说明了如何创建 {{site.data.keyword.cfee_full_notm}}，添加用户，创建组织和空间，部署应用程序以及将这些应用程序绑定到服务。

**注:**以下步骤适用于从**标准**套餐创建的 CFEE。如果从 **Eirini 技术预览**套餐创建了此 CFEE，请仅执行**步骤 1 到 6** 和步骤 **11**。步骤 8 到 11 中描述的功能在 _Eirini 技术预览_套餐中不受支持。请参阅 [Eirini 技术预览入门](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)。利用 _Eirini 技术预览_套餐，可以使用本机 Kubernetes 作为容器调度程序（而不是 Diego）来探索 CFEE。Kubernetes 调度程序在 CFEE 中用于在 Cloud Foundry 应用程序运行时中部署和运行应用程序，添加用户，创建组织和空间，部署应用程序以及将这些应用程序绑定到服务。 

## 步骤 1：创建 CFEE 实例
{: #create-environment}

您可以从 {{site.data.keyword.Bluemix_notm}}“目录”创建 {{site.data.keyword.cfee_full_notm}} (CFEE) 的实例。在创建 CFEE 实例之前，请访问[创建环境](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment)文档，以获取有关准备 {{site.data.keyword.Bluemix_notm}} 帐户、确保正确许可权以及创建 CFEE 实例的步骤的指导信息。


## 步骤 2：创建组织和空间
{: #create-orgsandspaces}

创建 {{site.data.keyword.cfee_full_notm}} 后，请参阅[创建组织和空间](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)，以获取有关如何通过创建组织和空间来构造环境的信息。{{site.data.keyword.cfee_full_notm}} 中的应用程序的作用域限定在特定空间内，而空间存在于特定组织内。组织的成员共享配额套餐、应用程序、服务实例和定制域。

创建组织时，为其分配配额。配额对可用于该组织的资源（内存、CPU 等）设置限制。您可以稍后分配不同的配额。在每个 CFEE 中提供了一组预先配置的配额，但您还可以在 CFEE 用户界面的**配额**页面中创建自己的定制配额。您可以通过从配额菜单调用_复制到缺省值_操作来使定制配额成为_缺省_配额，该配额会将定制配额的值复制到缺省配额中。

**注：**位于顶部 IBM Cloud 标题中的**_管理 > 帐户 > Cloud Foundry 组织_**菜单中提供的 _Cloud Foundry 组织_页面专用于公共 IBM Cloud 组织，**不适用于 CFEE 组织**。CFEE 组织在 CFEE 实例的_组织_页面中进行管理。打开 CFEE 用户界面，然后单击**_组织_**页面以创建和管理该 CFEE 的组织。

## 步骤 3：为组织和空间添加用户
{: #add-users}

向用于控制用户访问级别的特定角色分配下的组织和空间[添加用户](https://console.bluemix.net/docs/cloud-foundry/add-users.html)。用户必须事先具有对 CFEE 实例的访问权，才能将这些用户添加为该 CFEE 中的组织和空间的成员。请参阅[许可权](https://console.bluemix.net/docs/cloud-foundry/permissions.html)。

## 步骤 4：部署和查看应用程序
{: #deploy-apps}

准备就绪后，可以使用 {{site.data.keyword.Bluemix_notm}} 命令行界面来[部署应用程序](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html)。在用户界面中查看特定 CFEE 空间上下文中的已部署应用程序的列表，或以全局方式查看所有 CFEE 实例中已部署应用程序的列表。您还可以在这些视图中启动、停止或删除应用程序。

## 步骤 5：在 CFEE 空间中创建或添加 IBM Cloud 服务实例
{: #service-instances}

[创建服务](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)或[添加 IBM Cloud 帐户中可用的现有服务](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)。CFEE 空间中有可用的服务实例后，您可以将其绑定到在该空间中部署的 CFEE 应用程序。

## 步骤 6：将应用程序绑定到服务实例
{: #bind-apps}

[绑定应用程序](https://cloud.ibm.com/docs/cloud-foundry/binding.html)到服务实例别名，以便使用服务的功能。

在 [Cloud Foundry 仪表板](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中，您可以查看所有应用程序和服务的统一视图（*public* 和 *enterprise*）。在 Cloud Foundry 仪表板中，单击左侧导航窗格中的 *Public* 后，可以查看 IBM Cloud 帐户中可用的公共应用程序和服务。单击 *Enterprise* 后，可以查看所有 CFEE 环境、部署到 CFEE 空间中的应用程序，以及可用于 CFEE 空间的服务。
{:tip}

## 步骤 7：启用审计和日志记录持久存储（可选）
{: #enable-auditingandlogging}

启用[审计事件](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing)和[日志记录持久存储](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging)的环境。

## 步骤 8：启用监视工具（可选）
{: #enable-monitoring}

在 CFEE 实例 V2.2.0 或更高版本上，不会自动供应监视工具。在创建 CFEE 实例后，CFEE 管理员可以[启用监视工具](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)。监视工具集包含 Prometheus、Grafana 和 Alertmanager。

## 步骤 9：创建并保护 Cloud Foundry 域（可选）
{: #create-domains}

为 CFEE（共享域）中的所有应用程序或为特定组织（专用域）创建[域](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains)，并使用 SSL 证书保护这些域。

## 步骤 10：配置 Cloud Foundry buildback 的优先级划分顺序
{: #create-buildpacks}

Buildpack 为部署在 Cloud Foundry 环境中的应用程序提供运行时支持，为应用程序自动配置运行时并处理其依赖项。Cloud Foundry 包含一组用于通用语言和框架的 buildpack。[了解更多](https://docs.cloudfoundry.org/buildpacks/)有关 Cloud Foundry buildpack 的信息。  

您可以在 CFEE 用户界面的 **Buildpack** 页面中创建并上传定制 buildpack。buildpack 在优先级列表中具有序数位置。在应用程序登台期间，Cloud Foundry 将针对 buildpack 集检查应用程序的兼容性，从位置 1 开始。兼容性检查会顺着优先级列表继续，直到找到兼容的 buildpack。确保 buildpack 集的优先级顺序满足开发团队的需求。您可以通过将 buildpack 名称拖放到其他位置来更改 buildpack 在优先级顺序中的位置。您还可以通过 [Cloud Foundry CLI](https://docs.cloudfoundry.org/adminguide/buildpacks.html) 来管理 buildpack。

## 步骤 11：安装 Stratos Console 来管理应用程序（可选）
{: #install-stratos}

Stratos Console 是用于使用 Cloud Foundry 的基于 Web 的开放式源代码工具。可以选择在特定 CFEE 环境中安装并使用 Stratos Console 应用程序，以用于管理该环境的组织、空间和应用程序。

在 CFEE 实例中具有 IBM Cloud“管理员”或“编辑者”角色的用户可以在该 CFEE 实例中安装 Stratos Console 应用程序。

要安装 Strateos Console 应用程序，请执行以下操作：

1. 打开要安装 Stratos Console 的 CFEE 实例。
2. 单击概述页面上的**安装 Stratos Console**。该按钮仅对具有对该 CFEE 实例的管理员或编辑者许可权的用户显示。
3. 在“安装 Stratos Console”对话框中，选择安装选项。可以在 Cloud Foundry 单元或 Kubernetes 集群中安装 Stratos 应用程序。选择 Stratos Console 的版本以及要安装的应用程序实例数。如果是在 Cloud Foundry 单元中安装 Stratos Console 应用程序，那么系统将提示您提供部署应用程序的组织和空间。
4. 单击**安装**。

安装该应用程序需要大约 5 分钟时间。安装完成后，概述页面上原先显示的_安装 Stratos Console_ 按钮将改为 **Stratos Console** 按钮。_Stratos Console_ 按钮用于启动该控制台，并且可供所有具有 CFEE 实例访问权的用户使用。组织和空间成员资格分配可能会限制用户在 Stratos Console 中可以查看和管理的内容。

要启动 Stratos Console，请执行以下操作：

1. 打开安装了 Stratos Console 的 CFEE 实例。
2. 单击概述页面上的 **Stratos Console**。
3. Stratos Console 会在单独的浏览器选项卡中打开。首次打开该控制台时，由于使用的是自签名证书，系统会提示您接受两个连续警告。
4. 单击**登录**以打开该控制台。不需要任何凭证，因为应用程序使用的是您的 {{site.data.keyword.Bluemix_notm}} 凭证。

## 其他资源
{: #additional-resources}

您可以使用 `ibmcloud CFEE` CLI 命令在 CFEE 中执行某些管理任务。这些命令允许您获取有关 CFEE 实例的信息，以及管理其组织和空间的信息。请参阅 [IBM Cloud CLI CFEE 命令参考](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。

您可以在 [CFEE 视频播放列表](https://ibm.biz/CFEE-Playlist){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中找到有关各种 CFEE 主题的深入讨论和演示的视频。

有关 CFEE API 的信息，请参阅 CFEE [API 文档](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。
