---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 {{site.data.keyword.Bluemix_notm}} 中托管应用程序
{: #hosting_apps}

通过 {{site.data.keyword.Bluemix}}，您可以创建应用程序以及托管现有应用程序。只要您的应用程序是云就绪型应用程序，就可以将其移至 {{site.data.keyword.Bluemix_notm}}。{{site.data.keyword.Bluemix_notm}} 为您提供了多种方法来运行应用程序，例如 Cloud Foundry、IBM Containers 和虚拟机。

## 使应用程序成为云就绪型应用程序
{: #cloud-readyapps}

如果应用程序中遵循了以下所有原则，那么这就是云就绪型应用程序，可以迁移到 {{site.data.keyword.Bluemix_notm}}。如果应用程序中违反了某个原则，那么通常可以[修改应用程序](../apps/cloud-ready.html)以使其遵循原则。

## 迁移应用程序
{: #ht_hostapp}

您可以将应用程序以递增方式迁移到 {{site.data.keyword.Bluemix_notm}} 中，而不是将应用程序完全转移到云环境中。您可以先迁移应用程序的一部分，然后使用 Cloud Integration 服务来连接到现有数据或记录系统。

在云应用程序中，可能需要访问后端数据或服务，例如记录系统。在 {{site.data.keyword.Bluemix_notm}} 中，可以使用 Secure Gateway 服务在 {{site.data.keyword.Bluemix_notm}} 组织和企业后端网络之间建立一条安全的隧道。该服务支持 {{site.data.keyword.Bluemix_notm}} 上的应用程序访问后端网络的数据和服务。有关详细信息，请参阅 [Reaching enterprise backend with {{site.data.keyword.Bluemix_notm}} Secure Gateway via console ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}。

要将应用程序作为 Cloud Foundry 应用程序部署到 {{site.data.keyword.Bluemix_notm}}，请从 {{site.data.keyword.Bluemix_notm}}“目录”中选择运行时。运行时包含 Hello World 入门模板应用程序，您可以将其替换为自己的应用程序。如果找不到提供所需运行时的入门模板，那么可以通过在 cf push 命令中使用 -b 选项，将 Cloud Foundry 兼容的定制 buildpack 添加到 {{site.data.keyword.Bluemix_notm}} 中。有关详细信息，请参阅[使用社区 buildpack](byob.html)。

可以使用 {{site.data.keyword.Bluemix_notm}} 提供的以下工具和服务：

| 工具| 方法|
|:------|:--------|
| Cloud Foundry 命令行界面 (cf CLI)| 在本地客户机上管理代码，并使用 Cloud Foundry 命令行界面将应用程序手动推送到 {{site.data.keyword.Bluemix_notm}}。有关更多信息，请参阅[上传应用程序](../starters/upload_app.html)。|
| Eclipse| 在 Eclipse 中管理代码，并使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 来推送应用程序。|
| Git 集成| 在 GitHub 上管理代码，并将 Git 集成到 {{site.data.keyword.Bluemix_notm}} 中。您可以与其他开发者进行协作。落实代码中的更改时，应用程序将自动部署到 {{site.data.keyword.Bluemix_notm}}。无需手动推送应用程序。|
| {{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline| 在 DevOps GitHub 存储库上管理代码，并使用 DevOps Delivery Pipeline 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。|
{: caption="表 1. {{site.data.keyword.Bluemix_notm}} 工具" caption-side="top"}

如果 Cloud Foundry 平台不支持应用程序需求，那么可以使用可通过更多定制选项来设置、配置和维护运行时的容器或 VM。

## 使用 Continuous Delivery 中的工具链开发和部署应用程序
{:ht_cd}

[向应用程序添加工具链](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app)，然后使用 [Continuous Delivery 工具链 UI](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using) 来开发和部署应用程序。

## 使用 cf CLI 上传应用程序
{: #ht_cfcli}

可以在本地客户机上管理代码，并使用 Cloud Foundry 命令行界面将应用程序手动上传到 {{site.data.keyword.Bluemix_notm}}。如果更改了代码，必须将应用程序重新推送到 {{site.data.keyword.Bluemix_notm}} 才能运行更新后的代码。

执行以下步骤来迁移应用程序：

安装 Cloud Foundry 命令行界面。确保使用最新版本的 cf 命令行界面。
  1. 下载适用于您的操作系统的安装程序。
  2. 遵循工具向导来安装命令行。
  3. 使用以下命令验证 cf 命令行界面的版本：`cf -v`

可选：如果想要在将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 之前指定并保存部署详细信息，那么可以通过执行以下步骤来添加应用程序清单：

  1. 转至应用程序的工作目录，然后创建名为 manifest.yml（此为缺省名称）的文件。</li>
  2. 在清单文件中指定部署详细信息。以下示例显示了 Java™ 应用程序的清单文件。

  ```
  applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

有关可在此文件中使用的受支持选项的更多信息，请参阅[应用程序清单](depapps.html#appmanifest)。



### 推送应用程序

可以使用 `cf push` 命令上传应用程序。
  1. 通过运行以下命令来连接并登录到 {{site.data.keyword.Bluemix_notm}}。系统提示时，选择组织和空间。
  ```
cf login -a https://api.ng.bluemix.net
```
  如果您的组织使用的是单点登录，请添加 `-sso` 标志。



  2. 从应用程序目录中，输入带有应用程序名称的 cf push 命令。在 {{site.data.keyword.Bluemix_notm}} 环境中，应用程序名称必须是唯一的。


  ```
  cf push appname
  ```

  3. 可选：如果使用外部 buildpack，那么必须在 cf push 命令中使用 -b 选项。例如：

  ```
  cf push appname -b buildpack_URL
```

  有关详细信息，请参阅[使用社区 buildpack](byob.html)。



可选：如果更改了应用程序，那么必须重新输入 `cf push` 命令来上传这些更改。cf 命令行界面会使用您先前的选项并根据您对提示的响应，以新的代码段来更新应用程序的任何运行中实例。

#### 注：

* 使用 cf push 命令时，cf 命令行界面会将当前目录中的所有文件和目录复制到 {{site.data.keyword.Bluemix_notm}} 中。请确保应用程序目录中只包含必需的文件。
* 确保组织的内存足够供应用程序的所有实例使用。要查看组织的内存配额，请使用 cf org org_name。
* 有关 cf push 的更多信息，请参阅 [cf 命令](../cli/reference/cfcommands/index.html)。

## 迁移数据和使用服务
{: #ht_service}

将应用程序上传到 {{site.data.keyword.Bluemix_notm}} 后，从 {{site.data.keyword.Bluemix_notm}}“目录”中选择该应用程序连接到的服务，创建服务实例，将该实例绑定到该应用程序，然后重新启动该应用程序。

应用程序的 VCAP_SERVICES 环境变量是一种 JSON 对象，其中包含有关如何与 {{site.data.keyword.Bluemix_notm}} 中的服务实例进行交互的信息。这些信息包括服务实例名称、凭证和服务实例的连接 URL。

要在 {{site.data.keyword.Bluemix_notm}} 中运行代码，必须添加用于解析 VCAP_SERVICES 变量以获取有关服务连接的信息的代码逻辑。修改应用程序，以通过环境变量获取动态分配给服务实例的主机和端口。以下示例显示了如何获取 Ruby 应用程序中 Postgre SQL 服务实例的凭证：

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

要确保在为 {{site.data.keyword.Bluemix_notm}} 修改应用程序后，该应用程序可以在本地环境中运行，请检查是否存在为所有 {{site.data.keyword.Bluemix_notm}} Cloud Foundry 应用程序设置的 VCAP_SERVICES 环境变量。


# 相关链接
{: #rellinks}

## 相关链接
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [虚拟机](/docs/virtualmachines/vm_index.html)
* [Delivery Pipeline 入门](/docs/services/DeliveryPipeline/index.html)
* [使用 IBM Eclipse Tools for Bluemix 部署应用程序](/docs/manageapps/eclipsetools/eclipsetools.html)
* [The Twelve-Factor App ![外部链接图标](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
