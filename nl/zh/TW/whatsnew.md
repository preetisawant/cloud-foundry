---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment 新增功能

本文件說明在 {{site.data.keyword.cfee_full_notm}} 服務的這個日期前所發行之每個版本的新增功能。


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
