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

# Problemas Conhecidos (Limitações)
{: #known-issues}

## Instabilidade devido ao alto uso de CPU pelo exportador Firehose Prometheus
{: #instabilityCPU-issue}

Os ambientes do CFEE incluem um exportador Prometheus Firehose para coletar as métricas do Cloud Foundry nas solicitações _start_ e _stop_ http e https. Um ambiente do CFEE com um alto número de solicitações de HTTP pode fazer com que o exportador Prometheus Firehose use uma grande quantia de CPU. Isso pode levar a alguma instabilidade no ambiente já que o pod do exportador Firehouse é executado em um dos nós do trabalhador do plano de controle do Cloud Foundry.

É possível determinar se o pod do exportador Firehose está usando CPU alta e potencialmente causando instabilidade no ambiente do CFEE, por um dos métodos a seguir: 
1.  Verifique o uso geral de CPU do plano de controle do CF por meio da página Visão geral do CFEE para esse ambiente do CFEE. Veja um exemplo ilustrativo de alto uso de CPU abaixo:
![CPU alta na página Visão geral](img/FirehoseExporterIssue_OverviewMetrics.png)

2. Verifique o uso de CPU na página _Uso do recurso > Aplicativos_ e veja se há um número extraordinariamente alto de solicitações de HTTP. Veja um exemplo ilustrativo de alto uso de CPU abaixo:
![CPU alta na página Uso do recurso](img/FirehoseExporterIssue_ResourceUsage.png)

3. Verifique o console do POD Grafana (ativado na página _Monitoramento_) que mostra o uso de CPU para o pod do Firehouse. Veja um exemplo ilustrativo de alto uso de CPU abaixo:
![CPU alta no console do Grafana](img/FirehoseExporterIssue_Grafana.png)

Se o exportador Firehouse estiver usando a CPU entre 0.5 e 0.7 (50-70%) e a CPU do plano de controle geral estiver alta, talvez seja necessário desligar a coleta de métricas de solicitação de HTTP por meio das etapas a seguir:

1. Crie o  ` config.yaml `:

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml
   ```
   {: pre}
  
2. Edite o `config.yaml` e inclua a linha a seguir na matriz `spec.template.spec.containers.args`:

   ```
   --- filter.events=ContainerMetric, CounterEvent, ValueMetric          
   ```
   {: pre}

### Exemplo:

`config.yam` modificado:

```
  ...
  modelo:
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

O comando a seguir reconfiguraria e reiniciaria o pod do nó do trabalhador:

```
kubectl -n cf-monitoring apply -f config.yaml

```
{: pre}

Para obter mais informações sobre o exportador Firehose Prometheus, veja [Exportador Cloud Foundry Firehose Prometheus](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
