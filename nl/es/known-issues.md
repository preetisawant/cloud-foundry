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

# Problemas conocidos (limitaciones)
{: #known-issues}

## Inestabilidad debida al alto uso de CPU por parte del exportador Firehose Prometheus
{: #instabilityCPU-issue}

Los entornos CFEE incluyen un exportador de Prometheus Firehose para recopilar las métricas de Cloud Foundry en las solicitudes http y https _iniciar_ y _detener_. Un entorno CFEE con un alto número de solicitudes http puede hacer que el exportador de Prometheus firehose utilice una gran cantidad de CPU. Esto puede dar lugar a cierta inestabilidad en el entorno, ya que el pod del exportador de firehouse se ejecuta en uno de los nodos de trabajadores del panel de control de Cloud Foundry.

Puede determinar si el pod del exportador de firehose está teniendo un uso elevado de CPU, y potencialmente pueda provocar la inestabilidad en el entorno CFEE, mediante uno de los métodos siguientes: 
1.  Compruebe el uso general de la CPU del panel de control de CF a través de la página Visión general de CFEE para dicho entorno CFEE. Consulte un ejemplo ilustrativo de uso de CPU elevado a continuación:
![Uso elevado de CPU en Visión general](img/FirehoseExporterIssue_OverviewMetrics.png)

2. Compruebe el uso de CPU en la página _Uso de recursos > Aplicaciones_ y compruebe si hay un número de solicitudes de http inusualmente elevado. Consulte un ejemplo ilustrativo de uso de CPU elevado a continuación: ![Uso elevado de CPU en la página Uso de recursos](img/FirehoseExporterIssue_ResourceUsage.png)

3. Compruebe la consola de POD Grafana (iniciada desde la página _Supervisión_) que muestra el uso de CPU del pod de Firehose. Consulte un ejemplo ilustrativo de uso de CPU elevado a continuación:
![Uso elevado de CPU en la consola de Grafana](img/FirehoseExporterIssue_Grafana.png)

Si el exportador de cortafuegos está utilizando la CPU entre 0,5 y 0,7 (50-70%), y la CPU del panel de control general es alta, es posible que tenga que desactivar la recopilación de métricas siguiendo estos pasos:

1. Cree el archivo `config.yaml`:

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml
   ```
   {: pre}
  
2. Edite el archivo `config.yaml` y añada la línea siguiente en la matriz `spec.template.spec.containers.args`:

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```
   {: pre}

### Ejemplo

Archivo `config.yam` modificado:

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

El mandato siguiente reconfigurará y reiniciará el pod de nodo de trabajador:

```
kubectl -n cf-monitoring apply -f config.yaml

```
{: pre}

Para obtener más información sobre el exportador Firehose Prometheus, consulte [Exportador Firehose Prometheus de Cloud Foundry](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
