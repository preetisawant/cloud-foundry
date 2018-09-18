---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 建立及檢視服務實例
{: #creating-services}

{{site.data.keyword.cfee_full_notm}} 中所部署的應用程式可以連結至兩種類型的服務實例：
1. 本端 Cloud Foundry 服務分配管理系統所管理的服務實例（在 CFEE 本端）。這些接著可以有兩種類型：
   *  1a. 從現行 {{site.data.keyword.cfee_full_notm}} 實例之 Cloud Foundry 市場中建立的服務供應項目實例。這類型的服務實例需要環境中具有已登錄的服務分配管理系統。服務分配管理系統會顯示服務供應項目及方案的型錄，以及可從這些服務供應項目建立、移除、連結及取消連結實例。如需相關資訊，請參閱 Cloud Foundry 文件中的[管理服務分配管理系統](https://docs.cloudfoundry.org/services/managing-service-brokers.html)。
   * 1b. 使用者提供的服務實例。支援透過 CLI 來建立此類型，但不支援透過使用者介面。但是，使用者提供的服務實例將會列在使用者介面中。
2. 從 {{site.data.keyword.Bluemix}} 型錄建立且可在 {{site.data.keyword.Bluemix}} 帳戶中使用的公用服務實例。
CFEE 環境無法使用可在 {{site.data.keyword.Bluemix}} 帳戶中使用的公用服務實例，而公用服務實例也不能使用它們自己。為了讓公用服務實例（可在 {{site.data.keyword.Bluemix}} 帳戶中使用）變成可用於 CFEE 環境中的空間，必須在目標 CFEE 空間中建立服務實例的別名。別名作為實際公用服務實例的參照。在 CFEE 空間中建立服務別名之後，即可連結至該 CFEE 中的應用程式。服務別名可讓開發人員在 CFEE 環境所部署的應用程式中利用大量 {{site.data.keyword.Bluemix}} 服務型錄。


## 在 CFEE 空間中建立及檢視服務別名
{: #creating-services_inspace}

IBM Cloud 帳戶中可用的現有公用服務實例別名，可讓您將該服務實例連結至 CFEE 空間中所部署的應用程式。建立現有 {{site.data.keyword.Bluemix_notm}} 服務實例的別名，需要使用者存取實例本身。如需相關資訊，請參閱 {{site.data.keyword.Bluemix_notm}} 標頭的**管理 > 使用者**功能表下的「身分及存取」頁面，以檢查現行帳戶存取原則。

若要在 CFEE 的空間內建立服務實例別名，請執行下列動作：

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中，尋找可管理應用程式的 Cloud Foundry Enterprise Environment。
2. 在導覽窗格中移至**組織**，然後開啟應用程式所在的組織及空間。
3. 移至**空間**標籤，並找出包含應用程式的空間。
4. 在目標空間頁面中，移至**服務**標籤，然後按一下**建立服務**。這會開啟 {{site.data.keyword.cfee_full_notm}} 的**型錄**頁面。此頁面列出來自兩個來源的服務供應項目（請參閱_來源_ 直欄）：
   * IBM Cloud 型錄中的供應項目。
   * 本端 {{site.data.keyword.cfee_full_notm}} 市場中的供應項目。
5. 尋找並選取您要實例化的可用服務供應項目。
6. 根據服務供應項目的來源（IBM Cloud 或本端 CFEE），繼續下列其中一項：
   * **繼續**至 IBM Cloud 服務供應項目建立頁面，以提供在 IBM Cloud 中建立服務所需之新服務實例、地區和方案的名稱以及其他內容。按一下*建立* 之後，即會在 IBM Cloud 中建立服務實例。此外，也會在 {{site.data.keyword.cfee_full_notm}} 中建立該服務實例的別名。別名將可用於與 {{site.data.keyword.cfee_full_notm}} 中的應用程式連結。
   **附註：**以此形式建立 {{site.data.keyword.Bluemix_notm}} 時，除了建立可供 IBM Cloud 帳戶使用者使用的公用實例之外，還會在用來建立它的 {{site.data.keyword.cfee_full_notm}} 中建立該服務實例的別名。
   * 在本端 Cloud Foundry 市場中，**建立**服務實例。這樣會開啟一個對話框，供您提供新服務實例及方案的名稱。按一下*建立* 之後，會在 {{site.data.keyword.cfee_full_notm}} 中建立服務實例，並可用於與 {{site.data.keyword.cfee_full_notm}} 中的應用程式連結。

建立服務實例之後，即會在**服務**標籤下列出服務實例（如果已在本端 Cloud Foundry 市場中予以建立）或別名（如果已從 IBM Cloud 型錄建立服務實例）。


## 在廣域 Cloud Foundry 儀表板中建立及檢視所有 CFEE 環境中的服務別名
{: #creating-services_across}

您可以在廣域 Cloud Foundry 儀表板中查看所有服務實例別名（在所有 CFEE 實例中）的合併視圖。

1. 按一下「功能表」圖示 ![帳戶檢查](img/HamburgerMenu.png "顯示「功能表」圖示的畫面擷取") > **Cloud Foundry**，以開啟 Cloud Foundry 儀表板。
2. 按一下左導覽窗格中的**企業 > 服務**。
視圖中的表格會顯示下列資訊：

|元素|說明|
|-----------|---------------|
|服務別名|服務實例別名的名稱。|
|服務實例|從中建立別名的公用 IBM Cloud 服務實例。|
|供應項目|IBM Cloud 型錄中從中建立服務實例的服務供應項目。|
|CFEE|別名所在的 {{site.data.keyword.cfee_full}}。|
|組織|CFEE 實例中別名所在的組織。|
|空間|CFEE 實例中組織內別名所在的空間。|
{:caption="表 1. 重要元素的說明" caption-side="top"}

您可以在此視圖中執行下列動作：
* 依顯示為表格直欄的任何內容，排序表格中的項目。
* 存取該列最右側之別名的別名溢位功能表，以將應用程式連結至特定別名。
* 展開別名（列）來查看連結該別名的所有應用程式。
* 存取該列最右側之別名的應用程式溢位功能表，以啟動及停止應用程式。
* 按一下具有對應 CFEE、組織或空間的鏈結，以導覽至 CFEE、CFEE 組織或 CFEE 空間。

若要從廣域 Cloud Foundry 儀表板建立服務別名，請執行下列動作：
1. 按一下頁面頂端的**建立服務別名**按鈕。這會開啟_建立服務別名_ 對話框。此對話框會列出現行 IBM Cloud 帳戶中可用的所有公用服務實例。
2. 選取其中一個公用服務實例。
3. 按一下**建立**。建立之後，即會將新的服務實例別名新增至清單中。
服務別名也會出現在 CFEE 空間的服務清單中，而在此空間中，可以將它連結至該空間中的應用程式（CFEE >「組織」>「空間」>「服務」）。


