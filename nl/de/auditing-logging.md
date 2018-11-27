---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Audit und Protokollierung
{: #auditing-logging}

Die Funktionen für Audit und Protokollierung in einer {{site.data.keyword.cfee_full}} (CFEE) ermöglichen Administratoren das Überprüfen von Ereignissen, die in einer CFEE-Instanz auftreten, und Entwicklern das Verfolgen von Protokollereignissen, die von Cloud Foundry-Anwendungen generiert wurden.

Audit und Protokollierung werden in einer CFEE-Instanz durch die Integration der IBM Cloud-Services Log Analysis und Activity Tracker unterstützt.

## Audit
{: #auditing}

Mit einem Audit können CFEE-Administratoren überprüfbare Cloud Foundry-Aktivitäten verfolgen, die in einer CFEE-Instanz auftreten. Zu diesen Aktivitäten gehören Anmeldung, Erstellung von Organisationen und Bereichen, Benutzerzugehörigkeit und Rollenzuweisungen, Anwendungsbereitstellungen, Servicebindungen und Domänenkonfiguration. Das Audit wird durch die Integration mit dem Service Activity Tracker in der IBM Cloud unterstützt. Eine Instanz des Service Activity Tracker, die vom CFEE-Administrator ausgewählt wurde, wird automatisch für das Empfangen von Ereignissen konfiguriert, die für Aktionen stehen, die in Cloud Foundry und auf der CFEE-Steuerebene ausgeführt werden. Der Benutzer kann diese Ereignisse in der Benutzerschnittstelle der Activity Tracker-Serviceinstanz anzeigen und verwalten.

Gehen Sie wie folgt vor, um das Audit für eine CFEE-Instanz zu aktivieren:

1. Öffnen Sie die Benutzerschnittstelle der CFEE-Instanz und wechseln Sie im linken Navigationsbereich zu **Operationen > Audit**, um die Seite 'Protokollierung' zu öffnen.
2. Klicken Sie auf **Audit aktivieren** und wählen Sie eine der **Activity Tracker-Instanzen** aus, die im IBM Cloud-Konto verfügbar sind. Wenn keine Instanzen verfügbar sind, wird dem Benutzer eine Option zum Erstellen einer neuen Activity Tracker-Instanz im IBM Cloud-Katalog angezeigt.
3.  Sobald die Protokollierungspersistenz aktiviert ist, werden die Konfigurationsdetails auf der Seite angezeigt. Die Details umfassen die Konfiguration und einen Link zur Activity Tracker-Serviceinstanz selbst, zu der der Benutzer wechseln kann, um Auditereignisse anzuzeigen und zu verwalten.

Durch Klicken auf **Audit inaktivieren** können Sie das Audit inaktivieren; hierdurch wird die vorher hinzugefügte und konfigurierte Activity Tracker-Serviceinstanz entfernt. Mit dieser Aktion wird die Activity Tracker-Serviceinstanz nicht gelöscht.

## Protokollierungspersistenz
{: #logging}

Die Protokollierung von Cloud Foundry-Ereignissen wird durch die Integration mit dem Service Log Analysis in der IBM Cloud unterstützt. Eine Instanz des vom CFEE-Administrator ausgewählten Service Log Analysis wird automatisch zum Empfangen und Aufbewahren von Cloud Foundry-Protokollierungsereignisse konfiguriert, die von der CFEE-Instanz generiert wurden. Der Benutzer kann diese Protokollierungsereignisse in der Benutzerschnittstelle der Log Analysis-Serviceinstanz anzeigen und verwalten.

Gehen Sie wie folgt vor, um die Protokollierung für eine CFEE-Instanz zu aktivieren:

1. Stellen Sie sicher, dass Sie über eine [IAM-Zugriffsrichtlinie](https://console.bluemix.net/iam/#/users) verfügen, von der Ihnen die Rolle eines Editors, Operators oder Administrators für die Log Analysis-Serviceinstanz zugeordnet wird, in der die Protokollierungsereignisse gespeichert werden sollen.
2. Öffnen Sie die Benutzerschnittstelle der CFEE-Instanz und wechseln Sie im linken Navigationsbereich zu **Operationen > Protokollierung**, um die Seite 'Protokollierung' zu öffnen.
3. Klicken Sie auf **Protokollierungspersistenz aktivieren** und wählen Sie eine der **Log Analysis-Instanzen** aus, die im IBM Cloud-Konto verfügbar sind. Wenn keine Instanzen verfügbar sind, wird dem Benutzer eine Option zum Erstellen einer Instanz im IBM Cloud-Katalog angezeigt.
4. Sobald die Protokollierungspersistenz aktiviert ist, werden die Konfigurationsdetails auf der Seite angezeigt. Die Details umfassen die Konfiguration und einen Link zur Log Analysis-Serviceinstanz selbst, zu der der Benutzer wechseln kann, um Auditereignisse anzuzeigen und zu verwalten.

**Warnung:** Für das Aktivieren der Protokollierungspersistenz muss die Verwendung von CFEE-Steuerebene und -Zellen unterbrochen und erneut gestartet werden. Während des Neustarts ist die gesamte Verwaltungsfunktionalität verfügbar, einige in der CFEE-Instanz ausgeführte Anwendungen und Services stehen jedoch möglicherweise nicht zur Verfügung. Der Status der CFEE-Komponenten wird beim Neustart auf der Statusprüfungsseite abgebildet. Der Neustart nimmt etwa 20 Minuten in Anspruch.

Durch Klicken auf **Protokollierungspersistenz inaktivieren** können Sie die Protokollierungspersistenz inaktivieren; hierdurch wird die vorher hinzugefügte und konfigurierte Serviceinstanz entfernt. Mit dieser Aktion wird die Log Analysis-Serviceinstanz nicht gelöscht.

**Anmerkung:** Wenn Sie die Protokollierungspersistenz inaktivieren, werden weiterhin Cloud-Foundry-Protokollierungsereignisse generiert, aber nicht außerhalb der CFEE-Instanz persistent gespeichert.
