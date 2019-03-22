---

copyright:
  years: 2018
lastupdated: "2018-09-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 部署及檢視應用程式
{: #deploy_apps}

您可以使用指令行介面或整合開發環境 (IDE)，以將應用程式部署至 {{site.data.keyword.Bluemix}}。您也可以使用應用程式資訊清單來部署應用程式。當您使用應用程式資訊清單時，可讓您減少每次將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，必須指定的部署詳細資料數量。
{:shortdesc}

## 使用 Cloud Foundry 指令部署應用程式
{: #dep_apps}

[下載並安裝 Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。

在您安裝指令行介面之後，請遵循下列步驟：

1. 切換至您程式碼所在的目錄。`cd <your_directory>`
2. 移至 {{site.data.keyword.cfee_full}}「概觀」頁面，並找到環境的 API 端點。
3. 在指令行介面中，將 API 端點設為您環境的端點：

  ```
  cf api <api_endpoint>
  ```
  {: pre}

4. 登入環境

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  如果您使用聯合 ID，請使用 `-sso` 選項。

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **附註**：如果值包括空格（例如，`-o "my org"`），則您必須新增單引號或雙引號來括住 `username`、`org_name` 及 `space_name`。

5.  從 `<your_new_directory>`，使用 `bluemix app push` 指令，以將應用程式重新部署至 {{site.data.keyword.Bluemix_notm}}。如需 `cf app push` 指令的相關資訊，請參閱[上傳應用程式](/docs/starters/upload_app.html)。

  ```
  cf push <app_name>
  ```
  {: pre}

6.  瀏覽至 `https://<app_url>.<AppDomainName>`，以存取應用程式。

## 在使用者介面中檢視已部署的應用程式
{: #view_apps}

您可以檢視特定空間環境定義內或廣域跨所有 CFEE 實例的 CFEE 已部署應用程式。

### 檢視特定 CFEE 空間中已部署的應用程式
{: #view_specific}

若要檢視特定 CFEE 實例之特定空間中已部署的應用程式，請執行下列動作：
1. 移至 [{{site.data.keyword.Bluemix_notm}} 儀表板](https://console.bluemix.net/dashboard/apps/)，並開啟您要在其中建立組織的 {{site.data.keyword.cfee_full_notm}}。
2. 在 {{site.data.keyword.cfee_full_notm}} 使用者介面中，移至導覽窗格中的**組織**項目，以開啟_組織_ 頁面。
3. 移至頁面頂端的**空間**標籤。
4. 在__空間__標籤中，按一下表格中的某個空間，以開啟該空間的頁面。
5. 在__空間__頁面中，移至**應用程式**標籤。
6. _應用程式_ 標籤顯示該空間中已部署的所有應用程式。您可以選擇存取代表應用程式之列最右側的功能表，以「啟動」、「重新啟動」、「停止」或「刪除」應用程式。

您也可以展開應用程式的列，以檢視應用程式所連結的服務實例。

### 檢視在所有 CFEE 實例中部署的應用程式
{: #view_global}

若要檢視在所有 CFEE 實例中部署的所有應用程式，請執行下列動作：
1. 按一下「功能表」圖示 ![帳戶檢查](img/HamburgerMenu.png "顯示「功能表」圖示的畫面擷取") > **Cloud Foundry**，以開啟 Cloud Foundry 儀表板。
2. 按一下左導覽窗格中的**企業 > 應用程式**。
視圖中的表格會顯示下列資訊：

|元素|說明|
|-----------|---------------|
|名稱|應用程式的名稱。|
|實例|應用程式的實例數。|
|環境|應用程式部署所在的 {{site.data.keyword.cfee_full}} 環境。|
|組織|應用程式部署所在的組織。|
|空間|CFEE 實例中別名所在的組織。|
|記憶體|應用程式所使用的記憶體數量。|
|狀態|應用程式的狀態。|
{:caption="表 1. Cloud Foundry 儀表板應用程式表格中的直欄" caption-side="top"}

您可以選擇存取代表應用程式之列最右側的功能表，以「啟動」、「重新啟動」、「停止」或「刪除」應用程式。您可以在 CFEE 使用者介面中按一下任何應用程式、環境、組織或空間，以導覽至對應的頁面。

在此視圖中，您可以選擇依組織、空間及（或）應用程式名稱將應用程式分組。此功能可讓您將應用程式聯合至單一實體，這些應用程式可能有不同的名稱，以及（或）部署至不同 CFEE 組織或空間，但對應至相同的邏輯應用程式實體。例如，您可能有不同的應用程式代表更廣泛專案的元件，或部署至不同的交付階段（例如開發、測試、正式作業）但想要分組為相同邏輯實體的一部分來進行檢視。

若要將應用程式分組，請移至頁面右上角的**群組**下拉清單。
當您將應用程式分組時，每個產生的群組都會以表格中的單一項目來代表。您可以展開該列，以顯示該群組下的應用程式。

您可以在此視圖中執行下列動作：
* 依顯示為表格直欄的任何內容，排序表格中的項目。
* 存取該列最右側之別名的別名溢位功能表，以將應用程式連結至特定別名。
* 展開別名（列）來查看連結該別名的所有應用程式。
* 存取該列最右側之別名的應用程式溢位功能表，以啟動及停止應用程式。
* 按一下具有對應 CFEE、組織或空間的鏈結，以導覽至 CFEE、CFEE 組織或 CFEE 空間。

## 應用程式資訊清單
{: #appmanifest}

應用程式資訊清單包括套用至 `cf push` 指令的選項。您可以使用應用程式資訊清單，來減少每次將應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，必須指定的部署詳細資料數量。

在應用程式資訊清單中，您可以指定選項，例如要建立的應用程式實例數、要配置的記憶體及磁碟配額數量，以及其他環境變數。您也可以使用應用程式資訊清單，將應用程式部署自動化。資訊清單檔的預設名稱是 `manifest.yml`。

### 資訊清單檔中支援的選項

下表顯示您可以在應用程式資訊清單檔中使用的支援選項。如果您選擇使用 `manifest.yml` 以外的不同檔名，則必須使用 **-f** 選項與 `cf push` 指令搭配。在下列範例中，`appManifest.yml` 是檔名：

```
cf push -f appManifest.yml
```

|選項|說明|用法或範例|
|:----------|:--------------|:---------------|
| **buildpack** |自訂建置套件的 URL 或名稱。| `buildpack:` *buildpack_URL* |
| **disk_quota** |配置給應用程式的磁碟配額。預設值為 1 G。| `disk_quota: 500M` |
| **domain** |{{site.data.keyword.Bluemix_notm}} 中應用程式的網域名稱。| `domain:` ng.bluemix.net |
| **host** |{{site.data.keyword.Bluemix_notm}} 中應用程式的主機名稱。此值在 {{site.data.keyword.Bluemix_notm}} 環境中必須是唯一的值。| `host:` *host_name* |
| **name** |{{site.data.keyword.Bluemix_notm}} 中的應用程式名稱。此值在 {{site.data.keyword.Bluemix_notm}} 環境中必須是唯一的值。| `name:` *appname* |
| **path** |應用程式的位置。此值可以是相對路徑或絕對路徑。| `path:` *path_to_application* |
| **command** |應用程式的自訂啟動指令，或執行 Script 檔的指令。| `command:` *custom_command* `command:` *bash ./run.sh* |
| **memory** |要配置給應用程式的記憶體數量。預設值為 1G。| `memory: 512M` |
| **instances** |要為應用程式建立的實例數。| `instances: 2` |
| **timeout** |用來啟動應用程式的時間量上限（以秒為單位）。預設值是 60 秒。| `timeout: 80` |
| **no-route** |布林值，用以避免在應用程式只是在背景中執行時指派路徑給該應用程式。預設值是 **false**。| `no-route: true` |
| **random-route** |布林值，指派隨機路徑給應用程式。預設值是 **false**。| `random-route: true` |
| **services** |要連結至應用程式的服務。| `services: - mysql_maptest` |
| **env** |應用程式的自訂環境變數。| `env: DEV_ENV: production` |
{: caption="表 2. 資訊清單 YAML 檔案中支援的選項" caption-side="top"}

### 範例 manifest.yml 檔案
{: #sample}

下列範例顯示 Node.js 應用程式的資訊清單檔，該應用程式使用 {{site.data.keyword.Bluemix_notm}} 中的內建社群 Node.js 建置套件。

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
