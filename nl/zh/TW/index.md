---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 關於 {{site.data.keyword.cfee_full_notm}}
{: #about}

使用 {{site.data.keyword.cfee_full}} (CFEE)，您可以根據需求，將多個隔離的企業級 Cloud Foundry 平台實例化。{{site.data.keyword.Bluemix_notm}} Foundry Enterprise 服務實例會以您自己的帳戶在 {{site.data.keyword.Bluemix_notm}} 中執行。環境部署至隔離的硬體（Kubernetes 叢集）。您可以完全控制環境，包括存取控制、容量管理、變更管理、監視及服務。
{:shortdesc}

{{site.data.keyword.cfee_full}} 目前處於其測試版階段，我們希望能聽到您的意見！若要開始使用，請在 [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) 建立您自己的 {{site.data.keyword.cfee_full}} 實例，並[要求存取](http://ibm.biz/cfee-forum-signup) [IBM CFEE Slack 討論區](https://ibm-cfee.slack.com)來分享您的意見、提問以及與產品團隊接觸。{:tip}

一個成功的專案，需要花時間計劃和設計您需要哪些資源，以及您的企業需求為何。為了協助您開始使用，請考量下列問題：

* 您要開發多少個應用程式？其類型為何？
* 應用程式需要存取哪些服務？
* 誰可以在開發處理程序中分工合作？他們扮演什麼角色？
* 專案的每一個階段所需的隔離程度為何？
* 您的企業是否提供基礎架構資源？
* 貴公司的通訊方式？
* 是否有可以實作的命名標準，以清楚識別組織和空間用途？

在決定您需要哪種類型的雲端環境時，您會計劃帳戶、組織、空間、資源和團隊成員的結構。

對於大部分組織而言，單一 {{site.data.keyword.Bluemix_notm}} 帳戶就已足夠。如果您的組織有多個業務領域，則可以針對每個業務領域建立個別的 {{site.data.keyword.Bluemix_notm}} 帳戶，例如，大型銀行金融公司可能會針對零售和商業部門建立個別的帳戶。

下表提供部分重要元素的摘要。

|元素|說明|
|-----------|---------------|
|IBM Cloud 帳戶|CFEE 實例會建立在特定 IBM Cloud 帳戶下，如此該帳戶中的使用者便可根據針對那些使用者定義的角色及存取原則來使用。|
||用來建立 CFEE 實例的帳戶必須是「隨收隨付制」或「訂閱」帳戶類型（不能是「試用」帳戶）。|
|CFEE|用於管理應用程式的 IBM Cloud Foundry Enterprise Environment 服務。|
||提供於 IBM Cloud 型錄中。|
|CFEE 實例|由 IBM Cloud 帳戶中具有管理者或編輯者角色的使用者，在該帳戶下建立的 IBM Cloud Foundry Enterprise Environment 服務實例。|
||「IBM Cloud 帳戶」中可以有多個 CFEE 實例。|
||可以有一個以上的組織。|
|組織|包含一個以上的空間。|
||包含一個以上的組織管理員。|
||包含一個以上的團隊成員。每一個團隊成員可以被授與一個以上的角色。|
||使用費用（由部署在空間中的應用程式所產生）是在組織層次提報。|
|空間|包含一個以上的資源。|
||包含一個以上的應用程式。|
||包含一個以上的空間管理員。|
||包含一個以上的團隊成員。每一個使用者都必須已經是擁有組織中的團隊成員。每一個團隊成員可以被授與一個以上的角色。|
|團隊成員|可以新增至不同帳戶之間的一個以上組織和空間。|
||可以在相同的組織及/或空間內被賦予多個角色。|
|服務別名|IBM Cloud 中服務實例的別名。|
||可讓開發人員將其 IBM Cloud 帳戶中可用的現有服務實例，連結至部署在 CFEE 內之空間的應用程式。|
{:caption="表 1. 重要元素的說明" caption-side="top"}

## CFEE 及支援服務的佈建目標
{: #provisioning-targets}

以下是 CFEE 服務及相依服務（Kubernetes 服務、Compose for PostgreSQL 及 Cloud Object Storage 服務）可以佈建的地理區域、位置和資料中心。

|  **地理區域** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **CFEE 實例與 Kubernetes 叢集** | **Cloud Object Storage** | **Compose for PostgreSQL（CF 地區）** |
|----------------------------------------|-------------------|-------------------|-------------------|
|北美 |蒙特婁 (mon01) | us-geo | us-east |
|北美 |多倫多 (tor01) | us-geo| us-east |
|北美 | 華盛頓特區 (wdc04) | us-geo | us-east |
|北美 | 華盛頓特區 (wdc06) | us-geo | us-east | 
|北美 | 華盛頓特區 (wdc07) | us-geo | us-east |
|北美 | 達拉斯 (das10) | us-geo | us-south |
|北美 | 達拉斯 (das12) | us-geo | us-south |
|北美 | 達拉斯 (das13) | us-geo |us-south |
|北美 | 聖荷西 (sjc03) | us-geo | us-south |
|北美 | 聖荷西 (sjc04) | us-geo | us-south |
|南美 &nbsp; &nbsp;| 聖保羅 (sao01) |  us-geo | us-south |
|歐洲| 倫敦 (lon02) | eu-geo | eu-gb |
|歐洲| 倫敦 (lon04) | eu-geo | eu-gb |
|歐洲| 倫敦 (lon06) | eu-geo | eu-gb | 
|歐洲| 阿姆斯特丹 (ams03) | eu-geo | eu-de |
|歐洲| 奧斯陸 (osl01) |eu-geo | eu-de | 
|歐洲| 巴黎 (par01) | eu-geo | eu-de |
|歐洲| 法蘭克福 (fra02) | eu-geo | eu-de |
|歐洲| 法蘭克福 (fra04) | eu-geo | eu-de | 
|歐洲| 法蘭克福 (fra05) |  eu-geo | eu-de |
|亞太地區| 墨爾本 (mel01) | ap-geo | au-syd |
|亞太地區| 雪梨 (syd01) | ap-geo | au-syd |
|亞太地區| 雪梨 (syd04) | ap-geo | au-syd | 
|亞太地區| 香港 (hkg02) | ap-geo | au-syd |
|亞太地區| 香港 (seo01) | ap-geo | au-syd |
|亞太地區| 新加坡 (sng01) | ap-geo | au-syd |
|亞太地區| 東京 (gok02) | ap-geo | au-syd |
|亞太地區| 東京 (gok04) | ap-geo | au-syd |
|亞太地區| 東京 (gok05) | ap-geo | au-syd |

{: caption="表 2. CFEE 及支援服務的佈建目標" caption-side="top"}



例如，CFEE 服務可以佈建在歐洲的三個資料中心：阿姆斯特丹（1 個資料中心）、法蘭克福（3 個資料中心）、倫敦（3 個資料中心）、奧斯陸（1 個資料中心）和巴黎（1 個資料中心）。如果 CFEE 佈建在法蘭克福，Cloud Object Storage 服務實例將部署在 _eu-geo_ 地區，而 Compose for PostgreSQL 服務實例將部署在 _eu-de_ 公用 Cloud Foundry 地區。

