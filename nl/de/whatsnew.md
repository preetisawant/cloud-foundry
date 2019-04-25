---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Neuerungen in IBM Cloud Foundry Enterprise Environment

In diesem Dokument wird beschrieben, was in jeder Version neu ist, die bis zu diesem Datum des {{site.data.keyword.cfee_full_notm}}-Service freigegeben wurde.

## Version 2.2.0
{: #v220}

_Releasedatum:_ 01.04.2019

CFEE V2.2.0 enthält die folgenden Versionen ihrer Komponenten: 
* Cloud Foundry: V2.7.1.15.5
* Cloud Foundry-API: V2.115.0
* CFEE-Buildpacks: V0.1.5
* IBM Kubernetes Service: Es wurde keine Versionsaktualisierung bereitgestellt. **Wichtig:** Es wird empfohlen, dass Sie den Kubernetes-Cluster von CFEE auf V1.13 aktualisieren, bevor Sie ein Update auf CFEE V2.2.0 ausführen. (Dies ist erforderlich, wenn die CFEE-Instanz in einem isolierten Netz betrieben wird.) 

Die folgenden Änderungen wurden in Version 2.2.0 des {{site.data.keyword.cfee_full_notm}}-Service (CFEE) bereitgestellt. Zum Aktualisieren Ihrer CFEE-Version rufen Sie die Seite **Aktualisierungen und Skalierung** in der CFEE-Benutzerschnittstelle auf und klicken Sie auf **Aktualisieren**: 

* Neue Option zum **Erstellen** einer CFEE-Instanz in einem Kubernetes-Cluster **mit mehreren Zonen**. CFEE-Instanzen, die in einem Cluster mit mehreren Zonen erstellt werden, verteilen Anwendungsinstanzen nicht nur über die Workerknoten innerhalb eines Rechenzentrums, sondern auch über mehrere Rechenzentren hinweg, wodurch Ihre Anwendungen widerstandsfähiger gegen Infrastrukturausfälle sind. Darüber hinaus können CFEE-Instanzen mit mehreren Zonen **skaliert** werden, indem in den aktuellen Zonen zusätzliche Zellen hinzugefügt oder vorhandene Zellen entfernt werden. Beachten Sie, dass Sie keine Zonen in einer CFEE-Instanz mit mehreren Zonen hinzufügen oder entfernen können, nachdem die CFEE-Instanz erstellt wurde. 
* Instanzen von CFEE V2.2.0 können jetzt [innerhalb eines **isolierten Netzes** betrieben werden](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). Beachten Sie Folgendes, wenn die CFEE-Instanz in den VLANs eines isolierten Netzes bereitgestellt wird: Einige Endpunkte (IP-Adressen) [müssen identifiziert und ordnungsgemäß weitergeleitet werden](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points), damit die CFEE-Instanz betriebsbereit ist. Für eine CFEE-Instanz ist ein Kubernetes-Cluster mit V1.13 erforderlich, damit sie in einem isolierten Netz funktioniert. 
* Neue Funktion zum Binden von (in einem CFEE-Bereich bereitgestellten) Anwendungen an Serviceinstanzen über das interne IBM Netz. Mit dieser Funktion können Services, die IBM Cloud Service Endpoint unterstützen, ohne Zugriff auf das öffentliche Internet genutzt werden. 
* Tools für **Überwachung**: 
    * Die Überwachungstools (Prometheus, Grafana und Alertmanager) werden nicht mehr standardmäßig bereitgestellt, wenn Sie eine CFEE-Instanz erstellen. In CFEE V2.2.0 werden Überwachungstools nur nach expliziter Aktivierung durch CFEE-Administratoren bereitgestellt. Außerdem werden die Überwachungstools, wenn sie aktiviert sind, nicht mehr auf den Workerknoten der CFEE-Steuerebene bereitgestellt. Sie werden auf ihren eigenen Workerknoten außerhalb der Steuerebene bereitgestellt. Für die Aktivierung und Bereitstellung von Überwachungstools rufen Sie die CFEE-Seite _Überwachung_ (im linken Navigationsfenster) auf und klicken Sie auf **Überwachung aktivieren**.  
    * Wenn Sie eine vorhandene CFEE-Instanz auf Version 2.2.0 aktualisieren, werden die bestehenden Überwachungstools aus der Steuerebene gelöscht. Alle vorhandenen angepassten Konfigurationen der Überwachungstools gehen verloren.  
    *  Neue Funktionalität zum Ersetzen der standardmäßigen [Alertmanager-Konfiguration](https://prometheus.io/docs/alerting/configuration/) durch eine angepasste Konfiguration, die Ihnen die Anpassung der Verarbeitung, Gruppierung und Benachrichtigungsweiterleitung von Alerts ermöglicht. Auf der Seite _Überwachung_ können Sie die Standardkonfigurationsdatei _herunterladen_ und eine Konfigurationsdatei aus Ihrem lokalen Dateisystem _hochladen_. Hier finden Sie ein [Beispiel](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml) für eine Konfigurationsdatei. 
* Neue Funktion zum Kennzeichnen von CFEE-Instanzen in der {{site.data.keyword.Bluemix_notm}}[-_Ressourcenliste_](https://cloud.ibm.com/resources) und in der CFEE-Benutzerschnittstelle. 
* Allgemeine Verbesserungen der Benutzererfahrung im [**Cloud Foundry-Dashboard**](https://cloud.ibm.com/dashboard/cloudfoundry/overview) von {{site.data.keyword.Bluemix_notm}}. Im _Cloud Foundry-Dashboard_ werden umfassende Ansichten von CFEE-Instanzen, Anwendungen und öffentlichen Services angezeigt, die CFEE-Bereichen über einen Alias hinzugefügt wurden.  

**Hinweis:** Bei der Erstellung einer neuen CFEE-Instanz ist der neue Plan **Eirini - Technische Vorschau** verfügbar. Der Plan ist unabhängig von der oben beschriebenen V2.2.0, die nur für den Plan _Standard_ gilt. Mit dem Plan 'Eirini - Technische Vorschau' können Sie eine CFEE-Instanz mit nativem Kubernetes als Container-Scheduler (anstelle von Diego) verwenden. Weitere Informationen finden Sie unter [Einführung für  Eirini - Technische Vorschau](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini). 

Eine Demonstration der Neuerungen in CFEE V2.1.0 finden Sie in diesem [kurzen Video](https://ibm.biz/CFEE-V220){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link"). 


## Version 2.1.1
{: #v211}

_Releasedatum:_ 20.03.2019

Die folgenden Änderungen wurden in Version 2.1.1 des {{site.data.keyword.cfee_full_notm}}-Service (CFEE) bereitgestellt. Zum Aktualisieren der CFEE-Version rufen Sie die Seite _Aktualisierungen und Skalierung_ in der CFEE-Benutzerschnittstelle auf:

* Es wurden Probleme behoben, die eine erfolgreiche Bereitstellung verhindern.  


## Version 2.1.0
{: #v210}

_Releasedatum:_ 20.02.2019

**Hinweis:** Sie können nur von Version **2.0.2** auf diese Version aktualisieren. Aktualisieren Sie auf Version 2.0.2, bevor Sie auf Version 2.1.0 aktualisieren. 

Die folgenden Änderungen wurden in Version 2.1.0 des {{site.data.keyword.cfee_full_notm}}-Service (CFEE) bereitgestellt. Zum Aktualisieren Ihrer CFEE-Version rufen Sie die Seite **Aktualisierungen und Skalierung** in der CFEE-Benutzerschnittstelle auf und klicken Sie auf **Aktualisieren**: 

* Neue Funktion für automatische Skalierung, die Cloud Foundry-Anwendungsinstanzen basierend auf angepassten Regeln automatisch skaliert. Auf die automatische Skalierung kann über die CLI und die Stratos-Konsole zugegriffen werden. Die Stratos-Konsole kann optional über die Seite _Übersicht_ in der CFEE-Benutzerschnittstelle installiert und gestartet werden. Wählen Sie auf der Seite _Anwendungen_ der Stratos-Konsole eine Anwendung aus und suchen Sie die Registerkarte **Auto-Scaling**. Klicken Sie auf *Richtlinie erstellen*, um den Editor für automatische Skalierung zu starten und die Skalierungsrichtlinie für die Zielanwendung zu definieren.
  Weitere Informationen finden Sie in der [Dokumentation zur automatischen Skalierung](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps). 
* Neue Funktion zum Verwalten von Buildpacks über die CFEE-Benutzerschnittstelle einschließlich Drag-and-drop-Positionierung eines Buildpacks in der Prioritätenliste. Die Funktion ist auf der neuen Seite **Buildpacks** der CFEE-Benutzerschnittstelle (nicht in der Stratos-Konsole) verfügbar. In dem Release können nur komprimierte Buildpackdateien mit einer Größe von maximal 1 MB über die Benutzerschnittstelle hinzugefügt oder aktualisiert werden. Komprimierte Buildpackdateien mit einer Größe über 1 MB können Sie über die Befehle `cf create-buildpack` und `cf update-buildpack` hochladen.  
* Neue Funktion zum Verwalten von Organisationskontingenten über die Benutzerschnittstelle, einschließlich der Visualisierung, welche Organisationen eine bestimmtes Kontingent verwenden. Die Funktion ist auf der neuen Seite **Kontingente** der CFEE-Benutzerschnittstelle (nicht in der Stratos-Konsole) verfügbar. Sie können neue Kontingente erstellen und vorhandene Kontingente bearbeiten. Sie können auch die Werte des Standardkontingents mit den Werten eines beliebigen vorhandenen Kontingents aktualisieren, indem Sie die Option **In Standard kopieren** im Menü des Kontingents aufrufen. 
* Eine neue Seite **Einführung** in der Benutzerschnittstelle führt Benutzer zu den wichtigsten Tasks, um die Umgebung einzurichten und zu verwenden. 
* **Tags** können einer CFEE-Instanz in der IBM Cloud-Ressourcenliste hinzugefügt werden. In der Ressourcenliste hinzugefügte Tags werden auch im Header der CFEE-Übersichtsseite angezeigt. 
* **Cloud Foundry** Version 2.7.21. 
* **Stratos**-Konsole mit Version 2.3.0, die ein Sicherheitspatch beinhaltet. Beachten Sie, dass die Version der Stratos-Konsole durch einfaches Aktualisieren der CFEE-Version nicht aktualisiert wird. Sie müssen die Stratos-Konsole (auf der CFEE-Übersichtsseite) löschen und erneut installieren. Dabei wird automatisch die neueste Version der Stratos-Konsole verwendet. 
* Benutzer können die Seite für Kubernetes-**Cluster** von CFEE über das Überlaufmenü auf der CFEE-Übersichtsseite ansteuern. 

**Hinweis:** Wenn Sie ein Update von einer Version 2.0.x auf CFEE V2.1.0 durchführen, erfolgt das Update über eine einzige Aktion _Aktualisieren_, die sowohl die Steuerebene als auch die Zellen nacheinander aktualisiert. Wenn Sie ein Update von einer Version 1.x.x durchführen, erfordert das Update zwei separate Aktionen _Aktualisieren_; eine (die erste) für die Aktualisierung der Steuerebene und eine für die Aktualisierung der Zellen. 

Eine Demonstration der Neuerungen in CFEE V2.1.0 finden Sie in diesem [kurzen Video](https://ibm.biz/CFEE-V210){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link"). 


## Version 2.0.2
{: #v202}

_Releasedatum:_ 08.02.2019

Die folgenden Änderungen wurden in Version 2.0.2 des {{site.data.keyword.cfee_full_notm}}-Service (CFEE) bereitgestellt. Zum Aktualisieren der CFEE-Version rufen Sie die Seite _Aktualisierungen und Skalierung_ in der CFEE-Benutzerschnittstelle auf:

* Es wurden Probleme behoben, die eine erfolgreiche Aktualisierung der Version verhindern. Diese Version ist eine Voraussetzung für die Aktualisierung auf Version **2.1.0**. 


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
