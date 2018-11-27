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

# Problèmes connus (limitations)
{: #known-issues}

## Instabilité due à une utilisation élevée de l'unité centrale par l'exportateur Firehose Prometheus
{: #instabilityCPU-issue}

Les environnements CFEE comprennent un exportateur Prometheus Firehose pour la collecte de métriques Cloud Foundry sur les demandes de _démarrage_ et d'_arrêt_ http et https. Un environnement CFEE comprenant un nombre élevé de demandes http peut inciter l'exportateur Prometheus Firehose à utiliser un volume élevé d'unité centrale. Cela peut générer une certaine instabilité dans l'environnement dans la mesure où le pod de l'exportateur Firehose s'exécute sur l'un des noeuds worker du plan de contrôle Cloud Foundry.

Vous pouvez déterminer si le pod de l'exportateur Firehose utilise un volume élevé d'unité centrale et génère potentiellement une certaine instabilité dans l'environnement CFEE en utilisant l'une des méthodes suivantes : 
1.  Vérifiez l'utilisation d'unité centrale globale du plan de contrôle CF sur la page de présentation de CFEE pour cet environnement CFEE. Reportez-vous à l'exemple ci-dessous illustrant une utilisation élevée de l'unité centrale : ![Utilisation élevée d'unité centrale présentée sur la page de présentation](img/FirehoseExporterIssue_OverviewMetrics.png)

2. Consultez l'utilisation de l'unité centrale sur la page _Utilisation des ressources > Applications_ et vérifiez la présence d'un nombre de demandes http anormalement élevé. Reportez-vous à l'exemple ci-dessous illustrant une utilisation élevée de l'unité centrale : ![Utilisation élevée d'unité centrale présentée sur la page d'utilisation des ressources](img/FirehoseExporterIssue_ResourceUsage.png)

3. Vérifiez la console POD Grafana (démarrée à partir de la page _Surveillance_) qui affiche l'utilisation de l'unité centrale pour le pod Firehose. Reportez-vous à l'exemple ci-dessous illustrant une utilisation élevée de l'unité centrale : ![Utilisation élevée d'unité centrale présentée dans la console Grafana](img/FirehoseExporterIssue_Grafana.png)

Si l'exportateur Firehose utilise entre 0,5 et 0,7 (50-70 %) d'unité centrale et que l'unité centrale globale du plan de contrôle est élevée, vous devrez peut-être désactiver la collecte de métriques de demande http en procédant comme suit :

1. Créez le fichier `config.yaml` :

   ```
   kubectl -n cf-monitoring get deployment firehose-exporter -f yaml > config.yaml
   ```
   {: pre}
  
2. Editez le fichier `config.yaml` et ajoutez la ligne suivante dans le tableau `spec.template.spec.containers.args` :

   ```
   - --filter.events=ContainerMetric,CounterEvent,ValueMetric          
   ```
   {: pre}

### Exemple

Fichier `config.yam` modifié :

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

La commande suivante reconfigure et redémarre le pod de noeud worker :

```
kubectl -n cf-monitoring apply -f config.yaml

```
{: pre}

Pour plus d'informations sur l'exportateur Firehose Prometheus, voir [Cloud Foundry Firehose Prometheus exporter](https://github.com/bosh-prometheus/firehose_exporter){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
