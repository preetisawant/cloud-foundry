---

copyright:
  years: 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 监视 
{: #monitoring}

监视 {{site.data.keyword.cfee_full}} 实例及其支持的基础架构通过包含 Prometheus 和 Grafana 的开放式源代码工具集进行支持。该解决方案支持您对 Cloud Foundry 环境中度量值的警报进行分析、可视化和管理。有三个 Web 控制台用于进行监视：Grafana 控制台、Prometheus 控制台和 Prometheus AlertManager 控制台。

从 CFEE V2.2.0 开始，缺省情况下在创建环境时不启用监视工具。管理员可以在创建环境后启用监视。在 CFEE 用户界面中，转至左侧导航窗格中的_监视_页面，然后单击**启用**。启用监视会自动供应额外的 Kubernetes 工作程序节点（在同一 IBM Cloud 帐户中），并将监视工具安装到这些工作程序节点中。

**注：**要访问 {{site.data.keyword.cfee_full}} 实例中的监视功能，需要 CFEE 中的_管理员_或_编辑者_角色和支持 CFEE 实例的 Kubernetes 集群中的_操作员_角色（以及将 CFEE 分组到的资源组中的_查看者_角色）。支持 CFEE 实例的 Kubernetes 集群的缺省名称为 _`<CFEEname>`-cluster_。 

## Prometheus
{: #prometheus}

Prometheus 是一个开放式源代码系统监视和警报工具箱。自 2012 年推出以来，许多公司和组织采用了 Prometheus，该项目的开发者和用户社区非常活跃。
这是一个独立的开放式源代码项目，独立于任何公司进行维护。为了强调这一点，也为了说明项目的监管结构，Prometheus 在 2016 年加入了云原生计算基金会，成为继 Kubernetes 之后的第二个托管项目。有关更多信息，请参阅 [Prometheus 文档](https://prometheus.io/docs/introduction/overview/)。

Promtheus 生态系统由多个组件组成，其中许多组件是可选的：

* 主 Prometheus 服务器，用于抓取和存储时间序列数据。</li>
* [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/)，用于处理警报。</li>
* 各种特殊用途的导出器，如节点导出器、黑匣导出器等。</li>
* 推送网关，用于支持短期运行的作业。</li>

Prometheus 可直接从受检测作业中收集度量值，对于短期作业，还可通过中间推送网关来收集。Prometheus 会将所有收集的样本存储在本地，并对这些数据运行规则，以聚集和记录现有数据中的新时间序列，或者生成警报。 

## Grafana
{: #grafana}

Grafana 是一个开放式源代码分析平台，用于分析 Prometheus 收集的所有度量值。集群上部署的 Grafana 版本已配置为使用底层 Prometheus 数据库。Grafana 还包含一些很有价值的 Grafana 仪表板。有关更多信息，请参阅 [Grafana 文档](http://docs.grafana.org/guides/getting_started/)。

## 监视入门
{: #gettingStarted_monitor}

构成监视解决方案的 Prometheus 和 Grafana 组件已在支持 CFEE 实例的 Kubernetes 基础架构中预安装。要访问这些监视工具，需要转发 Prometheus、Prometheus AlertManager 和 Grafana 服务器的端口。这可通过 Kubernetes CLI 来完成。
下面将指导您完成安装必需 CLI、转发服务器端口以及启动控制台的步骤。

**注：**以下指示信息还在 {{site.data.keyword.cfee_full}} 用户界面中提供。打开 CFEE 实例用户界面，单击左侧导航窗格中的**监视**，然后转至**访问**选项卡以查看显示的指示信息。

### 先决条件

1. 检查[访问策略](https://console.bluemix.net/iam/#/users)，以确保您在支持环境的 Kubernetes 集群上至少具有“查看者”角色。
2. 安装 [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use)。
3. 安装 [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/)。如果您有现有的 Kubernetes CLI，建议您安装最新版本。
4. 安装 Container Service 插件：
```
ibmcloud plugin install container-service -r Bluemix
```
 
### 定制 Alertmanager 配置

Alertmanager 具有缺省的 [Alertmanager 配置](https://prometheus.io/docs/alerting/configuration/)文件，可定义用于对 Alertmanager 警报进行处理、分组和通知路由的策略。您可以下载缺省配置文件并在_监视_页面的**配置**选项卡中上传定制配置。
 
### 访问 Kubernetes 集群

1. 登录到 IBM Cloud 帐户：

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}
  
  如果您具有联合标识，请使用 __ibmcloud login -sso__ 登录到 IBM Cloud CLI。

2. 将要在其中工作的 IBM Cloud Container Service 区域（例如，us-south）设定为目标：

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}
    
3. 在 CLI 中设置集群的上下文： 

  a. 获取用于设置环境变量的命令，然后下载 Kubernetes 配置文件：

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}
    
  b. 设置 KUBECONFIG 环境变量。复制先前命令的输出并将其粘贴在终端中。命令输出应该类似于以下内容：
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### 转发服务器端口
4. 在 Kubernetes 集群中，为运行 Prometheus、AlertManager 和 Grafana 的 pod 设置端口转发。这将使您能够通过代理在本地计算机 (localhost) 上托管监视度量值：

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000 &''
  ```
  {: pre}
  
### 在本地 Web 代理上启动监视控制台

5. 启动 Grafana 控制台以查看有关所选度量值的分析。CFEE 实例中随附缺省 Grafana 仪表板。这些缺省仪表板是交互式仪表板，供您查看用于托管 CFEE 实例的基础架构（Kubernetes 集群）。启动 Grafana 控制台后，单击 Grafana 控制台顶部的**主页**按钮，以选择其中一个预先部署的仪表板（请参阅下面的列表），选择的仪表板将绘制对应度量值的图形：

   对于 CFEE V2.1.0 或更低版本，在 Grafana 中存在缺省 `admin` 用户，缺省密码设置为 `admin`。建议使用用户/密码 `admin/admin` 登录，然后将其更改为新的凭证。对于 CFEE V2.2.0 或更高版本，用户使用其 IBM 标识凭证自动进行认证。

     [启动 Grafana 控制台](https://localhost:3000)

   以下缺省仪表板随 CFEE 实例一起提供，可从_主页_下拉列表中获得。

    Cloud Foundry 仪表板：
   - _CF：单元容量_ 
        - 显示部署了 Cloud Foundry 应用程序的 Cloud Foundry 单元的常规状态。
   - _CF：Diego Cell 仪表板_ 
        - 显示 Cloud Foundry 单元和 Diego 组件的状态。
   - _CF：路由器_ 
        - 显示在 CFEE 环境中运行的 Cloud Foundry 路由器的状态。
  
   用于支持 CFEE 环境的 Kubernetes 基础架构的仪表板：
   - _部署_ 
        - 显示 Kubernetes 部署的状态。
   - _Kubernetes 集群运行状况_ 
        - 显示 Kubernetes 集群的运行状况。
   - _Kubernetes 集群状态_ 
        - 显示 Kubernetes 集群的状态。
   - _Kubernetes 资源请求_ 
        - 显示 Kubernetes 集群的已用 CPU、内存和其他参数。
   - _pod_ 
        - 显示在 Kubernetes 集群上运行的每个 pod 的详细信息。
   - _副本集_ 
        - 显示 Kubernetes 副本集的状态。       
   - _工作程序节点_ 
        - 显示 Kubernetes 集群的每个工作程序节点的详细信息。
   - _工作程序节点概述_ 
        - 显示 Kubernetes 基础架构的 CPU 和内存使用情况及其网络流量。
        
6. （可选）您还可以启动 Prometheus 控制台来查看 Prometheus 服务器收集的原始数据，以及启动 Prometheus Alertmanager 来管理 Prometheus 服务器发送的警报：

     [启动 Prometheus 服务器](https://localhost:9090)

     [启动 Prometheus Alertmanager 服务器](https://localhost:9093)

