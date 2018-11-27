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

# 准备帐户
{: #prepare}

CFEE 实例会部署在基础架构资源（IBM Container Service 中的 Kubernetes 工作程序节点）上，这些资源的相关费用会记入 IBM Cloud 帐户。这意味着在其中创建 CFEE 实例的 IBM Cloud 帐户必须是付费帐户（现买现付或预订帐户）。如果打算在其中创建 CFEE 实例的 IBM Cloud 帐户是试用帐户，那么尝试创建 CFEE 实例时，系统会要求您升级该帐户。升级 IBM Cloud 帐户后（从试用帐户升级到现买现付或预订帐户），IBM Cloud 帐户会链接到 SoftLayer 帐户（可通过该帐户来创建基础架构资源）。有关更多信息，请参阅[帐户类型](https://console.bluemix.net/docs/account/index.html#accounts)。这些基础架构资源的成本会显示在 IBM Cloud 发票中。

## 如何确定 IBM Cloud 帐户是否可以创建 CFEE 实例
{: #account-check}

您可以通过查看 IBM Cloud 条幅右上角的帐户信息来确定 IBM Cloud 帐户是试用帐户还是付费帐户，以及是否链接到 SoftLayer 帐户。

在以下示例中，用户 _Mary Smith_ 已登录到 IBM Cloud 帐户 _MyCompany_，这是一个试用帐户。![帐户检查](img/AccountExample_1.png)

在以下示例中，同一 IBM Cloud 帐户 _MyCompany_ 已升级到付费帐户。由于升级，该帐户现在已链接到 SoftLayer 帐户 _1684806_。这两个帐户都会显示在“帐户”字段中。![帐户检查](img/AccountExample_2.png)

如果 IBM Cloud 帐户是试用帐户，那么在您尝试创建 CFEE 实例时，系统将提示您升级该帐户。请参阅下面显示的屏幕：

![帐户检查](img/UpgradeAccountPage_1.png)

## 使用 SoftLayer 帐户而不升级 IBM Cloud 帐户
{: #account-linkswitching}

如果您在 IBM Cloud 帐户中具有“管理员”角色，那么可以使用 SoftLayer 帐户来创建 CFEE 实例，而不升级 IBM Cloud 帐户。


**警告：**如果您现在使用 SoftLayer 帐户，而将来更新 IBM Cloud 帐户（更新为现买现付帐户或预订帐户），那么更新后的 IBM Cloud 帐户在将来创建基础架构资源时仍可能会使用 Softlayer 帐户（其凭证是您现在设置的凭证）。此外，如果未来使用其他 SoftLayer 帐户创建 Cloud Foundry Enterprise Environment，那么 IBM Cloud 帐户中的用户可能无法访问该 SoftLayer 帐户（其凭证是您现在设置的）下创建的基础架构资源。建议您改为升级 IBM Cloud 帐户。

要使用 SoftLayer 帐户而不升级 IBM Cloud 帐户（请参阅以下屏幕以获取相关说明）：
1. 在未升级 IBM Cloud 帐户时显示的屏幕中，单击**使用 SoftLayer 帐户**。
2. 输入 SoftLayer 帐户中的**用户名**和 **API 密钥**。要获取 SoftLayer 的用户名和 API 密钥，请访问 [SoftLayer 控制台](https://control.softlayer.com)。登录到 SoftLayer 后，请选择要链接到 {{site.data.keyword.Bluemix_notm}} 帐户的帐户。选择帐户将打开该帐户的概要文件页面。向下滚动到页面末尾以找到该帐户的用户名和 API 密钥。您没有 API 密钥时，如果您是帐户所有者，那么可以生成该密钥。如果您不是帐户所有者，请要求帐户所有者来生成该密钥。
3. 单击**设置凭证**。

![帐户检查](img/UpgradeAccountPage_2.png)

**注：**您必须在 SoftLayer 帐户中拥有足够的许可权，才能通过 IBM Container Service 创建常规 Kubernetes 集群。如果您没有足够的许可权，请要求 SoftLayer 帐户管理员或授予您 SoftLayer 帐户访问权的用户来向您授予这些额外的许可权。
