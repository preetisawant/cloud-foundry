---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在生产环境中运行应用程序的最佳实践
{: #production}

Cloud Foundry 是在生产环境中运行云就绪型应用程序的极佳平台。这些最佳实践可帮助您使用 {{site.data.keyword.Bluemix_notm}} 运行生产 Cloud Foundry 应用程序。
{:shortdesc}

## 多个实例
{: #multiple_instances}

云就绪型应用程序可水平扩展，因此能够动态添加或除去应用程序实例。每个应用程序至少运行三个实例，以帮助避免在发生孤立事件或进行平台维护时出现意外停机时间。

## 监视选项
{: #monitoring}

通过 {{site.data.keyword.Bluemix_notm}}，可轻松使用 [Monitoring and Analytics](/docs/services/monana/index.html) 和 [New Relic ![外部链接图标](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window} 等服务来监视应用程序。有关更多信息，请查看[集成日志记录功能](../monitor_log/logging.html#logging_for_bluemix_apps)。

## 支持选项
{: #support}

{{site.data.keyword.Bluemix_notm}} 付费价格套餐提供了多种不同的帐户类型以及*可选*的付费支持。不管您的帐户类型是什么，如果您计划将应用程序放入 {{site.data.keyword.Bluemix_notm}} 上的生产环境，请考虑选择此选项。

不管是否使用付费支持，您都可以获取帮助，如[如何获取所需的支持？](../get-support/howtogetsupport.html)中所述，但为支持付费将有助于确保支持凭单获得应有程度的关注。
