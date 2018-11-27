---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# 管理域
{: #domains}

有两种类型的 Cloud Foundry 域：
* 可供 {{site.data.keyword.cfee_full_notm}} 内任何空间中的任何应用程序使用的共享域。要访问共享域，请转至 UI 左侧导航窗格中的**域**页面（在*操作*下）。
* 专用域仅可供特定组织内的应用程序和空间使用。要访问组织内的域，请转至 UI 左侧导航窗格中的**组织**页面，打开组织，然后转至**域**选项卡。

## 创建和删除域
{: #create-domains}

要创建共享域，请转至 {{site.data.keyword.cfee_full_notm}} 左侧导航窗格中的**域**。  

要访问专用域，请转至 UI 左侧导航窗格中的**组织**页面，打开组织，然后转至**域**选项卡。

在_域_页面（对于共享域）或特定组织的_域_选项卡（对于专用域）中，单击**创建域**以创建域，并输入唯一名称。

**注：**域名在 {{site.data.keyword.cfee_full_notm}} 的整个作用域中必须唯一。即，专用域不能采用给定 {{site.data.keyword.cfee_full_notm}} 内的任何共享域或专用域的名称。

您还可以在 Cloud Foundry CLI 中通过发出以下命令来创建共享域：
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
可以在 Cloud Foundry CLI 中通过发出以下命令来创建专用域：
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**注：**通过 Cloud Foundry CLI 创建的域将立即反映在 UI 中，但可能最长需要 1 小时才能生效。

要删除域，请转至与要删除的域相对应的表行最右侧的菜单，然后选择**删除域**。
  
您还可以在 CLoud Foundry CLI 中通过发出以下命令来删除共享域：
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## 上传 SSL 证书
 {: #upload-certificates}
 
您可以为域（共享域或专用域）上传 SSL 证书。在对应于要添加证书的域的表行中单击**上传**，选择包含证书的文件以及包含专用密钥的文件。
  
