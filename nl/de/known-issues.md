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

# Bekannte Probleme (Einschränkungen)
{: #known-issues}

## Instabilität aufgrund hoher CPU-Belastung durch die Exportkomponente Firehose Prometheus
{: #instabilityCPU-issue}

CFEE-Umgebungen umfassen eine Prometheus Firehose-Exportkomponente zur Erfassung von Cloud Foundry-Metriken in den HTTP- und HTTPS-Anforderungen _start_ und _stop_. Eine CFEE-Umgebung mit einer hohen Anzahl von HTTP-Anforderungen kann dazu führen, dass die Exportkomponente Prometheus Firehose einen großen CPU-Anteil belegt. Dies kann zu einer gewissen Instabilität in der Umgebung führen, da der Firehose Export-Pod auf einem der Workerknoten der Cloud Foundry-Steuerebene ausgeführt wird.

Mit einer der folgenden Methoden können Sie feststellen, ob der Firehose Export-Pod eine hohe CPU-Auslastung und möglicherweise eine Instabilität in der CFEE-Umgebung verursacht: 
1.  Überprüfen Sie die Gesamt-CPU-Nutzung der CF-Steuerebene über die CFEE-Übersichtsseite für diese CFEE-Umgebung. Sehen Sie sich dazu ein veranschaulichendes Beispiel einer hohen CPU-Nutzung an: ![Hohe CPU-Nutzung auf der Übersichtsseite](img/FirehoseExporterIssue_OverviewMetrics.png)

2. Überprüfen Sie die CPU-Belastung auf der Seite _Ressourcennutzung > Anwendungen_ und sehen Sie nach, ob eine ungewöhnlich hohe Anzahl an HTTP-Anforderungen vorhanden ist. Sehen Sie sich dazu ein veranschaulichendes Beispiel einer hohen CPU-Nutzung an: ![Hohe CPU-Nutzung auf der Seite 'Ressourcennutzung'](img/FirehoseExporterIssue_ResourceUsage.png)

3. Überprüfen Sie die POD Grafana-Konsole (wird über die Seite _Überwachung_ gestartet), in der die CPU-Auslastung für den Firehouse-Pod angezeigt wird. Sehen Sie sich dazu ein veranschaulichendes Beispiel einer hohen CPU-Nutzung an: ![Hohe CPU-Nutzung in der Grafana-Konsole](img/FirehoseExporterIssue_Grafana.png)

Wenn die Firehouse-Exportkomponente eine CPU-Auslastung von 0,5 bis 0,7 (50-70%) hat und die Gesamt-CPU-Auslastung der Steuerebene hoch ist, kann es notwendig sein, die Metrikenerfassung für HTTP-Anforderungen zu inaktivieren. Führen Sie dazu die folgenden Schritte aus:

1. Erstellen Sie `config.yaml`:

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml
   ```
   {: pre}
  
2. Bearbeiten Sie `config.yaml` und fügen Sie die folgende Zeile im Array `spec.template.spec.containers.args` hinzu:

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```
   {: pre}

### Beispiel

Geänderte Datei `config.yam`:

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

Der folgende Befehl würde den Workerknoten-Pod neu konfigurieren und erneut starten:

```
kubectl -n cf-monitoring apply -f config.yaml

```
{: pre}

Weitere Informationen zur Exportkomponente Firehose Prometheus finden Sie unter [Cloud Foundry Firehose Prometheus-Exportkomponente](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
