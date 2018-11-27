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


# 管理網域
{: #domains}

有兩種類型的 Cloud Foundry 網域：
* {{site.data.keyword.cfee_full_notm}} 之任何空間中任何應用程式可用的共用網域。若要存取共用網域，請移至使用者介面之左導覽窗格中的**網域**頁面（在*作業* 下方）。
* 僅適用於特定組織內應用程式及空間的專用網域。若要存取組織內的網域，請移至使用者介面之左導覽窗格中的**組織**頁面，並開啟組織，然後移至**網域**標籤。

## 建立及刪除網域
{: #create-domains}

若要建立共用網域，請移至 {{site.data.keyword.cfee_full_notm}} 之左導覽窗格中的**網域**。  

若要建立專用網域，請移至使用者介面之左導覽窗格中的**組織**頁面，並開啟組織，然後移至**網域**標籤。

位在_網域_ 頁面（適用於共用網域）或特定組織的_網域_ 標籤（適用於專用網域）之後，按一下**建立網域**來建立網域，然後輸入唯一名稱。

**附註：**網域名稱在 {{site.data.keyword.cfee_full_notm}} 的整個範圍內必須是唯一的。亦即，專用網域無法取得給定 {{site.data.keyword.cfee_full_notm}} 內任何共用或專用網域的名稱。

您也可以發出下列指令，從 Cloud Foundry CLI 建立共用網域：
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
您可以發出下列指令，從 Cloud Foundry CLI 建立專用網域：
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**附註：**從 Cloud Foundry CLI 建立的網域將立即反映在使用者介面中，但最多可能需要 1 小時才能生效。

若要刪除網域，請移至對應於您要刪除之網域的表格列最右邊的功能表，然後選取**刪除網域**。
  
您也可以發出下列指令，從 Cloud Foundry CLI 刪除共用網域：
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## 上傳 SSL 憑證
 {: #upload-certificates}
 
您可以上傳網域的 SSL 憑證（共用或專用）。在對應於要新增憑證之網域的表格列中按一下**上傳**，並選取包含憑證的檔案以及包含私密金鑰的檔案。
  
