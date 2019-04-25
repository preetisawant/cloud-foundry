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

# 创建组织和空间
{: #create_orgs}

{{site.data.keyword.cfee_full}} 中的应用程序的作用域限定在特定空间内，而空间存在于特定组织内。组织的成员共享配额套餐、应用程序、服务实例和定制域。创建组织和空间后，可以将用户添加到这些组织和空间并授予特定角色，这些角色将确定对这些组织和空间的访问和控制级别。要创建组织并为这些组织分配管理者，您需要对 {{site.data.keyword.cfee_full_notm}} 服务的“管理者”角色以及对要添加用户的特定环境实例的“管理员”角色。这些许可权可在 {{site.data.keyword.Bluemix}} 标题中**管理 > 用户**菜单下的_身份和访问权_页面中进行设置。
{: shortdesc}

## 创建组织
{: #create-org}

要在 {{site.data.keyword.cfee_full_notm}} 中创建组织，请执行以下操作：

1. 转至 [{{site.data.keyword.Bluemix_notm}} Cloud Foundry 环境仪表板](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments){: new_window}，然后打开要在其中创建组织的 {{site.data.keyword.cfee_full_notm}}。
2. 在 {{site.data.keyword.cfee_full_notm}} 用户界面中，转至导航窗格中的**组织**条目，以打开_组织_页面。
3. 单击**添加新项**。
4. 输入新组织的**名称**。
5. 在**管理者**下，至少标识一个用户。只有具有“管理者”角色的用户才能向该组织添加成员。
6. 在**配额套餐**下，选择一个可用的套餐。配额套餐限制了组织中应用程序的可用内存量、托管的最大应用程序实例数以及最大路径数。

除了管理组织成员资格外，组织管理者还可以创建、查看、编辑或删除组织内的空间。另外，组织管理者可以查看组织的使用情况和配额，邀请用户加入组织，管理组织中的成员资格和角色，以及管理组织的定制域。

要在组织内创建空间，请在_组织_页面中，转至**空间**选项卡，然后单击**添加新项**。组织的成员还可以在组织内创建和管理自己的空间。有关 Cloud Foundry 角色的更多信息，请参阅 [Cloud Foundry 访问权](https://cloud.ibm.com/docs/iam/cfaccess.html#cfroles){: new_window}。

**注**：对 {{site.data.keyword.cfee_full_notm}} 内组织和空间的访问权要求用户有权访问环境本身。如果用户无权访问 {{site.data.keyword.cfee_full_notm}}，那么将无法访问环境内的组织和空间，不管该用户在这些组织和空间中具备什么成员资格和角色。
