---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 許可權
{: #permissions}

開始建立及使用 {{site.data.keyword.cfee_full}} 服務實例之前，必須正確設定管理者及團隊其他人的許可權。

## 建立新環境所需的許可權
{: #perm-creating}

若要建立新的 {{site.data.keyword.cfee_full_notm}} 服務實例，要建立實例之帳戶的管理者必須將存取原則授與使用者：

* 存取 {{site.data.keyword.Bluemix}} 帳戶中的至少一個資源群組。資源群組容許將資源組織成自訂分組，以協助對這些資源的存取控制。當您建立新的環境實例時，系統會提示您輸入資源群組。

* 環境獲指派之資源群組中 {{site.data.keyword.cfee_full_notm}} 服務的管理者或編輯者角色。{{site.data.keyword.cfee_full_notm}} 服務中具有管理者或編輯者角色的使用者可以建立及刪除環境。但是只有具有管理角色的使用者才能將使用者指派給 {{site.data.keyword.cfee_full_notm}} 實例，或變更指派給該實例中使用者的角色。

* IBM Cloud Object Storage 服務的管理者或編輯者角色，這是 CFEE 服務的必要相依關係。IBM Cloud Object Storage 服務實例用來儲存在建立 ICFEE 應用程式容器期間所產生的資料（例如上傳的應用程式套件、建置套件及編譯的執行檔）。

* Compose for PostgreSQL 服務實例是 CFEE 服務的必要相依關係。Compose for PostgreSQL 用來將 Cloud Foundry 資料儲存至 CFEE 實例（例如，審核應用程式部署、啟動及停止事件；保留 CFEE 使用者成員資格、組織、空間、應用程式及服務連線的記錄）。該 Compose for PostgreSQL 服務實例部署至公用 Cloud Foundry 組織（與 CFEE 組織無關）。部署 Compose for PostgresSQL 實例的公用 Cloud Foundry 組織具有特定名稱：**_cfee-`<accountId>`_**，其中 "accountId" 是要佈建 CFEE（與 Compose for PostgreSQL 服務實例）的 IBM Cloud 帳戶 ID。帳戶擁有者建立 CFEE 實例時，會自動建立公用 Cloud Foundry 組織。不是帳戶擁有者的使用者嘗試建立 CFEE 實例（因此，CFEE 建立嘗試將會失敗）時，不會自動建立組織。因此，必須將建立 CFEE 實例但不是帳戶擁有者的任何 IBM Cloud 帳戶使用者新增至具有**管理者角色**的 **_cfee-`<accountId>`_** 公用 Cloud Foundry 組織。   

   若要將 IBM Cloud 帳戶中的使用者新增至 _cfee-`<accountId>`_ 公用組織，請執行下列動作：
    * 移至[**管理 > 帳戶 > Cloud Foundry 組織**](https://console.bluemix.net/account/organizations)。
    * 按一下 **_cfee-`<accountId>`_** 組織。
    * 移至頁面頂端的**使用者**標籤。
    * 尋找需要建立 CFEE 實例的使用者，然後按一下該使用者的**管理員**勾選框。如果您可以建立 CFEE 實例的使用者不在清單中，請按一下表格上方的**新增或邀請使用者**，以將使用者新增或邀請至 **_cfee-`<accountId>`_** 組織。

   **附註**：雖然會在 IBM Cloud 帳戶擁有者建立 CFEE 實例時隱含並自動建立 **_cfee-`<accountId>`_** 公用組織，但是帳戶擁有者（而且只有帳戶擁有者）可以改為手動建立公用 Cloud Foundry 組織，而不需要建立 CFEE 實例。IBM Cloud 帳戶擁有者可以在**管理 > 帳戶 > Cloud Foundry 組織**頁面中手動建立公用 _cfee-`<accountId>`_ 組織。如果您是帳戶擁有者，並建立公用 _cfee-`<accountId>`_ 組織，請確定將它命名為與 _cfee-`<accountId>`_ 完全相同。若要尋找 IBM Cloud 帳戶 ID，請移至[**管理 > 帳戶 > Cloud Foundry 組織**](https://console.bluemix.net/account/organizations)頁面，並查看瀏覽器中可用的頁面 URL。IBM Cloud 帳戶 ID 是頁面 URL 中後面有 `=` 的英數值集合。或者，您可以移至__管理 > 帳戶 > 使用者__，然後將游標移至工具提示上方，而工具提示位於頁面右上角的_帳戶_ 名稱左側。
   
* 環境獲指派之資源群組中 {{site.data.keyword.Bluemix_notm}} Container 服務的管理者或編輯者角色。{{site.data.keyword.cfee_full_notm}} 實例部署至 {{site.data.keyword.Bluemix_notm}} Container 服務所提供的容器叢集基礎架構。當您建立 {{site.data.keyword.cfee_full_notm}} 服務實例時，服務會自動建立已部署 {{site.data.keyword.cfee_full_notm}} 的 Kubernetes 叢集。需要有對 IBM Container 服務（特別是在環境獲指派的資源群組中）的存取權，才能建立該叢集基礎架構。

若要確認您具有建立 {{site.data.keyword.cfee_full_notm}} 實例所需的存取原則，請執行下列動作：
1. 移至 {{site.data.keyword.Bluemix_notm}} 標頭中的[**管理 > 帳戶 > 使用者**](https://console.bluemix.net/iam/#/users)功能表，以開啟**身分及存取**頁面。
2. 在「存取原則」標籤中，按一下將建立該環境的使用者。
3. 確認將建立環境之使用者的存取原則與先前所述的原則一致。

下列畫面說明 {{site.data.keyword.Bluemix_notm}} 之「身分及存取」頁面中出現的存取原則，以容許使用者建立 {{site.data.keyword.cfee_full_notm}} 實例。

![存取原則](img/AccessPolicies_Creator.png)

## 使用環境所需的許可權
{: #perm-working}

若要使用 {{site.data.keyword.cfee_full_notm}} 實例，使用者必須：
1. 已建立 {{site.data.keyword.cfee_full_notm}} 實例之 {{site.data.keyword.Bluemix_notm}} 帳戶的成員。
2. 帳戶管理者已授與下列_存取原則_（請參閱 {{site.data.keyword.Bluemix_notm}} 標頭的[**管理 > 帳戶 > 使用者**](https://console.bluemix.net/iam/#/users)功能表下的_身分及存取_ 頁面，以檢查現行帳戶存取原則）：
  - 存取 {{site.data.keyword.Bluemix_notm}} 帳戶中的至少一個資源群組。資源群組容許將資源組織成自訂分組，以協助對這些資源的存取控制。當您建立新的環境實例時，系統會提示您輸入資源群組。
  - 使用者必須獲指派對資源群組中 {{site.data.keyword.cfee_full_notm}} 服務的存取權，而在此資源群組下建立環境實例。使用者在 {{site.data.keyword.cfee_full_notm}} 實例中具有的存取及控制層次，取決於存取原則中所授與的角色：
     - 獲指派管理者或編輯者角色的使用者可以建立組織、將管理員指派給組織及空間、具有環境內所有組織及空間的完整許可權，以及使用 Cloud Controller API 來執行作業動作。這些使用者會自動獲指派 Cloud Foundry _使用者帳戶及鑑別範圍_ 中的 _cloud_controller.admin 範圍_。
     - 獲指派檢視者角色的使用者可以在主要 {{site.data.keyword.Bluemix_notm}} 儀表板中查看該環境，而且可以開啟其使用者介面。使用者對環境內特定組織及空間的存取，是由這些組織及空間管理員所指派的特定組織及空間角色所控管。如需相關資訊，請參閱[將使用者新增至組織](add-users.html)。

此圖說明存取 {{site.data.keyword.cfee_full_notm}} 所需的最小存取原則（出現在 {{site.data.keyword.Bluemix_notm}} _身分及存取_ 頁面中）。

![存取原則](img/AccessPolicies_User.png)

