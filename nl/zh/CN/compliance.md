---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# 合规性与法规
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) 是一个平台即服务。因此，客户机可以自由将服务实例用于它能够支持的任何内容。CFEE 和相依服务有权访问尽可能最少量的个人数据。

但是，应该明确指出的是，尽管 CFEE 控制平面（通过 UI/API/CLI）不会处理敏感数据（例如，HIPAA 数据），客户也应负责确保自己负责任地使用其 CFEE，因为所有依赖项均由客户在其 {{site.data.keyword.Bluemix_notm}} 帐户中管理和拥有。 

我们建议遵循以下最佳实践：
*  不要修改使用 CFEE 创建的相依服务（Kubernetes、Cloud Object Storage 和 Compose for PostgreSQL）。
*  通过 CFEE 服务本身（用户界面或命令行界面）而不是通过 Kubernetes 服务来更新和管理 CFEE。

Kubernetes 集群用于保存 CFEE 基础架构的大部分内容以及在 CFEE 上运行的所有应用程序，因为 Cloud Foundry 单元是基于 Kubernetes 节点进行部署的。此集群由客户的 SoftLayer 帐户拥有并管理。

CFEE 使用 Compose for PostgreSQL 来保存有关组织、空间、用户和角色的元数据。如果按照建议使用 CFEE 实例，那么不会公开任何敏感数据。但是，如果客户决定使用与其客户相关的个人或敏感信息来命名其组织和空间，那么 PostgreSQL 数据库可能会包含 HIPAA 或其他类型的敏感信息。

CFEE 使用此 Cloud Object Storage 实例来保存应用程序的 Droplet，以便可以对其执行部署、停止和启动等操作。这意味着 Cloud Object Storage 实例不会运行应用程序，而只是保存其映像。因此，如果遵循最佳实践使用 Cloud Object Storage 实例，那么它不会保存任何 HIPAA 敏感信息。客户应负责确保不将任何个人数据硬编码到其任何应用程序中（测试数据等）。
