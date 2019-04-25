---

copyright:
  years: 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Anwendungen automatisch skalieren
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} verfügt über integrierte Unterstützung für die automatische Skalierung von Cloud Foundry-Anwendungen, um die Anzahl der Anwendungsinstanzen über die folgenden Verfahren automatisch anzupassen:  
  * Dynamische Skalierung auf der Basis von Metriken für die Anwendungsleistung 
  * Geplante Skalierung auf Zeitbasis 

Diese Funktion wird basierend auf dem Open-Source-Projekt [App-Autoscaler][autoscaler_project] von Cloud Foundry angeboten. Eine Einführung finden Sie im [Benutzerhandbuch][autoscaler_user_guide].  

## Automatische Skalierung über die CLI verwalten

Sie können das Plug-in für die Befehlszeilenschnittstelle von App-Autoscaler (kurz: AutoScaler-CLI) verwenden, um Richtlinien zu verwalten und Metriken sowie das Skalierungsprotokoll abzufragen.  

### AutoScaler-CLI installieren
Verwenden Sie den folgenden Befehl, um die `AutoScaler-CLI` zu installieren, die ein Plug-in der Cloud Foundry-CLI ist.   

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

Der gleiche Befehl kann für die Aktualisierung des Plug-ins für die `AutoScaler-CLI` auf die neueste Version verwendet werden, wenn das Plug-in bereits installiert ist.  

### AutoScaler-CLI verwenden

Wenn Sie sich bereits bei einer Cloud Foundry-Umgebung in {{site.data.keyword.Bluemix}} angemeldet haben und in Ihrem Bereich Anwendungen gemäß den Beschreibungen im [Leitfaden für die Bereitstellung von Apps][deploy_app] ausgeführt werden, führen Sie die folgenden Schritte aus, um eine Skalierungsrichtlinie für Ihre Anwendung zu erstellen sowie Metriken und das Skalierungsprotokoll abzufragen.  

 *  (Optional) Überprüfen Sie, ob der standardmäßig definierte API-Endpunkt für App-Autoscaler korrekt ist.   

    Wird der Cloud Foundry-API-Endpunkt als `api.<DOMAIN>` dargestellt, muss der API-Endpunkt für App-Autoscaler wie folgt lauten: `autoscaler.<DOMAIN>`.  
    Verwenden Sie den folgenden Befehl, um die Einstellung für den API-Endpunkt von App-Autoscaler zu überprüfen. 

    ```
    cf asa
    ```
    {:codeblock} 

    Ist der API-Endpunkt für App-Autoscaler falsch, müssen Sie ihn mit dem folgenden Befehl zurücksetzen: 

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  Erstellen Sie eine JSON-Richtliniendatei auf Ihrer lokalen Maschine.  

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    Mit der obigen Richtlinie wird die Skalierung auf der Basis der Speicherauslastung ausgelöst, wenn die definierten Schwellenwerte mindestens `120 Sekunden` lang nicht eingehalten werden. Informationen zum Erstellen einer eigenen Richtlinie für die automatische Skalierung finden Sie im [Cloud Foundry-Benutzerhandbuch für App-Autoscaler][autoscaler_user_guide]. 

*  Ordnen Sie die Richtlinie Ihrer Anwendung zu. 

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (Optional) Darüber hinaus können Sie die zuletzt zusammengefassten Metriken Ihrer Anwendung abfragen. App-Autoscaler unterstützt mehrere [Metriktypen][metric_type], aber nur die in Ihrer Richtlinie definierten Metriken können abgerufen werden, d. h. im obigen Beispiel `memoryutil`.   

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (Optional) Verwenden Sie den folgenden Befehl, um das Skalierungsprotokoll abzufragen: 

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    Weitere Optionen für die Verwendung der Befehlszeile sind im [Cloud Foundry-Leitfaden für das Plug-in der App-Autoscaler-CLI][autoscaler_cli] beschrieben.  


## Automatische Skalierung über die Stratos-Konsole verwalten 

Neben der Befehlszeilenschnittstelle können Sie die Einstellungen für die automatische Skalierung auch über die Stratos-Konsole verwalten.  

Wenn Sie [stratos][stratos] in Ihrer Instanz von {{site.data.keyword.cfee_full}} (CFEE) installiert haben, rufen Sie die Registerkarte **Auto-Scaling** im Anwendungsdashboard auf, um eine Übersicht über die Richtlinie für automatische Skalierung und die letzten Skalierungsereignisse anzuzeigen.
Klicken Sie auf ein beliebiges Symbol in einer beliebigen Kachel, um den Richtlinieneditor zu starten und die Richtlinie zu bearbeiten. 

Wenn keine Richtlinie für automatische Skalierung definiert ist, enthält die Übersichtsseite keine Informationen. Klicken Sie auf **Richtlinie erstellen**, um den Richtlinieneditor zu starten und eine Richtlinie zu erstellen. 

Es wird empfohlen, das [Cloud Foundry-Benutzerhandbuch für App-Autoscaler][autoscaler_user_guide] zu lesen, um die grundlegenden Konzepte zu verstehen und eine ordnungsgemäße Richtlinie für automatische Skalierung zu definieren.  

### Statistikdaten für Metriken

Nachdem Sie eine Richtlinie auf der Basis eines oder mehrerer ausgewählter Metriktypen definiert haben, können Sie die neuesten Metrikwerte und den Metrikverlauf der letzten 30 Minuten anzeigen.  

**Hinweis:** Die Metriken sind Daten, die über alle Anwendungsinstanzen hinweg gemittelt werden, und nicht Rohdaten von jeder Anwendungsinstanz. 
    
### Skalierungsprotokoll

Auf der Registerkarte **Protokoll** des Richtlinieneditors werden die Skalierungsaktionen angezeigt, die von der Richtlinie für automatische Skalierung ausgelöst und für Ihre Anwendung ausgeführt wurden. Es werden auch Fehlernachrichten durch Skalierungsfehler angezeigt. Sie können das Skalierungsprotokoll während der letzten 30 Tage abfragen.  


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]: https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
