---

copyright:
  years: 2018
lastupdated: "2018-08-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Überwachung
{: #monitoring}

Die Überwachung einer {{site.data.keyword.cfee_full}}-Instanz und der zugehörigen unterstützten Infrastruktur wird durch ein Open-Source-Toolset unterstützt, das aus Prometheus und Grafana besteht.  Die Lösung ermöglicht das Analysieren, Visualisieren und Verwalten von Alerts für Metriken in der Cloud Foundry-Umgebung.  Für die Überwachung stehen drei Webkonsolen zur Verfügung: Eine Grafana-Konsole, eine Prometheus-Konsole und eine Prometheus Alert Manager-Konsole.

**Hinweis:** Für den Zugriff auf die Überwachungsfunktion in einer {{site.data.keyword.cfee_full}}-Instanz ist die Rolle _Administrator_ oder _Bearbeiter_ in dem Kubernetes-Cluster erforderlich, der die CFEE-Instanz unterstützt.  Der Standardname des Kubernetes-Clusters, der eine CFEE-Instanz unterstützt, lautet _`<CFEEname>`-cluster_.

## Prometheus
{: #prometheus}

Prometheus ist ein Open-Source-Toolkit für Systemüberwachung und Alertausgabe. Seit der Gründung im Jahr 2012 haben viele Unternehmen und Organisationen Prometheus übernommen und das Projekt verfügt über eine sehr aktive Entwickler- und Benutzer-Community.
Es handelt sich um ein eigenständiges Open-Source-Projekt, das unabhängig von Unternehmen gepflegt wird. Um dies zu betonen und die Governance-Struktur des Projekts zu verdeutlichen, wurde Prometheus 2016 nach Kubernetes als zweites gehostetes Projekt in die Cloud Native Computing Foundation aufgenommen. Weitere Informationen finden Sie in der [Prometheus-Dokumentation](https://prometheus.io/docs/introduction/overview/).

Das Ökosystem von Prometheus besteht aus mehreren Komponenten, von denen viele optional sind:

* Der wichtigste Prometheus-Server für das Scraping und Speichern der Zeitreihendaten.</li>
* Der [Alert-Manager](https://prometheus.io/docs/alerting/alertmanager/) zur Verarbeitung der Alerts.</li>
* Unterschiedliche Exportkomponente für besondere Zwecke, wie zum Beispiel Knotenexportprogramme, Blackbox-Exportkomponenten, etc.</li>
* Ein Push-Gateway zur Unterstützung von kurzlebigen Jobs.</li>

Prometheus erfasst Metriken aus instrumentierten Jobs entweder direkt oder über ein intermediäres Push-Gateway für kurzlebige Jobs. Dabei werden alle erfassten Stichproben lokal gespeichert und Regeln für diese Daten ausgeführt, um neue Zeitreihen aus vorhandenen Daten zu aggregieren und aufzuzeichnen oder um Alerts zu generieren.

## Grafana
{: #grafana}

Grafana ist eine Open-Source-Analyseplattform für alle Metriken, die von Prometheus erfasst werden. Die im Cluster bereitgestellte Grafana-Version ist bereits für die Verwendung der zugrunde liegenden Prometheus-Datenbank konfiguriert. Auch einige aussagekräftige Grafana-Dashboards sind enthalten.  Weitere Informationen finden Sie in der [Grafana-Dokumentation](http://docs.grafana.org/guides/getting_started/).

## Einführung in die Überwachung
{: #gettingStarted_monitor}

Die Komponenten Prometheus und Grafana, aus denen die Überwachungslösung besteht, sind in der Kubernetes Infrastruktur vorinstalliert, die die CFEE-Instanz unterstützt.  Für den Zugriff auf die Überwachungstools ist eine Weiterleitung zu den Ports der Prometheus-, Prometheus Alert Manager- und Grafana-Server erforderlich.  Diese wird über die Kubernetes-Befehlszeilenschnittstelle festgelegt.
Im Folgenden werden Sie durch die Schritte für die Installation der erforderlichen Benutzerschnittstellen, für die Weiterleitung der Server-Ports und das Starten der Konsolen geführt.

**Hinweis:** Die folgenden Anweisungen sind auch in der {{site.data.keyword.cfee_full}}-Benutzerschnittstelle verfügbar.  Öffnen Sie die Benutzerschnittstelle der CFEE-Instanz und klicken Sie im linken Navigationsbereich auf **Überwachung**, um die aufgeführten Anweisungen anzuzeigen.

### Voraussetzungen

1. Überprüfen Sie Ihre [Zugriffsrichtlinien](https://console.bluemix.net/iam/#/users), um sicherzustellen, dass Sie zumindest über die Rolle eines Anzeigeberechtigten für den Kubernetes-Cluster verfügen, der die Umgebung unterstützt.
2. Installieren Sie die [IBM Cloud-Befehlszeilenschnittstelle](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
3. Installieren Sie die [Kubernetes-Befehlszeilenschnittstelle](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  Wenn Sie bereits über eine Kubernetes-Befehlszeilenschnittstelle verfügen, wird empfohlen, die aktuelle Version zu installieren.
4. Installieren Sie das Plug-in für den Container-Service:
```
    ibmcloud plugin install container-service -r Bluemix
```

### Auf den Kubernetes-Cluster zugreifen

1. Melden Sie sich am IBM Cloud-Konto an:

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}

  Wenn Sie über eine föderierte ID verfügen, verwenden Sie für die Anmeldung an der IBM Cloud-Befehlszeilenschnittstelle __ibmcloud login -sso__.

2. Geben Sie die IBM Cloud Container Service-Region an, in der Sie arbeiten möchten (zum Beispiel us-south):

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}

3. Legen Sie den Kontext des Clusters in der Befehlszeilenschnittstelle fest:

  a. Rufen Sie den Befehl zum Festlegen der Umgebungsvariablen und Download der Kubernetes-Konfigurationsdateien ab:

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}

  b. Legen Sie einen Wert für die Umgebungsvariable KUBECONFIG fest. Kopieren Sie die Ausgabe des vorherigen Befehls und fügen Sie sie in das Terminal ein. Die Befehlsausgabe sieht in etwa wie folgt aus: __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### Weiterleitung für Server-Ports einrichten
4. Richten Sie die Portweiterleitung im Kubernetes-Cluster für die Pods ein, von denen Prometheus, Prometheus Alert Manager und Grafana ausgeführt wird. Auf diese Art können Sie die Überwachungsmetriken über den Proxy auf der lokalen Maschine hosten (localhost):

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000'
  ```
  {: pre}

### Überwachungskonsolen auf lokalem Web-Proxy starten

5. Starten Sie die Grafana-Konsole, um Analysen zu ausgewählten Metriken anzuzeigen.  Die Grafana-Standarddashboards sind in der CFEE-Instanz enthalten. Diese Standarddashboards sind interaktiv und bieten eine Ansicht der Infrastruktur, die zum Hosten der CFEE-Instanz verwendet wird. (Kubernetes-Cluster). Klicken Sie beim Starten der Grafana-Konsole oben in der Grafana-Konsole auf die Schaltfläche **Home**, um eines der vorab bereitgestellten Dashboards auszuwählen (siehe Liste unten), in der die entsprechenden Metriken grafisch dargestellt werden:

   In Grafana lauten der Standardbenutzername `admin` und das Standardkennwort `admin`. Es wird empfohlen, sich mit dem Benutzernamen und Kennwort `admin` anzumelden und anschließend neue Berechtigungsnachweise festzulegen:

     [Grafana-Konsole starten](https://localhost:3000)

   Die folgenden Standarddashboards werden mit der CFEE-Instanz bereitgestellt und sind im Dropdown-Menü _Home_ verfügbar.

   Dashboards für die Kubernetes-Infrastruktur, die die CFEE-Umgebung unterstützt:
   - Dashboard _Kubernetes-Kapazitätsplanung_
        - Zeigt die Kapazität der Kubernetes-Infrastruktur an.
   - Dashboard _Kubernetes-Clusterzustand_
        - Zeigt den Zustand des Kubernetes-Clusters an.
   - Dashboard _Kubernetes-Clusterstatus_
        - Zeigt den Status des Kubernetes-Clusters an.
   - Dashboard _Kubernetes-Ressourcenanforderungen_
        - Zeigt die Verwendung von CPU und Speicher sowie andere Parameter des Kubernetes-Clusters an.
   - Dashboard _Knoten_
        - Zeigt Details für jeden Workerknoten des Kubernetes-Clusters an.
   - Dashboard _Pods_
        - Zeigt Details für jeden Pod an, der im Kubernetes-Clusters ausgeführt wird.
   - Dashboard _Replikatgruppe_
        - Zeigt den Status der Kubernetes-Replikatgruppe an.
   - Dashboard _Bereitstellung_
        - Zeigt den Status der Kubernetes-Bereitstellung an.

   Cloud Foundry-Dashboards:
   - Dashboard _CF: Zellenkapazität_
        - Zeigt den allgemeinen Status der Cloud Foundry-Zellen an, in denen die Cloud Foundry-Anwendungen bereitgestellt werden.
   - Dashboard _CF: Router_
        - Zeigt den Status des Cloud Foundry-Routers an, der in Ihrer CFEE-Umgebung ausgeführt wird.
   - Dashboard _CF: Diego-Zelle_
        - Zeigt den Status der Cloud Foundry-Zellen und Diego-Komponenten an.

6. Optional können Sie auch die Prometheus-Konsole zum Anzeigen der vom Prometheus-Server erfassten Rohdaten sowie Prometheus Alert Manager zum Verwalten der vom Prometheus-Server gesendeten Alerts starten:

     [Prometheus-Server starten](https://localhost:9090)

     [Prometheus Alert Manager-Server starten](https://localhost:9093)
