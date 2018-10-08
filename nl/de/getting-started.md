---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Lernprogramm 'Einführung'
{: #getting-started}

{{site.data.keyword.cfee_full}} ist eine Cloudplattform zum Hosten von Apps und Services in der Cloud. {{site.data.keyword.cfee_full_notm}} erleichtert die Skalierung von Anwendungen bei zunehmender Nutzung und vereinfacht Laufzeit, Middleware und Infrastruktur, sodass Sie sich auf die Entwicklung der Anwendungen konzentrieren können.
{: shortdesc}

In diesem Lernprogramm 'Einführung' erfahren Sie, wie eine {{site.data.keyword.cfee_full_notm}}-Instanz erstellt, Benutzer hinzugefügt, eine Organisation und Bereiche erstellt, Anwendungen bereitgestellt und diese an Services gebunden werden.

## Erklärung der Berechtigungen
{: #permissions}

Für die Arbeit mit Instanzen von {{site.data.keyword.cfee_full_notm}} müssen Servicebenutzer über die korrekten Berechtigungen verfügen. Weitere Informationen finden Sie unter [Berechtigungen](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Schritt 1: Sicherstellen, dass mit dem {{site.data.keyword.Bluemix_notm}}-Konto Infrastrukturressourcen erstellt werden können
{: #accountprep-environment}

CFEE-Instanzen werden auf Infrastrukturressourcen bereitgestellt, bei denen es sich um Kubernetes-Workerknoten eines Kubernetes-Service handelt.  [Bereiten Sie Ihr IBM Cloud-Konto vor](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html), um sicherzustellen, dass mit ihm die Infrastrukturressourcen erstellt werden können, die für eine CFEE-Instanz erforderlich sind.

## Schritt 2: Erstellen der CFEE-Instanz
{: #creating-environment}

Stellen Sie vor dem Erstellen der CFEE-Instanz sicher, dass Sie sich in dem {{site.data.keyword.Bluemix_notm}}-Konto befinden, in dem Sie die Umgebung erstellen möchten, und dass Sie über die erforderlichen Zugriffsrichtlinien verfügen (siehe Schritt 1 oben).

1.  Öffnen Sie den {{site.data.keyword.Bluemix_notm}}-[Katalog](https://console.bluemix.net/catalog).

2.  Suchen Sie den {{site.data.keyword.cfee_full_notm}}-Service im Katalog und klicken Sie auf ihn, um die Übersichtsseite für den Service anzuzeigen.

3.  Auf der ersten Seite für die Erstellung wird eine Übersicht über die wichtigsten Funktionen des Service angezeigt. Klicken Sie auf **Weiter**.

4.  Konfigurieren Sie die CFEE-Instanz anhand der nachfolgenden Angaben:
    * Wählen Sie einen Plan aus (die Planverfügbarkeit kann während der Betaversion eingeschränkt sein).
    * Geben Sie einen **Namen** für die Serviceinstanz ein.
    * Wählen Sie die **Position** aus, an der die Serviceinstanz bereitgestellt werden soll. In der Liste der [verfügbaren Bereitstellungspositionen und Rechenzentren](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") können Sie nach geographischen Regionen nach CFEE und unterstützenden Services suchen. 
    * Wählen Sie die **Anzahl der Zellen** für die Cloud Foundry-Umgebung aus.
    * Wählen Sie den **Maschinentyp** aus, mit dem die Größe der Cloud-Foundry-Zellen (CPU und Speicher) festgelegt wird.
    * Wählen Sie eine **Ressourcengruppe** aus, in der die Umgebung zusammengefasst wird. Nur die Ressourcengruppen, auf die Sie im aktuellen IBM Cloud-Konto zugreifen können, werden in der Dropdown-Liste _Ressourcengruppen_ aufgelistet; dies bedeutet, dass Sie über die Berechtigung für den Zugriff auf mindestens eine Ressourcengruppe in dem Konto verfügen müssen, um eine CFEE-Instanz erstellen zu können.

5.  In den Feldern von **Compose for PostgreSQL** wählen Sie eine der öffentlichen Organisationen und dann einen der Bereiche aus, die in dieser Organisation verfügbar sind. Die Compose for PostgreSQL-Instanz wird im ausgewählten Bereich bereitgestellt. Der Compose for PostgreSQL-Service ist eine erforderliche Abhängigkeit des CFEE-Service.

**Anmerkung:** Nur Organisationen an der Position, an der Sie die CFEE-Instanz (siehe Schritt 4 oben) bereitstellen möchten und auf die Sie Zugriff haben, stehen für die Auswahl zur Verfügung.  Innerhalb einer bestimmten Organisation stehen nur Bereiche für die Auswahl zur Verfügung, für die Sie _Entwickler_-Zugriff haben. 

6.  Optional können Sie den Abschnitt **Infrastruktur** öffnen, um die Eigenschaften des Kubernetes-Clusters anzuzeigen, von dem die CFEE-Instanz unterstützt wird. Beachten Sie, dass der Wert für **Anzahl von Workerknoten** der Anzahl der Zellen plus 2 entspricht (zwei der bereitgestellten Kubernetes-Workerknoten unterstützen die CFEE-Steuerebene).
Der Kubernetes-Cluster, in dem die Umgebung bereitgestellt wird, wird im {{site.data.keyword.Bluemix_notm}} [Dashboard ](https://console.bluemix.net/dashboard/apps/) angezeigt. Weitere Informationen hierzu finden Sie in der [Kubernetes-Servicedokumentation](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov).

**Anmerkung:** Es wird empfohlen, das VLAN-Spanning zu aktivieren, wenn die Workerknoten im Kubernetes-Cluster in unterschiedlichen Teilnetzen bereitgestellt werden.  Workerknoten in unterschiedlichen Teilnetzen können die Konnektivität untereinander verhindern, wenn VLAN-Spanning inaktiviert ist.  Weitere Informationen finden Sie in der Dokumentation zum [VLAN-Spanning](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning).

7.  In der **Bestellübersicht** rechts auf der Seite werden die Kosten für die CFEE-Instanz und die Hilfsservices zusammen mit der geschätzten monatlichen Summe angezeigt.

8.  Klicken Sie auf **Erstellen**; daraufhin wird das Dashboard der Umgebung geöffnet und Fortschritt sowie Status der Erstellung werden angezeigt.

9.  Sobald die Bereitstellung gestartet ist, wird die Umgebung im {{site.data.keyword.Bluemix_notm}}-Dashboard und auch in den [Dashboards der Cloud Foundry-Umgebungen](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments) angezeigt.  Der Status gibt an, wann die Bereitstellung abgeschlossen ist.

Durch den automatisierten Prozess, von dem die Umgebung erstellt wird, wird die Infrastruktur in einem Kubernetes-Cluster bereitgestellt und so konfiguriert, dass sie verwendet werden kann. Der Prozess dauert zwischen 90 und 120 Minuten.

Sobald Sie die Umgebung erfolgreich erstellt haben, erhalten Sie mehrere E-Mails, die die Bereitstellung der CFEE und der unterstützenden Services bestätigen, sowie E-Mails, die Sie über den Status der entsprechenden Aufträge informieren.

## Schritt 3: Erstellen von Organisationen und Bereichen

Nach dem Erstellen der {{site.data.keyword.cfee_full_notm}}-Instanz finden Sie in [Organisationen und Bereiche erstellen](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html) Informationen zum Strukturieren der Umgebung durch die Erstellung von Organisationen und Bereichen. Die Apps in einer {{site.data.keyword.cfee_full_notm}}-Umgebung können in bestimmten Bereichen verwendet werden. Ein Bereich ist innerhalb einer bestimmten Organisation vorhanden. Mitglieder einer Organisation nutzen einen Kontingentplan, Anwendungen, Serviceinstanzen und angepasste Domänen gemeinsam.

**Hinweis:** Die Seite _Cloud Foundry-Organisationen_, die über das Menü **_Verwalten > Konto > Cloud Foundry-Organisationen_** im obersten IBM Cloud-Header verfügbar ist, ist ausschließlich für öffentliche IBM Cloud-Organisationen konzipiert, **nicht für CFEE-Organisationen**. CFEE-Organisationen werden über die Seite _Organisationen_ der jeweiligen CFEE-Instanz verwaltet.  Öffnen Sie die CFEE-Benutzerschnittstelle und klicken Sie auf die Seite **_Organisationen_**, um Organisationen für diese CFEE-Instanz zu erstellen und zu verwalten.

## Schritt 4: Hinzufügen von Benutzern zu Organisationen und Bereichen

[Fügen Sie Benutzer](https://console.bluemix.net/docs/cloud-foundry/add-users.html) zu diesen Organisationen und Bereichen mithilfe bestimmter Rollenzuordnungen hinzu, von denen ihre Zugriffsebene gesteuert wird.  Damit Benutzer als Mitglieder von Organisationen und Bereichen in einer CFEE-Instanz hinzugefügt werden können, müssen diese Benutzer vorher über Zugriff auf diese CFEE-Instanz verfügen. Informationen hierzu finden Sie in [Berechtigungen](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Schritt 5: Bereitstellen und Anzeigen von Anwendungen

Wenn  Sie bereit sind, können Sie mit dem [Bereitstellen der Anwendung](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle beginnen.  Zeigen Sie die Liste der bereitgestellten Anwendungen in der Benutzerschnittstelle an, entweder im Kontext eines bestimmten CFEE-Bereichs oder global für alle CFEE-Instanzen.  Sie können Anwendungen in diesen Ansichten auch starten, stoppen oder löschen.

## Schritt 6: Mit Services arbeiten

[Services erstellen](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#creating-services_inspace) oder [Vorhandene Services hinzufügen](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#adding-services_inspace), verfügbar im IBM Cloud-Konto.  Sobald eine Serviceinstanz in einem CFEE-Bereich verfügbar ist, können Sie sie an CFEE-Anwendungen binden, die in diesem Bereich bereitgestellt sind.

## Schritt 7: Binden von Anwendungen an Serviceinstanzen

[Binden Sie die App](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#bind_services) an einen Aliasnamen der Serviceinstanz, um die Funktionen des Service zu verwenden.

Ist Ihnen das [Cloud Foundry-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/overview) bekannt? Hier finden Sie eine konsolidierte Ansicht aller Anwendungen und Services in {{site.data.keyword.Bluemix_notm}}, sowohl _Public_ als auch _Enterprise_ (CFEE).  Im Cloud Foundry-Dashboard klicken Sie im linken Navigationsfenster auf _Public_, um die öffentlichen Anwendungen und Services anzuzeigen, die im IBM Cloud-Konto verfügbar sind.  Klicken Sie auf _Enterprise_, um alle CFEE-Umgebungen, in CFEE-Bereichen bereitgestellten Anwendungen und für CFEE-Bereiche verfügbare Services anzuzeigen.
{:tip}

## Schritt 8: Installieren der Stratos-Konsole zur Verwaltung von Anwendungen (optional)

Die Stratos-Konsole ist ein webbasiertes Open-Source-Tool für die Arbeit mit Cloud Foundry. Die Stratos-Konsolenanwendung kann optional in einer bestimmten CFEE-Umgebung installiert und verwendet werden, um ihre Organisationen, Bereiche und Anwendungen zu verwalten.

Benutzer mit der Rolle eines IBM Cloud-Administrators oder -Bearbeiters in der CFEE-Instanz können die Stratos-Konsolenanwendung in dieser CFEE-Instanz installieren.

Gehen Sie wie folgt vor, um die Stratos-Konsolenanwendung zu installieren:

1. Öffnen Sie die CFEE-Instanz, in der Sie die Stratos-Konsole installieren möchten.
2. Klicken Sie auf der Übersichtsseite auf **Stratos-Konsole installieren**. Die Schaltfläche wird nur Benutzern mit Administrator- oder Bearbeiterberechtigung für diese CFEE-Instanz angezeigt.
3. Wählen Sie im Dialog 'Stratos-Konsole installieren' eine Installationsoption aus. Sie können die Stratos-Konsolenanwendung entweder auf der CFEE-Steuerebene oder in einer der Zellen installieren. Wählen Sie eine Version der Stratos-Konsole und die Anzahl der Instanzen der Anwendung aus, die installiert werden sollen. Wenn Sie die Stratos-Konsolenanwendung in einer Zelle installieren, werden Sie aufgefordert, die Organisation und den Bereich für die Bereitstellung der Anwendung anzugeben.
4. Klicken Sie auf **Installieren**.

Die Installation der Anwendung dauert ca. fünf Minuten. Sobald die Installation abgeschlossen ist, wird auf der Übersichtsseite die Schaltfläche **Stratos-Konsole** anstatt der Schaltfläche _Stratos-Konsole installieren_ angezeigt. Mithilfe der Schaltfläche _Stratos-Konsole_ wird die Konsole gestartet; sie ist für alle Benutzer verfügbar, die über Zugriff auf die CFEE-Instanz verfügen. Durch die Zuweisungen von Organisations- und Bereichsmitgliedschaften kann eingeschränkt werden, was ein Benutzer in der Stratos-Konsole sehen und verwalten kann.

Gehen Sie wie folgt vor, um die Stratos-Konsole zu starten:

1. Öffnen Sie die CFEE-Instanz, in der die Stratos-Konsole installiert wurde.
2. Klicken Sie auf der Übersichtsseite auf **Stratos-Konsole**.
3. Die Stratos-Konsole wird daraufhin in einer separaten Browserregisterkarte geöffnet. Wenn Sie die Konsole zum ersten Mal öffnen, werden Sie aufgefordert, zwei aufeinanderfolgende Warnungen aufgrund von selbst signierten Zertifikaten zu akzeptieren.
4. Klicken Sie auf **Anmelden**, um die Konsole zu öffnen. Hierfür sind keine Berechtigungsnachweise erforderlich, da von der Anwendung Ihre {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweise verwendet werden.

Informationen zu den CFEE-APIs sind in der CFEE-[API-Dokumentation](https://console.bluemix.net/apidocs/cfaas){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") verfügbar.
{:tip}
