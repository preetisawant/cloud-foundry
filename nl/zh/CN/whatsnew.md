---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment 中的新增内容

本文档描述了 {{site.data.keyword.cfee_full_notm}} 服务到目前为止发布的每个版本中的新增内容。

## V1.1.0
{: #v101}

_发布日期：_2018 年 11 月 16 日

{{site.data.keyword.cfee_full_notm}} V1.1.0 服务中发布了以下更改：

* 新功能：
   * 将 CFEE 实例[更新](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update)为新版本。
   * 通过添加或删除 Cloud Foundry 单元来[扩展](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) CFEE 实例的容量。
   * 通过与自动配置的 IBM Cloud Activity Tracker 服务实例进行集成，[审计](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) Cloud Foundry 活动。
   * 通过自动配置的 IBM Cloud Log Analysis 服务实例，持久存储 Cloud Foundry [日志事件](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging)。
   * 新增 `ibmcloud cfee` [命令](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating)，用于检索和设置创建 CFEE 实例的许可权。该命令聚集并简化了 CFEE 服务和所需支持服务的许可权设置。
   * 新增 `ibmcloud catalog blacklist` 命令，用于简化 IBM Cloud 服务的[可视性控制](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)，即控制 IBM Cloud 服务对 IBM Cloud 帐户中用户的可视性。

* 已解决的问题：
   *  已解决的问题：访问单元度量值时发生间歇性错误
   
请参阅此[简短视频](https://ibm.biz/CFEE-V110){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中有关 CFEE V1.1.0 中新增内容的演示。

您可以在 [CFEE 视频播放列表](https://ibm.biz/CFEE-Playlist){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中找到有关各种 CFEE 主题的其他视频。
