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

# 알려진 문제점(제한사항)
{: #known-issues}

## Firehose Prometheus exporter의 높은 cpu 사용량으로 인한 불안정함
{: #instabilityCPU-issue}

CFEE 환경에는 http 및 https _start_ 및 _stop_ 요청의 Cloud Foundry 메트릭 수집을 위해 Prometheus Firehose exporter가 포함되어 있습니다. 많은 수의 http 요청이 있는 CFEE 환경은 Prometheus firehose exporter가 많은 양의 CPU를 사용하게 되는 원인을 제공할 수 있습니다. firehouse exporter 팟(Pod)이 Cloud Foundry 제어 플레인 작업자 노드 중 하나에서 실행되므로 이는 환경의 일부 불안정을 유발할 수 있습니다.

다음 방법 중 하나를 사용하여 firehose exporter 팟(pod)이 CPU를 많이 사용하고 있으며 CFEE 환경에서 불안정성을 유발할 수 있는지 판단할 수 있습니다. 
1.  해당 CFEE 환경의 CFEE 개요 페이지를 통해 CF 제어 플레인의 전체 CPU 사용량을 확인하십시오. 아래의 높은 cpu 사용량의 예시를 보십시오.
![개요 페이지의 높은 CPU 사용량](img/FirehoseExporterIssue_OverviewMetrics.png)

2. _리소스 사용량 > 애플리케이션_ 페이지에서 CPU 사용량을 확인하고 비정상적으로 많은 수의 http 요청이 있는지 확인하십시오. 아래의 높은 cpu 사용량의 예시를 보십시오.
![리소스 사용량 페이지의 높은 CPU 사용량](img/FirehoseExporterIssue_ResourceUsage.png)

3. Firehouse 팟(Pod)의 CPU 사용량을 표시하는 POD Grafana 콘솔(_모니터링_ 페이지에서 시작됨)을 확인하십시오. 아래의 높은 cpu 사용량의 예시를 보십시오.
![Grafana 콘솔의 높은 CPU 사용량](img/FirehoseExporterIssue_Grafana.png)

firehouse exporter가 0.5 및 0.7(50-70%) CPU 사이를 사용 중이며 전체 제어 플레인 CPU의 사용량이 높은 경우에는 다음 단계를 통해 http 요청 메트릭 수집을 중지해야 할 수 있습니다.

1. `config.yaml`을 작성하십시오.

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml
   ```
   {: pre}
  
2. `config.yaml`을 편집하고 `spec.template.spec.containers.args` 배열에 다음 행을 추가하십시오.

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```
   {: pre}

### 예

수정된 `config.yam`:

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

다음 명령은 작업자 노드 팟(Pod)을 재구성하고 다시 시작합니다.

```
kubectl -n cf-monitoring apply -f config.yaml

```
{: pre}

Firehose Prometheus exporter에 대한 자세한 정보는 [Cloud Foundry Firehose Prometheus exporter](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오.
