---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment 新增功能

本文件說明在 {{site.data.keyword.cfee_full_notm}} 服務的這個日期前所發行之每個版本的新增功能。

## 2.2.0 版
{: #v220}

_發行日期：_2019-04-01

CFEE 2.2.0 版包括其組成元件的下列版本：
* Cloud Foundry：2.7.1.15.5 版
* Cloud Foundry API：2.115.0 版
* CFEE 建置套件：0.1.5 版
* IBM Kubernetes Service：未提供任何版本更新。**重要事項：**建議您先將 CFEE Kubernetes 叢集更新為 1.13 版，再更新為 CFEE 2.2.0 版（CFEE 實例在隔離網路中運作時，此為必要項目）。

{{site.data.keyword.cfee_full_notm}} 服務 (CFEE) 2.2.0 版中發行了下列變更。若要更新 CFEE 版本，請移至 CFEE 使用者介面中的**更新與擴充**頁面，然後按一下**更新**：

* 在**多區域** Kubernetes 叢集中**建立** CFEE 實例的新選項。在多區域叢集上建立的 CFEE 實例不僅可以將應用程式實例配送至某資料中心內的各工作者節點，也可以配送至各資料中心，讓應用程式在基礎架構中斷時更具復原力。此外，多區域 CFEE 可以進行**調整**，方法是新增其他 Cell，或從目前區域中移除現有 Cell。請注意，您無法在建立 CFEE 實例之後，從多區域 CFEE 中新增或移除區域。
* CFEE 2.2.0 版實例現在可以[在**隔離網路**內運作](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)。請注意，如果在隔離網路的 VLAN 中部署 CFEE 實例，則部分端點（IP 位址）[必須適當地識別及遞送](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points)，才能讓 CFEE 實例變成可運作。CFEE 實例需要有 Kubernetes 叢集 1.13 版，才能在隔離網路中運作。
* 透過內部 IBM 網路將應用程式（部署至 CFEE 空間）連結至服務實例的新功能。此功能容許在不存取公用網際網路的情況下使用支援「IBM Cloud 服務端點」的服務。
* **監視**工具：
    * 當您建立 CFEE 時，依預設不再佈建監視工具（Prometheus、Grafana 及 Alertmanager）。在 CFEE 2.2.0 版中，只有在 CFEE 管理者明確啟用時，才會佈建監視工具。此外，啟用時，就不會再將監視工具佈建至 CFEE 控制平面工作者節點。它們在控制平面外部佈建於自己的工作者節點上。若要啟用及佈建監視工具，請移至 CFEE _監視_ 頁面（在左導覽窗格中），然後按一下**啟用監視**。 
    * 當您將現有 CFEE 更新為 2.2.0 版時，會從控制平面中刪除現有監視工具。監視工具的任何現有自訂配置都將遺失。 
    *  將預設 [Alertmanager 配置](https://prometheus.io/docs/alerting/configuration/)取代為容許您自訂警示處理、分組及通知遞送的自訂配置的新功能。在_監視_ 頁面中，您可以從本端檔案系統_下載_ 預設配置檔以及_上傳_ 配置檔。請參閱配置檔[範例](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml)。
* 標記 {{site.data.keyword.Bluemix_notm}} [_資源清單_](https://cloud.ibm.com/resources) 及 CFEE 使用者介面中的 CFEE 實例的新功能。
* {{site.data.keyword.Bluemix_notm}} [**Cloud Foundry 儀表板**](https://cloud.ibm.com/dashboard/cloudfoundry/overview)使用者體驗的一般改善。_Cloud Foundry 儀表板_ 顯示已建立別名至 CFEE 空間之 CFEE 實例、應用程式及公用服務的廣域視圖。 

**附註：**建立新的 CFEE 實例時，可以使用新的 **Eirini 技術預覽**方案。此方案與上述的 2.2.0 版無關，僅適用於_標準_ 方案。「Eirini 技術預覽」方案容許您使用原生 Kubernetes 作為容器排程器（而非 Diego）來探索 CFEE。如需相關資訊，請參閱[開始使用 Eirini 技術預覽](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)。

請參閱此[簡要視訊](https://ibm.biz/CFEE-V220){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中 CFEE 2.1.0 版新增功能的示範。


## 2.1.1 版
{: #v211}

_發行日期：_2019-03-20

{{site.data.keyword.cfee_full_notm}} 服務 (CFEE) 2.1.1 版中發行了下列變更。若要更新您的 CFEE 版本，請移至 CFEE 使用者介面的_更新與擴充_ 頁面：

* 已解決阻止成功佈建的問題。 


## 2.1.0 版
{: #v210}

_發行日期：_2019-02-20

**附註：**您只能從 **2.0.2** 版更新為此版本。在更新為 2.1.0 版之前，請先更新為 2.0.2 版。

{{site.data.keyword.cfee_full_notm}} 服務 (CFEE) 2.1.0 版中發行了下列變更。若要更新 CFEE 版本，請移至 CFEE 使用者介面中的**更新與擴充**頁面，然後按一下**更新**：

* 新的自動調整功能，根據自訂規則自動調整 Cloud Foundry 應用程式實例。可以從 CLI 及 Stratos 主控台存取自動調整。從 CFEE 使用者介面的_概觀_ 頁面中，可以選擇性地安裝及啟動 Stratos 主控台。在 Stratos 主控台的_應用程式_ 頁面中，選取應用程式，並尋找**自動調整**標籤。按一下*建立原則* 來啟動自動調整編輯器，以定義目標應用程式的調整原則。如需相關資訊，請參閱[自動調整文件](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps)。
* 從 CFEE 使用者介面管理建置套件的新功能，包括在優先順序清單中拖放置放建置套件。此功能適用於 CFEE 使用者介面（不是 Stratos 主控台）的新**建置套件**頁面。在此版本中，只有 1 MB（或更小）大小的建置套件 zip 檔案能透過使用者介面來新增或更新。您可以使用 `cf create-buildpack` 及 `cf update-buildpack` 指令，上傳大於 1 MB 的建置套件 zip 檔案。 
* 從使用者介面管理組織配額的新功能，包括視覺化使用特定配額的組織。此功能適用於 CFEE 使用者介面（不是 Stratos 主控台）的新**配額**頁面。您可以建立新的配額，以及編輯現有配額。您也可以從配額的功能表中呼叫**複製成預設值**，以使用任何現有配額的值來更新預設配額的值。
* 使用者介面中的新**開始使用**頁面會引導使用者前往最重要的設定及使用環境作業。
* **標籤**可以新增至 IBM Cloud 資源清單中的 CFEE 實例。資源清單中新增的標籤也會出現在 CFEE 概觀頁面的標頭中。
* **Cloud Foundry** 2.7.21 版。
* **Stratos** 主控台 2.3.0 版，包括安全修補程式。請注意，只是更新 CFEE 版本，並不會更新 Stratos 主控台版本。您需要刪除並重新安裝 Stratos 主控台（在「CFEE 概觀」頁面中），如此就會自動挑選最新的 Stratos 主控台版本。
* 使用者可以從 CFEE 概觀頁面的溢位功能表中，導覽至 CFEE 的 Kubernetes **叢集**頁面。

**附註：** 如果您將 CFEE 從 2.0.x 版更新為 2.1.0 版，只要一個_更新_ 動作就可以進行這項更新，而此動作會依序自動更新控制平面及 Cell 兩者。如果您從 1.x.x 版更新，則需要兩個個別的_更新_ 動作來進行更新：一個用於更新控制平面（第一個），另一個用於更新 Cell。

請參閱此[簡要視訊](https://ibm.biz/CFEE-V210){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中 CFEE 2.1.0 版新增功能的示範。


## 2.0.2 版
{: #v202}

_發行日期：_2019-02-08

{{site.data.keyword.cfee_full_notm}} 服務 (CFEE) 2.0.2 版中發行了下列變更。若要更新您的 CFEE 版本，請移至 CFEE 使用者介面的_更新與擴充_ 頁面：

* 已解決阻止成功版本更新的問題。此版本是更新為 **2.1.0** 版的必要項目。


## 2.0.1 版
{: #v201}

_發行日期：_2019-01-10

{{site.data.keyword.cfee_full_notm}} 服務 (CFEE) 2.0.1 版中發行了下列變更。若要更新您的 CFEE 版本，請移至 CFEE 使用者介面的_更新與擴充_ 頁面：

* 已解決導致自訂網域無法適當運作的問題。
* 已解決擷取新度量值時無法使用組織度量值的問題。


## 2.0.0 版
{: #v200}

_發行日期：_2018-12-13

{{site.data.keyword.cfee_full_notm}} 服務 (CFEE) 2.0.0 版中發行了下列變更。若要更新您的 CFEE 版本，請移至 CFEE 使用者介面的_更新與擴充_ 頁面：

* 已改良 CFEE 版本更新備援。
* 改良 CFEE 實例的作業可用性及備援。
* 用戶端憑證以便更安全地存取應用程式，容許伺服器只將應用程式存取權授與給經過認證的用戶端。
* 建立 CFEE 實例時，支援的 Kubernetes 叢集和 Cloud Object Storage 服務實例現在會建立在與 CFEE 服務實例相同的資源群組中（而不是在 "Default" 資源群組下）。
* 安全修補程式。
* `ibmcloud cfee` CLI 的改良：
    * 新指令以便用於從 CFEE 空間建立 IBM Cloud 服務實例，然後將它新增至該 CFEE 空間（`ibmcloud cfee service-create`、`ibmcloud cfee service-alias-create`）。
    * 新指令以便用於調整 CFEE 的容量（`ibmcloud cfee scale-up`、`ibmcloud cfee scale-down`）。
    * 改良指令以便用於管理 CFEE 實例 (`ibmcloud cfee environments`)。
    
      請更新 ibmcloud CLI (`ibmcloud update`) 以存取這些指令加強功能，並發出 `ibmcloud cfee -help` 以取得詳細資料。
      
**附註**：將 CFEE 實例更新至 2.0.0 版，只需要單一_更新_ 動作，它會同時更新控制平面與 Cell。CFEE 控制平面及 Cell 不需要個別進行更新。


## 1.1.2 版
{: #v112}

_發行日期：_2018-12-07

{{site.data.keyword.cfee_full_notm}} 服務 1.1.2 版中發行了下列變更：
* 清奈 (che01) 和米蘭 (mil01) 的新資料中心現在已可用於佈建 CFEE 實例。
* 安全修補程式。

## 1.1.1 版
{: #v111}

_發行日期：_2018-11-28

{{site.data.keyword.cfee_full_notm}} 服務 1.1.1 版中發行了下列變更：
* 安全修補程式。
   
## 1.1.0 版
{: #v110}

_發行日期：_2018-11-16

{{site.data.keyword.cfee_full_notm}} 服務 1.1.0 版中發行了下列變更：

* 新功能：
   * CFEE 實例可以佈建於[虛擬專用](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) Kubernetes 工作者節點，這些節點在專屬於您 IBM Cloud 帳戶的基礎架構上進行管理。
   * 東京 (tok05) 的新資料中心可用於佈建 CFEE 實例。
   * [更新](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) CFEE 實例至新版本。
   * 新增或刪除 Cloud Foundry Cell，以[調整](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) CFEE 實例的容量。
   * 透過與已自動配置的 IBM Cloud Activity Tracker 服務實例整合，以[審核](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) Cloud Foundry 活動。
   * 透過已自動配置的 IBM Cloud Log Analysis 服務實例，以持續保存 Cloud Foundry [日誌事件](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging)。
   * 「性能檢查」視圖，指出 CFEE 元件的作業狀態。
   * 新指令以便用於在指令行介面 (CLI) 上執行 CFEE 相關的動作：
     * `ibmcloud cfee create`、`ibmcloud cfee create-locations` 及 `ibmcloud cfee create-status` 指令，用於從指令行介面建立 CFEE 實例、取得可佈建 CFEE 的可用資料中心清單，以及檢查正在建立之 CFEE 的佈建狀態。
     * `ibmcloud cfee create-permission-get` 及 `ibmcloud cfee create-permission-set` [指令](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating)，以擷取及設定建立 CFEE 實例所需的許可權。這些指令會聚集及簡化 CFEE 服務和必要支援服務的許可權設定。
     * `ibmcloud catalog blacklist` 指令，以簡化 IBM Cloud 帳戶中使用者之 IBM Cloud 服務的[可見性控制](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)。

* 已解決的問題：
   *  已解決的問題：存取 Cell 度量值時發生間歇性錯誤
<br/>   
請參閱此[簡要視訊](https://ibm.biz/CFEE-V110){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中 CFEE 1.1.0 版新增功能的示範。您也可以在 [CFEE 視訊播放清單](https://ibm.biz/CFEE-Playlist){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中找到各種 CFEE 主題的其他視訊。
