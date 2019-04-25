---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2019-02-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 許可權
{: #permissions}

使用者開始建立及使用 {{site.data.keyword.cfee_full}} (CFEE) 服務之前，要在其中建立 CFEE 實例之帳戶的管理者必須先正確設定他們的許可權。 

## 許可權概觀
{: #perm-summary}

以下是在 CFEE 實例中執行各項作業所需之最低 [IAM](https://cloud.ibm.com/iam#/users) 及 [Cloud Foundry 角色指派](https://cloud.ibm.com/account/cloud-foundry)的摘要。剩下的小節會更詳細地說明這些許可權。

|  **作業** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|  **IAM 存取角色** &nbsp; &nbsp; &nbsp; |**Cloud Foundry 角色** &nbsp; &nbsp; &nbsp; |
|----------------------------------------|-------------------|-------------------|
|建立 CFEE |  <ul><li>要建立 CFEE 之資源群組中的檢視者角色。</li> <li>CFEE 服務中的編輯者角色。</li> <li>Kubernetes 服務中的管理者角色。</li> <li>編輯者平台角色，以及 IBM Cloud Object Storage 服務中的管理者服務存取角色。</li> </ul> | <ul><li>公用組織中的使用者角色。</li> <li>該公用組織中之空間的開發人員角色。</li></ul>|
|更新 CFEE 版本|  <ul><li>CFEE 資源群組中的檢視者角色。</li> <li>CFEE 服務中的編輯者平台角色。</li></li> <li>Kubernetes 服務中的操作員角色。</li> <li>Cloud Object Storage 服務中的編輯者角色。</li> </ul> | <ul><li>公用組織中的使用者角色。</li> <li>該公用組織中之空間的開發人員角色。</li></ul>|
|調整 CFEE 容量（新增/移除 Cell）|  <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的管理者角色。</li> <li>Kubernetes 服務中的操作員角色。</li> <li>Cloud Object Storage 服務中的編輯者角色。</li> </ul> | |
|監視 CFEE |  <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的編輯者角色。</li> <li>CFEE 的 Kubernetes 叢集中的操作員角色。</li></ul> |  |
|檢視 CFEE 資源用量|  <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的檢視者角色。</li></ul> |  |
|啟用 CFEE 審核| <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的編輯者角色。</li></ul> | <ul><li>部署 Activity Tracker 服務實例之公用 Cloud Foundry 空間中的審核員角色。</li></ul>  |
|檢視 CFEE 審核事件| <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的編輯者角色。</li></ul> | <ul><li>部署 Activity Tracker 服務實例之公用 Cloud Foundry 空間中的審核員角色。</li></ul>  |
|啟用 CFEE 日誌持續性| <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的編輯者角色。</li></ul> |<ul><li>部署 Log Analysis 服務實例之公用 Cloud Foundry 空間中的審核員角色。</li></ul>  |
|檢視 CFEE 持續保存日誌| <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的編輯者角色。</li></ul> | <ul><li>部署 Log Analysis 服務實例之公用 Cloud Foundry 空間中的審核員角色。</li></ul> |
|建立 CFEE 組織 | <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的編輯者角色。</li></ul> |  |
|建立 CFEE 空間 | <ul><li>CFEE 實例資源群組中的檢視者角色。</li> <li>CFEE 實例中的檢視者角色。</li></ul> | <ul><li>要建立空間之組織中的管理員。</li></ul> |
|管理共用網域|<ul><li>CFEE 實例資源群組中的檢視者。</li><li>CFEE 實例中的編輯者角色。</li></ul>|  |
|檢視共用網域|<ul><li>CFEE 實例資源群組中的檢視者。</li><li>CFEE 實例中的檢視者角色。</li></ul>|  |
|管理專用網域|<ul> <li>CFEE 實例資源群組中的檢視者。</li><li>CFEE 實例中的檢視者角色。</li></ul>| <ul><li>擁有網域之組織中的管理員角色。</li></ul>|
|檢視專用網域|<ul> <li>CFEE 實例資源群組中的檢視者。</li><li>CFEE 實例中的檢視者角色。</li></ul>|<ul><li>擁有網域之組織中的檢視者角色。</li></ul>|
|在 CFEE 空間中建立/刪除 IBM Cloud 服務實例| <ul><li>要建立 CFEE 之資源群組中的檢視者角色。</li> <li>CFEE 實例中的檢視者角色。</li> <li>要建立服務實例之資源群組中的編輯者，或是要實例化 IAM 管理服務之資源群組中的編輯者。</li> </ul>| <ul><li>建立服務實例（以及將自動新增/建立別名）之 CFEE 空間中的開發人員角色。</li></ul> |
|在 CFEE 空間中新增/移除 IBM Cloud 服務實例（亦即對 CFEE 空間中的 IBM Cloud 服務建立/刪除別名）| <ul><li>CFEE 實例資源群組中的檢視者角色。</li><li>CFEE 實例中的檢視者角色。</li><li>操作員平台角色及對要新增之服務實例的讀者服務角色。</li></ul>|<ul><li>要新增（建立別名）服務實例之 CFEE 空間中的開發人員角色。</li></ul> |
|在 CFEE 空間中連結或取消連結 IBM Cloud 服務實例|<ul> <li>要連結或取消連結之服務實例的資源群組中的編輯者。</li><li>CFEE 實例中的檢視者角色。</li><li>操作員平台角色及對要連結之服務實例的撰寫者服務角色。</li></ul> | <ul><li>要連結服務實例之 CFEE 空間中的開發人員角色。</li></ul> |
|發出 `cf` CLI 指令|<ul> <li>CFEE 實例資源群組中的檢視者角色。</li><li>CFEE 實例中的檢視者角色。</li></ul> | <ul><li>在執行指令所需組織/空間中的 Cloud Foundry 角色。</li></ul> |
{: caption="表 1. 在 CFEE 中執行作業所需的許可權" caption-side="top"}

## 建立新環境所需的許可權
{: #perm-creating}

若要建立新的 CFEE 服務實例，帳戶管理者必須授與存取原則給使用者，不只是對 CFEE 服務本身，還有對建立 CFEE 時自動建立的支援服務。

需要下列 Identity & Access Management (IAM) 存取原則，使用者才能建立 {{site.data.keyword.cfee_full_notm}} 實例：

* {{site.data.keyword.Bluemix}} 帳戶中，對 **_Default_** **資源群組**的 _Viewer_（或更高）存取權。資源群組容許將資源組織成自訂分組，以協助對這些資源的存取控制。當您建立新的環境實例時，系統會提示您輸入資源群組。需要有對 _Default_ 資源群組的存取權，因為這一定是需要 Kubernetes 叢集的資源群組。使用者可以在不同的資源群組中佈建 CFEE 實例，但 Kuberetes 叢集仍將會佈建到 _Default_ 資源群組。如果使用者在不同的使用者群組中佈建 CFEE，該使用者將需要該資源群組的檢視者存取權。

* 在獲指派環境的資源群組中，對 **{{site.data.keyword.cfee_full_notm}} 服務**資源的_管理者_ 或_編輯者_ 角色。在 {{site.data.keyword.cfee_full_notm}} 服務中具有管理者或編輯者角色的使用者，可以建立及刪除環境。但是只有具有管理角色的使用者，才能將使用者指派給 {{site.data.keyword.cfee_full_notm}} 實例，或變更指派給該實例中使用者的角色。
   
* **Kubernetes 服務**資源的_管理者_ 角色。{{site.data.keyword.cfee_full_notm}} 實例部署在 Kubernetes 服務所提供的容器叢集基礎架構上。當您建立 {{site.data.keyword.cfee_full_notm}} 服務實例時，服務會自動建立 Kubernetes 叢集。需要對 Kubernetes 服務的存取權，才能建立該叢集基礎架構。您可以將 Kubernetes 服務原則的存取權範圍界定在打算佈建 CFEE 實例的特定地區，或是將存取權範圍界定在所有地區。

* _管理者_ 或_編輯者_ 平台角色，以及 **IBM Cloud Object Storage 服務**的管理服務存取角色，而此服務是 CFEE 服務的必要相依關係。IBM Cloud Object Storage 服務實例用來儲存在建立 ICFEE 應用程式容器期間所產生的資料（例如：上傳的應用程式套件、建置套件及已編譯的執行檔）。

* Compose for PostgreSQL 服務實例是 CFEE 服務的必要相依關係。Compose for PostgreSQL 用來將 Cloud Foundry 資料儲存至 CFEE 實例（例如：審核應用程式部署、啟動及停止事件；保留 CFEE 使用者成員資格、組織、空間、應用程式及服務連線的記錄）。該 **Compose for PostgreSQL 服務**實例部署在您建立 {{site.data.keyword.cfee_full_notm}} 實例時所選取的公用 Cloud Foundry 組織（與 CFEE 組織無關）中。這表示，當您建立 {{site.data.keyword.cfee_full_notm}} 實例時，在打算佈建 CFEE 實例的位置中，需要至少具有一個組織的_管理員_ 存取權。您也需要具有該組織中至少一個空間的_開發人員_ 存取權。 

  如果您不是打算建立 CFEE 實例之位置中，至少一個公用組織的成員，請要求 IBM Cloud 管理者邀請您加入一個公用組織。如果您在帳戶中有管理者角色，可以執行下列動作將使用者新增至帳戶裡的公用組織及空間：

     * 移至[**管理 > 帳戶 > Cloud Foundry 組織**](https://console.bluemix.net/account/organizations)，然後按一下**新增組織**或選取現有的組織。
     * 移至組織頁面頂端的**使用者**標籤。
     * 尋找需要建立 CFEE 實例的使用者。如果您想要他/她能夠建立 CFEE 實例的使用者不在清單中，請按一下表格上方的**新增或邀請使用者**，以將使用者新增或邀請至組織。
     * 移至組織頁面頂端的**空間**標籤。
     * 找到要佈建 Compose for PostgreSQL 服務實例的空間，然後勾選 **Developer** 角色勾選框。

下列畫面說明 {{site.data.keyword.Bluemix_notm}} 之「身分及存取」頁面中出現的存取原則，以容許使用者建立 {{site.data.keyword.cfee_full_notm}} 實例。

![存取原則](img/AccessPolicies_Creator.png)

您可以使用 {{site.data.keyword.Bluemix}} 指令行來授與使用者許可權。您也可以在建立原則之指令所呼叫的 JSON 格式檔案中指定原則的參數（即服務、角色、地區等），以定義使用者的存取原則。如需相關資訊，請參閱[使用指令行指派 IAM 原則](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline)，或在指令行中發出 `ibmcloud iam -help`。請注意，這需要安裝 [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use)。
{:tip}

若要確認您具有建立 {{site.data.keyword.cfee_full_notm}} 實例所需的存取原則，請執行下列動作：
1. 移至 {{site.data.keyword.Bluemix_notm}} 標頭中的[**管理 > 存取 (IAM) > 使用者**](https://console.bluemix.net/iam/#/users)功能表，以開啟**身分及存取**頁面。
2. 在「存取原則」標籤中，按一下將建立環境的使用者，以便指派和檢視該使用者的存取原則。

如需在 {{site.data.keyword.Bluemix}} 中管理使用者及存取權的相關資訊（包括如何組織一組使用者及服務 ID 以協助一次將存取權指派給多位使用者），請參閱[管理使用者及存取權](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage)。

### 使用 CLI 加快設定建立環境的許可權
{: #permcli-creating}

您可以透過 `ibmcloud cfee create-permission-set` 加快設定用於建立 CFEE 實例的許可權。此指令容許 CFEE 管理者以單一指令設定必要的存取原則，以建立 CFEE 實例及其所有輔助服務。 

此指令會設定對 IAM _存取群組_ 的許可權，並將使用者新增至該_存取群組_。發出指令的管理者可以將現有_存取群組_ 併入指令中。如果未提供任何_存取群組_，則會自動建立預設 _cfee-provision-access-group_。

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

此指令會為目標使用者設定下列存取原則：

*  現行 IBM Cloud 帳戶中 Cloud Object Storage 及 CFEE 服務的「編輯者」角色。
*  現行 IBM Cloud 帳戶中「Kubernetes 服務」的「管理者」角色。
*  佈建 Compose for PostgreSQL 之現行組織中現行空間的「開發人員」角色。

如需指令的詳細資料，請發出下列指令：

```
cfee create-permission-set -help
```
{: pre}

您可以使用 `ibmcloud cfee create-permission-get` 來找出或驗證使用者適用的存取原則：

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## 使用環境所需的許可權
{: #perm-working}

若要使用 {{site.data.keyword.cfee_full_notm}} 實例，使用者必須：
1. {{site.data.keyword.cfee_full_notm}} 實例建立所在之 {{site.data.keyword.Bluemix_notm}} 帳戶的成員。
2. 帳戶管理者已授與下列 IAM _存取原則_（請參閱 {{site.data.keyword.Bluemix_notm}} 標頭的[**管理 > 存取 (IAM) > 使用者**](https://console.bluemix.net/iam/#/users)功能表下的_身分及存取_ 頁面，以檢查現行帳戶存取原則）：

    在 CFEE 實例中工作的任何使用者，都需要對下列項目的_檢視者_ 平台角色（或更高角色）：
  - CFEE 實例建立所在的資源群組。
  - CFEE 實例本身。 
  
   使用者在 CFEE 實例中具有的存取及控制層次，取決於存取原則中所授與的角色：

  - 具有 CFEE 實例_檢視者_ 角色的使用者，可看到它列在主要 {{site.data.keyword.Bluemix_notm}} 儀表板中，並開啟其使用者介面。對環境內特定組織及空間的使用者存取，是由這些組織及空間管理員所指派的特定組織及空間角色所控管。如需相關資訊，請參閱[將使用者新增至組織](add-users.html)。
  
  - 獲指派對 CFEE 實例之_管理者_ 或_編輯者_ 角色的使用者，可以建立組織、將管理員指派給組織及空間、具有對環境內所有組織及空間的完整許可權，以及透過 Cloud Controller API 來執行作業動作。這些使用者會自動被授與 Cloud Foundry _使用者帳戶及鑑別範圍_ 中的 _cloud_controller.admin 範圍_。

  - 使用者需要 CFEE 實例的_編輯者_ 平台角色或更高角色，以及 CFEE 佈建所在 Kubernetes 叢集的_操作員_ 角色或更高角色，才能**將 CFEE 更新至新版本**。

  - 使用者需要 CFEE 實例的_管理者_ 平台角色，以及 CFEE 佈建所在 Kubernetes 叢集的_操作員_ 角色或更高角色，才能針對 CFEE **變更容量**（新增或移除 Cell）。
 
  - 使用者需要 IBM Cloud 服務實例的_操作員_ 平台角色（或更高角色），才能**新增**該*服務實例* 至 CFEE 空間（亦即在 CFEE 空間中建立服務實例的別名）。
 
  - 使用者需要_操作員_ 平台角色（或更高角色）及 IBM Cloud 服務實例的_撰寫者_ 服務角色（或更高角色），才能將該服務實例**連結**至部署在 CFEE 空間的應用程式。


## 最佳作法：存取群組
{: #access-groups}

請考慮使用存取群組來管理及簡化 CFEE 的存取控制。存取群組容許您定義任意群組，以便對其指派存取原則。新增至存取群組的任何使用者，都會自動被指派該群組的存取原則。 

您可以從 IBM Cloud 使用者介面或透過 `ibmcloud` CLI 來建立和管理存取群組。 

從使用者介面，移至功能表列、按一下**管理 > 存取 (IAM)**，然後選取[存取群組](https://cloud.ibm.com/iam#/groups)。

或者，您可以使用 `ibmcloud` CLI：

1. 建立存取群組：

  ```
  ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
  ```
  {: pre}

2. 為該存取群組建立存取原則：

  ```
  ibmcloud iam access-group-policy-create GROUP_NAME
  ```
  {: pre}

3. 將使用者新增至存取群組：

  ```
  ibmcloud iam access-group-user-add <user-name> [<user-name2...]
  ```
  {: pre}

<br>
如需相關資訊，請參閱[設定存取群組](https://cloud.ibm.com/docs/iam/groups.html#groups)。
