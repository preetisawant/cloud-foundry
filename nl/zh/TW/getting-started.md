---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 入門指導教學
{: #getting-started}

{{site.data.keyword.cfee_full}} 是用於在雲端管理應用程式及服務的雲端平台。{{site.data.keyword.cfee_full_notm}} 可讓您隨著使用量成長而輕鬆擴充應用程式，並且簡化運行環境、中介軟體及基礎架構，以著重於開發應用程式。
{: shortdesc}

此入門指導教學顯示如何建立 {{site.data.keyword.cfee_full_notm}}、新增使用者、建立組織和空間、部署應用程式，以及將這些應用程式連結至服務。

## 瞭解許可權
{: #permissions}

若要使用 {{site.data.keyword.cfee_full_notm}} 實例，服務使用者必須具有正確的許可權。如需相關資訊，請參閱[許可權](https://console.bluemix.net/docs/cloud-foundry/permissions.html)。

## 步驟 1：確定 {{site.data.keyword.Bluemix_notm}} 帳戶可以建立基礎架構資源
{: #accountprep-environment}

CFEE 實例部署在基礎架構資源上，而基礎架構資源是來自 Kubernetes 服務的 Kubernetes 工作者節點。[準備 IBM Cloud 帳戶](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html)，確保它可以建立 CFEE 實例所需的基礎架構資源。

## 步驟 2：建立 CFEE 實例
{: #creating-environment}

建立 CFEE 之前，請確定您位於要建立環境的 {{site.data.keyword.Bluemix_notm}} 帳戶中，而且您具有必要的存取原則（根據上方的步驟 1）。

1.  開啟 {{site.data.keyword.Bluemix_notm}} [型錄](https://console.bluemix.net/catalog)。

2.  在型錄中找到 {{site.data.keyword.cfee_full_notm}} 服務，然後按一下它以開啟服務的概觀頁面。

3.  建立頁面的第一頁提供服務主要特性的概觀。按一下**繼續**。

4.  提供下列資訊，以配置要建立的 CFEE 實例：
    * 選取方案（方案可用性在測試版期間可能受限）。
    * 輸入服務實例的**名稱**。
    * 選取要在其中佈建服務實例的**位置**。請參閱[可用佈建位置及資料中心](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 的清單（依 CFEE 和支援服務的地理區域排列）。 
    * 針對 Cloud Foundry 環境，選取 **Cell 數目**。
    * 選取**機型**，其決定 Cloud Foundry Cell 的大小（CPU 及記憶體）。
    * 選取環境分組在其下的**資源群組**。只有您在現行 IBM Cloud 帳戶中有權存取的資源群組才會列在_資源群組_ 下拉清單中，這表示您必須有權在帳戶中存取至少一個資源群組，才能建立 CFEE。

5.  在 **Compose for PostgreSQL** 欄位中，選取其中一個公用組織，然後選取該組織中其中一個可用的空間。Compose for PostgreSQL 服務實例將佈建在選取的空間。Compose for PostgreSQL 服務是 CFEE 服務的必要相依關係。

**附註：**只有您打算佈建 CFEE 實例（上述步驟 4）的位置，以及您可存取的位置，當中的組織才可供選取。在特定的組織內，只有您具有_開發人員_ 存取權的空間可供選取。 

6.  （選用）開啟**基礎架構**區段，以查看支援 CFEE 實例的 Kubernetes 叢集內容。請注意，**工作者節點數目**等於 Cell 數目加 2（所佈建 Kubernetes 工作者節點中的其中兩個會支援 CFEE 控制平面）。在其上部署環境的 Kubernetes 叢集會出現在 {{site.data.keyword.Bluemix_notm}} [儀表板](https://console.bluemix.net/dashboard/apps/)中。如需相關資訊，請參閱 [Kubernetes Service 文件](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov)。

**附註：**我們建議如果 Kubernetes 叢集中的工作者節點是佈建在不同子網路，則請啟用 VLAN Spanning。如果停用 VLAN Spanning，不同子網路上的工作者節點可能會阻礙它們之間的連線功能。如需相關資訊，請參閱 [VLAN Spanning](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning) 文件。

7.  頁面右側中的**訂單摘要**會反映 CFEE 實例與輔助服務的成本，以及預估的每月總成本。

8.  按一下**建立**，以開啟環境儀表板，並指出建立進度和狀態。

9.  開始佈建之後，會在 {{site.data.keyword.Bluemix_notm}} 儀表板及 [Cloud Foundry 環境儀表板](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments)中顯示該環境。狀態指出佈建何時完成。

建立環境的自動化處理程序會將基礎架構部署至 Kubernetes 叢集，並配置它以供使用。此處理程序需要 90 - 120 分鐘。

順利建立環境之後，您會收到多封電子郵件，確認佈建 CFEE 及支援服務，也會收到通知您相對應訂單狀態的電子郵件。

## 步驟 3：建立組織及空間

在您建立 {{site.data.keyword.cfee_full_notm}} 之後，請參閱[建立組織及空間](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html)，以了解如何建立組織及空間來建構環境的相關資訊。{{site.data.keyword.cfee_full_notm}} 中的應用程式是以特定空間為範圍。空間則是存在於特定組織內。組織的成員會共用配額方案、應用程式、服務實例及自訂網域。

**附註：**_Cloud Foundry 組織_ 頁面可從位於頂端 IBM Cloud 標頭的**_管理 > 帳戶 > Cloud Foundry 組織_** 功能表中取得，它是要專用於公用 IBM Cloud 組織，**而非 CFEE 組織**。CFEE 組織是在 CFEE 實例的_組織_ 頁面中進行管理。開啟 CFEE 使用者介面，然後按一下**_組織_** 頁面以建立及管理該 CFEE 的組織。

## 步驟 4：將使用者新增至組織及空間

透過控制存取層次的特定角色指派，[新增使用者](https://console.bluemix.net/docs/cloud-foundry/add-users.html)至這些組織及空間。使用者必須先前已可存取 CFEE 實例，才能新增為 CFEE 中組織及空間的成員。請參閱[許可權](https://console.bluemix.net/docs/cloud-foundry/permissions.html)。

## 步驟 5：部署及檢視應用程式

當您準備就緒，就可以使用 {{site.data.keyword.Bluemix_notm}} 指令行介面來[部署應用程式](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)。在使用者介面中，檢視特定 CFEE 空間的環境定義內或廣域跨所有 CFEE 實例的已部署應用程式清單。您也可以從那些視圖啟動、停止或刪除應用程式。

## 步驟 6：使用服務

在 IBM Cloud 帳戶裡[建立服務](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#creating-services_inspace)或[新增現有可用服務](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#adding-services_inspace)。服務實例提供於 CFEE 空間之後，您便可以將它連結至部署在該空間的 CFEE 應用程式。

## 步驟 7：將應用程式連結至服務實例

[連結應用程式](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#bind_services)至服務實例別名，以使用服務的功能。

您知道 [Cloud Foundry 儀表板](https://console.bluemix.net/dashboard/cloudfoundry/overview)嗎？在那裡，您可以看到 {{site.data.keyword.Bluemix_notm}} 中所有應用程式及服務的合併視圖，不論是 _Public_ 還是 _Enterprise_ (CFEE)。在 Cloud Foundry 儀表板之後，請按一下左導覽窗格的 _Public_，即可看到 IBM Cloud 帳戶中可用的公用應用程式及服務。按一下 _Enterprise_ 可以看到所有 CFEE 環境、部署到 CFEE 空間的應用程式，以及 CFEE 空間可用的服務。
{:tip}

## 步驟 8：安裝 Stratos 主控台來管理應用程式（選用）

「Stratos 主控台」是用來使用 Cloud Foundry 的開放程式碼 Web 型工具。「Stratos 主控台」應用程式可以選擇性地安裝並用於特定 CFEE 環境，以管理其組織、空間及應用程式。

在 CFEE 實例具有 IBM Cloud 管理者或編輯者角色的使用者，可以在該 CFEE 實例中安裝「Stratos 主控台」應用程式。

若要安裝「Stratos 主控台」應用程式，請執行下列動作：

1. 開啟您要安裝 Stratos 主控台的 CFEE 實例。
2. 按一下概觀頁面上的**安裝 Stratos 主控台**。只有具有該 CFEE 實例之管理者或編輯者許可權的使用者才能看到此按鈕。
3. 在「安裝 Stratos 主控台」對話框中，選取安裝選項。您可以在 CFEE 控制平面上或其中一個 Cell 中安裝 Stratos 主控台應用程式。選取 Stratos 主控台的版本，以及要安裝之應用程式的實例數。如果您將 Stratos 主控台應用程式安裝在 Cell 中，則系統會提示您輸入要部署應用程式的組織及空間。
4. 按一下**安裝**。

應用程式需要大約 5 分鐘才能安裝。安裝完成之後，會在概觀頁面上出現 **Stratos 主控台**按鈕，代替_安裝 Stratos 主控台_ 按鈕。_Stratos 主控台_ 按鈕會啟動主控台，並且可供所有具有 CFEE 實例存取權的使用者使用。組織及空間成員資格指派可能會限制使用者在 Stratos 主控台中可以查看及管理的內容。

若要啟動 Stratos 主控台，請執行下列動作：

1. 開啟已安裝 Stratos 主控台的 CFEE 實例。
2. 按一下概觀頁面上的 **Stratos 主控台**。
3. Stratos 主控台會在個別的瀏覽器標籤中開啟。因為是自簽憑證，所以第一次開啟主控台時，系統會提示您接受兩次連續警告。
4. 按一下**登入**來開啟主控台。因為應用程式會使用您的 {{site.data.keyword.Bluemix_notm}} 認證，所以不需要認證。

CFEE API 的相關資訊提供於 CFEE [API 文件](https://console.bluemix.net/apidocs/cfaas){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
{:tip}
