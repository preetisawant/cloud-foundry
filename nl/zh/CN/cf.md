---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cloud Foundry 如何用于 {{site.data.keyword.cloud_notm}}
{: #howwork}

将某个应用程序部署到 Cloud Foundry 时，必须使用足够的信息来配置 {{site.data.keyword.cloud_notm}} 才能支持该应用程序。

* 对于移动应用程序，{{site.data.keyword.cloud_notm}} 包含表示移动应用程序后端的工件，例如移动应用程序用于与服务器进行通信的服务。
* 对于 Web 应用程序，必须确保将运行时和框架相关信息传递给 {{site.data.keyword.cloud_notm}}，以便 {{site.data.keyword.cloud_notm}} 能够设置正确的执行环境来运行应用程序。

每个执行环境（包括移动应用程序和 Web 应用程序）都与其他应用程序的执行环境相隔离。即使这些应用程序位于同一物理机器上，其执行环境也相互隔离。下图显示了有关 Cloud Foundry 如何管理 {{site.data.keyword.cloud_notm}} 中应用程序部署的基本流程：

![部署应用程序](images/deploy.png)

图 1. 部署应用程序

创建应用程序并将其部署到 Cloud Foundry 时，{{site.data.keyword.cloud_notm}} 环境会确定将应用程序或应用程序所表示的工件发送到哪个相应的虚拟服务器。对于移动应用程序，将在 {{site.data.keyword.cloud_notm}} 上创建移动后端投影。在云中运行的移动应用程序的任何代码最终都会在 {{site.data.keyword.cloud_notm}} 环境中运行。对于 Web 应用程序，在云中运行的代码是开发者部署到 {{site.data.keyword.cloud_notm}} 的应用程序本身。确定虚拟服务器时会考虑若干因素，包括：

* 机器上的已有负载
* 该虚拟服务器支持的运行时或框架。

选择虚拟服务器后，每个虚拟服务器上的应用程序管理器都会为应用程序安装正确的框架和运行时。然后，可以将应用程序部署到该框架。部署完成后，将启动应用程序工件。

下图显示部署了多个应用程序的虚拟服务器（也称为 Droplet Execution Agent (DEA)）的结构：

![虚拟服务器的设计](images/container-diego.png)

图 2. 虚拟服务器的设计

在每个虚拟服务器中，应用程序管理器都会与 {{site.data.keyword.cloud_notm}} 基础架构的其余部分进行通信，并会对部署到此虚拟服务器的应用程序进行管理。每个虚拟服务器都具有容器，用于隔离和保护应用程序。在每个容器中，{{site.data.keyword.cloud_notm}} 会安装每个应用程序所需的相应框架和运行时。

部署应用程序后，如果该应用程序具有 Web 接口（例如 Java Web 应用程序）或其他基于 REST 的服务（例如向移动应用程序公开的移动服务），那么该应用程序的用户可以使用正常的 HTTP 请求与其进行通信。

![调用 {{site.data.keyword.cloud_notm}} 应用程序](images/execute.png)

图 3. 调用 {{site.data.keyword.cloud_notm}} 应用程序

每个应用程序都可以有一个或多个关联的 URL，但所有这些 URL 都必须指向 {{site.data.keyword.cloud_notm}} 端点。当请求到达时，{{site.data.keyword.cloud_notm}} 会检查该请求，确定该请求针对的是哪个应用程序，然后选择某个应用程序实例来接收该请求。


## {{site.data.keyword.cloud_notm}} 中的 Cloud Foundry 体系结构
{: #architecture}

一般而言，在 {{site.data.keyword.cloud_notm}} Cloud Foundry 中运行应用程序时，您不必担心操作系统和基础架构层。诸如根文件系统和中间件组件这样的层已进行抽象化，以便您可以重点关注自己的应用程序代码。但是，如果需要有关应用程序运行位置的具体信息，可以了解有关这些层的更多信息。

有关详细信息，请参阅[查看 {{site.data.keyword.cloud_notm}} 基础架构层](cf.html#infralayers)。

作为开发者，您可以使用基于浏览器的用户界面与 {{site.data.keyword.cloud_notm}} 基础架构进行交互。还可以使用名为 cf 的 Cloud Foundry 命令行界面来部署 Web 应用程序。

不管是客户机（移动应用程序、外部运行的应用程序、基于 {{site.data.keyword.cloud_notm}} 构建的应用程序等）还是使用浏览器的开发者，都可以与 {{site.data.keyword.cloud_notm}} 托管的应用程序进行交互。客户机使用 REST 或 HTTP API 通过 {{site.data.keyword.cloud_notm}} 将请求路由到某个应用程序实例或组合服务。

下图显示了 {{site.data.keyword.cloud_notm}} 上高层次的 Cloud Foundry 体系结构。

![{{site.data.keyword.cloud_notm}} 体系结构](images/arch.png)

图 4. {{site.data.keyword.cloud_notm}} 上的 Cloud Foundry 体系结构

出于等待时间或安全考虑，可以将应用程序部署到不同的 {{site.data.keyword.cloud_notm}} 区域。您可以选择部署到一个区域或跨多个区域部署。


![多区域应用程序部署](images/multi-region.png)

图 5. 多区域应用程序部署

{{site.data.keyword.Bluemix_notm}} 基础架构层
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} 抽象化并隐藏操作系统和基础架构层，这样您就无需对这些内容进行管理。但是，有时您可能希望了解有关应用程序的操作系统和中间件的更多信息。
{:shortdesc}

### 查看 {{site.data.keyword.Bluemix_notm}} 基础架构层
{: #viewinfra}

可以运行 **bluemix app stacks** 命令来显示要将应用程序部署到其中的可用堆栈或根文件系统。还可以指定堆栈，方法是在运行 **bluemix app push** 命令时使用 *-s* 选项和 *stack_name*，其中 stack_name 是根文件系统，例如 `lucid64` 或 `cflinuxfs2`：


```
bluemix app push appName -s stack_name
```

可以使用 `cf buildpacks` 命令来显示作为运行时提供的供应用程序在其中运行的中间件组件，例如 WebSphere Liberty 概要文件和 SDK for Node.js。此外，可以使用以下命令来指定应用程序的运行时环境：


```
bluemix app push appName -b buildpackname
```
