---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cloud Foundry 如何與 {{site.data.keyword.cloud_notm}} 搭配運作
{: #howwork}

將應用程式部署至 Cloud Foundry 時，您必須使用足夠的資訊來配置 {{site.data.keyword.cloud_notm}}，才能支援該應用程式。

* 對於行動應用程式，{{site.data.keyword.cloud_notm}} 包含代表行動應用程式後端的構件，例如行動應用程式用來與伺服器進行通訊的服務。
* 對於 Web 應用程式，您必須確保將運行環境及架構的相關資訊傳遞給 {{site.data.keyword.cloud_notm}}，讓 {{site.data.keyword.cloud_notm}} 可以設定適當的執行環境來執行應用程式。

每一個執行環境（包括行動及 Web）都與其他應用程式的執行環境相隔離。即使這些應用程式位在相同的實體機器上，也一樣會隔離執行環境。下圖顯示 Cloud Foundry 如何管理 {{site.data.keyword.cloud_notm}} 中應用程式部署的基本流程：

![部署應用程式](images/deploy.png)

圖 1. 部署應用程式

當您建立應用程式並將其部署至 Cloud Foundry 時，{{site.data.keyword.cloud_notm}} 環境會判定傳送應用程式的適當虛擬伺服器，或將應用程式所代表的構件傳送至其中的適當虛擬伺服器。對於行動應用程式，將在 {{site.data.keyword.cloud_notm}} 上建立行動後端投射。在雲端中執行的行動應用程式的任何程式碼最終都會在 {{site.data.keyword.cloud_notm}} 環境中執行。對於 Web 應用程式，在雲端中執行的程式碼是開發人員部署至 {{site.data.keyword.cloud_notm}} 的應用程式本身。虛擬伺服器的判定是根據數個因素，包括：

* 機器上已有的負載。
* 該虛擬伺服器支援的運行環境或架構。

選擇虛擬伺服器之後，每一部虛擬伺服器上的應用程式管理程式都會為應用程式安裝適當的架構及運行環境。然後，即可將應用程式部署至該架構。部署完成之後，即會啟動應用程式構件。

下圖顯示已部署多個應用程式的虛擬伺服器結構（也稱為 Droplet Execution Agent，DEA）：

![虛擬伺服器的設計](images/container-diego.png)

圖 2. 虛擬伺服器的設計

在每一台虛擬伺服器中，應用程式管理程式都會與 {{site.data.keyword.cloud_notm}} 基礎架構的其餘部分進行通訊，並管理部署至此虛擬伺服器的應用程式。每一台虛擬伺服器都具有容器，用以隔離及保護應用程式。在每一個容器中，{{site.data.keyword.cloud_notm}} 會安裝每一個應用程式所需的適當架構及運行環境。

部署應用程式時，如果該應用程式具有 Web 介面（例如，Java Web 應用程式）或其他以 REST 為基礎的服務（例如，向行動應用程式公開的行動服務），則應用程式的使用者就可利用正常的 HTTP 要求與其進行通訊。

![呼叫 {{site.data.keyword.cloud_notm}} 應用程式](images/execute.png)

圖 3. 呼叫 {{site.data.keyword.cloud_notm}} 應用程式

每一個應用程式都可以有一個以上的相關聯 URL，但是它們必須全部指向 {{site.data.keyword.cloud_notm}} 端點。要求到達時，{{site.data.keyword.cloud_notm}} 會檢查該要求，並判定其適用的應用程式，然後選取用來接收該要求的應用程式實例。


## {{site.data.keyword.cloud_notm}} 中的 Cloud Foundry 架構
{: #architecture}

一般而言，您在 {{site.data.keyword.cloud_notm}} 的 Cloud Foundry 中執行應用程式時，不需要擔心作業系統及基礎架構層。例如根檔案系統及中介軟體元件等層會抽象化，因此您可以專注於應用程式碼。不過，如果您需要應用程式執行位置的明確資訊，可以進一步瞭解這些層。

如需詳細資料，請參閱[檢視 {{site.data.keyword.cloud_notm}} 基礎架構層](cf.html#infralayers)。

身為開發人員，您可以利用以瀏覽器為基礎的使用者介面，來與 {{site.data.keyword.cloud_notm}} 基礎架構互動。您也可以使用 Cloud Foundry 指令行介面（稱為 cf）來部署 Web 應用程式。

用戶端（可以是行動應用程式、外部執行的應用程式、以 {{site.data.keyword.cloud_notm}} 為建置基礎的應用程式，或使用瀏覽器的開發人員）可以與 {{site.data.keyword.cloud_notm}} 管理的應用程式互動。用戶端會使用 REST 或 HTTP API，透過 {{site.data.keyword.cloud_notm}} 將要求遞送到其中一個應用程式實例或複合式服務。

下圖顯示 {{site.data.keyword.cloud_notm}} 上的高階 Cloud Foundry 架構。

![{{site.data.keyword.cloud_notm}} 架構](images/arch.png)

圖 4. {{site.data.keyword.cloud_notm}} 上的 Cloud Foundry 架構

基於延遲或安全考量，您可以將應用程式部署至不同的 {{site.data.keyword.cloud_notm}} 地區。您可以選擇部署至一個地區，或是部署至多個地區。


![多地區應用程式開發](images/multi-region.png)

圖 5. 多地區應用程式部署

{{site.data.keyword.Bluemix_notm}} 基礎架構層
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} 會抽象化並隱藏作業系統與基礎架構層，因此您不需要管理它們。不過，您有時可能會想要更瞭解適用於您應用程式的作業系統及中介軟體。
{:shortdesc}

### 檢視 {{site.data.keyword.Bluemix_notm}} 基礎架構層
{: #viewinfra}

您可以執行 **bluemix app stacks** 指令，顯示要部署應用程式的可用堆疊（或根檔案系統）。您也可以在使用 **bluemix app push** 指令時，以 *-s* 選項和 *stack_name* 指定堆疊，其中 stack_name 是根檔案系統，例如 `lucid64` 或 `cflinuxfs2`：

```
bluemix app push appName -s stack_name
```

您可以使用 `cf buildpacks` 指令來顯示中介軟體元件，例如 WebSphere Liberty 設定檔和 SDK for Node.js，這些可用來作為您應用程式執行所在的運行環境。您也可以使用下列指令為您的應用程式指定運行環境：


```
bluemix app push appName -b buildpackname
```
