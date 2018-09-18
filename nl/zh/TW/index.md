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
{: #creating}

使用 {{site.data.keyword.cfee_full}} (CFEE)，您可以根據需求，將多個隔離的企業級 Cloud Foundry 平台實例化。{{site.data.keyword.Bluemix_notm}} Foundry Enterprise 服務實例會以您自己的帳戶在 {{site.data.keyword.Bluemix_notm}} 中執行。環境部署至隔離的硬體（Kubernetes 叢集）。您可以完全控制環境，包括存取控制、容量管理、變更管理、監視及服務。
{:shortdesc}

{{site.data.keyword.cfee_full}} 目前處於其測試版階段，我們希望能聽到您的意見！若要開始使用，請在 [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) 建立您自己的 {{site.data.keyword.cfee_full}} 實例，以及[要求存取](http://ibm.biz/cfee-forum-signup) [IBM CFEE Slack 討論區](https://ibm-cfee.slack.com)來分享您的意見、提問並參與產品團隊。
{:tip}

一個成功的專案，需要花時間計劃和設計您需要哪些資源，以及您的企業需求為何。為了協助您開始使用，請考量下列問題：

* 您要開發多少個應用程式及其類型為何？
* 應用程式需要存取哪些服務？
* 誰可以在開發處理程序中分工合作，及其所扮演的角色為何？
* 專案的每一個階段所需的隔離程度為何？
* 您的企業是否提供基礎架構資源？
* 貴公司的通訊方式？
* 是否有可以實作的命名標準，以清楚識別組織和空間用量？

在決定您需要哪種類型的雲端環境時，就要計劃帳戶、組織、空間、資源和團隊成員的結構。

對於大部分組織而言，單一 {{site.data.keyword.Bluemix_notm}} 帳戶就已足夠。如果您的組織有多個業務領域，則您可以針對每個業務領域建立個別的 {{site.data.keyword.Bluemix_notm}} 帳戶，例如，大型銀行金融公司可能會針對零售和商業部門建立個別的帳戶。

下表提供部分重要元素的摘要。

|元素|說明|
|-----------|---------------|
|IBM Cloud 帳戶|使用特定 IBM Cloud 帳戶建立 CFEE 實例，並根據針對該帳戶中的使用者所定義的角色及存取原則，讓該實例可供這些使用者使用。|
||用來建立 CFEE 實例的帳戶必須是「隨收隨付制」或「訂閱」帳戶類型（不是「試用」帳戶）。|
|CFEE|用於管理應用程式的 IBM Cloud Foundry Enterprise Environment 服務。|
||可在 IBM Cloud 型錄中使用。|
|CFEE 實例|由具有 IBM Cloud 帳戶中管理者或編輯者角色的使用者，以該帳戶建立的 IBM Cloud Foundry Enterprise Environment 服務實例。|
||「IBM Cloud 帳戶」中可能有多個 CFEE 實例。|
||可以有一個以上的組織。|
|組織|包括一個以上的空間。|
||包括一個以上的組織管理員。|
||包括一個以上的團隊成員。每一個團隊成員可以被授與一個以上的角色。|
||使用費用（由部署在空間中的應用程式所產生）是在組織層次提報。|
|空間|包括一個以上的資源。|
||包括一個以上的應用程式。|
||包括一個以上的空間管理員。|
||包括一個以上的團隊成員。每一個使用者都必須已經是擁有組織中的團隊成員。每一個團隊成員可以被授與一個以上的角色。|
|團隊成員|可以新增至不同帳戶的一個以上組織和空間中。|
||可以在相同的組織及/或空間內被賦予多個角色。|
|服務別名|IBM Cloud 中服務實例的別名。|
||可讓開發人員將其 IBM Cloud 帳戶中可用的現有服務實例，連結至其在 CFEE 空間內所部署的應用程式。|
{:caption="表 1. 重要元素的說明" caption-side="top"}

