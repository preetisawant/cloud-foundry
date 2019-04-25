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

# 创建环境
{: #create-environment}

## 先决条件
* 确保您位于要创建环境的 {{site.data.keyword.Bluemix_notm}} 帐户中。
* 在创建 {{site.data.keyword.cfee_full_notm}} 的实例之前，请确保您具有正确的[许可权](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html)。 
* [准备 IBM Cloud 帐户](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)，以确保它可以创建 CFEE 实例所需的基础架构资源（CFEE 实例将部署到 Kubernetes 服务中的 Kubernetes 工作程序节点中）。  

## 创建 CFEE 实例
1.  打开 {{site.data.keyword.Bluemix_notm}} [目录](https://cloud.ibm.com/catalog)。

2.  在目录中找到 {{site.data.keyword.cfee_full_notm}} 服务，然后单击该服务以打开服务的概述页面。第一个页面会提供服务主要功能的概述。单击**继续**。

3.  配置要创建的 CFEE 实例：
    * 选择套餐。请参阅 [Eirini 技术预览](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini)部分以获取有关此套餐的限制的描述。
    * 输入 CFEE 实例的**名称**。
    * 选择要将环境分组到其下的**资源组**。只有在当前 IBM Cloud 帐户中您有权访问的资源组才会列在_资源组_下拉列表中，这意味着您需要有权访问帐户中至少一个资源组，才能创建 CFEE。
    * 选择要在其中供应服务实例的**地理位置**和**位置**。对于 CFEE 和支持服务，可按地理位置查看其[可用供应位置和数据中心](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标") 的列表。 

4. CFEE 实例是在 Kubernetes 集群上供应的。Cloud Foundry 单元是在 Kuberente 集群中的工作程序专区内供应的。您可以配置集群的位置、硬件和加密：
    * 为 Kubernetes 集群选择硬件隔离：   
      * _虚拟共享_：集群中的基础架构资源（例如，系统管理程序和物理硬件）在您与其他 IBM 客户之间分发，但每个工作程序节点都是您的单租户。
      * _虚拟专用_：集群中的工作程序节点在专用于您帐户的基础架构上托管。
    * 缺省情况下，集群中的数据会加密。您可以选择关闭_加密本地磁盘_。
    * 选择将供应 Kubernetes 集群的**地理位置**和**区域**。
    * 选择将部署 Kubernetes 工作程序节点的**专区**。您可以选择在同一专区（**单专区**）或多个专区（**多专区**）中供应工作程序节点。**注**：创建多专区 CFEE 需要 [VLAN 生成](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning)，这在 {{site.data.keyword.Bluemix_notm}} 帐户已[启用 VRF](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) 时也受支持。
    
    将自动为所选专区检索可用的 VLAN。如果没有可用的 VLAN，那么将自动创建这些 VLAN。
    
    **注：在隔离网络上供应：**您可以将隔离网络中的 VLAN 作为目标。在隔离网络中创建 CFEE 实例时，为了成功供应 CFEE 实例，隔离网络中的策略（例如，calico 策略或 VRA 规则）必须允许 CFEE 实例的所有出站访问。创建 CFEE 后，可以恢复出站访问限制，但对 IBM Cloud 中特定服务和微服务的出站访问除外。有关更多信息，请参阅[在隔离网络中运行](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)文档。
    
    创建 CFEE 之后，环境要供应到的 Kubernetes 集群将显示在 {{site.data.keyword.Bluemix_notm}} [仪表板](https://https://cloud.ibm.com/catalog/dashboard/apps/)中（像 IBM Cloud 帐户中的任何其他资源一样）。有关更多信息，请参阅 [Kubernetes 服务文档](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov)。

5.  配置 CFEE 的容量：
    * 为 CFEE 选择**单元数**。这些应用程序单元将托管部署到 CFEE 中的应用程序。  
    * 选择**节点大小**，该值确定 Cloud Foundry 单元（CPU 和内存）的容量。
    
    除了上面指定的应用程序单元外，还会创建其他_控制平面单元_，并保留用于操作和控制您的 CFEE 中的 Cloud Foundry 平台。 

    **注：**如果在不同的子网上供应 Kubernetes 集群中的工作程序节点，那么建议您启用 VLAN Spanning。如果禁用 VLAN Spanning，那么系统可能会阻止不同子网上工作程序节点之间的连接。有关更多信息，请参阅 [VLAN Spanning](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning) 文档。

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

## Eirini 技术预览套餐
{: #eirini}

 利用 Eirini 技术预览套餐，可以使用本机 Kubernetes 作为容器调度程序（而不是 Diego）来探索 CFEE。Kubernetes 调度程序在 CFEE 中用于在 Cloud Foundry 应用程序运行时中部署和运行应用程序，添加用户，创建组织和空间，部署应用程序以及将这些应用程序绑定到服务。请参阅 [Eirini 项目](https://www.cloudfoundry.org/project-eirini/)文档，以获取有关 Cloud Foundry Foundation 的 Eirini 孵化器项目的更多信息。以下限制适用于从 Eirini 技术预览套餐创建的 CFEE 实例：
 
* 不支持带 `containerd` 的 Kubernetes。仅支持使用 Docker 的 Kuberetes 版本，不支持使用 `containerd` 的版本。支持 Docker 的最新版本的 IBM Container Service (IKS) 为 V1.10。
* 不支持 Cloud Foundry SSH。
* 不支持 Docker 映像的 `cf push`。
* 不支持 Kubernetes 本机 Eirini 登台。从 Eirini 技术预览套餐创建的 CFEE 实例使用 Eirini 来运行应用程序，但不用于登台应用程序。Diego 单元仍用于登台应用程序。
* 不支持重新启动特定应用程序实例 (`cf restart-app-instance`)。

 
