---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在正式作業環境中執行應用程式的最佳作法
{: #production}

Cloud Foundry 是一個傑出平台，可在正式作業環境中執行具有雲端功能的應用程式。這些最佳作法有助於使用 {{site.data.keyword.Bluemix_notm}} 來執行正式作業 Cloud Foundry 應用程式。
{:shortdesc}

## 多個實例
{: #multiple_instances}

具有雲端功能的應用程式可進行水平擴充，因此可以動態新增或移除應用程式實例。請至少為每一個應用程式執行三個實例，以協助避免在隔離的突發事件或平台維護時發生非預期地關閉。

## 監視選項
{: #monitoring}

{{site.data.keyword.Bluemix_notm}} 讓您可以使用服務（例如 [Monitoring and Analytics](/docs/services/monana/index.html) 及 [New Relic ![外部鏈結圖示](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}）輕鬆地監視應用程式。如需相關資訊，請參閱[整合記載功能](../monitor_log/logging.html#logging_for_bluemix_apps)。

## 支援選項
{: #support}

{{site.data.keyword.Bluemix_notm}} 付費定價方案使用*選用* 付費支援來提供若干不同的帳戶類型。不論帳戶的類型為何，如果您計劃在 {{site.data.keyword.Bluemix_notm}} 上讓應用程式進入正式作業，請考慮登記此選項。

不論是否使用付費支援，您都可以如[如何取得所需的支援？](../get-support/howtogetsupport.html)所述取得協助，但支付支援費用有助於確保支援問題單獲得它們所需的警示層次。
