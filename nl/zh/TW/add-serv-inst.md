---

copyright:
  years: 2018
lastupdated: "2019-04-03"

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
CFEE 環境無法單獨自動使用 {{site.data.keyword.Bluemix}} 帳戶中可用的公用服務實例。為了讓（{{site.data.keyword.Bluemix}} 帳戶中可用的）公用服務實例變成可用於 CFEE 環境中的空間，必須將它們明確地新增至目標 CFEE 空間。當您透過 CFEE 的使用者介面將公用服務實例_新增_ 至 CFEE 時，會將公用服務實例的別名放在 CFEE 中。{{site.data.keyword.Bluemix}} 服務實例新增（建立別名）至 CFEE 空間之後，它就可以連結至該 CFEE 空間中的應用程式。本可讓開發人員在 CFEE 環境所部署的應用程式中，利用大量 {{site.data.keyword.Bluemix}} 服務的型錄，同時容許對那些 {{site.data.keyword.Bluemix}} 服務的存取控制。

   除了將現有 {{site.data.keyword.Bluemix}} 服務實例新增至 CFEE 空間，您也可以從 CFEE 空間內建立新的 {{site.data.keyword.Bluemix}} 服務實例，這樣也會自動將它新增至該 CFEE 空間。
  
2. 本端 Cloud Foundry 服務分配管理系統所管理的服務實例（在 CFEE 本端）。這些接著可以有兩種類型：
   *  2a. 從現行 {{site.data.keyword.cfee_full_notm}} 實例之 Cloud Foundry Marketplace 中建立的服務供應項目實例。此類型的服務實例需要環境中有已登錄的服務分配管理系統可用。服務分配管理系統會顯示服務供應項目及方案的型錄，並且可以從這些服務供應項目建立、移除、連結及取消連結實例。如需相關資訊，請參閱 Cloud Foundry 文件中的 [Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html)。
   * 2b. 使用者提供的服務實例。支援透過「指令行介面 (CLI)」來進行此類型的建立作業，但不支援透過使用者介面進行。儘管如此，使用者提供的服務實例將會列在使用者介面中。
   
您也可以從 CFEE 的使用者介面或使用 CLI，從 CFEE 空間建立服務實例（請參閱下列各節）。使用此指令從 CFEE 建立服務實例，具有雙重結果：
* 在公用 {{site.data.keyword.Bluemix}} 中建立服務實例。
* 在從中建立服務實例的 CFEE 空間內，建立該公用服務實例的別名。
    
下列各節說明如何利用使用者介面及 Cloud Foundry CLI 來新增、建立、控制存取及連結服務實例。
   

## 檢視所有 CFEE 環境中的 {{site.data.keyword.Bluemix_notm}} 服務實例
{: #viewing-services_across}

移至 [Cloud Foundry 服務儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/services)，以查看 {{site.data.keyword.Bluemix_notm}} 帳戶中（您有存取權的）所有 {{site.data.keyword.Bluemix_notm}} 服務實例的合併視圖，並查看哪些服務實例已新增到哪些 CFEE 空間。

此視圖顯示帳戶中可用的所有 {{site.data.keyword.Bluemix_notm}} 服務實例，並指出哪些服務實例已新增（建立別名）到哪些 CFEE 空間。展開服務實例即可顯示它已新增到的 CFEE 空間。您可以進一步展開它們以查看服務實例連結的那些 CFEE 空間裡的應用程式。  

從此視圖中，您也可以連結部署到已新增那些服務實例之 CFEE 空間的應用程式。移至位於相對應服務（可用於特定 CFEE 空間）之表格列最右邊的功能表，然後選取**連結至應用程式**。

## 將現有 {{site.data.keyword.Bluemix_notm}} 服務實例新增至 CFEE 空間
{: #adding-services-inspace}

您可以將 {{site.data.keyword.Bluemix_notm}} 服務實例連結至部署到 CFEE 空間中的應用程式。IBM Cloud 服務實例必須要先新增至應用程式部署所在的 CFEE 空間，才能夠連結至部署在 CFEE 中的應用程式。必須先完成下列各項，您才能將 {{site.data.keyword.Bluemix_notm}} 服務實例新增至 CFEE 空間：
* 要新增其實例的服務不能是 Cloud Foundry 服務。只有支援資源群組及 IAM 的 {{site.data.keyword.Bluemix_notm}} 服務才能新增（建立別名）至 CFEE。實例化進入公用 Cloud Foundry 組織、空間及角色的服務無法新增（建立別名）至 CFEE。{{site.data.keyword.Bluemix_notm}} 服務正在逐步利用資源群組的好處。服務移至使用資源群組取代 Cloud Foundry 組織及空間之後，您可以將任何先前已存在的該服務實例移轉至資源群組，那時便可以新增至 CFEE。請參閱[將 Cloud Foundry 服務實例移轉至資源群組](https://cloud.ibm.com/docs/resources/instance_migration.html#migrate)。
* {{site.data.keyword.Bluemix_notm}} 服務必須提供在 CFEE 實例所在的同一個 {{site.data.keyword.Bluemix_notm}} 帳戶。
* 您必須具有 {{site.data.keyword.Bluemix_notm}} 服務實例本身的_操作員_ 平台角色（或更高角色）。如需相關資訊，請參閱 {{site.data.keyword.Bluemix_notm}} 標頭的**管理 > 使用者**功能表下的「身分及存取」頁面，以檢查現行帳戶存取原則。

若要將現有的 {{site.data.keyword.Bluemix_notm}} 服務實例新增至 CFEE 空間：
1. 移至 [Cloud Foundry 服務儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/services)。  
2. 從清單找到 {{site.data.keyword.Bluemix_notm}} 服務實例，並呼叫相對應表格列最右邊的功能表。
3. 選取**新增服務**。
4. 在_新增服務_ 對話框中，選取您要新增服務的 CFEE、組織及空間，然後按一下**新增**。
5. 展開目標 {{site.data.keyword.Bluemix_notm}} 服務，以尋找服務新增到的新 CFEE。


或者，您可以從您要新增 {{site.data.keyword.Bluemix_notm}} 服務實例的 CFEE 空間內新增它：
1. 在 {{site.data.keyword.Bluemix_notm}} [儀表板](https://cloud.ibm.com/dashboard)或 [Cloud Foundry 服務儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/services)中，尋找管理您應用程式的 Cloud Foundry Enterprise Environment。
2. 在導覽窗格中移至**組織**，然後開啟應用程式所在的組織及空間。
3. 移至**空間**標籤，並找出包含應用程式的空間。
4. 在目標空間頁面中，移至**服務**標籤，然後按一下**新增服務**。這會開啟__新增服務__對話框。頁面會列出 {{site.data.keyword.Bluemix_notm}} 帳戶中可用的服務實例。
5. 尋找並選取您要新增至 CFEE 空間的可用服務實例。 
6. 服務實例將會新增至 CFEE 空間中可用的服務清單。

   **附註：**當您將 {{site.data.keyword.Bluemix_notm}} 服務新增至 CFEE 空間時，會在該空間裡建立該服務實例的別名。當您從 CFEE 空間**移除**服務實例（從位於表格中相對應服務實例列最右邊的功能表）時，並不會從公用帳戶刪除服務。此動作只會從特定的 CFEE 帳戶中將它移除，且無法再連結至該 CFEE 空間中的應用程式。此外，當您從 {{site.data.keyword.Bluemix_notm}} 帳戶刪除服務實例本身時，任何 CFEE 空間便無法再使用該服務。 

## 從 CFEE 空間的使用者介面建立 {{site.data.keyword.Bluemix_notm}} 服務實例
{: #creating-services-inspace}

您可以從 CFEE 空間內建立 {{site.data.keyword.Bluemix_notm}} 服務實例。建立 {{site.data.keyword.Bluemix_notm}} 服務實例會導致下列幾點：
* 在 IBM Cloud 中建立 {{site.data.keyword.Bluemix_notm}} 服務實例。這相等於從 {{site.data.keyword.Bluemix_notm}} [型錄](https://cloud.ibm.com/catalog)建立服務實例。
* {{site.data.keyword.Bluemix_notm}} 服務實例的別名會新增（建立別名）至當初起始建立動作所在的 CFEE 空間。別名服務實例（在 CFEE 空間中）是對實際服務實例（在 IBM Cloud 帳戶中）的參照。服務實例別名容許開發人員與服務實例互動（例如連結至應用程式），方法是自動處理所有用於與服務實例互動的認證。

若要從 CFEE 空間內建立服務實例，請執行下列動作：
1. 在目標空間頁面中，移至**服務**標籤，然後按一下**建立服務**。這會開啟 {{site.data.keyword.cfee_full_notm}} 的 **Marketplace** 視圖。此視圖列出來自兩個來源的服務供應項目（請參閱__來源__ 直欄）：
   * {{site.data.keyword.Bluemix_notm}} 型錄中的供應項目。
   * 本端 {{site.data.keyword.cfee_full_notm}} Marketplace 中的供應項目。
5. 尋找並選取您要實例化的可用服務供應項目。 
6. 根據服務供應項目的來源（IBM Cloud 型錄或本端 CFEE Marketplace），繼續下列其中一項：
   * 如果選取的服務供應項目是 {{site.data.keyword.Bluemix_notm}} 型錄供應項目，您將會看到有一個**繼續**到 IBM Cloud 服務供應項目建立頁面的按鈕。這是可從 {{site.data.keyword.Bluemix_notm}} 型錄取得的同一頁面。在此頁面中，您會提供在 IBM Cloud 中建立服務所需之新服務實例名稱、地區和方案以及其他內容。建立服務實例之後，即會在 IBM Cloud 中建立服務實例並自動新增至現行 CFEE 空間。
   * 如果選取的服務供應項目來自本端 CFEE 型錄，您將會看到有一個**建立**服務實例的按鈕。系統會提示您輸入現行 CFEE 中的組織及空間，服務實例將會建立在其中。

## 使用 Cloud Foundry CLI 從 CFEE 空間建立 {{site.data.keyword.Bluemix_notm}} 服務實例
{: #creating-services_cli}

您可以從 CLI 在 CFEE 的空間建立服務實例。從 CLI 在 CFEE 空間建立服務，相等於從使用者介面在該空間建立。亦即，建立服務有下列雙重結果：
* 在 IBM Cloud 中建立 {{site.data.keyword.Bluemix_notm}} 服務實例。這相等於從 {{site.data.keyword.Bluemix_notm}} [型錄](https://cloud.ibm.com/catalog)建立服務實例。
* {{site.data.keyword.Bluemix_notm}} 服務實例會新增（建立別名）至當初起始建立動作所在的 CFEE 空間。

從 CFEE 空間建立服務實例，與從 CLI 建立服務實例，兩者的差異在於所建立之服務實例的生命週期。當您在 CFEE 空間使用者介面中建立服務實例時，所建立之服務實例的生命週期是在 {{site.data.keyword.Bluemix_notm}} 帳戶中從服務實例本身控制。這表示對於服務方案的更新是從 {{site.data.keyword.Bluemix_notm}} 帳戶中的實例控制，而不是從 CFEE 空間。或者，如果服務實例是從 CLI 建立，則服務的生命週期是從 CFEE 空間控制（服務是從 CFEE 空間更新）。

從 CLI 建立的服務實例也會顯示在使用者介面中，並且在服務實例名稱旁以 `*` 表示。

若要使用 CLI 建立服務實例，請遵循下列步驟：

1. 下載並安裝 {{site.data.keyword.Bluemix}} 指令行介面（如果尚未這樣做）。[下載 Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。

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
  
5. 建立服務：您可以發出 `cf create-service` 指令，在發出指令的 CFEE 空間中建立服務實例。使用此指令從 CFEE 建立服務實例，具有雙重結果：
    * 使用 `instance_name` 參數所提供的名稱，在公用 {{site.data.keyword.Bluemix}} 中建立服務實例。如果指令中未提供 `instance_name`，則 {{site.data.keyword.Bluemix}} 資源控制程式會提供一個名稱。  
    * 使用 `SERVICE_INSTANCE` 所指定的名稱，在從中發出指令的 CFEE 空間內，建立該公用服務實例的別名。請注意，公用服務實例的名稱不會自動與 CFEE 中的服務實例同名。因此，如果您要為公用服務實例及 CFEE 中的服務實例（公用服務實例的別名）賦予相同的名稱，則需要在下列指令中同時指定 `instance_name` 及 `SERVICE_INSTANCE`（具有相同值）：

  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"instance_name":"value", "resource_group":"value", "target":"value"}'
  ```
  {: pre}
  
下列範例會在 "bluemix-us-south" 地區中建立名為 "myCloudant" 的 Cloudant 服務實例（標準方案）（公用實例及 CFEE 別名兩者同名），並將它分組至特定資源群組：

  ```
  cf create-service cloudant standard myCloudant -c '{"instance_name":"myCloudant", "resource_group":"b0daaf6c3ccd4392a266da916cce2e8c", "target":"bluemix-us-south"}'
  ```
  {: pre}

 可以發出具有選用參數的 `create-service` 指令來處理特定使用案例：
 
   * 實例名稱 (`instance_name`)：容許您指定在公用 {{site.data.keyword.Bluemix}} 中建立之服務實例的自訂名稱。如果未提供 `instance_name` 值，則公用中公用服務實例的預設名稱將會與 `SERVICE_INSTANCE`（CFEE 中實例的名稱）不同。建議您使用此參數來控制公用服務實例的名稱，或者，如果您要提供與 CFEE 中服務實例相同的名稱（公用服務實例的別名），則建議使用此參數。
   * 資源群組 (`resource_group`)。容許您指定要放置新實例的資源群組。"resource_group" (`resource_group`)。請注意，此參數的值必須是資源群組的 ID（_資源群組 ID_），而不是資源群組的名稱（_資源群組名稱_）。您可以使用 `ibmcloud resource groups` 指令，找到特定資源群組的_資源群組 ID_。
   * 目標部署地區 (`target`)。要在其中佈建服務實例的地區。請注意，部分服務不需要指定目標。不過，如果建立的服務需要目標但未提供時，指令將會失敗。

您可以選擇性地提供包含那些參數的 JSON 檔案。例如：
  ```
  {
    "NewCloudant": 
        {  
        "instance_name":"myCloudant",
        "resource_group": "b0daaf6c3ccd4392a266da916cce2e8c",
        "target": "bluemix-us-south"
        }
   }
  ```
  {: pre}
  
然後，可以呼叫 JSON 檔案作為 `cf create-service` 指令的一部分。JSON 檔案的路徑可以是絕對路徑或相對路徑：
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
您可以發出下列指令來取得更多詳細資料：
  ```
  cf create-service -help
  ```
<br>
  如需相關資訊，請參閱 Cloud Foundry 文件中的 [Managing Service Instances with the cf CLI](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
  
## 從 CFEE 的使用者介面將服務連結至應用程式
{: #bind-services-ui}

具有_操作員_ 平台角色（或更高角色）及 {{site.data.keyword.Bluemix_notm}} 服務實例之_撰寫者_ 服務角色（或更高角色）的使用者可以將該實例連結至 CFEE 空間中所部署的應用程式，不論是從 [Cloud Foundry 服務儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/services)還是從 CFEE 空間使用者介面的「服務」標籤。   

若要從 [Cloud Foundry 服務儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/services)，將服務實例連結至應用程式，請執行下列動作：
1. 移至 [Cloud Foundry 服務儀表板](https://cloud.ibm.com/dashboard/cloudfoundry/services)，以查看 {{site.data.keyword.Bluemix_notm}} 帳戶中您可用的所有 {{site.data.keyword.Bluemix_notm}} 服務實例的合併視圖。視圖預期也會顯示哪些 {{site.data.keyword.Bluemix_notm}} 服務實例可用於（已建立別名至）哪些 CFEE 空間。您可以展開服務實例，以顯示它已新增到的 CFEE 空間。您可以進一步展開它們以查看服務實例連結的那些 CFEE 空間裡的應用程式。 
2. 找到您要連結的 {{site.data.keyword.Bluemix_notm}} 服務實例。
3. 展開相對應的視圖，以查看服務實例新增到的所有 CFEE 空間。如果該服務實例尚未新增至應用程式部署所在的 CFEE 空間，請從該列最右邊的功能表選取**新增**，讓服務實例可用於目標 CFEE 空間內。
4. 移至位於對應至可使用服務實例之 CFEE/空間的那列最右邊的功能表，然後選取**連結應用程式**。
5. 在__連結應用程式__對話框中，選取您要連結的應用程式。 

   **附註：**如果要連結的服務同時支援公用 (external) 及專用 (internal) 端點（請參閱 [IBM Cloud 服務端點](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about)），以及（或）支援多個[服務存取角色](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am)（指定可透過連結執行的服務實例可容許的動作），則多步驟對話框會提示您選取端點類型（公用或專用）及（或）特定服務角色。
6. 應用程式現在會連結至服務實例。您可以展開表格中的服務實例，以查看與其連結的應用程式（在特定 CFEE 空間中）。


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

## 使用 Cloud Foundry CLI 將服務連結至應用程式
{: #bind-services-cli}

您可以使用 `cf bind-service` 指令，在 CFEE 中將服務實例連結至應用程式：

 ```
  cf bind-service APP_NAME SERVICE_INSTANCE -c '{"parameter": "value"}' 
  ```
  {: pre}

在下列情況下，指令需要特殊參數：

* 使用 `cf bind-service` 指令將應用程式連結至服務實例，而該服務實例支援透過 IBM Cloud 專用網路連接至 IBM Cloud 服務的 [IBM Cloud 服務端點](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about)。若要將應用程式（部署於 CFEE）連結至同時支援公用 (external) 及專用 (internal) 端點的服務，您需要指定要用於連結的端點。在下列範例中，指令會使用 "internal" 端點來連結服務：

  ```
  cf bind-service myApplication myServiceInstance -c '{"service-endpoints":"internal"}' 
  ```
  {: pre}

* 服務具有多個[服務存取角色](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am)。服務存取角色指定可透過連結執行的服務實例可容許的動作。您可以透過 `role` 參數來指定特定服務存取角色。在下列範例中，連結指定 "writer" 服務存取角色：

  ```
  cf bind-service myApplication myServiceInstance -c '{"role": "writer"}' 
  ```
  {: pre}
<br>
如需使用 `cf bind-service` CLI 指令連結應用程式的相關資訊，請參閱 Cloud Foundry 文件中的[連結服務實例](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。

## 服務可見性
{: #service_visibility}

客戶可以控制誰可以從 CFEE 環境建立新的 IBM Cloud 服務。他們也可以控制誰可以將現有 IBM Cloud 服務新增至 CFEE 空間。此控制的方式是控制服務供應項目（及/或那些服務供應項目的實例）對使用者的可見性。

### 控制服務實例的建立作業
{: #control_servicecreation}

控制服務建立作業的完成方式是針對 IBM Cloud 帳戶中的所有使用者或特定 Cloud Foundry 組織中的使用者，控制「IBM Cloud 型錄」中服務供應項目的可見性。

#### 控制 IBM Cloud 帳戶中使用者對 IBM Cloud 型錄的可見性
{: #creation_accountvisibility}

IBM Cloud 帳戶管理者（具有所有啟用 IAM 功能服務之_管理者_ 角色的使用者）可以防止服務或服務方案顯示於給定 **IBM Cloud 帳戶**中所有使用者的型錄。帳戶管理者可以將帳戶中所有使用者的服務或服務方案列入黑名單，以防止所有帳戶使用者使用服務。將服務列入黑名單，將防止該帳戶中的使用者在 IBM Cloud 型錄中看到該服務（或服務方案）。這是透過 `ibmcloud catalog blacklist` 指令完成，語法如下：

  ```
  ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]
  ```

您可以以最簡單的形式使用 `catalog backlist` 指令，讓現行帳戶中的使用者看不到服務供應項目（其所有方案）：

  ```
  Ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]

  ```
  {: pre}

您不僅可以將整個服務供應項目的可見性列入黑名單，還可以將特定地區中的特定方案列入黑名單。因此，您還是需要使用廣域型錄中對應項目的 ID，而非名稱。如果您要防止使用者看到特定地區中的特定方案，則可以發出下列指令：

  ```
  Ibmcloud catalog blacklist -add <catalogEntryID>
  ```
  {: pre}
  
 若要移除黑名單中的服務，請執行下列指令：
 ```
  Ibmcloud catalog blacklist -remove <catalogEntryID>
  ```
  {: pre}
 
您可以透過下列指令，找到給定型錄項目的 ID（例如，服務的方案及其部署地區）。此指令會傳回給定服務的所有方案及其部署地區：

  ```
  ibmcloud catalog service <thisService>
  ```
  {: pre}

您可以發出下列指令，找到 `ibmcloud catalog blacklist` 的更多詳細資料：

  ```
  Ibmcloud catalog blacklist -help
  ```
  {: pre}


#### 控制 Cloud Foundry 組織中使用者的可見性
{: #creation_orgvisibility}

您可以使用 `cf enable-service-access` 及 `cf disable-service-access` 指令來控制對特定 **Cloud Foundry 組織**之服務的存取。在這裡，存取的控制點是 Cloud Foundry（非「IBM Cloud 帳戶」）。請注意，這是原生 `cf` 指令（非 `ibmcloud` 指令）。 

透過 `cf` CLI 設定服務可見性時，請考量下列項目：

*  `cf` 指令會針對特定 Cloud Foundry 組織的所有使用者，啟用及（或）停用服務供應項目（選擇性地啟用及（或）停用特定服務供應項目方案）
* 啟用的運作方式是建置組織「白名單」。亦即，確實存取服務的 Cloud Foundry 組織併入清單（相對於先前所述 `ibmcloud` 指令中的「黑名單」方式，其運作方式是定義看不到帳戶使用者的服務清單）。這表示可以使用此方式存取型錄服務的控制，而不是藉由定義哪些組織看不到服務（黑名單），而是藉由定義哪些組織可以看到它（白名單）。
*  當您將組織新增至白名單以提供該組織對服務（或服務方案）的存取時，將會實際停用（排除）所有其他組織存取該服務（或服務方案）。亦即，在您將組織列入白名單之後，將會停用所有其他組織存取該服務（或服務方案）。
*  在您將組織新增至「可以查看」清單之前，必須停用所有組織的可見性。如果所有組織目前都可以使用服務方案，則您無法停用對該方案的存取。

根據上述一般行為，建議您發出下列指令來控制組織對服務的存取：

  * **停用**存取所有組織的服務方案：
  ```
  cf disable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}
  
  下列範例停用對所有 MyOrg 成員的 Cloudant 服務標準方案的存取：
  ```
  cf disable-service-access cloudant -p standard -o MyOrg
  ```
  {: pre}

  
  * **啟用**存取特定 CFEE 組織的服務方案。這會針對指令中未特別啟用的所有其他組織，停用服務方案。 
  ```
  cf enable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}

<br>  
**附註：**建議您針對整個服務執行 Cloud Foundry 啟用及停用服務指令，而非針對特定方案。


### 控制對現有服務實例的存取
{: #control_serviceaddition}

CFEE 空間中的開發人員可以使用 IBM Cloud 帳戶中可用的現有服務實例。在 CFEE 的特定空間內，使用者可以將服務實例**新增**至該空間（請參閱上面的[新增現有服務實例](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)）。將服務實例新增至 CFEE 空間會建立服務實例的別名（參照），以讓開發人員將服務實例連結至已部署至該 CFEE 空間的應用程式，就像它是實際服務實例一樣。

帳戶管理者可以透過 [IAM 存取原則](https://cloud.ibm.com/docs/iam/iamusermanage.html#iamusermanage)來控制服務實例的使用。從使用者介面或 ibmcloud CLI 中，他們可以將角色指派給服務實例本身或那些實例所在的資源群組。開發人員需要先具有對服務實例（或其資源群組）的_檢視者_ 角色或更高角色，才能將該實例新增至空間。

您可以在 [CFEE 視訊播放清單](https://ibm.biz/CFEE-Playlist){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示") 中找到具有 CFEE 服務深度討論及示範的視訊。
{:tip}
