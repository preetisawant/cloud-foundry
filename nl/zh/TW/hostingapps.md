---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 在 {{site.data.keyword.Bluemix_notm}} 中管理應用程式
{: #hosting_apps}

使用 {{site.data.keyword.Bluemix}}，您可以建立應用程式，以及管理現有應用程式。只要應用程式具有雲端功能，就可以將應用程式移至 {{site.data.keyword.Bluemix_notm}}。{{site.data.keyword.Bluemix_notm}} 提供許多讓您執行應用程式的方法，例如，Cloud Foundry、IBM Containers 及 Virtual Machines。

## 使應用程式具有雲端功能
{: #cloud-readyapps}

如果在應用程式中觀察到下列所有原則，即表示應用程式具有雲端功能，而且可以移轉至 {{site.data.keyword.Bluemix_notm}}。如果應用程式違反原則，您通常可以[修改應用程式](../apps/cloud-ready.html)來遵守原則。

## 移轉應用程式
{: #ht_hostapp}

您可以漸進式地將應用程式移轉至 {{site.data.keyword.Bluemix_notm}}，而不要將應用程式全面轉移至雲端環境。您可以先移轉應用程式的某個部分，並使用 Cloud Integration 服務以連接至現有資料或記錄系統。

在您的雲端應用程式中，您可能需要存取後端資料或服務（例如，記錄系統）。在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用 Secure Gateway 服務以在 {{site.data.keyword.Bluemix_notm}} 組織與企業後端網路之間建立安全通道。服務可讓 {{site.data.keyword.Bluemix_notm}} 上的應用程式存取後端網路的資料及服務。如需詳細資料，請參閱[透過主控台使用 {{site.data.keyword.Bluemix_notm}} Secure Gateway 來連接企業後端 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}。

若要將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 以作為 Cloud Foundry 應用程式，請從 {{site.data.keyword.Bluemix_notm}} 型錄中選取運行環境。此運行環境包含入門範本 Hello World 應用程式，您可以將它取代為自己的應用程式。如果您找不到提供您想要之運行環境的入門範本，則可以使用 -b 選項與 cf push 指令搭配，將自訂 Cloud Foundry 相容建置套件帶到 {{site.data.keyword.Bluemix_notm}}。如需詳細資料，請參閱[使用社群建置套件](byob.html)。

您可以使用 {{site.data.keyword.Bluemix_notm}} 所提供的下列工具及服務：

| 工具| 方法|
|:------|:--------|
| Cloud Foundry 指令行介面 (cf cli)| 在本端用戶端上管理您的程式碼，並且使用 Cloud Foundry 指令行介面，手動將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。如需相關資訊，請參閱[上傳應用程式](../starters/upload_app.html)。|
| Eclipse| 在 Eclipse 中管理您的程式碼，並且使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 來推送應用程式。|
| Git 整合| 在 GitHub 上管理程式碼，並且 將 Git 整合至 {{site.data.keyword.Bluemix_notm}}。您可以與其他開發人員分工合作。確定程式碼中的變更時，會自動將您的應用程式部署至 {{site.data.keyword.Bluemix_notm}}。您不需要手動推送應用程式。|
| {{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline | 在 DevOps GitHub 儲存庫上管理程式碼，並且使用 DevOps Delivery Pipeline 將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。|
{: caption="表 1. {{site.data.keyword.Bluemix_notm}} 工具" caption-side="top"}

如果 Cloud Foundry 平台不支援您的應用程式需求，您可以使用容器或 VM，在其中利用其他自訂的選項來設定、配置及維護運行環境。

## 在 Continuous Delivery 中使用工具鏈開發及部署應用程式
{:ht_cd}

將[工具鏈新增至應用程式](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app)，然後使用 [Continuous Delivery 工具鏈使用者介面](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using)來開發及部署應用程式。

## 使用 cf cli 上傳應用程式
{: #ht_cfcli}

您可以在本端用戶端上管理您的程式碼，並且使用 Cloud Foundry 指令行介面，手動將應用程式上傳至 {{site.data.keyword.Bluemix_notm}}。如果您變更程式碼，則必須重新將應用程式推送至 {{site.data.keyword.Bluemix_notm}}，以執行更新過的程式碼。

請採取下列步驟來移轉應用程式：

安裝 Cloud Foundry 指令行介面。請確定使用最新版本的 cf 指令行介面。
  1. 下載適用於您作業系統的安裝程式。
  2. 遵循工具精靈以安裝指令行。
  3. 使用下列指令來驗證 cf 指令行介面的版本：`cf -v`

選用項目：如果您要先指定並儲存部署詳細資料，再將應用程式推送至 {{site.data.keyword.Bluemix_notm}}，則可以採取下列步驟來新增應用程式資訊清單：

  1. 移至應用程式的工作目錄，並建立標題為 manifest.yml（此為預設名稱）的檔案。</li>
  2. 在資訊清單檔中，指定部署詳細資料。下列範例顯示 Java™ 應用程式的資訊清單檔。

  ```
  applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

如需可在此檔案中使用之受支援選項的相關資訊，請參閱[應用程式資訊清單](depapps.html#appmanifest)。



### 推送應用程式

您可以使用 `cf push` 指令來上傳應用程式。
  1. 執行下列指令，以連接並登入 {{site.data.keyword.Bluemix_notm}}。請在提示時選取您的組織及空間。
  ```
  cf login -a https://api.ng.bluemix.net
  ```
  如果您的組織使用「單一登入」，請新增 `-sso` 旗標。



  2. 從您的應用程式目錄，輸入 cf push 指令與應用程式名稱。應用程式名稱在 {{site.data.keyword.Bluemix_notm}} 環境中必須是唯一的。

  ```
  cf push appname
  ```

  3. 選用項目：如果您使用外部建置套件，則必須使用 -b 選項與 cf push 指令搭配。例如：

  ```
  cf push appname -b buildpack_URL
  ```

  如需詳細資料，請參閱[使用社群建置套件](byob.html)。



選用項目：如果您變更應用程式，則必須重新輸入 `cf push` 指令來上傳那些變更。cf 指令行介面會使用您先前的選項以及對提示的回應，以新的程式碼片段來更新應用程式的任何執行中實例。

#### 附註：

* 使用 cf push 指令時，cf 指令行介面會將所有檔案及目錄從現行目錄複製到 {{site.data.keyword.Bluemix_notm}}。確定應用程式目錄中只有所需的檔案。
* 確定您的組織有足夠的記憶體可供應用程式的所有實例使用。若要檢視您組織的記憶體配額，請使用 cf org org_name。
* 如需 cf push 的相關資訊，請參閱 [cf 指令](../cli/reference/cfcommands/index.html)。

## 移轉資料及使用服務
{: #ht_service}

將應用程式上傳至 {{site.data.keyword.Bluemix_notm}} 之後，請從 {{site.data.keyword.Bluemix_notm}} 型錄中選取您應用程式所連接的服務、建立服務實例、將實例連結至應用程式，然後重新啟動應用程式。

您應用程式的 VCAP_SERVICES 環境變數是 JSON 物件，而此物件包含如何與 {{site.data.keyword.Bluemix_notm}} 中的服務實例互動的相關資訊。此資訊包括服務實例名稱、認證，以及與服務實例的連線 URL。

若要在 {{site.data.keyword.Bluemix_notm}} 中執行程式碼，您必須新增程式碼邏輯，以剖析 VCAP_SERVICES 變數來取得服務連線的相關資訊。請修改應用程式，以透過環境變數來取得服務實例的動態指派主機及埠。下列範例顯示如何在 Ruby 應用程式中取得 Postgre SQL 服務實例的認證：

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

若要確定在修改 {{site.data.keyword.Bluemix_notm}} 的應用程式之後可以在本端環境中執行您的應用程式，請檢查 VCAP_SERVICES 環境變數是否存在（此環境變數是針對所有 {{site.data.keyword.Bluemix_notm}} Cloud Foundry 應用程式所設定）。


# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [Virtual Machines](/docs/virtualmachines/vm_index.html)
* [開始使用 Delivery Pipeline](/docs/services/DeliveryPipeline/index.html)
* [使用 IBM Eclipse Tools for Bluemix 來部署應用程式](/docs/manageapps/eclipsetools/eclipsetools.html)
* [The Twelve-Factor App ![外部鏈結圖示](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console ![外部鏈結圖示](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
