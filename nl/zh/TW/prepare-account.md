---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 準備帳戶
{: #prepare}

CFEE 實例部署在基礎架構資源（IBM Container 服務中的 Kubernetes 工作者節點）上，這些資源的費用將計入 IBM Cloud 帳戶。這表示用來建立 CFEE 實例的 IBM Cloud 帳戶必須是付費帳戶（「隨收隨付制」或「訂閱」帳戶）。如果您打算用來建立 CFEE 實例的 IBM Cloud 帳戶是試用帳戶，則在您嘗試建立 CFEE 實例時，系統會要求您升級帳戶。升級 IBM Cloud 帳戶（從試用帳戶升級至「隨收隨付制」或「訂閱」帳戶）時，IBM Cloud 帳戶會鏈結至 SoftLayer 帳戶（藉此可以用來建立基礎架構資源）。如需相關資訊，請參閱[帳戶類型](https://console.bluemix.net/docs/account/index.html#accounts)。這些基礎架構資源的成本會顯示在 IBM Cloud 發票中。

## 如何判定 IBM Cloud 帳戶是否可以建立 CFEE 實例
{: #account-check}

您可以查看 IBM Cloud 橫幅右上角的帳戶資訊，以判定 IBM Cloud 帳戶是試用帳戶還是付費帳戶，以及它是否鏈結至 SoftLayer 帳戶。

在下列範例中，_Mary Smith_ 使用者已登入 IBM Cloud 帳戶 _MyCompany_，這是一個試用帳戶。![帳戶檢查](img/AccountExample_1.png)

在下列範例中，相同的 IBM Cloud 帳戶 _MyCompany_ 已升級為付費帳戶。升級之後，該帳戶現在鏈結至 SoftLayer 帳戶 _1684806_。兩個帳戶都會顯示在「帳戶」欄位中。
![帳戶檢查](img/AccountExample_2.png)

如果 IBM Cloud 帳戶是試用帳戶，則在您嘗試建立 CFEE 實例時，系統會提示您升級。請參閱下面顯示的畫面：

![帳戶檢查](img/UpgradeAccountPage_1.png)

## 使用 SoftLayer 帳戶而不是升級 IBM Cloud 帳戶
{: #account-linkswitching}

如果您在 IBM Cloud 帳戶中具有「管理者」角色，則可以在不升級 IBM Cloud 帳戶的情況下，使用 SoftLayer 帳戶來建立 CFEE 實例。


**警告：**如果您現在使用 SoftLayer 帳戶，而且未來更新 IBM Cloud 帳戶（成為「隨收隨付制」或「訂閱」帳戶），則在建立未來的基礎架構資源時，更新過的 IBM Cloud 仍然可以使用 SoftLayer 帳戶（您現在設定其認證）。此外，如果您未來使用不同的 SoftLayer 帳戶來建立 Cloud Foundry Enterprise Environment，則 IBM Cloud 帳戶中的使用者可能無法存取使用您現在設定認證之 SoftLayer 帳戶所建立的基礎架構資源。建議您改為升級 IBM Cloud 帳戶。

若要在不升級 IBM Cloud 帳戶的情況下使用 SoftLayer 帳戶，請執行下列動作（如需說明，請參閱下列的畫面）：
1. 在未升級 IBM Cloud 帳戶時所顯示的畫面中，按一下**使用 SoftLayer 帳戶**。
2. 輸入 SoftLayer 帳戶的**使用者名稱**及 **API 金鑰**。若要取得 SoftLayer 的「使用者名稱」及「API 金鑰」，請存取 [SoftLayer 主控台](https://control.softlayer.com)。登入 SoftLayer 之後，請選取您要鏈結至 {{site.data.keyword.Bluemix_notm}} 帳戶的帳戶。選取帳戶會開啟帳戶的設定檔頁面。向下捲動至頁面尾端，以尋找帳戶的使用者名稱及 API 金鑰。如果您沒有 API 金鑰，且您是帳戶擁有者的話，則可以產生它。如果您不是帳戶擁有者，請要求帳戶擁有者產生它。
3. 按一下**設定認證**。

![帳戶檢查](img/UpgradeAccountPage_2.png)

**附註：**您必須在 SoftLayer 帳戶中具有足夠的許可權，才能從 IBM Container 服務建立一般的 Kubernetes 叢集。如果沒有，請要求 SoftLayer 帳戶管理者或提供您 SoftLayer 帳戶存取權的使用者，將這些額外的許可權授與給您。
