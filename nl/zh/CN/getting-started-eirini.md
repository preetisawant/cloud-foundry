---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Eirini 技术预览入门
{: #getting-started-eirini}

{{site.data.keyword.cfee_full}} (CFEE) 是一种云平台，用于在云中托管应用程序和服务。通过 {{site.data.keyword.cfee_full_notm}}，可以在使用量增长时轻松扩展应用程序，这简化了运行时、中间件和基础架构，使您能够专注于开发应用程序。
{: shortdesc}

本入门教程说明了如何使用 Eirini 技术预览套餐创建 {{site.data.keyword.cfee_full_notm}}，添加用户，创建组织和空间，部署应用程序以及将这些应用程序绑定到服务。请参阅 [Eirini 项目](https://www.cloudfoundry.org/project-eirini/)，以获取有关 Cloud Foundry Foundation 的 Eirini 孵化器项目的信息。

## 了解许可权
{: #permissions}

您需要正确的访问策略才能创建 {{site.data.keyword.cfee_full_notm}} 的实例。有关更多信息，请参阅[许可权](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)。

## 步骤 1：确保 {{site.data.keyword.Bluemix_notm}} 帐户可以创建基础架构资源
{: #accountprep-environment}

CFEE 实例会部署到 Kubernetes 服务的 Kubernetes 工作程序节点中。[准备 IBM Cloud 帐户](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)，以确保该帐户可以为 CFEE 实例创建必需的基础架构资源。

## 步骤 2：创建 CFEE 实例
{: #create-environment}

创建 CFEE 之前，请确保您已登录到要在其中创建环境的 {{site.data.keyword.Bluemix_notm}} 帐户中，并且具有所需的访问策略（上面的步骤 1）。

1.  打开 {{site.data.keyword.Bluemix_notm}} [目录](https://cloud.ibm.com/catalog)。

2.  在目录中找到 {{site.data.keyword.cfee_full_notm}} 服务，然后单击该服务以打开服务的概述页面。第一个页面会提供服务主要功能的概述。单击**继续**。

3.  配置要创建的 CFEE 实例：
    * 选择 _Eirini 技术预览_套餐。
    * 输入 CFEE 实例的**名称**。
    * 选择要将环境分组到其下的**资源组**。只有在当前 IBM Cloud 帐户中您有权访问的资源组才会列在_资源组_下拉列表中，这意味着您需要有权访问帐户中至少一个资源组，才能创建 CFEE。
    * 选择要在其中供应服务实例的**地理位置**和**位置**。对于 CFEE 和支持服务，可按地理位置查看其[可用供应位置和数据中心](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 的列表。 

4. CFEE 实例是在 Kubernetes 集群上供应的。Cloud Foundry 单元是在 Kuberente 集群中的工作程序专区内供应的。您可以配置集群的位置、硬件和加密：
    * 为 Kubernetes 集群选择硬件隔离：   
      * _虚拟共享_：集群中的基础架构资源（例如，系统管理程序和物理硬件）在您与其他 IBM 客户之间分发，但每个工作程序节点都是您的单租户。
      * _虚拟专用_：集群中的工作程序节点在专用于您帐户的基础架构上托管。
    * 缺省情况下，集群中的数据会加密。您可以选择关闭_加密本地磁盘_。
    * 选择将供应 Kubernetes 集群的**地理位置**和**区域**。
    * 选择将部署 Kubernetes 工作程序节点的**专区**。将自动为所选专区检索可用的 VLAN。如果没有可用的 VLAN，那么将自动创建这些 VLAN。从 CFEE V2.2.0 开始，CFEE 实例可以在**隔离网络**后面运行。您可以通过选择隔离网络中的专用 VLAN，将 CFEE 实例供应到隔离网络中。创建 CFEE 后，CFEE 的 Compose for PostgreSQL 和 Cloudant Object Storage 实例的 IP 地址以及 Kubernetes 集群的应用程序负载均衡器 ([ALB](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress)) 必须由网络管理员在隔离网络中路由，CFEE 才能正常运行。
    
    创建 CFEE 之后，环境要供应的 Kubernetes 集群将显示在 {{site.data.keyword.Bluemix_notm}} [仪表板](https://cloud.ibm.com/dashboard/apps/)中（像 IBM Cloud 帐户中的任何其他资源一样）。有关更多信息，请参阅 [Kubernetes 服务文档](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov)。

5.  配置 CFEE 的容量：
    * 为 CFEE 选择**单元数**。这些应用程序单元将托管部署到 CFEE 中的应用程序。  
    * 选择**节点大小**，该值确定 Cloud Foundry 单元（CPU 和内存）的容量。
    
    除了上面指定的应用程序单元外，还会创建其他_控制平面单元_，并保留用于操作和控制您的 CFEE 中的 Cloud Foundry 平台。 

    **注：**如果在不同的子网上供应 Kubernetes 集群中的工作程序节点，那么建议您启用 VLAN Spanning。如果禁用 VLAN Spanning，那么系统可能会阻止不同子网上工作程序节点之间的连接。有关更多信息，请参阅 [VLAN Spanning](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning) 文档。
    
6.  在 **Compose for PostgreSQL** 字段中，选择某个公共组织，然后选择该组织中某个可用的空间。在所选空间中，将会供应 Compose for PostgreSQL 实例。Compose for PostgreSQL 服务是 CFEE 服务必需的依赖项。

    **注：**在 _Compose for PostgreSQL_ 下，只有您要在其中供应 CFEE 实例（上面的步骤 4）并且有权访问的位置中的组织才可供选择。在特定的组织内，只有您对其拥有 _developer_ 访问权的空间才可供选择。 

7.  页面右侧的**订单摘要**反映了 CFEE 实例和辅助服务的成本以及每月估算总计。

8.  单击**创建**，这将打开环境仪表板并指示创建进度和状态。

**注：**创建过程启动后，CFEE 的表行会显示在 {{site.data.keyword.Bluemix_notm}} 仪表板、_资源列表_和 [Cloud Foundry 环境仪表板](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments)中。表行中的状态指示创建何时完成。

创建环境的自动化过程会将基础架构部署到 Kubernetes 集群中，并对其进行配置，使其可供随时使用。此过程需要 90 到 120 分钟。

创建 CFEE 后，您会收到多封确认供应 CFEE 和支持服务的电子邮件，还会收到通知您对应订单状态的电子邮件。

在创建 CFEE 实例时，会在同一个 IBM Cloud 帐户中创建三个额外的支持服务实例。这些支持服务实例以 CFEE 实例名称来命名。因此，创建一个 CFEE 将导致在 IBM Cloud 帐户中创建总共四个服务实例：
* CFEE 实例（“_cfeename_”）。
* Kubernetes 集群（“_cfeename_-cluster”）。该集群提供供应了 CFEE 实例的基础架构。
* Cloud Object Storage 实例（“_cfeename_-cos”）。该实例用于存储在创建 CFEE 应用程序容器期间生成的数据（例如，上传的应用程序包、buildpack 和已编译的可执行文件）。
* Compose for PosgreSQL 实例（“_cfeename_-postgres”）。该实例用于在 CFEE 实例上存储 Cloud Foundry 数据（例如，审计应用程序部署，启动和停止事件；保留 CFEE 用户成员资格、组织、空间、应用程序和服务连接的记录）。 

## 步骤 3：创建组织和空间
{: #create-orgsandspaces}

创建 {{site.data.keyword.cfee_full_notm}} 后，请参阅[创建组织和空间](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)，以获取有关如何通过创建组织和空间来构造环境的信息。{{site.data.keyword.cfee_full_notm}} 中的应用程序的作用域限定在特定空间内，而空间存在于特定组织内。组织的成员共享配额套餐、应用程序、服务实例和定制域。

创建组织时，为其分配配额。配额对资源设置限制（内存、CPU 等），可用于该组织。您可以稍后分配不同的配额。在每个 CFEE 中提供了一组预先配置的配额，但您还可以在 CFEE 用户界面的**配额**页面中创建自己的定制配额。您可以通过从配额菜单调用_复制到缺省值_操作来使定制配额成为_缺省_配额，该配额会将定制配额的值复制到缺省配额中。

**注：**位于顶部 IBM Cloud 标题中的**_管理 > 帐户 > Cloud Foundry 组织_**菜单中提供的 _Cloud Foundry 组织_页面专用于公共 IBM Cloud 组织，**不适用于 CFEE 组织**。CFEE 组织在 CFEE 实例的_组织_页面中进行管理。打开 CFEE 用户界面，然后单击**_组织_**页面以创建和管理该 CFEE 的组织。

## 步骤 4：将用户添加到组织和空间
{: #add-users}

向用于控制用户访问级别的特定角色分配下的组织和空间[添加用户](https://cloud.ibm.com/docs/cloud-foundry/add-users.html)。用户必须事先具有对 CFEE 实例的访问权，才能将这些用户添加为该 CFEE 中的组织和空间的成员。请参阅[许可权](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)。

## 步骤 5：部署和查看应用程序
{: #deploy-apps}

准备就绪后，可以使用 {{site.data.keyword.Bluemix_notm}} 命令行界面来[部署应用程序](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)。在用户界面中查看特定 CFEE 空间上下文中的已部署应用程序的列表，或以全局方式查看所有 CFEE 实例中已部署应用程序的列表。您还可以在这些视图中启动、停止或删除应用程序。

## 步骤 6：创建 IBM Cloud 服务实例或将其添加到 CFEE 空间
{: #service-instances}

[创建服务](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)或[添加 IBM Cloud 帐户中可用的现有服务](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)。CFEE 空间中有可用的服务实例后，您可以将其绑定到在该空间中部署的 CFEE 应用程序。

## 步骤 7：将应用程序绑定到服务实例
{: #bind-apps}

[绑定应用程序](https://console.bluemix.net/docs/cloud-foundry/binding.html)到服务实例别名，以便使用服务的功能。

在 [Cloud Foundry 仪表板](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中，您可以查看所有应用程序和服务的统一视图（*public* 和 *enterprise*）。在 Cloud Foundry 仪表板中，单击左侧导航窗格中的 *Public* 后，可以查看 IBM Cloud 帐户中可用的公共应用程序和服务。单击 *Enterprise* 后，可以查看所有 CFEE 环境、部署到 CFEE 空间中的应用程序，以及可用于 CFEE 空间的服务。
{:tip}

## 步骤 8：安装 Stratos Console 来管理应用程序（可选）
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
