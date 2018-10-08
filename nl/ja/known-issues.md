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

# 既知の問題 (制限事項)
{: #known-issues}

## Firehose Prometheus エクスポーターによる大量の CPU 使用が原因の不安定性

CFEE 環境には、http および https の_開始_ 要求および_停止_ 要求に関する Cloud Foundry メトリックを収集するための Prometheus Firehose エクスポーターが含まれています。http 要求の数が多い CFEE 環境では、Prometheus Firehose エクスポーターが大量の CPU を使用する可能性があります。その結果として環境が不安定になることがあります。これは、Firehouse エクスポーター・ポッドは Cloud Foundry 制御プレーン・ワーカー・ノードの 1 つで実行されるためです。

以下のいずれかの方法で、Firehose エクスポーター・ポッドが多くの CPU を使用していて、CFEE 環境を不安定にしている可能性があるかどうかを判別できます。 
1.  CFEE 環境の CFEE 概要ページを介して、CF 制御プレーンの全体的な CPU 使用量をチェックします。以下の高 CPU 使用例をご覧ください。
![「概要」ページの高 CPU](img/FirehoseExporterIssue_OverviewMetrics.png)

2. _「リソース使用量」 > 「アプリケーション」_ページで CPU 使用量をチェックし、異常なほど多数の http 要求がないか確認します。以下の高 CPU 使用例をご覧ください。
![「リソース使用量」ページの高 CPU](img/FirehoseExporterIssue_ResourceUsage.png)

3. Firehouse ポッドの CPU 使用量が表示された POD Grafana コンソール (_「モニタリング」_ページから起動される) をチェックします。以下の高 CPU 使用例をご覧ください。
![Grafana コンソールの高 CPU](img/FirehoseExporterIssue_Grafana.png)

Firehouse エクスポーターが 0.5 から 0.7 (50 から 70%) の CPU を使用していて、全体的な制御プレーン CPU が高い場合、以下の手順に従って http 要求メトリック収集をオフにする必要がある可能性があります。

1. `config.yaml` を作成します。

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml.
   ```
   {: pre}
  
2. `config.yaml` を編集して、`spec.template.spec.containers.args` 配列に以下の行を追加します。

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```

### 例

元の `config.yam`:

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

以下のコマンドは、ワーカー・ノード・ポッドを再構成し、再始動します。

```
kubectl -n cf-monitoring apply -f config.yaml.

```

Firehose Prometheus エクスポーターについて詳しくは、[Cloud Foundry Firehose Prometheus エクスポーター](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。
