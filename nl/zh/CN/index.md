---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-29-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 关于 {{site.data.keyword.cfee_full_notm}}
{: #about}

欢迎使用 {{site.data.keyword.cfee_full}} 服务。

通过 {{site.data.keyword.cfee_full}} (CFEE)，您可以根据需要将多个隔离的企业级 Cloud Foundry 平台实例化。{{site.data.keyword.Bluemix_notm}} Foundry Enterprise 服务的实例会在 {{site.data.keyword.Bluemix_notm}} 中您自己的帐户中运行。该环境部署在隔离的硬件（Kubernetes 集群）上。您对环境具有完全控制权，包括访问控制、容量、版本更新、资源使用情况和监视。此外，通过将 CFEE 集成到 {{site.data.keyword.Bluemix_notm}} 中，开发者能够利用其 {{site.data.keyword.Bluemix_notm}} 帐户中可用的服务。用户可以将这些服务添加到 CFEE 中，并将其绑定到部署在 CFEE 空间中的应用程序。

了解如何[**开始**](https://console.bluemix.net/docs/cloud-foundry/getting-started.html#getting-started)创建和使用 CFEE 实例。

{:shortdesc}

## CFEE 的关键元素
{: #key-elements}

下表提供了 {{site.data.keyword.cfee_full}} 服务关键元素的摘要：

|元素| 描述 |
|-----------|---------------|
|IBM Cloud 帐户|CFEE 实例在特定 IBM Cloud 帐户下创建，可根据为该帐户中的用户定义的角色和访问策略，供这些用户使用。|
||在其中创建 CFEE 实例的帐户必须是现买现付或预订帐户类型（而不是试用帐户）。|
|CFEE|用于托管应用程序的 IBM Cloud Foundry Enterprise Environment 服务。|
||在 IBM Cloud“目录”中提供。|
|CFEE 实例|由在 IBM Cloud 帐户中具有“管理员”或“编辑者”角色的用户在该帐户下创建的 IBM Cloud Foundry Enterprise Environment 服务的实例。|
||一个 IBM Cloud 帐户中可以有多个 CFEE 实例。|
||可以有一个或多个组织。|
|组织|包含一个或多个空间。|
||包含一个或多个组织管理者。|
||包含一个或多个团队成员。可以向每个团队成员授予一个或多个角色。|
||由空间内部署的应用程序生成的使用量费用在组织级别进行报告。|
|空间|包含一个或多个资源。|
||包含一个或多个应用程序。|
||包含一个或多个空间管理者。|
||包含一个或多个团队成员。每个用户必须已经是所属组织中的团队成员。可以向每个团队成员授予一个或多个角色。|
|团队成员|可以添加到跨不同帐户的一个或多个组织和空间。|
||可以向其指定同一组织和/或空间内的多个角色。|
|服务别名|IBM Cloud 中服务实例的别名。|
||允许开发者将其 IBM Cloud 帐户中可用的现有服务实例绑定到部署在 CFEE 内的空间中的应用程序。|
{:caption="表 1. 关键元素描述" caption-side="top"}

## 为 CFEE 和支持服务供应目标
{: #provisioning-targets}

下面是可用于供应的 CFEE 服务和相依服务（Kubernetes 服务、Compose for PostgreSQL 和 Cloud Object Storage 服务）所在的地理位置、位置和数据中心：

|**地理位置**|**CFEE 实例和 Kubernetes 集群**|**Cloud Object Storage**|**Compose for PostgreSQL（CF 区域）**|
|----------------------------------------|-------------------|-------------------|-------------------|
|北美|蒙特利尔 (mon01)|us-geo|us-east|
|北美|多伦多 (tor01)|us-geo|us-east|
|北美|华盛顿 (wdc04)|us-geo|us-east|
|北美|华盛顿 (wdc06)|us-geo|us-east| 
|北美|华盛顿 (wdc07)|us-geo|us-east|
|北美|达拉斯 (das10)|us-geo|us-south|
|北美|达拉斯 (das12)|us-geo|us-south|
|北美|达拉斯 (das13)|us-geo|us-south|
|北美|圣何塞 (sjc03)|us-geo|us-south|
|北美|圣何塞 (sjc04)|us-geo|us-south|
|南美|圣保罗 (sao01)|us-geo|us-south|
|欧洲|伦敦 (lon02)|eu-geo|eu-gb|
|欧洲|伦敦 (lon04)|eu-geo|eu-gb|
|欧洲|伦敦 (lon06)|eu-geo|eu-gb| 
|欧洲|阿姆斯特丹 (ams03)|eu-geo|eu-de|
|欧洲|奥斯陆 (osl01)|eu-geo|eu-de| 
|欧洲|巴黎 (par01)|eu-geo|eu-de|
|欧洲|法兰克福 (fra02)|eu-geo|eu-de|
|欧洲|法兰克福 (fra04)|eu-geo|eu-de| 
|欧洲|法兰克福 (fra05)|eu-geo|eu-de|
|亚太地区|墨尔本 (mel01)|ap-geo|au-syd|
|亚太地区|悉尼 (syd01)|ap-geo|au-syd|
|亚太地区|悉尼 (syd04)|ap-geo|au-syd| 
|亚太地区|香港特别行政区 (hkg02)|ap-geo|au-syd|
|亚太地区|香港特别行政区 (seo01)|ap-geo|au-syd|
|亚太地区|新加坡 (sng01)|ap-geo|au-syd|
|亚太地区|东京 (gok02)|ap-geo|au-syd|
|亚太地区|东京 (gok04)|ap-geo|au-syd|
|亚太地区|东京 (gok05)|ap-geo|au-syd|
{: caption="表 2. 为 CFEE 和支持服务供应目标" caption-side="top"}

**例如**，CFEE 服务可以在欧洲的三个数据中心供应：阿姆斯特丹（1 个数据中心）、法兰克福（3 个数据中心）、伦敦（3 个数据中心）、奥斯陆（1 个数据中心）和巴黎（1 个数据中心）。如果在法兰克福供应 CFEE，那么 Cloud Object Storage 服务实例将部署在 _eu-geo_ 区域，而 Compose for PostgreSQL 服务实例将部署在 _eu-de_ 公共 Cloud Foundry 区域。

您可以在 [CFEE 视频播放列表](https://ibm.biz/CFEE_Playlist){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中找到有关使用 CFEE 中服务的详细信息和演示的视频。
{:tip}
