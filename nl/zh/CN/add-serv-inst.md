---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 创建和查看服务实例
{: #creating-services}

部署在 {{site.data.keyword.cfee_full_notm}} 中的应用程序可以绑定到两种类型的服务类型：
1. 由本地 Cloud Foundry 服务代理程序（相对于 CFEE 的本地代理程序）管理的服务实例。这些实例可以为以下两种类型中的任一类型：
   *  1a. 通过当前 {{site.data.keyword.cfee_full_notm}} 实例的 Cloud Foundry 市场创建的服务产品的实例。此类型的服务实例需要已注册服务代理程序在环境中可用。服务代理程序显示服务产品和套餐的目录，并从这些服务产品启用实例的创建、除去、绑定和取消绑定操作。有关更多信息，请参阅 Cloud Foundry 文档中的[管理服务代理程序](https://docs.cloudfoundry.org/services/managing-service-brokers.html)。
   * 1b. 用户提供的服务实例。此类型服务实例的创建通过 CLI（而不是通过用户界面）予以支持。但是，用户提供的服务实例将在用户界面中列出。
2. 通过 {{site.data.keyword.Bluemix}}“目录”创建并在 {{site.data.keyword.Bluemix}} 帐户中可用的公共服务实例。
{{site.data.keyword.Bluemix}} 帐户中可用的公共服务实例本身不能直接供 CFEE 环境使用。为了使公共服务实例（在 {{site.data.keyword.Bluemix}} 帐户中可用）变为可供 CFEE 环境中的空间使用，必须在目标 CFEE 空间中创建该服务实例的别名。别名充当实际公共服务实例的引用。在 CFEE 空间中创建了服务别名后，可以将其绑定到该 CFEE 中的应用程序。通过服务别名，开发者能够在 CFEE 环境中部署的应用程序中利用大量 {{site.data.keyword.Bluemix}} 服务。


## 在 CFEE 空间中创建和查看服务别名
{: #creating-services_inspace}

通过 IBM Cloud 帐户中可用的现有公共服务实例的别名，可以将该服务实例绑定到部署在 CFEE 空间中的应用程序。创建现有 {{site.data.keyword.Bluemix_notm}} 服务实例的别名需要用户具有对该实例本身的访问权。有关更多信息，请查看 {{site.data.keyword.Bluemix_notm}} 标题中**管理 > 用户**菜单下的“身份和访问权”页面，以检查当前帐户访问策略。

要在 CFEE 中的空间内创建服务实例别名，请执行以下操作：

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，找到托管应用程序的 Cloud Foundry Enterprise Environment。
2. 转至导航窗格中的**组织**，然后打开该应用程序所在的组织和空间。
3. 转至**空间**选项卡，并找到包含该应用程序的空间。
4. 在目标空间页面中，转至**服务**选项卡，然后单击**创建服务**。这将打开 {{site.data.keyword.cfee_full_notm}} 的**目录**页面。该页面会列出两个源中的服务产品（请查看_源_列）：
   * IBM Cloud“目录”中的产品。
   * 本地 {{site.data.keyword.cfee_full_notm}} 市场中的产品。
5. 查找并选择要实例化的可用服务产品。
6. 根据服务产品的来源（IBM Cloud 或本地 CFEE），继续执行下列其中一项操作：
   * **继续**到 IBM Cloud 服务产品创建页面，以提供新服务实例名称、区域、套餐以及在 IBM Cloud 中创建服务所需的其他属性。单击*创建*后，将在 IBM Cloud 中创建服务实例。此外，将在 {{site.data.keyword.cfee_full_notm}} 中创建该服务实例的别名。别名将可用于与 {{site.data.keyword.cfee_full_notm}} 中的应用程序绑定。**注：**以这种方式创建 {{site.data.keyword.Bluemix_notm}} 时，除了会在 IBM Cloud 帐户中创建可供用户使用的公共实例外，还会在创建了服务实例的 {{site.data.keyword.cfee_full_notm}} 中创建该服务实例的别名。
   * 在本地 Cloud Foundry 市场中**创建**服务实例。这将打开一个对话框，在其中可提供新服务实例的名称和套餐。单击*创建*后，将在 {{site.data.keyword.cfee_full_notm}} 中创建服务实例，并且该服务实例可用于与 {{site.data.keyword.cfee_full_notm}} 中的应用程序绑定。

创建服务实例后，服务实例（如果服务实例是在本地 Cloud Foundry 市场中创建的）或别名（如果服务实例是通过 IBM Cloud“目录”创建的）会列在**服务**选项卡下。


## 在全局 Cloud Foundry 仪表板中创建和查看所有 CFEE 环境中的服务别名
{: #creating-services_across}

您可以在全局 Cloud Foundry 仪表板中查看所有服务实例别名（在所有 CFEE 实例中）的统一视图。

1. 单击“菜单”图标 ![帐户检查](img/HamburgerMenu.png "显示“菜单”图标的屏幕截图") > **Cloud Foundry** 以打开 Cloud Foundry 仪表板。
2. 单击左侧导航窗格中的**企业 > 服务**。
视图中的表显示了以下信息：

|元素| 描述 |
|-----------|---------------|
|服务别名|服务实例别名的名称。|
|服务实例|据以创建别名的公共 IBM Cloud 服务实例。|
|产品|IBM Cloud“目录”中据以创建服务实例的服务产品。|
|CFEE|别名所在的 {{site.data.keyword.cfee_full}}。|
|组织|别名所在的 CFEE 实例中的组织。|
|空间|别名所在的 CFEE 实例中组织内的空间。|
{:caption="表 1. 关键元素描述" caption-side="top"}

可以在此视图中执行以下操作：
* 按显示为表列的任意属性对表中的项排序。
* 通过访问行最右边的别名的别名溢出菜单，将应用程序绑定到特定别名。
* 展开别名（行）以查看与该别名绑定的所有应用程序。
* 通过访问行最右边的别名的应用程序溢出菜单，启动和停止应用程序。
* 通过单击 CFEE、CFEE 组织或 CFEE 空间的链接，浏览至相应的 CFEE、组织或空间。

要在全局 Cloud Foundry 仪表板中创建服务别名，请执行以下操作：
1. 单击页面顶部的**创建服务别名**按钮。这将打开_创建服务别名_对话框。此对话框列出当前 IBM Cloud 帐户中可用的所有公共服务实例。
2. 选择其中一个公共服务实例。
3. 单击**创建**。创建后，新服务实例别名将添加到列表中。
服务别名还将显示在 CFEE 空间中的服务列表中，在其中可以将服务别名绑定到该空间中的应用程序（CFEE >“组织”>“空间”>“服务”）。


