---



copyright:

  years: 2018

lastupdated: "2019-01-08"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# 常見問題
{: #cfeefaq}

## IBM Cloud Foundry Enterprise Environment (CFEE) 與公用 Cloud Foundry 之間的差異為何？
{: #cfee_diff}

您可以使用 {{site.data.keyword.cloud}} Foundry Public 來執行使用 Cloud Foundry 的雲端原生應用程式，以進行簡單設定、功能強大的調整，以及資料流量管理。您也可以輕鬆存取所有 {{site.data.keyword.cloud}} 服務。

您可以將 {{site.data.keyword.cfee_full}} 用於與 Cloud Foundry Public 搭配使用的所有項目，同時建立及管理專用於管理企業之 Cloud Foundry 應用程式的隔離環境。


## 新的供應項目與先前的 IBM Cloud Foundry 供應項目有何不同？
{: #cfOfferings_diff}

關於公用多方承租戶，最值得注意的差異無疑是隔離內容。而關於 IBM Cloud 基礎架構上的現有單一承租戶供應項目，則主要的兩項差異是基礎架構覆蓋區減少（因此降低成本），以及這類單一承租戶環境的服務整合模型。

## 我可以在哪裡找到 CFEE 服務？
{: #where}

您可以在 {{site.data.keyword.Bluemix_notm}} [型錄](https://cloud.ibm.com/catalog)中找到並實例化 {{site.data.keyword.cfee_full}} 服務。

## 可以在地區資料中心內有多個 CFEE 環境嗎？
{: #multiple-cfees}

是，您可以依需求在[這些地區](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 建立所需數目的 CFEE 實例。

## CFEE 環境是否可以佈建至多個資料中心（多區域）？
{: #multizone}
是。從 CFEE 2.2.0 版開始，可以將 CFEE 基礎架構（Kubernetes 叢集節點）配送至給定地區內的多個資料中心（區域）。 

## 我需要以某個最小容量啟動嗎？
{: #minimum-capacity}

是。建立 CFEE 實例需要最少兩個 Cloud Foundry Cell，而且每個都有 4 核心的 16GB RAM、25GB SSD 主要磁碟、100GB SSD 次要磁碟及 1000Mbps 網路速度。

## 在其中部署 CFEE 的基礎 IaaS 為何？
{: #why-kubs}

CFEE 服務可在 Kubernetes 容器上執行，容許較低的基礎架構成本與更有效率的作業，因為 Kubernetes 是相當智慧型的 IaaS，可自動執行許多作業活動。 

## 建立 CFEE 時，我有哪些隔離選項？
{: #isolation}

您在已部署 CFEE 實例的 Kubernetes 基礎架構類型上有兩個硬體選項：_虛擬共用_ 或_虛擬專用_ 硬體。使用_虛擬共用_ 硬體，您與其他 IBM 客戶之間會分佈工作者節點（其中已部署 Cloud Foundry 平台容器）。使用_虛擬專用_，會在您帳戶專用的硬體上管理工作者節點。請注意，在這兩種情況（_虛擬共用_ 及_虛擬專用_）下，每個工作者節點都是客戶的單一承租戶。這表示，執行應用程式的 Cloud Foundry Cell 未與其他客戶共用。

## CFEE 是否可以在隔離網路內運作？
{: #isolation}

是。從 2.2.0 版開始，IBM® Cloud Foundry Enterprise Environment (CFEE) 實例可以在隔離網路內運作，用於保護環境免於發生外部威脅。如需詳細資料，請參閱[在隔離網路中運作](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)文件。

## 我可以調整 CFEE 容量嗎？
{: #scaling}

是，您可以新增或移除 Cloud Foundry Cell，隨需求變更來擴增或縮減 CFEE 容量。

## 我可以將 CFEE 升級至新版本嗎？它如何運作？
{: #upgrading}
是。有新的 CFEE 版本時，CFEE 使用者介面會通知您。您可以控制何時更新至新版本。CFEE 管理者會在使用者介面中呼叫 CFEE 版本更新。CFEE 版本更新可能包裝新版本的元件或支援服務（例如，Cloud Foundry、Kubernetes 等）。請先更新 CFEE 控制平面，然後再更新 Cloud Foundry Cell。更新處理程序已最佳化，以盡可能減少干擾。

## 建立 CFEE 實例要採取哪些動作？
{: #create}

您可以在 {{site.data.keyword.Bluemix_notm}} 型錄中找到所列出的 CFEE 服務。您需要有已升級的 {{site.data.keyword.Bluemix_notm}} 帳戶，以及 CFEE 服務和其支援服務 (Kubernetes、Cloud Object Storage 及 Compose for PostgreSQL) 的許可權。在具有這些許可權之後，您只需要提供環境的名稱，然後按一下_建立_。建立大約需要 90 分鐘。

## 我可以在 CFEE 中使用 {{site.data.keyword.Bluemix_notm}} 服務嗎？
{: #Services-ibmcloud}

當然！藉由在 {{site.data.keyword.Bluemix_notm}} 中整合，CFEE 中的開發人員可以建立 {{site.data.keyword.Bluemix_notm}} 服務實例（或使用現有實例），並將它們連結至 CFEE 空間中所部署的應用程式。

## 我可以在 CFEE 中擁有自己的服務嗎？
{: #Services-ibmcloud}

是。管理者可以在 CFEE 中登錄服務分配管理系統，並讓自訂服務方案可供該 CFEE 中的使用者使用。本端 MCFEE 市場包括來自 {{site.data.keyword.Bluemix_notm}} 型錄的服務，以及 CFEE 的本端服務分配管理系統所管理的所有客戶服務。

## 如何控制使用者對 CFEE 的存取？
{: #Services}

就像任何其他 {{site.data.keyword.Bluemix_notm}} 服務一樣，可透過 _Identity & Access Management_ (IAM) 來控制對 CFEE 的存取。使用特定角色來指派使用者存取原則（個別或透過存取群組），可將特定 CFEE 存取層次提供給它們。除了對 CFEE 服務的存取之外，還會透過 Cloud Foundry 成員資格以及指派給特定組織及空間中使用者的角色來控制對 CFEE 中 Cloud Foundry 組織及空間的存取。

