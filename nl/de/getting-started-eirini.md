---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Einführung für Eirini - Technische Vorschau
{: #getting-started-eirini}

{{site.data.keyword.cfee_full}} (CFEE) ist eine Cloudplattform zum Hosten von Apps und Services in der Cloud. {{site.data.keyword.cfee_full_notm}} erleichtert die Skalierung von Anwendungen bei zunehmender Nutzung und vereinfacht Laufzeit, Middleware und Infrastruktur, sodass Sie sich auf die Entwicklung der Anwendungen konzentrieren können.
{: shortdesc}

In diesem Lernprogramm 'Einführung' erfahren Sie, wie mit dem Plan 'Eirini - Technische Vorschau' eine {{site.data.keyword.cfee_full_notm}}-Instanz erstellt, Benutzer hinzugefügt, eine Organisation und Bereiche erstellt, Anwendungen bereitgestellt und diese an Services gebunden werden. Weitere Informationen zum Inkubatorprojekt Eirini der Cloud Foundry Foundation finden Sie unter [Projekt Eirini](https://www.cloudfoundry.org/project-eirini/). 

## Erklärung der Berechtigungen
{: #permissions}

Vor der Erstellung von Instanzen von {{site.data.keyword.cfee_full_notm}} benötigen Sie die korrekten Zugriffsrichtlinien. Weitere Informationen finden Sie unter [Berechtigungen](https://cloud.ibm.com/docs/cloud-foundry/permissions.html).

## Schritt 1: Sicherstellen, dass mit dem {{site.data.keyword.Bluemix_notm}}-Konto Infrastrukturressourcen erstellt werden können
{: #accountprep-environment}

CFEE-Instanzen werden über den Kubernetes-Service in Kubernetes-Workerknoten bereitgestellt.  [Bereiten Sie Ihr IBM Cloud-Konto vor](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html), um sicherzustellen, dass mit ihm die Infrastrukturressourcen erstellt werden können, die für eine CFEE-Instanz erforderlich sind.

## Schritt 2: Erstellen der CFEE-Instanz
{: #create-environment}

Stellen Sie vor dem Erstellen der CFEE-Instanz sicher, dass Sie sich in dem {{site.data.keyword.Bluemix_notm}}-Konto befinden, in dem Sie die Umgebung erstellen möchten, und dass Sie über die erforderlichen Zugriffsrichtlinien verfügen (siehe Schritt 1 oben).

1.  Öffnen Sie den {{site.data.keyword.Bluemix_notm}}-[Katalog](https://cloud.ibm.com/catalog). 

2.  Suchen Sie den {{site.data.keyword.cfee_full_notm}}-Service im Katalog und klicken Sie auf ihn, um die Übersichtsseite für den Service anzuzeigen.  Auf dieser ersten Seite wird eine Übersicht über die wichtigsten Funktionen des Service angezeigt. Klicken Sie auf **Weiter**.

3.  Konfigurieren der zu erstellenden CFEE-Instanz:
    * Wählen Sie den Plan _Eirini - Technische Vorschau_ aus. 
    * Geben Sie einen **Namen** für die CFEE-Instanz ein.
    * Wählen Sie eine **Ressourcengruppe** aus, in der die Umgebung zusammengefasst wird. Nur die Ressourcengruppen, auf die Sie im aktuellen IBM Cloud-Konto zugreifen können, werden in der Dropdown-Liste _Ressourcengruppen_ aufgelistet; dies bedeutet, dass Sie über die Berechtigung für den Zugriff auf mindestens eine Ressourcengruppe in dem Konto verfügen müssen, um eine CFEE-Instanz erstellen zu können.
    * Wählen Sie die **Geografie** und den **Standort** aus, in denen die Instanz bereitgestellt werden soll. In der Liste der [verfügbaren Bereitstellungsstandorte und Rechenzentren](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") können Sie nach geographischen Regionen nach CFEE und unterstützenden Services suchen. 

4. CFEE-Instanzen werden in einem Kubernetes-Cluster bereitgestellt. Cloud Foundry-Zellen werden innerhalb der Workerzonen im Kubernetes-Cluster bereitgestellt. Sie können den Standort, die Hardware und die Verschlüsselung des Clusters konfigurieren: 
    * Wählen Sie die Hardwareisolierung für den Kubernetes-Cluster aus:    
      * _Virtuell gemeinsam genutzt_: Die Infrastrukturressourcen im Cluster, z. B. der Hypervisor und die physische Hardware, werden von Ihnen und anderen IBM Kunden gemeinsam genutzt, aber jeden Workerknoten nutzen Sie als einziger Tenant. 
      * _Virtuell dediziert_: Die Workerknoten im Cluster werden auf Infrastruktur gehostet, die Ihrem Konto zugeordnet ist. 
    * Die Daten im Cluster werden standardmäßig verschlüsselt. Sie haben die Möglichkeit, die _Verschlüsselung der lokalen Platte_ zu inaktivieren. 
    * Wählen Sie die **Geografie** und **Region** aus, in denen der Kubernetes-Cluster bereitgestellt wird. 
    * Wählen Sie die **Zone** aus, in der die Kubernetes-Workerknoten bereitgestellt werden. Verfügbare VLANs werden automatisch für die ausgewählten Zonen abgerufen. Wenn keine VLANs verfügbar sind, werden sie automatisch erstellt. Ab CFEE V2.2.0 können CFEE-Instanzen hinter einem **isolierten Netz** ausgeführt werden. Sie können eine CFEE-Instanz in einem isolierten Netz bereitstellen, indem Sie private VLANs in dem isolierten Netz auswählen. Nachdem die CFEE-Instanz erstellt wurde, muss der Netzadministrator die IP-Adressen für die Compose for PostgreSQL- und Cloudant Object Storage-Instanzen der CFEE-Instanz sowie für die Application Load Balancer ([ALBs](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress)) des Kubernetes-Clusters in das isolierte Netz weiterleiten, damit die CFEE-Instanz betriebsbereit ist. 
    
    Nachdem die CFEE-Instanz erstellt wurde, wird der Kubernetes-Cluster, in dem die Umgebung bereitgestellt wird, (wie jede andere Ressource in Ihrem IBM Cloud-Konto) im {{site.data.keyword.Bluemix_notm}}-[Dashboard](https://cloud.ibm.com/dashboard/apps/) angezeigt. Weitere Informationen hierzu finden Sie in der [Kubernetes-Servicedokumentation](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov).

5.  Konfigurieren der CFEE-Kapazität:
    * Wählen Sie die **Anzahl der Zellen** für die CFEE aus. Dies sind die Anwendungszellen, die die Anwendungen hosten, die in der CFEE-Instanz bereitgestellt werden.   
    * Wählen Sie die **Knotengröße** aus, die die Kapazität der Cloud Foundry-Zellen (CPU und Speicher) bestimmt. 
    
    Zusätzlich zu den Anwendungszellen, die Sie oben angeben, werden zusätzliche _Zellen der Steuerebene_ erzeugt und für den Betrieb und die Steuerung der Cloud Foundry-Plattform in Ihrer CFEE-Instanz reserviert.  

    **Anmerkung:** Es wird empfohlen, das VLAN-Spanning zu aktivieren, wenn die Workerknoten im Kubernetes-Cluster in unterschiedlichen Teilnetzen bereitgestellt werden.  Workerknoten in unterschiedlichen Teilnetzen können die Konnektivität untereinander verhindern, wenn VLAN-Spanning inaktiviert ist.  Weitere Informationen finden Sie in der Dokumentation zum [VLAN-Spanning](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning).
    
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

## Schritt 3: Erstellen von Organisationen und Bereichen
{: #create-orgsandspaces}

Nach dem Erstellen der {{site.data.keyword.cfee_full_notm}}-Instanz finden Sie in [Organisationen und Bereiche erstellen](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) Informationen zum Strukturieren der Umgebung durch die Erstellung von Organisationen und Bereichen. Die Apps in einer {{site.data.keyword.cfee_full_notm}}-Umgebung können in bestimmten Bereichen verwendet werden. Ein Bereich ist innerhalb einer bestimmten Organisation vorhanden. Mitglieder einer Organisation nutzen einen Kontingentplan, Anwendungen, Serviceinstanzen und angepasste Domänen gemeinsam.

Wenn Sie eine Organisation erstellen, ordnen Sie ihr ein Kontingent zu. Das Kontingent definiert Begrenzungen für die Ressourcen (Hauptspeicher, CPU etc.), die für diese Organisation verfügbar sind. Sie können zu einem späteren Zeitpunkt ein anderes Kontingent zuordnen. Es gibt eine Reihe vorkonfigurierter Kontingente, die in jeder CFEE-Instanz verfügbar sind, aber Sie können auch eigene angepasste Kontingente auf der Seite **Kontingente** der CFEE-Benutzerschnittstelle erstellen. Sie können ein angepasstes Kontingent zum _Standardkontingent_ machen, indem Sie die Aktion _In Standard kopieren_ im Menü des Kontingents ausführen. Dadurch werden die Werte des angepassten Kontingents in das Standardkontingent kopiert. 

**Hinweis:** Die Seite _Cloud Foundry-Organisationen_, die über das Menü **_Verwalten > Konto > Cloud Foundry-Organisationen_** im obersten IBM Cloud-Header verfügbar ist, ist ausschließlich für öffentliche IBM Cloud-Organisationen konzipiert, **nicht für CFEE-Organisationen**. CFEE-Organisationen werden über die Seite _Organisationen_ der jeweiligen CFEE-Instanz verwaltet.  Öffnen Sie die CFEE-Benutzerschnittstelle und klicken Sie auf die Seite **_Organisationen_**, um Organisationen für diese CFEE-Instanz zu erstellen und zu verwalten.

## Schritt 4: Hinzufügen von Benutzern zu Organisationen und Bereichen
{: #add-users}

[Fügen Sie Benutzer](https://cloud.ibm.com/docs/cloud-foundry/add-users.html) zu diesen Organisationen und Bereichen mithilfe bestimmter Rollenzuordnungen hinzu, von denen ihre Zugriffsebene gesteuert wird.  Damit Benutzer als Mitglieder von Organisationen und Bereichen in einer CFEE-Instanz hinzugefügt werden können, müssen diese Benutzer vorher über Zugriff auf diese CFEE-Instanz verfügen. Informationen hierzu finden Sie in [Berechtigungen](https://cloud.ibm.com/docs/cloud-foundry/permissions.html).

## Schritt 5: Bereitstellen und Anzeigen von Anwendungen
{: #deploy-apps}

Wenn  Sie bereit sind, können Sie mit dem [Bereitstellen der Anwendung](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle beginnen.  Zeigen Sie die Liste der bereitgestellten Anwendungen in der Benutzerschnittstelle an, entweder im Kontext eines bestimmten CFEE-Bereichs oder global für alle CFEE-Instanzen.  Sie können Anwendungen in diesen Ansichten auch starten, stoppen oder löschen.

## Schritt 6: Erstellen oder Hinzufügen von IBM Cloud-Serviceinstanzen zu CFEE-Bereichen
{: #service-instances}

[Services erstellen](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) oder [Vorhandene Services hinzufügen](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace), verfügbar im IBM Cloud-Konto.  Sobald eine Serviceinstanz in einem CFEE-Bereich verfügbar ist, können Sie sie an CFEE-Anwendungen binden, die in diesem Bereich bereitgestellt sind.

## Schritt 7: Binden von Anwendungen an Serviceinstanzen
{: #bind-apps}

[Binden Sie die App](https://console.bluemix.net/docs/cloud-foundry/binding.html) an einen Aliasnamen der Serviceinstanz, um die Funktionen des Service zu verwenden.

Im [Cloud Foundry-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") wird eine konsolidierte Ansicht aller Anwendungen und Services angezeigt, sowohl der *öffentlichen* als auch der *unternehmensspezifischen*.  Im Cloud Foundry-Dashboard klicken Sie im linken Navigationsfenster auf *Public*, um die öffentlichen Anwendungen und Services anzuzeigen, die im IBM Cloud-Konto verfügbar sind.  Klicken Sie auf *Enterprise*, um alle CFEE-Umgebungen, in CFEE-Bereichen bereitgestellten Anwendungen und für CFEE-Bereiche verfügbare Services anzuzeigen.
{:tip}

## Schritt 8: Installieren der Stratos-Konsole zur Verwaltung von Anwendungen (optional)
{: #install-stratos}

Die Stratos-Konsole ist ein webbasiertes Open-Source-Tool für die Arbeit mit Cloud Foundry. Die Stratos-Konsolenanwendung kann optional in einer bestimmten CFEE-Umgebung installiert und verwendet werden, um ihre Organisationen, Bereiche und Anwendungen zu verwalten.

Benutzer mit der Rolle eines IBM Cloud-Administrators oder -Bearbeiters in der CFEE-Instanz können die Stratos-Konsolenanwendung in dieser CFEE-Instanz installieren.

Gehen Sie wie folgt vor, um die Stratos-Konsolenanwendung zu installieren:

1. Öffnen Sie die CFEE-Instanz, in der Sie die Stratos-Konsole installieren möchten.
2. Klicken Sie auf der Übersichtsseite auf **Stratos-Konsole installieren**. Die Schaltfläche wird nur Benutzern mit Administrator- oder Bearbeiterberechtigung für diese CFEE-Instanz angezeigt.
3. Wählen Sie im Dialog 'Stratos-Konsole installieren' eine Installationsoption aus. Sie können die Stratos-Anwendung entweder in einer Cloud Foundry-Zelle oder im Kubernetes-Cluster installieren. Wählen Sie eine Version der Stratos-Konsole und die Anzahl der Instanzen der Anwendung aus, die installiert werden sollen. Wenn Sie die Stratos-Konsolenanwendung in einer Cloud Foundry-Zelle installieren, werden Sie aufgefordert, die Organisation und den Bereich für die Bereitstellung der Anwendung anzugeben.
4. Klicken Sie auf **Installieren**.

Die Installation der Anwendung dauert ca. fünf Minuten. Sobald die Installation abgeschlossen ist, wird auf der Übersichtsseite die Schaltfläche **Stratos-Konsole** anstatt der Schaltfläche _Stratos-Konsole installieren_ angezeigt. Mithilfe der Schaltfläche _Stratos-Konsole_ wird die Konsole gestartet; sie ist für alle Benutzer verfügbar, die über Zugriff auf die CFEE-Instanz verfügen. Durch die Zuweisungen von Organisations- und Bereichsmitgliedschaften kann eingeschränkt werden, was ein Benutzer in der Stratos-Konsole sehen und verwalten kann.

Gehen Sie wie folgt vor, um die Stratos-Konsole zu starten:

1. Öffnen Sie die CFEE-Instanz, in der die Stratos-Konsole installiert wurde.
2. Klicken Sie auf der Übersichtsseite auf **Stratos-Konsole**.
3. Die Stratos-Konsole wird daraufhin in einer separaten Browserregisterkarte geöffnet. Wenn Sie die Konsole zum ersten Mal öffnen, werden Sie aufgefordert, zwei aufeinanderfolgende Warnungen aufgrund von selbst signierten Zertifikaten zu akzeptieren.
4. Klicken Sie auf **Anmelden**, um die Konsole zu öffnen. Hierfür sind keine Berechtigungsnachweise erforderlich, da von der Anwendung Ihre {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweise verwendet werden.


## Zusätzliche Ressourcen
{: #additional-resources}

In einer CFEE-Instanz können Sie eine Reihe von Verwaltungstasks mit `ibmcloud CFEE`-Befehlen in der Befehlszeilenschnittstelle ausführen. Mit den Befehlen können Sie Informationen zu einer CFEE-Instanz abrufen und die zugehörigen Organisationen und Bereiche verwalten. Informationen hierzu finden Sie unter [CFEE-Befehlsreferenz für IBM Cloud-Befehlszeilenschnittstelle](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").

Videos mit umfassenden Diskussionen und Vorführungen zu verschiedenen CFEE-Themen finden Sie in der [CFEE-Videowiedergabeliste](https://ibm.biz/CFEE-Playlist){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").

Informationen zu den CFEE-APIs finden Sie in der [API-Dokumentation](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") der CFEE-Instanz.
