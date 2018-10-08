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

# 建立組織及空間
{: #create_orgs}

{{site.data.keyword.cfee_full}} 中的應用程式是以特定空間為範圍。空間則是存在於特定組織內。組織的成員會共用配額方案、應用程式、服務實例及自訂網域。建立組織及空間之後，即可將使用者新增至其中，並且具有可決定對這些組織及空間之存取及控制層次的特定角色。若要建立組織，並指派這些組織的管理員，您需要 {{site.data.keyword.cfee_full_notm}} 服務以及要新增使用者之特定環境實例的管理者角色。這些許可權設定於 {{site.data.keyword.Bluemix}} 標頭之**管理 > 使用者**功能表下的_身分及存取_ 頁面。
{: shortdesc}

## 建立組織
{: #create-org}

若要在 {{site.data.keyword.cfee_full_notm}} 中建立組織，請執行下列動作：

1. 移至 [{{site.data.keyword.Bluemix_notm}} Cloud Foundry Environment 儀表板](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments){: new_window}，並開啟您要在其中建立組織的 {{site.data.keyword.cfee_full_notm}}。
2. 在 {{site.data.keyword.cfee_full_notm}} 使用者介面中，移至導覽窗格中的**組織**項目，以開啟_組織_ 頁面。
3. 按一下**新增**。
4. 輸入新組織的**名稱**。
5. 在**管理員**下，識別至少一位使用者。只有具有「管理員」角色的使用者才能將成員新增至該組織。
6. 在**配額方案**下，選取可用的方案。配額方案會限制組織中應用程式可用的記憶體、所管理的應用程式實例數上限，以及路徑數目上限。

除了管理組織成員資格之外，組織管理員還可以建立、檢視、編輯或刪除組織內的空間。組織管理員也可以檢視組織的用量及配額、邀請使用者加入組織、管理組織中的成員資格及角色，以及管理組織的自訂網域。

若要在組織內建立空間，請在_組織_ 頁面中，移至**空間**標籤，然後按一下**新增**。組織的成員也可以在組織內建立及管理他們自己的空間。如需 Cloud Foundry 角色的相關資訊，請參閱 [Cloud Foundry 存取](https://console.bluemix.net/docs/iam/cfaccess.html#cfroles){: new_window}。

**附註**：存取 {{site.data.keyword.cfee_full_notm}} 內的組織及空間，需要使用者有權存取環境本身。使用者無權存取 {{site.data.keyword.cfee_full_notm}}，就無法存取環境內的組織及空間，而不論他們在這些組織及空間中的成員資格及角色為何。
