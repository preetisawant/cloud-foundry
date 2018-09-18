---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 部署和查看应用程序
{: #deploy_apps}

您可以使用命令行界面或集成开发环境 (IDE) 将应用程序部署到 {{site.data.keyword.Bluemix}}。您还可以使用应用程序清单来部署应用程序。通过使用应用程序清单，可减少每次将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时必须指定的部署详细信息的数量。
{:shortdesc}

## 使用 Cloud Foundry 命令部署应用程序
{: #dep_apps}

下载并安装 {{site.data.keyword.Bluemix}} 命令行界面。[下载 {{site.data.keyword.Bluemix_notm}} CLI ](https://clis.ng.bluemix.net){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。

安装命令行界面后，请执行以下步骤：

1. 切换到代码所在的目录。`cd <your_directory>`
2. 转至 {{site.data.keyword.cfee_full}}“概述”页面并找到环境的 API 端点。
3. 在命令行界面中，将 API 端点设置为您的环境的端点：

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. 登录到环境：

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  如果使用的是联合标识，请使用 `-sso` 选项。

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **注**：如果 `username`、`org_name` 和 `space_name` 的值包含空格，那么必须用单引号或双引号将其括起，例如 `-o "my org"`。

5.  在 `<your_new_directory>` 中，使用 `bluemix app push` 命令将应用程序重新部署到 {{site.data.keyword.Bluemix_notm}}。有关 `cf app push` 命令的更多信息，请参阅[上传应用程序](/docs/starters/upload_app.html)。

  ```
  cf push <app_name>
  ```
  {: pre}

6.  通过浏览至 `https://<app_url>.<AppDomainName>` 来访问应用程序。

## 在用户界面中查看部署的应用程序
{: #view_apps}

您可以查看特定空间上下文中 CFEE 部署的应用程序，或以全局方式查看所有 CFEE 实例中部署的应用程序。

### 查看特定 CFEE 空间中部署的应用程序
{: #view_specific}

要查看特定 CFEE 实例的特定空间中部署的应用程序，请执行以下操作：
1. 转至 [{{site.data.keyword.Bluemix_notm}} 仪表板](https://console.bluemix.net/dashboard/apps/)，然后打开要在其中创建组织的 {{site.data.keyword.cfee_full_notm}}。
2. 在 {{site.data.keyword.cfee_full_notm}} 用户界面中，转至导航窗格中的**组织**条目，以打开_组织_页面。
3. 转至页面顶部的**空间**选项卡。
4. 在__空间__选项卡中，单击表中的某个空间以打开该空间的页面。
5. 在__空间__页面中，转至**应用程序**选项卡。
6. _应用程序_选项卡会显示该空间中部署的所有应用程序。
（可选）可以通过访问表示应用程序的行最右边的菜单来启动、重新启动、停止或删除应用程序。

您还可以展开应用程序所在行以查看应用程序绑定到的服务实例。

### 查看所有 CFEE 实例中部署的应用程序
{: #view_global}

要查看所有 CFEE 实例上部署的所有应用程序，请执行以下操作：
1. 单击“菜单”图标 ![帐户检查](img/HamburgerMenu.png "显示“菜单”图标的屏幕截图") > **Cloud Foundry** 以打开 Cloud Foundry 仪表板。
2. 单击左侧导航窗格中的**企业 > 应用程序**。
视图中的表显示了以下信息：

|元素| 描述 |
|-----------|---------------|
|名称|应用程序的名称。|
|实例数|应用程序的实例数。|
|环境|部署了应用程序的 {{site.data.keyword.cfee_full}} 环境。|
|组织|部署了应用程序的组织。|
|空间|别名所在的 CFEE 实例中的组织。|
|内存|应用程序使用的内存量。|
|状态|应用程序的状态。|
{:caption="表 1. 关键元素描述" caption-side="top"}

（可选）可以通过访问表示应用程序的行最右边的菜单来启动、重新启动、停止或删除应用程序。可以在 CFEE 用户界面中单击任何应用程序、环境、组织或空间，以浏览至相应的页面。

在此视图中，可以选择按组织、空间和/或应用程序名称对应用程序进行分组。通过此功能，可以将可能具有不同名称和/或部署在不同 CFEE 组织或空间中，但对应于同一个逻辑应用程序实体的应用程序合并到单个实体中。例如，您可能有不同的应用程序，有的表示更广泛项目的组件，或者有的部署在不同交付阶段（例如，开发、测试或生产）中，但您希望将这些应用程序分组在一起，作为同一逻辑实体的一部分进行查看。

要对应用程序进行分组，请转至位于页面右上角的**组**下拉列表。
对应用程序进行分组时，生成的每个组由表中的单个条目表示。可以展开该行以显示该组下的应用程序。

可以在此视图中执行以下操作：
* 按显示为表列的任意属性对表中的项排序。
* 通过访问行最右边的别名的别名溢出菜单，将应用程序绑定到特定别名。
* 展开别名（行）以查看与该别名绑定的所有应用程序。
* 通过访问行最右边的别名的应用程序溢出菜单，启动和停止应用程序。
* 通过单击 CFEE、CFEE 组织或 CFEE 空间的链接，浏览至相应的 CFEE、组织或空间。

## 应用程序清单
{: #appmanifest}

应用程序清单包含应用于 `cf push` 命令的选项。可以使用应用程序清单来减少每次将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时必须指定的部署详细信息的数量。

在应用程序清单中，可以指定多个选项，例如要创建的应用程序实例数、要分配的内存量和磁盘配额，以及其他环境变量。您还可以使用应用程序清单来自动执行应用程序部署。清单文件的缺省名称为 `manifest.yml`。

### 清单文件中的受支持选项

下表显示了可在应用程序清单文件中使用的受支持选项。如果选择使用除 `manifest.yml` 以外的其他文件名，那么必须将 **-f** 选项用于 `cf push` 命令。在以下示例中，`appManifest.yml` 是文件名：

```
cf push -f appManifest.yml
```

|选项| 描述 |用法或示例|
|:----------|:--------------|:---------------|
|**buildpack**|定制 buildpack 的 URL 或名称。|`buildpack:` *buildpack_URL*|
|**disk_quota**|为应用程序分配的磁盘配额。缺省值为 1G。|`disk_quota: 500M`|
|**domain**|{{site.data.keyword.Bluemix_notm}} 中应用程序的域名。|`domain:` ng.bluemix.net|
|**host**|{{site.data.keyword.Bluemix_notm}} 中应用程序的主机名。此值在 {{site.data.keyword.Bluemix_notm}} 环境中必须唯一。|`host:` *host_name*|
|**name**|{{site.data.keyword.Bluemix_notm}} 中的应用程序名称。此值在 {{site.data.keyword.Bluemix_notm}} 环境中必须唯一。|`name:` *appname*|
|**path**|应用程序的位置。此值可以是相对路径，也可以是绝对路径。|`path:` *path_to_application*|
|**command**|应用程序的定制启动命令，或用于运行脚本文件的命令。|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**|为应用程序分配的内存量。缺省值为 1G。|`memory: 512M`|
|**instances**|要为应用程序创建的实例数。|`instances: 2`|
|**timeout**|用于启动应用程序的最大时间量（以秒为单位）。缺省值为 60 秒。|`timeout: 80`|
|**no-route**|布尔值，用于阻止将路径分配给仅在后台运行的应用程序。缺省值为 **false**。|`no-route: true`|
|**random-route**|布尔值，用于将随机路径分配给应用程序。缺省值为 **false**。|`random-route: true`|
|**services**|要绑定到应用程序的服务。|`services: - mysql_maptest`|
|**env**|应用程序的定制环境变量。|`env: DEV_ENV: production`|
{: caption="表 2. 清单 YAML 文件中的受支持选项" caption-side="top"}

### 样本 manifest.yml 文件
{: #sample}

以下示例显示了在 {{site.data.keyword.Bluemix_notm}} 中使用内置社区 Node.js buildpack 的 Node.js 应用程序的清单文件。

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
