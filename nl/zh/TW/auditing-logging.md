---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 審核及記載
{: #auditing-logging}

{{site.data.keyword.cfee_full}} (CFEE) 中的審核及記載功能容許管理者審核 CFEE 實例中發生的事件，並讓開發人員追蹤從其 Cloud Foundry 應用程式產生的日誌事件。

透過與 Log Analysis 及 Activity Tracker IBM Cloud 服務整合，支援 CFEE 中的審核及記載。

## 審核
{: #auditing}

審核容許 CFEE 管理者追蹤 CFEE 實例中發生的 Cloud Foundry 可審核活動。這些活動包括登入、組織及空間的建立、使用者成員資格及角色指派、應用程式部署、服務連結及網域配置。透過與 IBM Cloud 中的 Activity Tracker 服務整合，支援審核。會自動配置 CFEE 管理者所選取的 Activity Tracker 服務實例，以接收代表 Cloud Foundry 內及 CFEE 控制平面上執行之動作的事件。使用者可以在 Activity Tracker 服務實例的使用者介面中查看及管理這些事件。

若要啟用 CFEE 實例的審核，請執行下列動作：

1. 開啟 CFEE 的使用者介面以及左導覽窗格中的**作業 > 審核**項目，以開啟「記載」頁面。
2. 按一下**啟用審核**，然後選取 IBM Cloud 帳戶中可用的其中一個 **Activity Tracker 實例**。如果沒有可用的實例，則使用者會看到在 IBM Cloud 型錄中建立新 Activity Tracker 實例的選項。
3.  啟用審核之後，頁面上會顯示配置詳細資料。詳細資料包括配置的狀態，以及 Activity Tracker 服務實例本身的鏈結，而使用者可以前往該鏈結，以查看及管理審核事件。

您可以按一下**停用審核**來停用「審核」，這會移除先前新增及配置的 Activity Tracker 服務實例。此動作不會刪除 Activity Tracker 服務實例。

## 記載持續性
{: #logging}

透過與 IBM Cloud 中的 Log Analysis 服務整合，支援 Cloud Foundry 事件的記載。會自動配置 CFEE 管理者所選取的 Log Analysis 服務實例，以接收及持續保存從 CFEE 實例產生的 Cloud Foundry 記載事件。使用者可以在 Log Analysis 服務實例的使用者介面中查看及管理這些記載事件。

若要啟用 CFEE 實例的記載，請執行下列動作：

1. 確定您有 [IAM 存取原則](https://cloud.ibm.com/iam/#/users)，可將打算持續保存記載事件之 Log Analysis 服務實例的編輯者、操作員或管理者角色指派給您。
2. 開啟 CFEE 的使用者介面以及左導覽窗格中的**作業 > 記載**項目，以開啟「記載」頁面。
3. 按一下**啟用持續性**，然後選取 IBM Cloud 帳戶中可用的其中一個 **Log Analysis 實例**。如果沒有可用的實例，則使用者會看到在 IBM Cloud 型錄中建立實例的選項。
4. 啟用記載持續性之後，頁面中會顯示配置詳細資料。詳細資料包括配置的狀態，以及 Log Analysis 服務實例本身的鏈結，而使用者可以前往該鏈結，以查看及管理記載事件。

**警告：**啟用「記載持續性」需要干擾性重新啟動 CFEE 控制平面及 Cell。在重新啟動期間，會提供所有管理功能，但此 CFEE 實例中執行的部分應用程式及服務可能會無法使用。在重新啟動期間，CFEE 元件的狀態將會反映在「性能檢查」頁面中。重新啟動大約需要 20 分鐘。

您可以按一下**停用日誌持續性**來停用「日誌持續性」，這會移除先前新增及配置的服務實例。此動作不會刪除 Log Analysis 服務實例。

**附註：**當您停用日誌持續性時，仍然會產生 Cloud Foundry 記載事件，但它們不會持續保存在 CFEE 實例外部。
