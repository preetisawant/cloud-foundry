---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment 中的新增内容

本文档描述了 {{site.data.keyword.cfee_full_notm}} 服务到目前为止发布的每个版本中的新增内容。

## V2.2.0
{: #v220}

_发布日期：_2019-04-01

CFEE V2.2.0 包含以下版本的组成组件：
* Cloud Foundry：V2.7.1.15.5
* Cloud Foundry API：V2.115.0
* CFEE Buildpack：V0.1.5
* IBM Kubernetes 服务：未提供版本更新。**重要信息：**我们建议在更新到 CFEE V2.2.0 之前，将 CFEE Kubernetes 集群更新为 V1.13（在隔离网络中运行 CFEE 实例时是必需的）。

{{site.data.keyword.cfee_full_notm}} V2.0.0 服务 (CFEE) 中发布了以下更改。要更新 CFEE 的版本，请转至 CFEE 用户界面中的**更新和缩放**页面，然后单击**更新**：

* 用于在**多专区** Kubernetes 集群中**创建** CFEE 实例的新选项。在多专区集群上创建的 CFEE 实例会分发应用程序实例，不仅跨数据中心内的工作程序节点分发，还跨数据中心分发，使应用程序更能抵御基础架构中断。此外，多专区 CFEE 可以通过添加更多单元或从当前专区中除去现有单元来进行**缩放**。请注意，一旦创建了 CFEE 实例，就无法在多专区 CFEE 中添加或除去专区。
* 现在，CFEE V2.2.0 实例可以[在**隔离网络**中运行](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)。请注意，如果 CFEE 实例部署在隔离网络中的 VLAN 中，那么[必须识别并正确路由](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points)一些端点（IP 地址），以使 CFEE 实例能够正常运行。CFEE 实例需要 Kubernetes 集群 V1.13 才能在隔离网络中运行。
* 新功能，用于通过内部 IBM 网络将应用程序（部署到 CFEE 空间）绑定到服务实例。该功能允许在不访问公用因特网的情况下使用支持 IBM Cloud Service 端点的服务。
* **监视**工具：
    * 缺省情况下，在创建 CFEE 时，不会再供应监视工具（Prometheus、Grafana 和 Alertmanager）。在 CFEE V2.2.0 中，只有 CFEE 管理员显式启用了监视工具时，才会供应监视工具。此外，在启用时，不会再将监视工具供应到 CFEE 控制平面工作程序节点中。它们在控制平面外部供应给自己的工作程序节点。要启用和供应监视工具，请转至 CFEE _监视_页面（在左侧导航窗格中），然后单击**启用监视**。 
    * 在将现有 CFEE 更新到 V2.2.0 时，会从控制平面中删除现有监视工具。监视工具的任何现有定制配置都将丢失。 
    *  新功能，用于将缺省 [Alertmanager 配置](https://prometheus.io/docs/alerting/configuration/)替换为定制配置，该配置允许您定制警报的处理、分组和通知路由。在_监视_页面中，您将能够_下载_缺省配置文件，并从本地文件系统_上传_配置文件。请参阅配置文件[示例](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml)。
* 新功能，用于在 {{site.data.keyword.Bluemix_notm}} [_资源列表_](https://cloud.ibm.com/resources)和 CFEE 用户界面中标记 CFEE 实例。
* 全面改进 {{site.data.keyword.Bluemix_notm}} [**Cloud Foundry 仪表板**](https://cloud.ibm.com/dashboard/cloudfoundry/overview)的用户体验。_Cloud Foundry 仪表板_显示在 CFEE 空间中创建了别名的 CFEE 实例、应用程序和公共服务的全局视图。 

**注：**创建新的 CFEE 实例时，提供了新的 **Eirini 技术预览**套餐。此套餐独立于上述 V2.2.0，仅适用于_标准_套餐。利用 Eirini 技术预览套餐，可以使用本机 Kubernetes 作为容器调度程序（而不是 Diego）来探索 CFEE。有关更多信息，请参阅 [Eirini 技术预览入门](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)。

请参阅此[简短视频](https://ibm.biz/CFEE-V220){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中有关 CFEE V2.1.0 中新增内容的演示。


## V2.1.1
{: #v211}

_发布日期：_2019-03-20

{{site.data.keyword.cfee_full_notm}} V2.1.1 服务 (CFEE) 中发布了以下更改。要更新 CFEE 的版本，请在 CFEE 用户界面中，转至_更新和扩展_页面。

* 已解决导致无法成功供应的问题。 


## V2.1.0
{: #v210}

_发布日期：_2019-02-20

**注：**只能从 V**2.0.2** 更新到此版本。在更新到 V2.1.0 之前，请更新为 V2.0.2。

{{site.data.keyword.cfee_full_notm}} V2.1.0 服务 (CFEE) 中发布了以下更改。要更新 CFEE 的版本，请转至 CFEE 用户界面中的**更新和缩放**页面，然后单击**更新**：

* 新的自动缩放功能，用于根据定制规则自动缩放 Cloud Foundry 应用程序实例。可以从 CLI 以及从 Stratos 控制台访问自动缩放。在 CFEE 用户界面的_概述_页面中，可以选择安装和启动 Stratos 控制台。在 Stratos 控制台的_应用程序_页面中，选择一个应用程序，并查找**自动缩放**选项卡。单击*创建策略*以启动自动缩放编辑器，用于定义目标应用程序的缩放策略。有关更多信息，请参阅[自动缩放文档](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps)。
* 新功能，用于在 CFEE 用户界面中管理 buildapck，包括在优先级列表中拖放定位 buildpack。该功能在 CFEE 用户界面（而不是 Stratos 控制台）的新 **Buildpack** 页面中可用。在该发行版中，只能通过用户界面添加或更新大小为 1 MB（或更小）的 buildpack zip 文件。您可以使用 `cf create-buildpack` 和 `cf update-buildpack` 命令来上传大于 1 MB 的 buildpack zip 文件。 
* 新功能，用于从用户界面管理组织配额，包括可视化哪些组织正在使用特定配额。该功能在 CFEE 用户界面（而不是 Stratos 控制台）的新**配额**页面中可用。您可以创建新的配额并编辑现有配额。您还可以通过从配额菜单中调用**复制到缺省值**，使用任何现有配额中的值来更新缺省配额的值。
* 用户界面中的新**入门**页面将指导用户执行最重要的任务来设置和使用环境。
* **标记**可以添加到 IBM Cloud 资源列表中的 CFEE 实例。资源列表中添加的标记也会显示在 CFEE 概述页面的标题中。
* **Cloud Foundry** V2.7.21。
* **Stratos** 控制台 V2.3.0，其中包含安全补丁。请注意，只更新 CFEE 版本是不会更新 Stratos 控制台版本的。您需要删除并重新安装 Stratos 控制台（在 CFEE 概述页面中），它会自动选取最新的 Stratos 控制台版本。
* 用户可以从 CFEE 的概述页面中的溢出菜单导航到 CFEE 的 Kubernetes **集群**页面。

**注：**如果从 V2.0.x 版本更新为 CFEE V2.1.0，那么更新会通过单个_更新_操作来执行，该操作会按顺序自动更新控制平面和序列中的单元。如果从 V1.x.x 版本进行更新，那么更新需要两个单独的_更新_操作，一个用于更新控制平面（第一个），另一个用于更新单元。

请参阅此[简短视频](https://ibm.biz/CFEE-V210){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中有关 CFEE V2.1.0 中新增内容的演示。


## V2.0.2
{: #v202}

_发布日期：_2019-02-08

{{site.data.keyword.cfee_full_notm}} V2.0.2 服务 (CFEE) 中发布了以下更改。要更新 CFEE 的版本，请在 CFEE 用户界面中，转至_更新和扩展_页面。

* 已解决导致无法成功更新版本的问题。此版本是更新为 V**2.1.0** 的先决条件。


## V2.0.1
{: #v201}

_发布日期：_2019 年 1 月 10 日

{{site.data.keyword.cfee_full_notm}} V2.0.1 服务 (CFEE) 中发布了以下更改。要更新 CFEE 的版本，请在 CFEE 用户界面中，转至_更新和扩展_页面。

* 解决了阻止定制域正常运行的问题。
* 解决了导致在检索新度量值时无法获得组织度量值的问题。


## V2.0.0
{: #v200}

_发布日期：_2018 年 12 月 13 日

{{site.data.keyword.cfee_full_notm}} V2.0.0 服务 (CFEE) 中发布了以下更改。要更新 CFEE 的版本，请在 CFEE 用户界面中，转至_更新和扩展_页面。

* 改进了 CFEE 版本更新弹性。
* 改进了 CFEE 实例的运行可用性和弹性。
* 通过客户端证书更安全地访问应用程序，允许服务器仅向经过认证的客户机授予应用程序访问权。
* 现在，创建 CFEE 实例时，会在该 CFEE 服务实例所在的资源组中（而不是在“Default”资源组下）创建支持 Kubernetes 集群和 Cloud Object Storage 服务实例。
* 安全补丁。
* 改进了 `ibmcloud cfee` CLI：
    * 新增用于通过 CFEE 空间创建 IBM Cloud 服务实例并将其添加到该 CFEE 空间的命令（`ibmcloud cfee service-create` 和 `ibmcloud cfee service-alias-create`）。
    * 新增用于扩展 CFEE 容量的命令（`ibmcloud cfee scale-up` 和 `ibmcloud cfee scale-down`）。
    * 改进了用于管理 CFEE 实例的命令 (`ibmcloud cfee environments`)。
    
      更新 ibmcloud CLI (`ibmcloud update`) 以访问这些命令增强功能，并可发出 `ibmcloud cfee -help` 来获取更多详细信息。
      
**注**：将 CFEE 实例更新到 V2.0.0 时，只需要一个_更新_操作就可同时更新控制平面和单元。CFEE 控制平面和单元不需要分别进行更新。


## V1.1.2
{: #v112}

_发布日期：_2018 年 12 月 7 日

{{site.data.keyword.cfee_full_notm}} V1.1.2 服务中发布了以下更改：
* 金奈和米兰的新数据中心 che01 和 mil01 现在可用于供应 CFEE 实例。
* 安全补丁。

## V1.1.1
{: #v111}

_发布日期：_2018 年 11 月 28 日

{{site.data.keyword.cfee_full_notm}} V1.1.1 服务中发布了以下更改：
* 安全补丁。
   
## V1.1.0
{: #v110}

_发布日期：_2018 年 11 月 16 日

{{site.data.keyword.cfee_full_notm}} V1.1.0 服务中发布了以下更改：

* 新功能：
   * 可以在您的 IBM Cloud 帐户专用基础架构上托管的[虚拟专用](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) Kubernetes 工作程序节点上供应 CFEE 实例。
   * 东京的新数据中心 tok05 可用于供应 CFEE 实例。
   * 将 CFEE 实例[更新](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update)为新版本。
   * 通过添加或删除 Cloud Foundry 单元来[扩展](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) CFEE 实例的容量。
   * 通过与自动配置的 IBM Cloud Activity Tracker 服务实例进行集成，[审计](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) Cloud Foundry 活动。
   * 通过自动配置的 IBM Cloud Log Analysis 服务实例，持久存储 Cloud Foundry [日志事件](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging)。
   * 运行状况检查视图，用于指示 CFEE 组件的运行状态。
   * 新增用于在命令行界面 (CLI) 上执行 CFEE 相关操作的命令：
     * `ibmcloud cfee create`、`ibmcloud cfee create-locations` 和 `ibmcloud cfee create-status` 命令用于通过命令行界面创建 CFEE 实例，获取可供应 CFEE 的可用数据中心列表，以及检查要创建的 CFEE 的供应状态。
     * `ibmcloud cfee create-permission-get` 和 `ibmcloud cfee create-permission-set` [命令](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating)用于检索和设置创建 CFEE 实例所需的许可权。该命令聚集并简化了 CFEE 服务和所需支持服务的许可权设置。
     * `ibmcloud catalog blacklist` 命令用于针对 IBM Cloud 帐户中的用户简化 IBM Cloud 服务的[可视性控制](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)。

* 已解决的问题：
   *  已解决的问题：访问单元度量值时发生间歇性错误
<br/>   
请参阅此[简短视频](https://ibm.biz/CFEE-V110){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中有关 CFEE V1.1.0 中新增内容的演示。您还可以在 [CFEE 视频播放列表](https://ibm.biz/CFEE-Playlist){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中找到有关各种 CFEE 主题的其他视频。
