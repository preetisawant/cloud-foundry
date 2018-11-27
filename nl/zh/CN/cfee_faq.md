---



copyright:

  years: 2018

lastupdated: "2018-11-09"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# 常见问题
{: #cfeefaq}

## IBM Cloud Foundry Enterprise Environment (CFEE) 与公共 Cloud Foundry 有何不同？
{: #cfee_diff}

您可以使用 {{site.data.keyword.cloud}} Foundry Public 来运行使用 Cloud Foundry 的云本机应用程序，以获得简单设置、强大的扩展功能和流量管理功能。您还有权轻松访问所有 {{site.data.keyword.cloud}} 服务。

您不仅可以像使用 Cloud Foundry Public 一样，将 {{site.data.keyword.cfee_full}} 用于所有内容，还可以将其用于创建和管理隔离环境，以专门为您的企业托管 Cloud Foundry 应用程序。


## 新产品与先前的 IBM Cloud Foundry 产品有何不同？
{: #cfOfferings_diff}

对于公共多租户，最值得关注的差异当然是隔离特性。对于 IBM Cloud 基础架构上的现有单租户产品，主要的两个差异是减少了基础架构占用量（因而降低了成本），以及在此类单租户环境中引入了服务集成模型。

## 在哪里可以找到 CFEE 服务？
{: #where}

您可以在{{site.data.keyword.Bluemix_notm}}[目录](https://console.stage1.bluemix.net/catalog)中找到 {{site.data.keyword.cfee_full}} 服务并对其实例化。

## 在一个区域数据中心内可以拥有多个 CFEE 环境吗？
{: #multiple-cfees}

可以，您可以根据需要在[这些区域](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 中创建任意数量的 CFEE 实例。

## 需要从某个最小容量开始吗？
{: #minimum-capacity}

需要。创建 CFEE 实例至少需要两个 Cloud Foundry 单元，每个单元 4 个核心，每个核心包含 16 GB RAM、1 个 25 GB SSD主磁盘、1 个 100 GB SSD 辅助磁盘和 1000 Mbps 网络速度。

## 在其中部署 CFEE 的底层 IaaS 是什么？
{: #why-kubs}

CFEE 服务在 Kubernetes 容器上运行，这使得基础架构成本更低，运行效率更高，因为 Kubernetes 是一种非常智能的 IaaS，可自动执行许多业务活动。 

## 创建 CFEE 时有哪些隔离选项？
{: #isolation}

对于在其中部署 CFEE 实例的 Kubernetes 基础架构类型，有两个硬件选项：_虚拟共享_或_虚拟专用_硬件。使用_虚拟共享_硬件时，工作程序节点（在其中部署 Cloud Foundry 平台容器）会在您与其他 IBM 客户之间分布。使用_虚拟专用_硬件时，工作程序节点在仅供您帐户专用的硬件上托管。请注意，在这两种情况下（_虚拟共享_和_虚拟专用_），每个工作程序节点都是客户的单租户。这意味着，运行应用程序的 Cloud Foundry 单元不会与其他客户共享。

## 可以扩展 CFEE 的容量吗？
{: #scaling}

可以，您可以根据自己的需求变化，通过添加或除去 Cloud Foundry 单元，向上或向下扩展 CFEE 容量。

## 可以将 CFEE 升级到新版本吗？该怎么做？
{: #upgrading}
可以。有新的 CFEE 版本时，CFEE 用户界面会通知您。您可控制何时更新为新版本。CFEE 版本更新由 CFEE 管理员在用户界面中进行调用。CFEE 版本更新可能会打包其组件或支持服务（例如，Cloud Foundry、Kubernetes 等）的新版本。您可首先更新 CFEE 控制平面，然后更新 Cloud Foundry 单元。更新过程已经过优化，可最大限度地减少中断。

## 创建 CFEE 实例需要多长时间？
{: #create}

您可以找到在 {{site.data.keyword.Bluemix_notm}}“目录”中列出的 CFEE 服务。您需要具有升级的 {{site.data.keyword.Bluemix_notm}} 帐户以及对 CFEE 服务及其支持的服务（Kubernetes、Cloud Object Storage 和 Compose for PostgreSQL）的许可权。您具有这些许可权后，只需为环境提供名称，然后单击_创建_即可。创建大约需要 90 分钟。

## 可以在 CFEE 中使用 {{site.data.keyword.Bluemix_notm}} 服务吗？
{: #Services-ibmcloud}

当然！通过将 CFEE 集成在 {{site.data.keyword.Bluemix_notm}} 中，CFEE 中的开发者可以创建 {{site.data.keyword.Bluemix_notm}} 服务实例（或使用现有实例），并将其绑定到部署在 CFEE 空间中的应用程序。

## 我可以在 CFEE 中提供自己的服务吗？
{: #Services-ibmcloud}

可以。管理员可以在 CFEE 中注册服务代理程序，然后使定制服务套餐可供该 CFEE 中的用户使用。本地 MCFEE 市场包含 {{site.data.keyword.Bluemix_notm}}“目录”中的服务以及 CFEE 本地服务代理程序管理的任何客户服务。

## 如何控制用户对 CFEE 的访问权？
{: #Services}

与其他任何 {{site.data.keyword.Bluemix_notm}} 服务一样，对 CFEE 的访问权可通过_身份和访问权管理_ (IAM) 进行控制。通过使用特定角色为用户分配访问策略（单独分配或通过访问组分配），可授予用户对 CFEE 的特定访问级别。除了对 CFEE 服务的访问权之外，对 CFEE 中 Cloud Foundry 组织和空间的访问权也可通过 Cloud Foundry 成员资格和分配给特定组织和空间中用户的角色进行控制。

