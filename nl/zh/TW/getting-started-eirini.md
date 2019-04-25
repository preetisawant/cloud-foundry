---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 開始使用 Eirini 技術預覽
{: #getting-started-eirini}

{{site.data.keyword.cfee_full}} (CFEE) 是用於在雲端管理應用程式及服務的雲端平台。{{site.data.keyword.cfee_full_notm}} 可讓您隨著使用量成長而輕鬆擴充應用程式，並且簡化運行環境、中介軟體及基礎架構，以著重於開發應用程式。
{: shortdesc}

此入門指導教學顯示如何從 Eirini 技術預覽方案建立 {{site.data.keyword.cfee_full_notm}}、新增使用者、建立組織和空間、部署應用程式，以及將這些應用程式連結至服務。
如需 Cloud Foundry Foundation 中 Eirini Incubator 專案的相關資訊，請參閱 [Eirini 專案](https://www.cloudfoundry.org/project-eirini/)。

## 瞭解許可權
{: #permissions}

您需要有正確的存取原則才能建立 {{site.data.keyword.cfee_full_notm}} 的實例。如需相關資訊，請參閱[許可權](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)。

## 步驟 1：確定 {{site.data.keyword.Bluemix_notm}} 帳戶可以建立基礎架構資源
{: #accountprep-environment}

CFEE 實例部署在來自 Kubernetes 服務的 Kubernetes 工作者節點。[準備 IBM Cloud 帳戶](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)，確保它可以建立 CFEE 實例所需的基礎架構資源。

## 步驟 2：建立 CFEE 實例
{: #create-environment}

建立 CFEE 之前，請確定您位於要建立環境的 {{site.data.keyword.Bluemix_notm}} 帳戶中，而且您具有必要的存取原則（上方的步驟 1）。

1.  開啟 {{site.data.keyword.Bluemix_notm}} [型錄](https://cloud.ibm.com/catalog)。

2.  在型錄中找到 {{site.data.keyword.cfee_full_notm}} 服務，然後按一下它以開啟服務的概觀頁面。第一頁提供服務主要特性的概觀。按一下**繼續**。

3.  配置要建立的 CFEE 實例：
    * 選取 _Eirini 技術預覽_ 方案。
    * 輸入 CFEE 實例的**名稱**。
    * 選取環境分組在其下的**資源群組**。只有您在現行 IBM Cloud 帳戶中有權存取的資源群組才會列在_資源群組_ 下拉清單中，這表示您必須有權在帳戶中存取至少一個資源群組，才能建立 CFEE。
    * 選取要在其中佈建服務實例的**地理**和**位置**。請參閱[可用佈建位置及資料中心](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 的清單（依 CFEE 和支援服務的地理區域排列）。 

4. CFEE 實例佈建在 Kubernetes 叢集上。Cloud Foundry Cell 佈建在 Kubernetes 叢集的工作者節點區域內。您可以配置叢集的位置、硬體及加密：
    * 選取 Kubernetes 叢集的硬體隔離：   
      * _虛擬共用_：叢集中的基礎架構資源（例如 Hypervisor 及實體硬體）會配送給您及其他 IBM 客戶，但每個工作者節點對您而言都是單一承租戶。
      * _虛擬專用_：叢集中的工作者節點是在專用於您帳戶的基礎架構上進行管理。
    * 依預設，會加密叢集中的資料。您可以選擇關閉_加密本端磁碟_。
    * 選取**地理位置**及**地區**，以在其中佈建 Kubernetes 叢集。
    * 選取**區域**，以在其中部署 Kubernetes 工作者節點。自動擷取所選取區域的可用 VLAN。如果沒有任何可用的 VLAN，則會自動予以建立。從 CFEE 2.2.0 版開始，CFEE 實例可以在**隔離網路**後面運作。您可以選取隔離網路中的專用 VLAN，來將 CFEE 實例佈建至隔離網路。建立 CFEE 之後，網路管理者就必須在隔離網路中遞送 CFEE Compose for PostgreSQL 及 Cloudant Object Storage 實例的 IP 位址，以及 Kubernetes 叢集的「應用程式負載平衡器 ([ALB](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress))」的 IP 位址，CFEE 才會變成運作中。
    
    建立 CFEE 之後，在其中佈建環境的 Kubernetes 叢集就會出現（就像 IBM Cloud 帳戶中的任何其他資源一樣）在 {{site.data.keyword.Bluemix_notm}} [儀表板](https://cloud.ibm.com/dashboard/apps/)中。如需相關資訊，請參閱 [Kubernetes Service 文件](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov)。

5.  配置 CFEE 的容量：
    * 選取 CFEE 的 **Cell 數目**。這些是管理部署至 CFEE 之應用程式的應用程式 Cell。  
    * 選取**節點大小**，其決定 Cloud Foundry Cell 的容量（CPU 及記憶體）。
    
    除了您在上面指定的應用程式 Cell 之外，還會建立及保留其他_控制平面 Cell_，用於操作及控制 CFEE 中的 Cloud Foundry 平台。 

    **附註：**我們建議如果 Kubernetes 叢集中的工作者節點是佈建在不同子網路，則請啟用 VLAN Spanning。如果停用 VLAN Spanning，不同子網路上的工作者節點可能會阻礙它們之間的連線功能。如需相關資訊，請參閱 [VLAN Spanning](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning) 文件。
    
6.  在 **Compose for PostgreSQL** 欄位中，選取其中一個公用組織，然後選取該組織中其中一個可用的空間。Compose for PostgreSQL 服務實例將佈建在選取的空間。Compose for PostgreSQL 服務是 CFEE 服務的必要相依關係。

    **附註：**在 _Compose for PostgreSQL_ 下，只有您打算佈建 CFEE 實例（上述步驟 4）的位置，以及您可存取的位置，當中的組織才可供選取。在特定的組織內，只有您具有_開發人員_ 存取權的空間可供選取。 

7.  頁面右側中的**訂單摘要**會反映 CFEE 實例與輔助服務的成本，以及預估的每月總成本。

8.  按一下**建立**，以開啟環境儀表板，並指出建立進度和狀態。

**附註：**建立程序開始之後，在 {{site.data.keyword.Bluemix_notm}} 儀表板的_資源清單_，以及 [Cloud Foundry 環境儀表板](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments)中，會顯示 CFEE 的表格列。表格列中的狀態指出建立的完成時間。

建立環境的自動化處理程序會將基礎架構部署至 Kubernetes 叢集，並配置它以供使用。此處理程序需要 90 - 120 分鐘。

建立 CFEE 之後，您會收到多封電子郵件，確認佈建 CFEE 及支援服務，也會收到通知您相對應訂單狀態的電子郵件。

建立 CFEE 實例時，在相同的 IBM Cloud 帳戶中會額外建立三個支援服務實例。那些支援服務實例會以 CFEE 實例名稱來命名。因此，建立 CFEE 會導致在 IBM Cloud 帳戶中建立總計 4 個服務實例：
* CFEE 實例 ("_cfeename_")。
* Kubernetes 叢集 ("_cfeename_-cluster")。叢集提供在其中佈建 CFEE 實例的基礎架構。
* Cloud Object Storage 實例 ("_cfeename_-cos")。實例用來儲存在建立 CFEE 應用程式容器期間所產生的資料（例如：上傳的應用程式套件、建置套件及已編譯的執行檔）。
* Compose for PosgreSQL 實例 ("_cfeename_-postgres")。實例用來將 Cloud Foundry 資料儲存至 CFEE 實例（例如：審核應用程式部署、啟動及停止事件；保留 CFEE 使用者成員資格、組織、空間、應用程式及服務連線的記錄）。 

## 步驟 3：建立組織及空間
{: #create-orgsandspaces}

在您建立 {{site.data.keyword.cfee_full_notm}} 之後，請參閱[建立組織及空間](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)，以了解如何建立組織及空間來建構環境的相關資訊。{{site.data.keyword.cfee_full_notm}} 中的應用程式是以特定空間為範圍。空間則是存在於特定組織內。組織的成員會共用配額方案、應用程式、服務實例及自訂網域。

當您建立組織時，請指派其配額。資源的配額集限制（記憶體、CPU 等）適用於該組織。您可於稍後指派不同的配額。每個 CFEE 中都有一組預先配置的配額，但您也可以在 CFEE 使用者介面的**配額**頁面中建立自己的自訂配額。您可以將自訂配額設為_預設_ 配額，方法是從配額的功能表中呼叫_複製成預設值_ 動作，以將自訂配額的值複製成預設配額。

**附註：**_Cloud Foundry 組織_ 頁面可從位於頂端 IBM Cloud 標頭的**_管理 > 帳戶 > Cloud Foundry 組織_** 功能表中取得，它是要專用於公用 IBM Cloud 組織，**而非 CFEE 組織**。CFEE 組織是在 CFEE 實例的_組織_ 頁面中進行管理。開啟 CFEE 使用者介面，然後按一下**_組織_** 頁面以建立及管理該 CFEE 的組織。

## 步驟 4：將使用者新增至組織及空間
{: #add-users}

透過控制存取層次的特定角色指派，[新增使用者](https://cloud.ibm.com/docs/cloud-foundry/add-users.html)至這些組織及空間。使用者必須先前已可存取 CFEE 實例，才能新增為 CFEE 中組織及空間的成員。請參閱[許可權](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)。

## 步驟 5：部署及檢視應用程式
{: #deploy-apps}

當您準備就緒，就可以使用 {{site.data.keyword.Bluemix_notm}} 指令行介面來[部署應用程式](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)。在使用者介面中，檢視特定 CFEE 空間的環境定義內或廣域跨所有 CFEE 實例的已部署應用程式清單。您也可以從那些視圖啟動、停止或刪除應用程式。

## 步驟 6：建立或新增 IBM Cloud 服務實例至 CFEE 空間
{: #service-instances}

在 IBM Cloud 帳戶裡[建立服務](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)或[新增現有可用服務](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)。服務實例提供於 CFEE 空間之後，您便可以將它連結至部署在該空間的 CFEE 應用程式。

## 步驟 7：將應用程式連結至服務實例
{: #bind-apps}

[連結應用程式](https://console.bluemix.net/docs/cloud-foundry/binding.html)至服務實例別名，以使用服務的功能。

在 [Cloud Foundry 儀表板](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中，您可以看到所有應用程式及服務的合併視圖，不論是*公用* 還是*企業*。在 Cloud Foundry 儀表板之後，請按一下左導覽窗格的 *Public*，即可看到 IBM Cloud 帳戶中可用的公用應用程式及服務。按一下 *Enterprise* 可以看到所有 CFEE 環境、部署到 CFEE 空間的應用程式，以及 CFEE 空間可用的服務。
{:tip}

## 步驟 8：安裝 Stratos 主控台來管理應用程式（選用）
{: #install-stratos}

「Stratos 主控台」是用來使用 Cloud Foundry 的開放程式碼 Web 型工具。「Stratos 主控台」應用程式可以選擇性地安裝並用於特定 CFEE 環境，以管理其組織、空間及應用程式。

在 CFEE 實例具有 IBM Cloud 管理者或編輯者角色的使用者，可以在該 CFEE 實例中安裝「Stratos 主控台」應用程式。

若要安裝「Stratos 主控台」應用程式，請執行下列動作：

1. 開啟您要安裝 Stratos 主控台的 CFEE 實例。
2. 按一下概觀頁面上的**安裝 Stratos 主控台**。只有具有該 CFEE 實例之管理者或編輯者許可權的使用者才能看到此按鈕。
3. 在「安裝 Stratos 主控台」對話框中，選取安裝選項。您可以將 Stratos 應用程式安裝在 Cloud Foundry Cell 或 Kubernetes 叢集中。選取 Stratos 主控台的版本，以及要安裝之應用程式的實例數。如果您將 Stratos 主控台應用程式安裝在 Cloud Foundry Cell 中，則系統會提示您輸入要部署應用程式的組織及空間。
4. 按一下**安裝**。

應用程式需要大約 5 分鐘才能安裝。安裝完成之後，會在概觀頁面上出現 **Stratos 主控台**按鈕，代替_安裝 Stratos 主控台_ 按鈕。_Stratos 主控台_ 按鈕會啟動主控台，並且可供所有具有 CFEE 實例存取權的使用者使用。組織及空間成員資格指派可能會限制使用者在 Stratos 主控台中可以查看及管理的內容。

若要啟動 Stratos 主控台，請執行下列動作：

1. 開啟已安裝 Stratos 主控台的 CFEE 實例。
2. 按一下概觀頁面上的 **Stratos 主控台**。
3. Stratos 主控台會在個別的瀏覽器標籤中開啟。因為是自簽憑證，所以第一次開啟主控台時，系統會提示您接受兩次連續警告。
4. 按一下**登入**來開啟主控台。因為應用程式會使用您的 {{site.data.keyword.Bluemix_notm}} 認證，所以不需要認證。


## 其他資源
{: #additional-resources}

您可以在 CFEE 中使用 `ibmcloud CFEE` CLI 指令來執行部分管理作業。這些指令容許您取得 CFEE 實例的相關資訊，以及用來管理其組織及空間。請參閱 [IBM Cloud CLI CFEE 指令參考手冊](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。

您可以在 [CFEE 視訊播放清單](https://ibm.biz/CFEE-Playlist){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中找到各種 CFEE 主題深度討論及示範的視訊。

CFEE [API 文件](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中提供 CFEE API 的相關資訊。
