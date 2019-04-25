---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 建立環境
{: #create-environment}

## 必要條件
* 確定您位於要建立環境的 {{site.data.keyword.Bluemix_notm}} 帳戶中。
* 確定在建立 {{site.data.keyword.cfee_full_notm}} 實例之前，您具有正確的[許可權](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html)。 
* [準備 IBM Cloud 帳戶](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)，確保它可以建立 CFEE 實例所需的基礎架構資源（CFEE 實例部署在來自 Kubernetes 服務的 Kubernetes 工作者節點）。  

## 建立 CFEE 實例
1.  開啟 {{site.data.keyword.Bluemix_notm}} [型錄](https://cloud.ibm.com/catalog)。

2.  在型錄中找到 {{site.data.keyword.cfee_full_notm}} 服務，然後按一下它以開啟服務的概觀頁面。第一頁提供服務主要特性的概觀。按一下**繼續**。

3.  配置要建立的 CFEE 實例：
    * 選取方案。如需此方案限制的說明，請參閱 [Eirini 技術預覽](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini)小節。
    * 輸入 CFEE 實例的**名稱**。
    * 選取環境分組在其下的**資源群組**。只有您在現行 IBM Cloud 帳戶中有權存取的資源群組才會列在_資源群組_ 下拉清單中，這表示您必須有權在帳戶中存取至少一個資源群組，才能建立 CFEE。
    * 選取要在其中佈建服務實例的**地理**和**位置**。請參閱[可用佈建位置及資料中心](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 的清單（依 CFEE 和支援服務的地理區域排列）。 

4. CFEE 實例佈建在 Kubernetes 叢集上。Cloud Foundry Cell 佈建在 Kubernetes 叢集的工作者節點區域內。您可以配置叢集的位置、硬體及加密：
    * 選取 Kubernetes 叢集的硬體隔離：   
      * _虛擬共用_：叢集中的基礎架構資源（例如 Hypervisor 及實體硬體）會配送給您及其他 IBM 客戶，但每個工作者節點對您而言都是單一承租戶。
      * _虛擬專用_：叢集中的工作者節點是在專用於您帳戶的基礎架構上進行管理。
    * 依預設，會加密叢集中的資料。您可以選擇關閉_加密本端磁碟_。
    * 選取**地理位置**及**地區**，以在其中佈建 Kubernetes 叢集。
    * 選取**區域**，以在其中部署 Kubernetes 工作者節點。您可以選擇在相同區域（**單一區域**）或多個區域（**多區域**）中佈建工作者節點。**請注意**，建立多區域 CFEE 需要 [VLAN Spanning](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning)，這在 {{site.data.keyword.Bluemix_notm}} 帳戶為[已啟用 VRF 功能](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud)時也予以支援。
    
    自動擷取所選取區域的可用 VLAN。如果沒有任何可用的 VLAN，則會自動予以建立。
    
    **附註：在隔離網路上佈建：**您可以將目標設為隔離網路中的 VLAN。在隔離網路中建立 CFEE 實例時，隔離網路中的原則（例如 Calico 原則或 VRA 規則）必須容許來自 CFEE 實例的「所有」出埠存取，才能順利佈建 CFEE。建立 CFEE 之後，即可恢復出埠存取限制，但不含 IBM Cloud 中特定服務及微服務的出埠存取。如需相關資訊，請參閱[在隔離網路中運作](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)文件。
    
    建立 CFEE 之後，在其中佈建環境的 Kubernetes 叢集就會出現（就像 IBM Cloud 帳戶中的任何其他資源一樣）在 {{site.data.keyword.Bluemix_notm}} [儀表板](https://https://cloud.ibm.com/catalog/dashboard/apps/)中。如需相關資訊，請參閱 [Kubernetes Service 文件](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov)。

5.  配置 CFEE 的容量：
    * 選取 CFEE 的 **Cell 數目**。這些是管理部署至 CFEE 之應用程式的應用程式 Cell。  
    * 選取**節點大小**，其決定 Cloud Foundry Cell 的容量（CPU 及記憶體）。
    
    除了您在上面指定的應用程式 Cell 之外，還會建立及保留其他_控制平面 Cell_，用於操作及控制 CFEE 中的 Cloud Foundry 平台。 

    **附註：**我們建議如果 Kubernetes 叢集中的工作者節點是佈建在不同子網路，則請啟用 VLAN Spanning。如果停用 VLAN Spanning，不同子網路上的工作者節點可能會阻礙它們之間的連線功能。如需相關資訊，請參閱 [VLAN Spanning](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning) 文件。

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

## Eirini 技術預覽方案
{: #eirini}

 「Eirini 技術預覽」方案容許您使用原生 Kubernetes 作為容器排程器（而非 Diego）來探索 CFEE。Kubernetes 排程器用於 CFEE，以在 Cloud Foundry 應用程式運行環境中部署及執行應用程式、新增使用者、建立組織和空間、部署應用程式，以及將這些應用程式連結至服務。如需 Cloud Foundry Foundation 中 Eirini Incubator 專案的相關資訊，請參閱 [Eirini 專案](https://www.cloudfoundry.org/project-eirini/)文件。
 下列限制適用於從「Eirini 技術預覽」方案建立的 CFEE 實例:
 
* 不支援具有 `containerd` 的 Kubernetes。僅支援使用 Docker 的 Kubernetes 版本，而非 `containerd`。支援 Docker 的最新 IBM Container Service (IKS) 版本為 1.10 版。
* 不支援 Cloud Foundry SSH。
* 不支援 Docker 映像檔的 `cf push`。
* 不支援 Kubernetes 原生 Eirini 編譯打包。從 Eirini 技術預覽方案建立的 CFEE 實例會使用 Eirini 來執行應用程式，而不是將它們編譯打包。Diego Cell 仍然用於編譯打包應用程式。
* 不支援重新啟動特定應用程式實例 (`cf restart-app-instance`)。

 
