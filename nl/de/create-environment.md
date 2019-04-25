---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Umgebung erstellen
{: #create-environment}

## Voraussetzungen
* Stellen Sie sicher, dass Sie sich in dem {{site.data.keyword.Bluemix_notm}}-Konto befinden, in dem Sie die Umgebung erstellen möchten. 
* Stellen Sie sicher, dass Sie die korrekten [Berechtigungen](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html) haben, bevor Sie Instanzen von {{site.data.keyword.cfee_full_notm}} erstellen.  
* [Bereiten Sie Ihr IBM Cloud-Konto vor](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html), um sicherzustellen, dass mit ihm die Infrastrukturressourcen erstellt werden können, die für eine CFEE-Instanz erforderlich sind (CFEE-Instanzen werden über den Kubernetes-Service in Kubernetes-Workerknoten bereitgestellt).   

## CFEE-Instanz erstellen
1.  Öffnen Sie den {{site.data.keyword.Bluemix_notm}}-[Katalog](https://cloud.ibm.com/catalog). 

2.  Suchen Sie den {{site.data.keyword.cfee_full_notm}}-Service im Katalog und klicken Sie auf ihn, um die Übersichtsseite für den Service anzuzeigen.  Auf dieser ersten Seite wird eine Übersicht über die wichtigsten Funktionen des Service angezeigt. Klicken Sie auf **Weiter**.

3.  Konfigurieren der zu erstellenden CFEE-Instanz:
    * Wählen Sie einen Plan aus. Im Abschnitt [Eirini - Technische Vorschau](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) finden Sie eine Beschreibung der Einschränkungen dieses Plans. 
    * Geben Sie einen **Namen** für die CFEE-Instanz ein.
    * Wählen Sie eine **Ressourcengruppe** aus, in der die Umgebung zusammengefasst wird. Nur die Ressourcengruppen, auf die Sie im aktuellen IBM Cloud-Konto zugreifen können, werden in der Dropdown-Liste _Ressourcengruppen_ aufgelistet; dies bedeutet, dass Sie über die Berechtigung für den Zugriff auf mindestens eine Ressourcengruppe in dem Konto verfügen müssen, um eine CFEE-Instanz erstellen zu können.
    * Wählen Sie die **Geografie** und den **Standort** aus, in denen die Instanz bereitgestellt werden soll. In der Liste der [verfügbaren Bereitstellungsstandorte und Rechenzentren](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") können Sie nach geographischen Regionen nach CFEE und unterstützenden Services suchen. 

4. CFEE-Instanzen werden in einem Kubernetes-Cluster bereitgestellt. Cloud Foundry-Zellen werden innerhalb der Workerzonen im Kubernetes-Cluster bereitgestellt. Sie können den Standort, die Hardware und die Verschlüsselung des Clusters konfigurieren: 
    * Wählen Sie die Hardwareisolierung für den Kubernetes-Cluster aus:    
      * _Virtuell gemeinsam genutzt_: Die Infrastrukturressourcen im Cluster, z. B. der Hypervisor und die physische Hardware, werden von Ihnen und anderen IBM Kunden gemeinsam genutzt, aber jeden Workerknoten nutzen Sie als einziger Tenant. 
      * _Virtuell dediziert_: Die Workerknoten im Cluster werden auf Infrastruktur gehostet, die Ihrem Konto zugeordnet ist. 
    * Die Daten im Cluster werden standardmäßig verschlüsselt. Sie haben die Möglichkeit, die _Verschlüsselung der lokalen Platte_ zu inaktivieren. 
    * Wählen Sie die **Geografie** und **Region** aus, in denen der Kubernetes-Cluster bereitgestellt wird. 
    * Wählen Sie die **Zonen** aus, in denen die Kubernetes-Workerknoten bereitgestellt werden. Sie haben die Möglichkeit, die Workerknoten in derselben Zone (**Eine Zone**) oder in mehreren Zonen (**Mehrere Zonen**) bereitzustellen. **Beachten Sie,** dass für die Erstellung einer CFEE-Instanz mit mehreren Zonen [VLAN-Spanning](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning) erforderlich ist. Diese Funktion wird auch unterstützt, wenn das {{site.data.keyword.Bluemix_notm}}-Konto für [VRF aktiviert](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) ist. 
    
    Verfügbare VLANs werden automatisch für die ausgewählten Zonen abgerufen. Wenn keine VLANs verfügbar sind, werden sie automatisch erstellt. 
    
    **Hinweis: Bereitstellung in einem isolierten Netz:** Sie können VLANs in einem isolierten Netz als Ziel verwenden. Wird die CFEE-Instanz in einem isolierten Netz erstellt, müssen die Richtlinien in dem isolierten Netz (z. B. Calico-Richtlinien oder VRA-Regeln) den GESAMTEN ausgehenden Zugriff der CFEE-Instanz zulassen, damit die CFEE-Instanz erfolgreich bereitgestellt werden kann. Sobald die CFEE-Instanz erstellt wurde, können die Beschränkungen für den ausgehenden Zugriff wiedereingesetzt werden, mit Ausnahme des ausgehenden Zugriffs auf bestimmte Services und Mikroservices in der IBM Cloud. Weitere Informationen finden Sie in der Dokumentation [Betrieb in einem isolierten Netz](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). 
    
    Nachdem die CFEE-Instanz erstellt wurde, wird der Kubernetes-Cluster, in dem die Umgebung bereitgestellt wird, (wie jede andere Ressource in Ihrem IBM Cloud-Konto) im {{site.data.keyword.Bluemix_notm}}-[Dashboard](https://https://cloud.ibm.com/catalog/dashboard/apps/) angezeigt. Weitere Informationen hierzu finden Sie in der [Kubernetes-Servicedokumentation](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov).

5.  Konfigurieren der CFEE-Kapazität:
    * Wählen Sie die **Anzahl der Zellen** für die CFEE aus. Dies sind die Anwendungszellen, die die Anwendungen hosten, die in der CFEE-Instanz bereitgestellt werden.   
    * Wählen Sie die **Knotengröße** aus, die die Kapazität der Cloud Foundry-Zellen (CPU und Speicher) bestimmt. 
    
    Zusätzlich zu den Anwendungszellen, die Sie oben angeben, werden zusätzliche _Zellen der Steuerebene_ erzeugt und für den Betrieb und die Steuerung der Cloud Foundry-Plattform in Ihrer CFEE-Instanz reserviert.  

    **Anmerkung:** Es wird empfohlen, das VLAN-Spanning zu aktivieren, wenn die Workerknoten im Kubernetes-Cluster in unterschiedlichen Teilnetzen bereitgestellt werden.  Workerknoten in unterschiedlichen Teilnetzen können die Konnektivität untereinander verhindern, wenn VLAN-Spanning inaktiviert ist.  Weitere Informationen finden Sie in der Dokumentation zum [VLAN-Spanning](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning).

6.  In den Feldern von **Compose for PostgreSQL** wählen Sie eine der öffentlichen Organisationen und dann einen der Bereiche aus, die in dieser Organisation verfügbar sind. Die Compose for PostgreSQL-Instanz wird im ausgewählten Bereich bereitgestellt. Der Compose for PostgreSQL-Service ist eine erforderliche Abhängigkeit des CFEE-Service.

    **Anmerkung:** Unter _Compose for PostgreSQL_ stehen nur Organisationen an dem Standort, an dem Sie die CFEE-Instanz (siehe Schritt 4 oben) bereitstellen möchten und auf den Sie Zugriff haben, für die Auswahl zur Verfügung.  Innerhalb einer bestimmten Organisation stehen nur Bereiche für die Auswahl zur Verfügung, für die Sie _Entwickler_-Zugriff haben. 

7.  In der **Bestellübersicht** rechts auf der Seite werden die Kosten für die CFEE-Instanz und die Hilfsservices zusammen mit der geschätzten monatlichen Summe angezeigt.

8.  Klicken Sie auf **Erstellen**; daraufhin wird das Dashboard der Umgebung geöffnet und Fortschritt sowie Status der Erstellung werden angezeigt.

**Anmerkung:** Nach dem Starten des Erstellungsprozesses wird eine Tabellenzeile für CFEE im {{site.data.keyword.Bluemix_notm}}-Dashboard, in der _Ressourcenliste_ und im [Dashboard der Cloud Foundry-Umgebungen](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments) angezeigt.  Der Status in der Tabellenzeile gibt an, wann die Erstellung abgeschlossen ist.

Durch den automatisierten Prozess, von dem die Umgebung erstellt wird, wird die Infrastruktur in einem Kubernetes-Cluster bereitgestellt und so konfiguriert, dass sie verwendet werden kann. Der Prozess dauert zwischen 90 und 120 Minuten.

Sobald die CFEE erstellt ist, erhalten Sie mehrere E-Mails, die die Bereitstellung der CFEE und der unterstützenden Services bestätigen, sowie E-Mails, die Sie über den Status der entsprechenden Aufträge informieren.

Wenn Sie eine CFEE-Instanz erstellen, werden drei zusätzliche unterstützende Serviceinstanzen im IBM Cloud-Konto erstellt. Diese unterstützenden Serviceinstanzen werden nach dem CFEE-Instanznamen benannt. So werden bei der Erstellung einer CFEE insgesamt vier Serviceinstanzen im IBM Cloud-Konto erstellt:
* CFEE-Instanz ("_cfeename_").
* Kubernetes-Cluster ("_cfeename_-cluster"). Der Cluster stellt die Infrastruktur bereit, in der die CFEE-Instanz bereitgestellt wird.
* Cloud Object Storage-Instanz ("_cfeename_-cos"). Die Instanz wird zum Speichern von Daten verwendet, die während der Erstellung der CFEE-Anwendungscontainer generiert wurden (z. B. hochgeladene Anwendungspakete, Buildpacks und kompilierte ausführbare Dateien).
* Compose for PosgreSQL-Instanz ("_cfeename_-postgres"). Die Instanz wird zum Speichern von Cloud Foundry-Daten für die CFEE-Instanz verwendet (zum Beispiel die Protokollierung der Anwendungsbereitstellung sowie der Start- und Stoppereignisse oder das Aufbewahren der Datensätze der CFEE-Benutzermitgliedschaft, -Organisationen, -Bereiche, -Anwendungen und -Serviceverbindungen). 

## Plan 'Eirini - Technische Vorschau'
{: #eirini}

 Mit dem Plan 'Eirini - Technische Vorschau' können Sie eine CFEE-Instanz mit nativem Kubernetes als Container-Scheduler (anstelle von Diego) verwenden. Der Kubernetes-Scheduler wird in der CFEE-Instanz genutzt, um Apps in der Cloud Foundry-Anwendungslaufzeit bereitzustellen und auszuführen, Benutzer hinzuzufügen, eine Organisation und Bereiche zu erstellen, Apps bereitzustellen und diese Apps an Services zu binden. Weitere Informationen zum Inkubatorprojekt Eirini der Cloud Foundry Foundation finden Sie in der Dokumentation zum [Projekt Eirini](https://www.cloudfoundry.org/project-eirini/). Die folgenden Einschränkungen gelten für CFEE-Instanzen, die mit dem Plan 'Eirini - Technische Vorschau' erstellt werden: 
 
* Kubernetes mit `containerd` wird nicht unterstützt. Es werden nur Kubernetes-Versionen unterstützt, die Docker anstelle von `containerd`verwenden. Die neueste Version von IBM Container Service (IKS), die Docker unterstützt, ist V1.10. 
* Cloud Foundry SSH wird nicht unterstützt. 
* `cf push` von Docker-Images wird nicht unterstützt. 
* Das native Eirini-Staging von Kubernetes wird nicht unterstützt. Mit dem Plan 'Eirini - Technische Vorschau' erstellte CFEE-Instanzen verwenden Eirini für die Ausführung von Apps, jedoch nicht für das Staging von Apps. Für das Staging von Apps werden weiterhin Diego-Zellen verwendet. 
* Der Neustart bestimmter App-Instanzen (`cf restart-app-instance`) wird nicht unterstützt. 

 
