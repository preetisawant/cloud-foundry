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

# 入門指導教學
{: #getting-started}

{{site.data.keyword.cfee_full}} (CFEE) 是用於在雲端管理應用程式及服務的雲端平台。{{site.data.keyword.cfee_full_notm}} 可讓您隨著使用量成長而輕鬆擴充應用程式，並且簡化運行環境、中介軟體及基礎架構，以著重於開發應用程式。
{: shortdesc}

此入門指導教學顯示如何建立 {{site.data.keyword.cfee_full_notm}}、新增使用者、建立組織和空間、部署應用程式，以及將這些應用程式連結至服務。

**附註：**後續步驟適用於從**標準**方案建立的 CFEE。如果是從 **Eirini 技術預覽**方案建立此 CFEE，請遵循**僅步驟 1 到 6** 及步驟 **11**。_Eirini 技術預覽_ 方案不支援步驟 8 到 11 中所說明的功能。請參閱[開始使用 Eirini 技術預覽](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)。
_Eirini 技術預覽_ 方案容許您使用原生 Kubernetes 作為容器排程器（而非 Diego）來探索 CFEE。Kubernetes 排程器用於 CFEE，以在 Cloud Foundry 應用程式運行環境中部署及執行應用程式、新增使用者、建立組織和空間、部署應用程式，以及將這些應用程式連結至服務。 

## 步驟 1：建立 CFEE 實例
{: #create-environment}

您可以從 {{site.data.keyword.Bluemix_notm}} 型錄建立 {{site.data.keyword.cfee_full_notm}}(CFEE) 實例。建立 CFEE 實例之前，請造訪[建立環境](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment)文件，以取得準備 {{site.data.keyword.Bluemix_notm}} 帳戶的指引來確保正確的許可權，以及建立 CFEE 實例的步驟。


## 步驟 2：建立組織及空間
{: #create-orgsandspaces}

在您建立 {{site.data.keyword.cfee_full_notm}} 之後，請參閱[建立組織及空間](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)，以了解如何建立組織及空間來建構環境的相關資訊。{{site.data.keyword.cfee_full_notm}} 中的應用程式是以特定空間為範圍。空間則是存在於特定組織內。組織的成員會共用配額方案、應用程式、服務實例及自訂網域。

當您建立組織時，請指派其配額。資源的配額集限制（記憶體、CPU 等）適用於該組織。您可於稍後指派不同的配額。每個 CFEE 中都有一組預先配置的配額，但您也可以在 CFEE 使用者介面的**配額**頁面中建立自己的自訂配額。您可以將自訂配額設為_預設_ 配額，方法是從配額的功能表中呼叫_複製成預設值_ 動作，以將自訂配額的值複製成預設配額。

**附註：**_Cloud Foundry 組織_ 頁面可從位於頂端 IBM Cloud 標頭的**_管理 > 帳戶 > Cloud Foundry 組織_** 功能表中取得，它是要專用於公用 IBM Cloud 組織，**而非 CFEE 組織**。CFEE 組織是在 CFEE 實例的_組織_ 頁面中進行管理。開啟 CFEE 使用者介面，然後按一下**_組織_** 頁面以建立及管理該 CFEE 的組織。

## 步驟 3：將使用者新增至組織及空間
{: #add-users}

透過控制存取層次的特定角色指派，[新增使用者](https://console.bluemix.net/docs/cloud-foundry/add-users.html)至這些組織及空間。使用者必須先前已可存取 CFEE 實例，才能新增為 CFEE 中組織及空間的成員。請參閱[許可權](https://console.bluemix.net/docs/cloud-foundry/permissions.html)。

## 步驟 4：部署及檢視應用程式
{: #deploy-apps}

當您準備就緒，就可以使用 {{site.data.keyword.Bluemix_notm}} 指令行介面來[部署應用程式](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html)。在使用者介面中，檢視特定 CFEE 空間的環境定義內或廣域跨所有 CFEE 實例的已部署應用程式清單。您也可以從那些視圖啟動、停止或刪除應用程式。

## 步驟 5：建立或新增 IBM Cloud 服務實例至 CFEE 空間
{: #service-instances}

在 IBM Cloud 帳戶裡[建立服務](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)或[新增現有可用服務](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)。服務實例提供於 CFEE 空間之後，您便可以將它連結至部署在該空間的 CFEE 應用程式。

## 步驟 6：將應用程式連結至服務實例
{: #bind-apps}

[連結應用程式](https://cloud.ibm.com/docs/cloud-foundry/binding.html)至服務實例別名，以使用服務的功能。

在 [Cloud Foundry 儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中，您可以看到所有應用程式及服務的合併視圖，不論是*公用* 還是*企業*。在 Cloud Foundry 儀表板之後，請按一下左導覽窗格的 *Public*，即可看到 IBM Cloud 帳戶中可用的公用應用程式及服務。按一下 *Enterprise* 可以看到所有 CFEE 環境、部署到 CFEE 空間的應用程式，以及 CFEE 空間可用的服務。
{:tip}

## 步驟 7：啟用審核及記載持續性（選用）
{: #enable-auditingandlogging}

啟用環境以便[審核事件](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing)及[記載持續性](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging)。

## 步驟 8：啟用監視工具（選用）
{: #enable-monitoring}

監視工具不會自動佈建在 CFEE 實例 2.2.0 版或更新版本上。CFEE 管理者可以在建立 CFEE 實例之後[啟用監視工具](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)。監視工具集包括 Prometheus、Grafana 及 Alertmanager。

## 步驟 9：建立及保護 Cloud Foundry 網域（選用）
{: #create-domains}

針對 CFEE 中的所有應用程式建立[網域](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains)（共用網域），或是針對特定組織建立網域（專用網域），並使用 SSL 憑證保護它們。

## 步驟 10：配置 Cloud Foundry 建置套件的優先順序
{: #create-buildpacks}

建置套件為 Cloud Foundry 環境中部署的應用程式提供運行環境支援，以自動配置應用程式的運行環境，並處理其相依關係。Cloud Foundry 包括一組適用於一般語言及架構的建置套件。[進一步瞭解](https://docs.cloudfoundry.org/buildpacks/) Cloud Foundry 建置套件。  

您可以在 CFEE 使用者介面的**建置套件**頁面中建立及上傳自訂建置套件。建置套件具有優先順序清單中的序數位置。在應用程式編譯打包期間，Cloud Foundry 會根據建置套件集來檢查應用程式的相容性，從位置 1 開始。相容性檢查會沿著優先順序清單向下繼續進行，直到找到相容的建置套件為止。請確定建置套件集的優先順序序列符合開發團隊的需求。您可以將建置套件名稱拖放到不同的位置，來變更建置套件在優先順序序列中的位置。您也可以透過 [Cloud Foundry CLI](https://docs.cloudfoundry.org/adminguide/buildpacks.html) 來管理建置套件。

## 步驟 11：安裝 Stratos 主控台來管理應用程式（選用）
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
