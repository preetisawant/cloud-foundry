---

copyright:

  years: 2018
lastupdated: "2018-12-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Aktualisierung und Skalierung
{: #update-scale}

Aktualisieren Sie die {{site.data.keyword.cfee_full_notm}}-Serviceinstanz auf die neuste Version, um die neuesten CFEE-Funktionen und -Korrekturen zu erhalten. CFEE-Aktualisierungen können neue Versionen für unterstützende Services von Cloud Foundry und CFEE enthalten (Kubernetes, Cloud Object Storage oder Compose for PostgreSQL).  Nicht jede CFEE-Aktualisierung enthält jedoch eine neue Version unterstützender Services von Cloud Foundry und CFEE. 

Die Aktualisierungen der CFEE-Version werden auf der Steuerebene durchgeführt, in der die CFEE-Komponenten und Zellen enthalten sind. Sie können die Kapazität der CFEE-Instanz auch durch das Hinzufügen oder Entfernen von Anwendungszellen skalieren.

**Anmerkung:** Während einer Versionsaktualisierung oder dem Hinzufügen bzw. Entfernen von Zellen sind möglicherweise einige Metriken (zum Beispiel für Hauptspeicher und CPU) nicht verfügbar, die auf den Seiten _Übersicht_, _Ressourcennutzung_ sowie _Aktualisierung und Skalierung_ angezeigt werden.

## CFEE-Version aktualisieren
{: #update}

Die Benutzer benötigen die folgenden Berechtigungen, um eine CFEE-Instanz auf eine neue Version aktualisieren zu können:
   * Die Rolle _Editor_ oder eine höhere Rolle für eine CFEE-Instanz.
   * Die Rolle _Operator_ oder eine höhere Rolle für den Kubernetes-Cluster, in dem die CFEE-Instanz bereitgestellt wird.

Die Aktualisierung der CFEE-Version einer CFEE-Instanz ist ein zweistufiger Prozess. Aktualisieren Sie zuerst die Steuerebene, in der die CFEE-Komponenten betrieben werden. Aktualisieren Sie danach die Zellen, in denen die Anwendungen bereitgestellt werden.

Beim Aktualisieren einer CFEE-Instanz auf eine neue Version gelten die folgenden Regeln und Einschränkungen:
* Die Steuerebene muss zuerst aktualisiert werden. Sobald die Steuerebene aktualisiert wurde, können die Zellen aktualisiert werden.
* Anwendungszellen können nur auf die Version der Steuerebene aktualisiert werden.  Somit können die Zellen der Steuerebene eine höhere CFEE-Version als die Anwendungszellen aufweisen, umgekehrt ist dies jedoch nicht möglich.

Gehen Sie wie folgt vor, um die CFEE-Version der CFEE-Instanz zu aktualisieren:
1. Wechseln Sie zum [{{site.data.keyword.Bluemix_notm}}-Dashboard](https://console.bluemix.net/dashboard/apps/) und öffnen Sie die {{site.data.keyword.cfee_full_notm}}-Instanz, die Sie aktualisieren möchten.
2. Wechseln Sie in der {{site.data.keyword.cfee_full_notm}}-Instanz im Navigationsbereich zum Eintrag **Zellen**, um die Seite 'Zellen' zu öffnen.
3. (Optional) In der Tabelle _Steuerebene_ können Sie die Zeile erweitern, um die Workerknoten in der Steuerebene anzuzeigen.
4. Klicken Sie auf **Aktualisieren**.
5. Wählen Sie im Dialog _Steuerebene aktualisieren_ eine der verfügbaren CFEE-Versionen aus und klicken Sie auf **Aktualisieren**. Die Aktualisierung dauert etwa 45 Minuten. In der Versionsbeschreibung werden die Details zu den Versionen der Komponenten angegeben, die im ausgewählten CFEE-Versionspaket enthalten sind; zusätzlich wird ein Link zum Dokument _Neuerungen_ bereitgestellt, in dem der Inhalt beschrieben wird, der in dieser Version bereitgestellt wird.
6. In der Spalte _Knotenstatus_ wird der Fortschritt der Aktualisierung angezeigt. Sobald die Aktualisierung abgeschlossen ist, wird in der Spalte _Version_ die neue CFEE-Version angegeben.
7. Sobald die Aktualisierung der Zellen der Steuerebene abgeschlossen ist, suchen Sie die Tabelle _Zellen_ und klicken Sie auf **Aktualisieren**.
8. Wählen Sie im Dialog _Steuerebene aktualisieren_ die CFEE-Version aus und klicken Sie auf *Aktualisieren*. Es ist nur eine Version für die Zellen verfügbar, weil die Anwendungszellen nur auf die Version der Steuerebene aktualisiert werden können. In einer einzigen Aktualisierungsaktion werden alle Zelle aktualisiert.
9. Zellen werden nacheinander aktualisiert. In der Spalte _Knotenstatus_ wird der Fortschritt der Aktualisierung für jede Zelle angezeigt. Wenn die Zellen aktualisiert werden, wird ihre neue Version in der Spalte _Version_ angezeigt.

## Unterbrechungen während der Versionsaktualisierung
{: #update-disruption}

Die Aktualisierung der Cloud Foundry-Steuerebene verläuft ohne Unterbrechungen.  Die Aktualisierung der Cloud Foundry-Zellen auf eine neue CFEE-Version kann jedoch zu Unterbrechungen beim Betrieb der CFEE-Umgebung führen.  Da eine Zelle nach der anderen aktualisiert wird, werden Anwendungsinstanzen, die in einer Zelle ausgeführt werden, wieder aktiv, sobald die Aktualisierung abgeschlossen ist, während andere Zellen während ihrer Aktualisierung noch inaktiv sind. Dennoch können einige Anwendungen und Services, die in der CFEE ausgeführt werden, unter bestimmten Umständen nicht mehr verfügbar sein. Wenn eine CFEE-Instanz beispielsweise über zwei Cloud Foundry-Zellen mit voller Kapazität verfügt, ist eine Anwendung mit nur einer Instanz während der Versionsaktualisierung inaktiv, da die Anwendungsinstanz während der Aktualisierung der Zelle nicht in eine andere Zelle verschoben werden kann; aus diesem Grund ist die Anwendung nicht verfügbar.  Selbst bei der Verwendung von drei Zellen und drei Instanzen pro Anwendung kann es während einer Versionsaktualisierung zu temporären Unterbrechungen bei der Anwendungsverfügbarkeit kommen. 

Während der Versionsaktualisierung können Abweichungen zwischen den Metriken für Hauptspeicher und CPU auftreten, die in den Messanzeigen der Zellenknoten auf der CFEE-Seite _Übersicht_ angezeigt werden (vom Kubernetes-Cluster generiert) und denselben Metriken, die im Dashboard _Nodes_ in Grafana angezeigt werden (auf der Betriebssystemebene generiert).

Der Status der CFEE-Komponenten wird während der Aktualisierung auf der Statusprüfungsseite abgebildet.  Der Neustart nimmt etwa 45 Minuten in Anspruch.

## Richtlinie für Versionszyklus und Unterstützung
{: #version-cycle}

Für den Cloud Foundry Enterprise Environment-Service wird normalerweise regelmäßig eine neue Version freigegeben. Für die Version des Service wird das folgende semantische Versionierungsformat verwendet: _**Hauptversion.Nebenversion.Patch**_ (https://semver.org/)

Für die _Nebenversion_ werden regelmäßige Aktualisierungen freigegeben (in der Regel monatlich). Für die _Hauptversion_ werden auch Aktualisierungen freigegeben, aber nicht so oft (in der Regel nur bei einer wichtigen Änderung).  Bei einer Aktualisierung auf eine _Hauptversion_ können während dem Upgrade Unterbrechungen auftreten. _Patches_ stellen eine Korrektur bereit und werden auf die letzte verfügbare Version angewendet. 

Um Systemausfallzeiten zu vermeiden, ist es nur zulässig, CFEE-Instanzen um maximal zwei _Hauptversionen_ oberhalb der aktuellen Version zu aktualisieren. Wenn die CFEE-Instanz aus dem vorherigen Beispiel die Version 3.1.2 aufweist und auf Version 7.0.0 aktualisiert werden soll, muss die CFEE-Instanz zunächst auf Version 5.x.x und anschließend auf die gewünschte Version 7.0.0 aktualisiert werden.

Neue Funktionen und Erweiterungen von vorhandenen Funktionen, die regelmäßig bereitgestellt werden, werden nur in der neuesten Version verfügbar. Kritische Korrekturen werden in der neuesten Version nur in den letzten drei _Hauptversionen_ (der neuesten Version und den beiden vorherigen Versionen) bereitgestellt. Beispiel: Wenn die Versionen 4.x.x, 3.x.x und 2.x.x verfügbar sind, werden die Versionen 1.x.x nicht unterstützt (die Patches werden somit nicht mit Korrekturen für die Versionen 1.x.x bereitgestellt).  

Patches werden für die neueste verfügbare Version einer bestimmten _Hauptversion_ bereitgestellt. Wenn beispielsweise Version 3.1.2 einer CFEE-Instanz ausgeführt wird, die neueste verfügbare Version in _Hauptversion_ 3.x.x jedoch Version 3.3.4 ist, werden alle Patches auf der Codebasis von Version 3.3.x bereitgestellt; dies bedeutet, dass das Patch in der (neuen) Version 3.3.5 bereitgestellt wird. Die CFEE-Instanz mit der Version 3.1.2 muss auf Version 3.3.5 aktualisiert werden, damit das neue Patch angewendet werden kann (durch eine Aktualisierung nur auf Version 3.3.4 wird nicht das Problem gelöst, das mit dem Patch behoben wird, der nur für Version 3.3.5 bereitgestellt wird).

## CFEE-Infrastruktur skalieren
{: #scale}

Die Benutzer benötigen die folgenden Berechtigungen, um Cloud Foundry-Zellen zu einer CFEE-Instanz hinzuzufügen oder aus einer CFEE-Instanz entfernen zu können:
* Die Rolle _Administrator_ oder eine höhere Rolle für eine CFEE-Instanz.
* Die Rolle _Operator_ oder eine höhere Rolle für den Kubernetes-Cluster, in dem die CFEE-Instanz bereitgestellt wird.

Gehen Sie wie folgt vor, um Anwendungszellen in der CFEE-Instanz hinzuzufügen
1. Wechseln Sie zum [{{site.data.keyword.Bluemix_notm}}-Dashboard](https://console.bluemix.net/dashboard/apps/) und öffnen Sie die {{site.data.keyword.cfee_full_notm}}-Umgebung, in der Sie Zellen hinzufügen möchten.
2. Klicken Sie neben der Tabelle _Zellen_ auf **Zelle hinzufügen**; daraufhin wird die Seite _Cloud-Foundry-Zellen hinzufügen_ geöffnet.
3. Wählen Sie auf der Seite _Cloud Foundry-Zellen hinzufügen_ die Anzahl der Zellen aus, die hinzugefügt werden sollen. Auf der Seite werden auch die Geografie und der Standort der CFEE-Instanz angezeigt, an dem die Zellen hinzugefügt werden. Außerdem werden die aktuelle Anzahl der Zellen und die Kapazität der Zellen angezeigt, die hinzugefügt werden sollen (diese Angabe ist mit der Kapazität der aktuellen Zellen identisch). Im rechten Teilfenster der Seite werden die geschätzten Kosten für die hinzugefügten Zellen zusammen mit den neuen geschätzten Gesamtkosten für die Umgebung angezeigt.
4. Klicken Sie auf **Hinzufügen**.  
5. Rufen Sie die Seite _Knoten_ auf. In der Tabelle _Zellen_ wird für jeden neuen Knoten eine neue Zeile hinzugefügt. In der Spalte _Knotenstatus_ wird der Fortschritt beim Hinzufügen der Zellen zur CFEE-Umgebung und Bereitstellen der Zelle in der CFEE-Umgebung angezeigt.
