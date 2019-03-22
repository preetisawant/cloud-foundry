---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# 法規遵循
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) 是平台即服務 (PaaS)。因此，客戶能免費使用服務實例，以進行能夠支援的所有項目。CFEE 及相依服務能夠存取儘可能最少的個人資料量。

不過，應該釐清的一點是，即使 CFEE 控制平面（透過使用者介面/API/CLI）不會處理機密資料（例如 HIPAA 資料），客戶還是必須負責確保他們以負責任的方式使用其 CFEE，因為所有相依關係都是由其 {{site.data.keyword.Bluemix_notm}} 帳戶中的客戶所管理及擁有。 

建議使用下列最佳作法：
*  不要修改使用 CFEE（Kubernetes、Cloud Object Storage 及 Compose for PostgreSQL）所建立的相依服務。
*  透過 CFEE 服務本身（使用者介面或指令行介面）來更新及管理 CFEE，而不是透過 Kubernetes 服務。

Kubernetes 叢集用來保留大部分 CFEE 基礎架構，以及在 CFEE 上執行的所有應用程式，因為 Cloud Foundry Cell 部署在 Kubernetes 節點上方。此叢集由客戶的 SoftLayer 帳戶所擁有及管理。

CFEE 會使用 Compose for PostgreSQL 資料庫來保留組織、空間、使用者及角色的 meta 資料。如果依建議使用 CFEE 實例，則不會公開任何機密資料。不過，如果客戶決定以其客戶的個人或機密性資訊來命名組織及空間，則 PostgreSQL 資料庫可能會包含 HIPAA 或其他類型的機密性資訊。

CFEE 會使用 Cloud Object Storage 實例來保留應用程式的 Droplet，因此可以部署、停止、啟動它們等等。這表示，Cloud Object Storage 實例未執行應用程式，而是只保留其映像檔。因此，如果使用 Cloud Object Storage 實例時遵循最佳作法，它並不會保留任何 HIPAA 機密性資訊。客戶有責任確保不會將個人資料寫入其任何應用程式（測試資料等）。
