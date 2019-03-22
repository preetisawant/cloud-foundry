---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Neuerungen in IBM Cloud Foundry Enterprise Environment

In diesem Dokument wird beschrieben, was in jeder Version neu ist, die bis zu diesem Datum des {{site.data.keyword.cfee_full_notm}}-Service freigegeben wurde.


## Version 2.0.1
{: #v201}

_Releasedatum:_ 10.01.2019

Die folgenden Änderungen wurden in Version 2.0.1 des {{site.data.keyword.cfee_full_notm}}-Service (CFEE) bereitgestellt. Zum Aktualisieren der CFEE-Version rufen Sie die Seite _Aktualisierungen und Skalierung_ in der CFEE-Benutzerschnittstelle auf:

* Ein Problem wurde behoben, das die korrekte Ausführung angepasster Domänen verhinderte. 
* Ein Problem wurde behoben, das bewirkte, dass beim Abrufen neuer Metriken keine Organisationsmetriken verfügbar waren. 


## Version 2.0.0
{: #v200}

_Releasedatum:_ 13.12.2018

Die folgenden Änderungen wurden in Version 2.0.9 des {{site.data.keyword.cfee_full_notm}}-Service (CFEE) bereitgestellt. Zum Aktualisieren der CFEE-Version rufen Sie die Seite _Aktualisierungen und Skalierung_ in der CFEE-Benutzerschnittstelle auf:

* Verbesserte Ausfallsicherheit der CFEE-Versionsaktualisierung. 
* Verbesserungen der operationalen Verfügbarkeit und Ausfallsicherheit von CFEE-Instanzen. 
* Clientseitige Zertifikate für einen sichereren Zugriff auf Anwendungen, die es dem Server ermöglichen, den Anwendungszugriff nur zertifizierten Clients zu erteilen. 
* Bei der Erstellung einer CFEE-Serviceinstanz werden der unterstützende Kubernetes-Cluster und Cloud Object Storage-Service nun in derselben Ressourcengruppe erstellt wie die CFEE-Serviceinstanz (nicht mehr unter der Ressourcengruppe 'Standard'). 
* Sicherheitspatch. 
* Verbesserungen an der `ibmcloud cfee`-Befehlszeilenschnittstelle: 
    * Neue Befehle für das Erstellen einer IBM Cloud-Serviceinstanz auf der Basis eines CFEE-Bereichs und Hinzufügen dieser Instanz zu diesem CFEE-Bereich (`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`). 
    * Neue Befehle für die Skalierung der Kapazität einer CFEE (`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`). 
    * Verbesserungen des Befehls zum Verwalten von CFEE-Instanzen (`ibmcloud cfee environments`). 
    
      Aktualisieren Sie die ibmcloud-Befehlszeilenschnittstelle (`ibmcloud update`), um auf diese Befehlserweiterungen zuzugreifen. Mit `ibmcloud cfee -help` können Sie zusätzliche Details aufrufen. 
      
**Anmerkung**: Für die Aktualisierung einer CFEE-Instanz auf Version 2.0.0 ist nur eine einzelne _update_-Aktion erforderlich, mit der sowohl die Steuerebene als auch die Zellen aktualisiert werden. Für die CFEE-Steuerebene und die Zellen sind keine separaten Aktualisierungen erforderlich. 


## Version 1.1.2
{: #v112}

_Releasedatum:_ 07.12.2018

Die folgenden Änderungen wurden in Version 1.1.2 des {{site.data.keyword.cfee_full_notm}}-Service bereitgestellt: 
* Neue Rechenzentren in Chennai (che01) und Mailand (mil01) stehen nun für die Bereitstellung von CFEE-Instanzen zur Verfügung. 
* Sicherheitspatch. 

## Version 1.1.1
{: #v111}

_Releasedatum:_ 28.11.2018

Die folgenden Änderungen wurden in Version 1.1.1 des {{site.data.keyword.cfee_full_notm}}-Service bereitgestellt: 
* Sicherheitspatch. 
   
## Version 1.1.0
{: #v110}

_Releasedatum:_ 16.11.2018

Die folgenden Änderungen wurden in Version 1.1.0 des {{site.data.keyword.cfee_full_notm}}-Service bereitgestellt: 

* Neue Funktionen:
   * CFEE-Instanzen können auf [virtuellen dedizierten](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) Kubernetes-Workerknoten in einer Infrastruktur bereitgestellt werden, die Ihrem IBM Cloud-Konto zugeordnet ist. 
   * Ein neues Rechenzentrum in Tokio (tok05) steht für die Bereitstellung von CFEE-Instanzen zur Verfügung. 
   * [Aktualisierung](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) einer CFEE-Instanz auf eine neue Version.
   * [Skalierung](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) der Kapazität einer CFEE-Instanz durch Hinzufügen oder Löschen von Cloud Foundry-Zellen.
   * [Audit](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) für Cloud Foundry-Aktivitäten durch Integration einer automatisch konfigurierten IBM Cloud Activity Tracker-Serviceinstanz.
   * Persistente Cloud Foundry-[Protokollierungsereignisse](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) mithilfe einer automatisch konfigurierten IBM Cloud Log Analysis-Serviceinstanz.
   * Ansicht 'Statusprüfung', in der der Betriebsstatus der CFEE-Komponenten angezeigt wird. 
   * Neue Befehle zum Ausführen von CFEE-bezogenen Aktionen in der Befehlszeilenschnittstelle (Command Line Interface, CLI): 
     * Die Befehle `ibmcloud cfee create`, `ibmcloud cfee create-locations` und `ibmcloud cfee create-status` zum Erstellen von CFEE-Instanzen über die Befehlszeilenschnittstelle, Abrufen einer Liste mit verfügbaren Rechenzentren, in denen eine CFEE bereitgestellt werden kann, und Überprüfen des Bereitstellungsstatus einer erstellten CFEE. 
     * Die [Befehle](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) `ibmcloud cfee create-permission-get` und `ibmcloud cfee create-permission-set` zum Abrufen und Festlegen der Berechtigungen, die für die Erstellung von CFEE-Instanzen erforderlich sind. Durch die Befehle wird die Einstellung der Berechtigungen für den CFEE-Service und für die erforderlichen unterstützenden Services zusammengefasst und vereinfacht.
     * Befehl `ibmcloud catalog blacklist` zum Vereinfachen der [Sichtbarkeitssteuerung](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) für die IBM Cloud-Services für Benutzer in einem IBM Cloud-Konto.

* Behobene Probleme:
   *  Behobenes Problem: Sporadisch auftretender Fehler beim Zugriff auf Zellenmetriken
<br/>   
Eine Demonstration der Neuerungen in CFEE Version 1.1.0 sehen Sie in diesem [Kurzvideo](https://ibm.biz/CFEE-V110){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").  Weitere Videos zu unterschiedlichen CFEE-Themen finden Sie in der [CFEE-Videowiedergabeliste](https://ibm.biz/CFEE-Playlist){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link"). 
