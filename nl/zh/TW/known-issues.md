---

copyright:
  years: 2018
lastupdated: "2018-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 已知問題（限制）
{: #known-issues}

## 由於 Firehose Prometheus 匯出程式的高 CPU 使用率而致的不穩定性
{: #instabilityCPU-issue}

CFEE 環境包含 Prometheus Firehose 匯出程式，以便收集關於 http 及 https _start_ 及 _stop_ 要求的 Cloud Foundry 度量值。具有大量 http 要求的 CFEE 環境，可能會導致 Prometheus Firehose 匯出程式使用大量的 CPU。這可能導致環境中的部分不穩定性，因為 Firehouse 匯出程式 Pod 在其中一個 Cloud Foundry 控制平面工作者節點上執行。

您可以使用下列其中一種方法，判定 Firehose 匯出程式 Pod 的 CPU 使用率是否偏高，並且可能在 CFEE 環境中造成不穩定性： 
1.  透過該 CFEE 環境的「概觀」頁面，檢查 CF 控制平面的整體 CPU 使用率。請參閱底下的高 CPU 使用率說明範例：
![「概觀」頁面中的高 CPU](img/FirehoseExporterIssue_OverviewMetrics.png)

2. 檢查_資源用量 > 應用程式_ 頁面中的 CPU 使用率，看看是否有不尋常的大量 http 要求。請參閱底下的高 CPU 使用率說明範例：
![「資源用量」頁面中的高 CPU](img/FirehoseExporterIssue_ResourceUsage.png)

3. 檢查顯示 Firehose Pod CPU 使用率的 POD Grafana 主控台（從_監視_ 頁面啟動）。請參閱底下的高 CPU 使用率說明範例：
![Grafana 主控台中的高 CPU](img/FirehoseExporterIssue_Grafana.png)

如果 Firehose 匯出程式使用介於 0.5 到 0.7 (50-70%) 之間的 CPU，而整體控制平面 CPU 很高，您可能需要透過下列步驟關閉 http 要求度量值收集：

1. 建立 `config.yaml`：

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml
   ```
   {: pre}
  
2. 編輯 `config.yaml` 並在 `spec.template.spec.containers.args` 陣列中新增下行：

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```
   {: pre}

### 範例

已修改的 `config.yam`：

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

下列指令會重新配置並重新啟動工作者節點 Pod：

```
kubectl -n cf-monitoring apply -f config.yaml

```
{: pre}

如需 Firehose Prometheus 匯出程式的相關資訊，請參閱 [Cloud Foundry Firehose Prometheus 匯出程式](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")。
