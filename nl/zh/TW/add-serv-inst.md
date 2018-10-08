---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 使用服務
{: #workingwith-services}

{{site.data.keyword.cfee_full_notm}} 中所部署的應用程式可以連結至兩種類型的服務實例：
1. 從 {{site.data.keyword.Bluemix}} 型錄建立且可在 {{site.data.keyword.Bluemix}} 帳戶中使用的公用服務實例。  
CFEE 環境無法單獨使用 {{site.data.keyword.Bluemix}} 帳戶中可用的公用服務實例。為了讓（{{site.data.keyword.Bluemix}} 帳戶中可用的）公用服務實例變成可用於 CFEE 環境中的空間，必須將它們明確地新增至目標 CFEE 空間。{{site.data.keyword.Bluemix}} 服務實例新增至 CFEE 空間之後，它可以連結至該 CFEE 空間中的應用程式。本可讓開發人員在 CFEE 環境所部署的應用程式中，利用大量 {{site.data.keyword.Bluemix}} 服務的型錄，同時容許對那些 {{site.data.keyword.Bluemix}} 服務的存取控制。

   除了將現有 {{site.data.keyword.Bluemix}} 服務實例新增至 CFEE 空間，您也可以從 CFEE 空間內建立新的 {{site.data.keyword.Bluemix}} 服務實例，這樣也會自動將它新增至該 CFEE 空間。

2. 本端 Cloud Foundry 服務分配管理系統所管理的服務實例（在 CFEE 本端）。這些接著可以有兩種類型：
   *  2a. 從現行 {{site.data.keyword.cfee_full_notm}} 實例之 Cloud Foundry Marketplace 中建立的服務供應項目實例。此類型的服務實例需要環境中有已登錄的服務分配管理系統可用。服務分配管理系統會顯示服務供應項目及方案的型錄，並且可以從這些服務供應項目建立、移除、連結及取消連結實例。如需相關資訊，請參閱 Cloud Foundry 文件中的 [Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html)。
   * 2b. 使用者提供的服務實例。支援透過 CLI 來進行此類型的建立作業，但不支援透過使用者介面進行。儘管如此，使用者提供的服務實例將會列在使用者介面中。
   

## 檢視所有 CFEE 環境中的 {{site.data.keyword.Bluemix_notm}} 服務實例
{: #viewing-services_across}

移至 [Cloud Foundry 服務儀表板](https://console.bluemix.net/dashboard/cloudfoundry/services)，以查看 {{site.data.keyword.Bluemix_notm}} 帳戶中（您有存取權的）所有 {{site.data.keyword.Bluemix_notm}} 服務實例的合併視圖，並查看哪些服務實例已新增到哪些 CFEE 空間。

此視圖顯示帳戶中可用的所有 {{site.data.keyword.Bluemix_notm}} 服務實例，並指出哪些服務實例已新增（建立別名）到哪些 CFEE 空間。展開服務實例即可顯示它已新增到的 CFEE 空間。您可以進一步展開它們以查看服務實例連結的那些 CFEE 空間裡的應用程式。  

從這個視圖，您也可以連結部署到已新增那些服務實例之 CFEE 空間的應用程式。移至位於相對應服務（可用於特定 CFEE 空間）之表格列最右邊的功能表，然後選取**連結至應用程式**。

## 將現有 {{site.data.keyword.Bluemix_notm}} 服務實例新增至 CFEE 空間
{: #adding-services_inspace}

您可以將 {{site.data.keyword.Bluemix_notm}} 服務實例連結至部署到 CFEE 空間中的應用程式。IBM Cloud 服務實例必須要先新增至應用程式部署所在的 CFEE 空間，才能夠連結至部署在 CFEE 中的應用程式。必須先完成下列各項，您才能將 {{site.data.keyword.Bluemix_notm}} 服務實例新增至 CFEE 空間：
* {{site.data.keyword.Bluemix_notm}} 服務必須提供在 CFEE 實例所在的同一個 {{site.data.keyword.Bluemix_notm}} 帳戶。
* 您必須具有 {{site.data.keyword.Bluemix_notm}} 服務實例本身的存取權。如需相關資訊，請參閱 {{site.data.keyword.Bluemix_notm}} 標頭的**管理 > 使用者**功能表下的「身分及存取」頁面，以檢查現行帳戶存取原則。

若要將現有的 {{site.data.keyword.Bluemix_notm}} 服務實例新增至 CFEE 空間：
1. 移至 [Cloud Foundry 服務儀表板](https://console.bluemix.net/dashboard/cloudfoundry/services)。  
2. 從清單找到 {{site.data.keyword.Bluemix_notm}} 服務實例，並呼叫相對應表格列最右邊的功能表。
3. 選取**新增服務**。
4. 在_新增服務_ 對話框中，選取您要新增服務的 CFEE、組織及空間，然後按一下**新增**。
5. 展開目標 {{site.data.keyword.Bluemix_notm}} 服務，以尋找服務新增到的新 CFEE。


或者，您可以從您要新增 {{site.data.keyword.Bluemix_notm}} 服務實例的 CFEE 空間內新增它：
1. 在 {{site.data.keyword.Bluemix_notm}} [儀表板](https://console.bluemix.net/dashboard)或 [Cloud Foundry 服務儀表板](https://console.bluemix.net/dashboard/cloudfoundry/services)中，尋找管理您應用程式的 Cloud Foundry Enterprise Environment。
2. 在導覽窗格中移至**組織**，然後開啟應用程式所在的組織及空間。
3. 移至**空間**標籤，並找出包含應用程式的空間。
4. 在目標空間頁面中，移至**服務**標籤，然後按一下**新增服務**。這會開啟__新增服務__對話框。頁面會列出 {{site.data.keyword.Bluemix_notm}} 帳戶中可用的服務實例。
5. 尋找並選取您要新增至 CFEE 空間的可用服務實例。 
6. 服務實例將會新增至 CFEE 空間中可用的服務清單。

   **附註：**當您將 {{site.data.keyword.Bluemix_notm}} 服務新增至 CFEE 空間時，會在該空間裡建立該服務實例的別名。當您從 CFEE 空間**移除**服務實例（從位於表格中相對應服務實例列最右邊的功能表）時，並不會從公用帳戶刪除服務。此動作只會從特定的 CFEE 帳戶移除它，且再也無法連結至該 CFEE 空間中的應用程式。此外，當您從 {{site.data.keyword.Bluemix_notm}} 帳戶刪除服務實例本身時，任何 CFEE 空間便無法再使用該服務。 

## 從 CFEE 空間使用者介面建立 {{site.data.keyword.Bluemix_notm}} 服務實例
{: #creating-services_inspace}
您可以從 CFEE 空間內建立 {{site.data.keyword.Bluemix_notm}} 服務實例。建立 {{site.data.keyword.Bluemix_notm}} 服務實例會導致下列幾點：
* 在 IBM Cloud 中建立 {{site.data.keyword.Bluemix_notm}} 服務實例。這相等於從 {{site.data.keyword.Bluemix_notm}} [型錄](https://console.bluemix.net/catalog)建立服務實例。
* {{site.data.keyword.Bluemix_notm}} 服務實例會新增（建立別名）至當初起始建立動作所在的 CFEE 空間。


若要從 CFEE 空間內建立服務實例，請執行下列動作：
1. 在目標空間頁面中，移至**服務**標籤，然後按一下**建立服務**。這會開啟 {{site.data.keyword.cfee_full_notm}} 的 **Marketplace** 視圖。此視圖列出來自兩個來源的服務供應項目（請參閱__來源__ 直欄）：
   * {{site.data.keyword.Bluemix_notm}} 型錄中的供應項目。
   * 本端 {{site.data.keyword.cfee_full_notm}} Marketplace 中的供應項目。
5. 尋找並選取您要實例化的可用服務供應項目。 
6. 根據服務供應項目的來源（IBM Cloud 型錄或本端 CFEE Marketplace），繼續下列其中一項：
   * 如果選取的服務供應項目是 {{site.data.keyword.Bluemix_notm}} 型錄供應項目，您將會看到有一個**繼續**到 IBM Cloud 服務供應項目建立頁面的按鈕。這是可從 {{site.data.keyword.Bluemix_notm}} 型錄取得的同一頁面。在此頁面中，您會提供在 IBM Cloud 中建立服務所需之新服務實例名稱、地區和方案以及其他內容。建立服務實例之後，即會在 IBM Cloud 中建立服務實例並自動新增至現行 CFEE 空間。
   * 如果選取的服務供應項目來自本端 CFEE 型錄，您將會看到有一個**建立**服務實例的按鈕。系統會提示您輸入現行 CFEE 中的組織及空間，服務實例將會建立在其中。

## 使用 CLI 從 CFEE 空間建立 {{site.data.keyword.Bluemix_notm}} 服務實例
{: #creating-services_cli}

您可以從 CLI 在 CFEE 的空間建立服務實例。從 CLI 在 CFEE 空間建立服務，相等於從使用者介面在該空間建立。亦即，建立服務有下列雙重結果：
* 在 IBM Cloud 中建立 {{site.data.keyword.Bluemix_notm}} 服務實例。這相等於從 {{site.data.keyword.Bluemix_notm}} [型錄](https://console.bluemix.net/catalog)建立服務實例。
* {{site.data.keyword.Bluemix_notm}} 服務實例會新增（建立別名）至當初起始建立動作所在的 CFEE 空間。

從 CFEE 空間建立服務實例，與從 CLI 建立它，兩者的差異在於所建立之服務實例的生命週期。當您在 CFEE 空間使用者介面中建立服務實例時，所建立之服務實例的生命週期是在 {{site.data.keyword.Bluemix_notm}} 帳戶中從服務實例本身控制。這表示對於服務方案的更新是從 {{site.data.keyword.Bluemix_notm}} 帳戶中的實例控制，而不是從 CFEE 空間。或者，如果服務實例是從 CLI 建立，服務的生命週期會從 CFEE 空間控制（服務是從 CFEE 空間更新）。

從 CLI 建立的服務實例也會顯示在使用者介面中，並且在服務實例名稱旁以 ` * ` 表示。

若要使用 CLI 建立服務實例，請遵循下列步驟：

1. 下載並安裝 {{site.data.keyword.Bluemix}} 指令行介面（如果尚未完成的話）。[下載 Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。

2. 移至 {{site.data.keyword.cfee_full}}「概觀」頁面，並找到環境的 API 端點。

3. 在指令行介面中，將 API 端點設為您 CFEE 環境的端點：

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. 登入 CFEE 環境：

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  如果您使用聯合 ID，請使用 `-sso` 選項：

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. 建立服務：
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  （選用）您可以提供一個檔案，將參數包含在有效的必要 JSON 物件中，以便建立特定服務。參數檔的路徑可以是檔案的絕對路徑或相對路徑：
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  以下是有效 JSON 物件的範例：
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   如需從 CLI 建立服務的說明，請發出下列指令：
  
  ```
  cf cs -help
  ```
  如需相關資訊，請參閱 Cloud Foundry 文件中的 [Managing Service Instances with the cf CLI](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
  
## 將服務連結至應用程式
{: #bind_services}

您可以將服務實例連結至部署在 CFEE 中的應用程式，不論是從 [Cloud Foundry 服務儀表板](https://console.bluemix.net/dashboard/cloudfoundry/services)還是從 CFEE 空間頁面的「服務」標籤。  

若要從 [Cloud Foundry 服務儀表板](https://console.bluemix.net/dashboard/cloudfoundry/services)，將服務實例連結至應用程式，請執行下列動作：
1. 移至 [Cloud Foundry 服務儀表板](https://console.bluemix.net/dashboard/cloudfoundry/services)，以查看 {{site.data.keyword.Bluemix_notm}} 帳戶中您可用的所有 {{site.data.keyword.Bluemix_notm}} 服務實例的合併視圖。視圖預期也會顯示哪些 {{site.data.keyword.Bluemix_notm}} 服務實例可用於（已建立別名至）哪些 CFEE 空間。您可以展開服務實例，以顯示它已新增到的 CFEE 空間。您可以進一步展開它們以查看服務實例連結的那些 CFEE 空間裡的應用程式。 
2. 找到您要連結的 {{site.data.keyword.Bluemix_notm}} 服務實例。
3. 展開相對應的視圖，以查看服務實例新增到的所有 CFEE 空間。如果該服務實例尚未新增至應用程式部署所在的 CFEE 空間，請從該列最右邊的功能表選取**新增**，讓服務實例可用於目標 CFEE 空間內。
4. 移至位於對應至可使用服務實例之 CFEE/空間的那列最右邊的功能表，然後選取**連結應用程式**。
5. 在__連結應用程式__對話框中，選取您要連結的應用程式。
6. 應用程式現在會連結至應用程式部署所在 CFEE 空間中的服務實例。您可以展開表格中的對應列，以查看 CFEE 空間中的已連結應用程式。


若要從 CFEE 空間的__服務__頁面，將應用程式連結至服務實例，請執行下列動作：

1. 開啟應用程式部署所在的 CFEE 使用者介面。
2. 在左導覽窗格中移至**組織**，然後開啟應用程式部署所在的組織及空間。
3. 移至**空間**標籤，並找出包含應用程式的空間。
4. 在目標空間頁面中，移至**服務**標籤。
5. 在**服務實例**的表格中，移至對應至您要連結之服務實例的那列最右側的__動作__功能表，然後選取**連結**。
6. 選取您要連結至服務實例的應用程式。

若要取消應用程式與服務實例的連結，請執行下列動作：

1. 在空間的**服務**標籤中，展開目標服務實例，以顯示與其連結的應用程式。
2. 移至應用程式列中的「動作」功能表，然後選取**取消連結服務**。

請參閱 Cloud Foundry 文件中的[連結服務實例](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")，以取得使用 CLI 連結應用程式的相關資訊。


