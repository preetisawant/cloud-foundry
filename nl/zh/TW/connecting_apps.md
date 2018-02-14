---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# 管理連線
{: #connect_app}

您可以從服務儀表板的**連線**標籤中，將服務連接至現有或新的 {{site.data.keyword.Bluemix}} 應用程式。將 Cloud Foundry 服務連接至 Cloud Foundry 應用程式時會建立其間的連結，而且您可以從**連線**標籤中取消連結、新增其他連線或刪除連線。

不過，當您將「{{site.data.keyword.Bluemix_notm}} 身分及存取管理 (IAM)」所管理的服務實例連接至 Cloud Foundry 應用程式時，會使用您指定的連結資訊在對應的 Cloud Foundry 空間中自動建立 IAM 所管理的服務別名。此別名會以 IAM 受管理服務的 Cloud Foundry 服務實例來代表。
{:shortdesc}

## 何謂別名？
{: #what_is_alias}

別名是資源群組內 IAM 受管理服務與組織或空間內 Cloud Foundry 應用程式之間的連線。在 {{site.data.keyword.Bluemix_notm}} 主控台中，連線（別名）會以 Cloud Foundry 服務實例來代表。您可以藉由修改代表您連線的服務實例來管理別名。

別名類似於符號鏈結，它會保留對遠端資源的參照，並支援跨平台的實例的交互作業能力和重複使用。例如，您可以在資源群組中建立服務的實例，然後從任何可用的 Cloud Foundry 地區中重複使用它，方法是在那些地區的組織或空間中建立別名。

下列規則適用於別名：

* 別名不需要額外費用，但每一個別名都會計入您在 Cloud Foundry 組織中的配額。
* 在 {{site.data.keyword.Bluemix_notm}} 主控台中，每個 Cloud Foundry 空間只能建立一個別名。不過，使用 {{site.data.keyword.Bluemix_notm}} CLI 可以為每個空間建立多個別名。如需相關資訊，請參閱[用來管理資源群組及資源的指令](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources)。
* 如果您具有許可權，則可以在 IAM 受管理服務與相同帳戶中任何空間、組織及地區內的任何 Cloud Foundry 應用程式之間建立多個連線。
* 相同空間中從 IAM 受管理服務實例到不同 Cloud Foundry 應用程式的多個連線，將會使用相同的別名。
* 取消連結 IAM 受管理服務實例，*不會* 刪除代表別名的 Cloud Foundry 服務實例。
* 刪除 IAM 受管理服務實例所連接的 Cloud Foundry 應用程式，*不會* 刪除代表別名的 Cloud Foundry 實例。
* 刪除 IAM 受管理服務實例，*會* 刪除代表別名的 Cloud Foundry 服務實例。

## 在 IAM 受管理服務與 Cloud Foundry 應用程式之間建立連線（別名）
{: #creating_alias}

若要將 IAM 受管理服務實例連接至 Cloud Foundry 應用程式，請執行下列動作：

1. 移至儀表板。

2. 按一下應用程式的名稱，以開啟應用程式詳細資料視圖。

3. 按一下**連接現有項目**，然後從現有 Cloud Foundry 應用程式中進行選擇。或者，按一下**建立連線**，以建立要連接的 Cloud Foundry 應用程式。

4. 指定**連線的存取角色**。此值會設定 IAM 服務存取角色。如需相關資訊，請參閱 [IAM 存取](/docs/iam/users_roles.html#userroles)。

5. 您可以選擇性地提供**連線的服務 ID**，方法是容許 IAM 為您產生唯一值，或提供現有服務 ID。如需相關資訊，請參閱[建立及管理服務 ID](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids)。

6. 按一下**建立**。

## 檢視別名

在 IAM 受管理服務與 Cloud Foundry 應用程式之間建立連線之後，別名就會顯示在所連接 Cloud Foundry 應用程式的**連線**標籤上。此外，在儀表板上，別名會顯示為執行中的 Cloud Foundry 服務實例，而且只有在您開啟它時，才會包含**連線**標籤。

1. 移至儀表板。
2. 從 **Cloud Foundry 服務**表格中，按一下服務實例的名稱，以開啟服務詳細資料視圖。如果它只有**連線**標籤，則它是別名。

## 刪除別名

刪除別名的最簡單方式是刪除 IAM 受管理服務實例。不過，您可以維護 IAM 受管理服務實例，並改為直接刪除別名。

1. 移至儀表板。
2. 從 **Cloud Foundry 服務**表格中，按一下服務實例的名稱，以開啟服務詳細資料視圖。如果它只有**連線**標籤，則它是別名。
3. 刪除實例。

## 建立多個 Cloud Foundry 服務之間的連線
{: #cf}

如需將 Cloud Foundry 服務連結至另一個 Cloud Foundry 服務的詳細資料，請參閱[在另一個服務中使用服務](../apps/reqnsi.html#add_service)。
