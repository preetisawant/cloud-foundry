---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment 中的新增内容

本文档描述了 {{site.data.keyword.cfee_full_notm}} 服务到目前为止发布的每个版本中的新增内容。


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
