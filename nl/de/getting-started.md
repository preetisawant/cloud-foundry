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

# Lernprogramm 'Einführung'
{: #getting-started}

{{site.data.keyword.cfee_full}} (CFEE) ist eine Cloudplattform zum Hosten von Apps und Services in der Cloud. {{site.data.keyword.cfee_full_notm}} erleichtert die Skalierung von Anwendungen bei zunehmender Nutzung und vereinfacht Laufzeit, Middleware und Infrastruktur, sodass Sie sich auf die Entwicklung der Anwendungen konzentrieren können.
{: shortdesc}

In diesem Lernprogramm 'Einführung' erfahren Sie, wie eine {{site.data.keyword.cfee_full_notm}}-Instanz erstellt, Benutzer hinzugefügt, eine Organisation und Bereiche erstellt, Anwendungen bereitgestellt und diese an Services gebunden werden.

**Hinweis:** Die folgenden Schritte gelten für CFEE-Instanzen, die mit dem Plan **Standard** erstellt wurden. Wenn diese CFEE-Instanz mit dem Plan **Eirini - Technische Vorschau** erstellt wurde, führen Sie **nur die Schritte 1 bis 6** und den Schritt **11** aus. Die in den Schritten 8 bis 11 beschriebenen Funktionen werden im Plan _Eirini - Technische Vorschau_ nicht unterstützt. Siehe [Einführung für Eirini - Technische Vorschau](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).
Mit dem Plan _Eirini - Technische Vorschau_ können Sie eine CFEE-Instanz mit nativem Kubernetes als Container-Scheduler (anstelle von Diego) verwenden. Der Kubernetes-Scheduler wird in der CFEE-Instanz genutzt, um Apps in der Cloud Foundry-Anwendungslaufzeit bereitzustellen und auszuführen, Benutzer hinzuzufügen, eine Organisation und Bereiche zu erstellen, Apps bereitzustellen und diese Apps an Services zu binden.  

## Schritt 1: Erstellen der CFEE-Instanz
{: #create-environment}

Sie können eine Instanz von {{site.data.keyword.cfee_full_notm}} (CFEE) über den {{site.data.keyword.Bluemix_notm}}-Katalog erstellen. Lesen Sie vor der Erstellung der CFEE-Instanz die Dokumentation [Umgebung erstellen](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment). Sie enthält Hinweise zur Vorbereitung Ihres {{site.data.keyword.Bluemix_notm}}-Kontos, zur Überprüfung der Berechtigungen und zu den Schritten zur Erstellung der CFEE-Instanz. 


## Schritt 2: Erstellen von Organisationen und Bereichen
{: #create-orgsandspaces}

Nach dem Erstellen der {{site.data.keyword.cfee_full_notm}}-Instanz finden Sie in [Organisationen und Bereiche erstellen](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) Informationen zum Strukturieren der Umgebung durch die Erstellung von Organisationen und Bereichen. Die Apps in einer {{site.data.keyword.cfee_full_notm}}-Umgebung können in bestimmten Bereichen verwendet werden. Ein Bereich ist innerhalb einer bestimmten Organisation vorhanden. Mitglieder einer Organisation nutzen einen Kontingentplan, Anwendungen, Serviceinstanzen und angepasste Domänen gemeinsam.

Wenn Sie eine Organisation erstellen, ordnen Sie ihr ein Kontingent zu. Das Kontingent definiert Begrenzungen für die Ressourcen (Hauptspeicher, CPU etc.), die für diese Organisation verfügbar sind. Sie können zu einem späteren Zeitpunkt ein anderes Kontingent zuordnen. Es gibt eine Reihe vorkonfigurierter Kontingente, die in jeder CFEE-Instanz verfügbar sind, aber Sie können auch eigene angepasste Kontingente auf der Seite **Kontingente** der CFEE-Benutzerschnittstelle erstellen. Sie können ein angepasstes Kontingent zum _Standardkontingent_ machen, indem Sie die Aktion _In Standard kopieren_ im Menü des Kontingents ausführen. Dadurch werden die Werte des angepassten Kontingents in das Standardkontingent kopiert. 

**Hinweis:** Die Seite _Cloud Foundry-Organisationen_, die über das Menü **_Verwalten > Konto > Cloud Foundry-Organisationen_** im obersten IBM Cloud-Header verfügbar ist, ist ausschließlich für öffentliche IBM Cloud-Organisationen konzipiert, **nicht für CFEE-Organisationen**. CFEE-Organisationen werden über die Seite _Organisationen_ der jeweiligen CFEE-Instanz verwaltet.  Öffnen Sie die CFEE-Benutzerschnittstelle und klicken Sie auf die Seite **_Organisationen_**, um Organisationen für diese CFEE-Instanz zu erstellen und zu verwalten.

## Schritt 3: Hinzufügen von Benutzern zu Organisationen und Bereichen
{: #add-users}

[Fügen Sie Benutzer](https://console.bluemix.net/docs/cloud-foundry/add-users.html) zu diesen Organisationen und Bereichen mithilfe bestimmter Rollenzuordnungen hinzu, von denen ihre Zugriffsebene gesteuert wird.  Damit Benutzer als Mitglieder von Organisationen und Bereichen in einer CFEE-Instanz hinzugefügt werden können, müssen diese Benutzer vorher über Zugriff auf diese CFEE-Instanz verfügen. Informationen hierzu finden Sie in [Berechtigungen](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Schritt 4: Bereitstellen und Anzeigen von Anwendungen
{: #deploy-apps}

Wenn  Sie bereit sind, können Sie mit dem [Bereitstellen der Anwendung](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html) in der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle beginnen.  Zeigen Sie die Liste der bereitgestellten Anwendungen in der Benutzerschnittstelle an, entweder im Kontext eines bestimmten CFEE-Bereichs oder global für alle CFEE-Instanzen.  Sie können Anwendungen in diesen Ansichten auch starten, stoppen oder löschen.

## Schritt 5: Erstellen oder Hinzufügen von IBM Cloud-Serviceinstanzen zu CFEE-Bereichen
{: #service-instances}

[Services erstellen](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) oder [Vorhandene Services hinzufügen](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace), verfügbar im IBM Cloud-Konto.  Sobald eine Serviceinstanz in einem CFEE-Bereich verfügbar ist, können Sie sie an CFEE-Anwendungen binden, die in diesem Bereich bereitgestellt sind.

## Schritt 6: Binden von Anwendungen an Serviceinstanzen
{: #bind-apps}

[Binden Sie die App](https://cloud.ibm.com/docs/cloud-foundry/binding.html) an einen Aliasnamen der Serviceinstanz, um die Funktionen des Service zu verwenden.

Im [Cloud Foundry-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") wird eine konsolidierte Ansicht aller Anwendungen und Services angezeigt, sowohl der *öffentlichen* als auch der *unternehmensspezifischen*.  Im Cloud Foundry-Dashboard klicken Sie im linken Navigationsfenster auf *Public*, um die öffentlichen Anwendungen und Services anzuzeigen, die im IBM Cloud-Konto verfügbar sind.  Klicken Sie auf *Enterprise*, um alle CFEE-Umgebungen, in CFEE-Bereichen bereitgestellten Anwendungen und für CFEE-Bereiche verfügbare Services anzuzeigen.
{:tip}

## Schritt 7: Aktivieren der Auditfunktion und der Protokollierungspersistenz (optional)
{: #enable-auditingandlogging}

Aktivieren Sie die Umgebung für [Auditereignisse](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) und [Protokollierungspersistenz](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging).

## Schritt 8: Aktivieren von Überwachungstools (optional)
{: #enable-monitoring}

Überwachungstools werden nicht automatisch für CFEE-Instanzen mit V2.2.0 oder höher bereitgestellt. CFEE-Administratoren können [Überwachungstools aktivieren](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring), nachdem die CFEE-Instanz erstellt wurde. Das Toolset für Überwachung umfasst Prometheus, Grafana und Alertmanager. 

## Schritt 9: Erstellen und Schützen der Cloud Foundry-Domänen (optional)
{: #create-domains}

Erstellen Sie [Domänen](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains) für alle Anwendungen in der CFEE (gemeinsam genutzte Domänen) oder für eine bestimmte Organisation (private Domänen) und schützen Sie diese durch SSL-Zertifikate.

## Schritt 10: Konfigurieren der Priorisierungsreihenfolge der Cloud Foundry-Buildpacks
{: #create-buildpacks}

Buildpacks stellen die Laufzeitunterstützung für Anwendungen bereit, die in einer Cloud Foundry-Umgebung bereitgestellt wurden. Automatisch konfigurieren sie die Laufzeit für eine Anwendung und verarbeiten ihre Abhängigkeiten. Cloud Foundry enthält eine Reihe von Buildpacks für gängige Sprachen und Frameworks. Rufen Sie [weitere Informationen](https://docs.cloudfoundry.org/buildpacks/) zu Cloud Foundry-Buildpacks auf.   

Auf der Seite **Buildpacks** der CFEE-Benutzerschnittstelle können Sie angepasste Buildpacks erstellen und hochladen. Buildpacks ist in der Prioritätenliste eine Ordinalzahl zugeordnet. Während des Staging einer Anwendung überprüft Cloud Foundry die Kompatibilität der Anwendung mit der Gruppe der Buildpacks, beginnend mit Position 1. Die Kompatibilitätsprüfungen werden in der Prioritätenliste fortgesetzt, bis ein kompatibles Buildpack gefunden wird. Stellen Sie sicher, dass die Prioritätsreihenfolge der Buildpacks den Anforderungen Ihrer Entwicklerteams entspricht. Sie können die Position eines Buildpacks in der Prioritätsreihenfolge ändern, indem Sie den Buildpacknamen per Drag-and-drop an eine andere Position ziehen. Sie können die Buildpacks auch über die [Cloud Foundry-CLI](https://docs.cloudfoundry.org/adminguide/buildpacks.html) verwalten. 

## Schritt 11: Installieren der Stratos-Konsole zur Verwaltung von Anwendungen (optional)
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
