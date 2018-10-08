---

copyright:
  years: 2018
lastupdated: "2018-09-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 已知问题（限制）
{: #known-issues}

## 由于 Firehose Prometheus 导出器的高 CPU 使用率而导致不稳定

CFEE 环境包含 Prometheus Firehose 导出器，用于收集有关 HTTP 和 HTTPS _启动_和_停止_请求的 Cloud Foundry 度量值。具有大量 HTTP 请求的 CFEE 环境可能会导致 Prometheus Firehose 导出器使用大量 CPU。这可能会造成环境中有些不稳定，因为 Firehose 导出器 pod 在其中一个 Cloud Foundry 控制平面工作程序节点上运行。

您可以通过下列其中一种方法来确定 Firehose 导出器 pod 的 CPU 使用率是否很高，而可能导致 CFEE 环境不稳定： 
1.  通过 CFEE 环境的“CFEE 概述”页面检查 CF 控制平面的总体 CPU 使用率。请参阅下面的高 CPU 使用率说明示例：![“概述”页面中的高 CPU](img/FirehoseExporterIssue_OverviewMetrics.png)

2. 在_资源使用情况 > 应用程序_页面中检查 CPU 使用率，并查看是否存在异常多的 HTTP 请求。请参阅下面的高 CPU 使用率说明示例：![“资源使用情况”页面中的高 CPU](img/FirehoseExporterIssue_ResourceUsage.png)

3. 检查 POD Grafana 控制台（从_监视_页面启动）中显示的 Firehouse pod 的 CPU 使用率。请参阅下面的高 CPU 使用率说明示例：![Grafana 控制台中的高 CPU](img/FirehoseExporterIssue_Grafana.png)

如果 Firehouse 导出器的 CPU 使用率介于 0.5 到 0.7 (50-70%) 之间，并且总体控制平面的 CPU 使用率很高，那么可能需要通过以下步骤关闭 HTTP 请求度量值收集：

1. 创建 `config.yaml`：

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml.
   ```
   {: pre}
  
2. 编辑 `config.yaml`，并在 `spec.template.spec.containers.args` 数组中添加以下行：

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```

### 示例

原始 `config.yam`：

```
  ...
  template:
  ...
    spec:
      containers:
      - args:
        ...
        - --doppler.metric-expiration=10m
        - --metrics.environment=IBM-Cloud-Foundry-Enterprise-Environment
        - --filter.events=ContainerMetric,CounterEvent,ValueMetric
        image: boshprometheus/firehose-exporter
```  

以下命令将重新配置并重新启动工作程序节点 pod：

```
kubectl -n cf-monitoring apply -f config.yaml.

```

有关 Firehose Prometheus 导出器的更多信息，请参阅 [Cloud Foundry Firehose Prometheus 导出器](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")。
