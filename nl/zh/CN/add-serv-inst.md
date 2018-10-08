---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 使用服务
{: #workingwith-services}

部署在 {{site.data.keyword.cfee_full_notm}} 中的应用程序可以绑定到两种类型的服务类型：
1. 通过 {{site.data.keyword.Bluemix}}“目录”创建并在 {{site.data.keyword.Bluemix}} 帐户中可用的公共服务实例。
  
{{site.data.keyword.Bluemix}} 帐户中可用的公共服务实例本身不能直接供 CFEE 环境使用。为了使公共服务实例（在 {{site.data.keyword.Bluemix}} 帐户中可用）变为可供 CFEE 环境中的空间使用，必须将其明确添加到目标 CFEE 空间。将 {{site.data.keyword.Bluemix}} 服务实例添加到 CFEE 空间后，即可以将其绑定到该 CFEE 空间中的应用程序。这允许开发者在 CFEE 环境中部署的应用程序中利用大量 {{site.data.keyword.Bluemix}} 服务，同时允许对这些 {{site.data.keyword.Bluemix}} 服务进行访问控制。

   除了将现有的 {{site.data.keyword.Bluemix}} 服务实例添加到 CFEE 空间外，还可以在 CFEE 空间内创建新的 {{site.data.keyword.Bluemix}} 服务实例，这样也会自动将新实例添加到该 CFEE 空间。

2. 由本地 Cloud Foundry 服务代理程序（相对于 CFEE 的本地代理程序）管理的服务实例。这些实例可以为以下两种类型中的任一类型：
   *  2a. 通过当前 {{site.data.keyword.cfee_full_notm}} 实例的 Cloud Foundry 市场创建的服务产品的实例。此类型的服务实例需要已注册服务代理程序在环境中可用。服务代理程序显示服务产品和套餐的目录，并从这些服务产品启用实例的创建、除去、绑定和取消绑定操作。有关更多信息，请参阅 Cloud Foundry 文档中的[管理服务代理程序](https://docs.cloudfoundry.org/services/managing-service-brokers.html)。
   * 2b. 用户提供的服务实例。此类型服务实例的创建通过 CLI（而不是通过用户界面）予以支持。但是，用户提供的服务实例将在用户界面中列出。
   

## 查看所有 CFEE 环境中的 {{site.data.keyword.Bluemix_notm}} 服务实例
{: #viewing-services_across}

转至 [Cloud Foundry 服务仪表板](https://console.bluemix.net/dashboard/cloudfoundry/services)，以查看 {{site.data.keyword.Bluemix_notm}} 帐户中您有权访问的所有 {{site.data.keyword.Bluemix_notm}} 服务实例的统一视图，并查看哪些实例已添加到哪些 CFEE 空间。

此视图显示帐户中可用的所有 {{site.data.keyword.Bluemix_notm}} 服务实例，并指示哪些已添加（创建别名）到哪些 CFEE 空间。展开服务实例可显示添加了该实例的 CFEE 空间。您可以进一步展开这些空间，以查看这些 CFEE 空间中所添加服务实例已绑定到的应用程序。  

在此视图中，还可以将已部署到 CFEE 空间中的应用程序绑定到空间中已添加的这些服务实例。转至位于相应服务（可用于特定 CFEE 空间）的表行最右侧的菜单，然后选择**绑定到应用程序**。

## 向 CFEE 空间添加现有 {{site.data.keyword.Bluemix_notm}} 服务实例
{: #adding-services_inspace}

您可以将 {{site.data.keyword.Bluemix_notm}} 服务实例绑定到 CFEE 空间中部署的应用程序。要能够将 IBM Cloud 服务实例绑定到 CFEE 中部署的应用程序，必须先将该实例添加到部署了该应用程序的 CFEE 空间。要能够向 CFEE 空间添加 {{site.data.keyword.Bluemix_notm}} 服务实例，需要先满足以下条件：
* {{site.data.keyword.Bluemix_notm}} 服务必须在 CFEE 实例所在的 {{site.data.keyword.Bluemix_notm}} 帐户中可用。
* 您必须有权访问 {{site.data.keyword.Bluemix_notm}} 服务实例本身。有关更多信息，请查看 {{site.data.keyword.Bluemix_notm}} 标题中**管理 > 用户**菜单下的“身份和访问权”页面，以检查当前帐户访问策略。

要向 CFEE 空间添加现有 {{site.data.keyword.Bluemix_notm}} 服务实例，请执行以下操作：
1. 转至 [Cloud Foundry 服务仪表板](https://console.bluemix.net/dashboard/cloudfoundry/services)。  
2. 从列表中找到 {{site.data.keyword.Bluemix_notm}} 服务实例，并调用相应表行最右侧的菜单。
3. 选择**添加服务**。
4. 在_添加服务_对话框中，选择要添加服务的 CFEE、组织和空间，然后单击**添加**。
5. 展开目标 {{site.data.keyword.Bluemix_notm}} 服务以找到已添加服务的新 CFEE。


或者，可以在要添加 {{site.data.keyword.Bluemix_notm}} 服务实例的 CFEE 空间内添加该服务实例：
1. 在 {{site.data.keyword.Bluemix_notm}} [仪表板](https://console.bluemix.net/dashboard)或 [Cloud Foundry 服务仪表板](https://console.bluemix.net/dashboard/cloudfoundry/services)中，找到托管应用程序的 Cloud Foundry Enterprise Environment。
2. 转至导航窗格中的**组织**，然后打开该应用程序所在的组织和空间。
3. 转至**空间**选项卡，并找到包含该应用程序的空间。
4. 在目标空间页面中，转至**服务**选项卡，然后单击**添加服务**。这将打开__添加服务__对话框。该页面列出了 {{site.data.keyword.Bluemix_notm}} 帐户中可用的服务实例。
5. 查找并选择要添加到 CFEE 空间的可用服务实例。 
6. 服务实例将添加到 CFEE 空间中可用的服务列表中。

   **注：**向 CFEE 空间添加 {{site.data.keyword.Bluemix_notm}} 服务时，会在该空间中创建该服务实例的别名。从 CFEE 空间中**除去**服务实例时（通过位于表中相应服务实例行最右侧的菜单），不会从公共帐户中删除该服务。该操作只会从特定的 CFEE 帐户中除去该服务，并且该服务不再可用于绑定到该 CFEE 空间中的应用程序。此外，从 {{site.data.keyword.Bluemix_notm}} 帐户中删除服务实例本身时，该服务将不再可用于任何 CFEE 空间。 

## 在 CFEE 空间 UI 中创建 {{site.data.keyword.Bluemix_notm}} 服务实例
{: #creating-services_inspace}
您可以在 CFEE 空间内创建 {{site.data.keyword.Bluemix_notm}} 服务实例。创建 {{site.data.keyword.Bluemix_notm}} 服务实例会生成以下结果：
* 在 IBM Cloud 中创建 {{site.data.keyword.Bluemix_notm}} 服务实例。这等同于在 {{site.data.keyword.Bluemix_notm}} [目录](https://console.bluemix.net/catalog)中创建服务实例。
* 将 {{site.data.keyword.Bluemix_notm}} 服务实例添加（创建别名）到启动创建操作的 CFEE 空间中。


要在 CFEE 空间内创建服务实例，请执行以下操作：
1. 在目标空间页面中，转至**服务**选项卡，然后单击**创建服务**。这将打开 {{site.data.keyword.cfee_full_notm}} 的**市场**视图。该视图会列出两个源中的服务产品（请查看__源__列）：
   * {{site.data.keyword.Bluemix_notm}}“目录”中的产品。
   * 本地 {{site.data.keyword.cfee_full_notm}} 市场中的产品。
5. 查找并选择要实例化的可用服务产品。 
6. 根据服务产品的来源（IBM Cloud“目录”或本地 CFEE 市场），继续执行下列其中一项操作：
   * 如果所选服务产品是 {{site.data.keyword.Bluemix_notm}}“目录”产品，您将看到一个按钮用于**继续**到 IBM Cloud 服务产品创建页面。此页面与 {{site.data.keyword.Bluemix_notm}}“目录”中提供的页面相同。在此页面中，您可提供新服务实例名称、区域、套餐以及在 IBM Cloud 中创建服务所需的其他属性。在 IBM Cloud 中创建服务实例后，该实例将自动添加到当前 CFEE 空间。
   * 如果所选服务产品来自本地 CFEE 目录，您将看到一个按钮用于**创建**服务实例。系统将提示您提供将在其中创建服务实例的当前 CFEE 中的组织和空间。

## 使用 CLI 在 CFEE 空间中创建 {{site.data.keyword.Bluemix_notm}} 服务实例
{: #creating-services_cli}

您可以通过 CLI 在 CFEE 的空间中创建服务实例。通过 CLI 在 CFEE 空间中创建服务等同于通过 UI 在该空间中创建服务。也就是说，创建服务会产生以下双重结果：
* 在 IBM Cloud 中创建 {{site.data.keyword.Bluemix_notm}} 服务实例。这等同于在 {{site.data.keyword.Bluemix_notm}} [目录](https://console.bluemix.net/catalog)中创建服务实例。
* 将 {{site.data.keyword.Bluemix_notm}} 服务实例添加（创建别名）到启动创建操作的 CFEE 空间中。

在 CFEE 空间中创建服务实例与在 CLI 中创建服务实例的区别在于所创建服务实例的生命周期。在 CFEE 空间 UI 中创建服务实例时，所创建服务实例的生命周期通过 {{site.data.keyword.Bluemix_notm}} 帐户中的服务实例本身进行控制。这意味着服务套餐的更新是通过 {{site.data.keyword.Bluemix_notm}} 帐户中的实例控制的，而不是通过 CFEE 空间控制的。或者，如果服务实例是在 CLI 中创建的，那么服务的生命周期通过 CFEE 空间进行控制（服务通过 CFEE 空间更新）。

在 CLI 中创建的服务实例也会显示在 UI 中，并在服务实例名称旁边用 `*` 指示。

要使用 CLI 创建服务实例，请执行以下步骤：

1. 下载并安装 {{site.data.keyword.Bluemix}} 命令行界面（如果尚未安装）。[下载 Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。

2. 转至 {{site.data.keyword.cfee_full}}“概述”页面并找到环境的 API 端点。

3. 在命令行界面中，将 API 端点设置为您的 CFEE 环境的端点：

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. 登录到 CFEE 环境：

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  如果使用的是联合标识，请使用 `-sso` 选项：

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. 创建服务：
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  （可选）可以提供包含创建特定服务所需的有效 JSON 对象中参数的文件。
  参数文件的路径可以是文件的绝对路径或相对路径：
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  下面是有效 JSON 对象的示例：
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   有关在 CLI 中创建服务的帮助，请发出以下命令：
  
  ```
  cf cs -help
  ```
有关更多信息，请参阅 Cloud Foundry 文档中的[使用 cf CLI 管理服务实例](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。
  
## 将服务绑定到应用程序
{: #bind_services}

您可以在 [Cloud Foundry 服务仪表板](https://console.bluemix.net/dashboard/cloudfoundry/services)或 CFEE 空间页面的“服务”选项卡中，将服务实例绑定到 CFEE 中部署的应用程序。  

要在 [Cloud Foundry 服务仪表板](https://console.bluemix.net/dashboard/cloudfoundry/services)中将服务实例绑定到应用程序，请执行以下操作：
1. 转至 [Cloud Foundry 服务仪表板](https://console.bluemix.net/dashboard/cloudfoundry/services)，以查看 {{site.data.keyword.Bluemix_notm}} 帐户中可用的所有 {{site.data.keyword.Bluemix_notm}} 服务实例的统一视图。该视图还旨在显示哪些 {{site.data.keyword.Bluemix_notm}} 服务实例在哪些 CFEE 空间中可用（创建了别名）。可以展开服务实例以显示添加了该服务实例的 CFEE 空间。您可以进一步展开这些空间，以查看这些 CFEE 空间中所添加服务实例已绑定到的应用程序。 
2. 找到要绑定的 {{site.data.keyword.Bluemix_notm}} 服务实例。
3. 展开相应的视图以查看添加了该服务实例的所有 CFEE 空间。如果尚未将该服务实例添加到部署了应用程序的 CFEE 空间，请从行最右侧的菜单中选择**添加**，以使该服务实例在目标 CFEE 空间中可用。
4. 转至与其中服务实例可用的 CFEE/空间相对应的行最右侧的菜单，然后选择**绑定应用程序**。
5. 在__绑定应用程序__对话框中，选择要绑定的应用程序。
6. 现在，应用程序会绑定到部署了应用程序的 CFEE 空间中的服务实例。可以展开行以显示表中的相应行，从而查看 CFEE 空间中绑定的应用程序。


要在 CFEE 空间的__服务__页面中将应用程序绑定到服务实例，请执行以下操作：

1. 打开部署了应用程序的 CFEE 用户界面。
2. 转至左侧导航窗格中的**组织**，然后打开部署了该应用程序的组织和空间。
3. 转至**空间**选项卡，并找到包含该应用程序的空间。
4. 在目标空间页面中，转至**服务**选项卡。
5. 在**服务实例**表中，转至与要绑定的服务实例相对应的行最右侧的__操作__菜单，然后选择**绑定**。
6. 选择要绑定到服务实例的应用程序。

要取消应用程序与服务实例的绑定，请执行以下操作：

1. 在空间的**服务**选项卡中，展开目标服务实例以显示与其绑定的应用程序。
2. 转至应用程序行中的“操作”菜单，然后选择**取消绑定服务**。

有关使用 CLI 绑定应用程序的更多信息，请参阅 Cloud Foundry 文档中的[绑定服务实例](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。


