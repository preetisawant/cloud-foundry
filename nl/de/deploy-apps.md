---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Anwendungen bereitstellen und anzeigen
{: #deploy_apps}

Sie können Anwendungen für {{site.data.keyword.Bluemix}} mithilfe der Befehlszeilenschnittstelle oder der integrierten Entwicklungsumgebungen (IDEs) bereitstellen. Darüber hinaus können Anwendungen mithilfe von Anwendungsmanifesten bereitgestellt werden. Bei Verwendung eines Anwendungsmanifests wird die Anzahl der Bereitstellungsdetails reduziert, die Sie jedes Mal angeben müssen, wenn Sie die Anwendung in {{site.data.keyword.Bluemix_notm}} bereitstellen.
{:shortdesc}

## Anwendungen mit Cloud Foundry-Befehl bereitstellen
{: #dep_apps}

Laden Sie die {{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunter und installieren Sie sie. [Laden Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle herunter.](https://clis.ng.bluemix.net){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").

Führen Sie nach der Installation der Befehlszeilenschnittstelle die folgenden Schritte aus:

1. Wechseln Sie in das Verzeichnis, in dem sich Ihr Code befindet. `cd <your_directory>`
2. Wechseln Sie auf die {{site.data.keyword.cfee_full}}-Übersichtsseite und suchen Sie den API-Endpunkt der Umgebung.
3. Legen Sie in der Befehlszeilenschnittstelle den API-Endpunkt als Endpunkt der Umgebung fest:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Melden Sie sich an der Umgebung an.

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Wenn Sie eine eingebundene ID nutzen, verwenden Sie die Option `-sso`.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **Hinweis:** Wenn der Wert ein Leerzeichen enthält, müssen `username`, `org_name` und `space_name` in einfache oder doppelte Anführungszeichen eingeschlossen werden. Beispiel: `-o "my org"`.

5.  Führen Sie im `neuen Verzeichnis` mit dem Befehl `bluemix app push` ein erneutes Staging Ihrer App in {{site.data.keyword.Bluemix_notm}} durch. Weitere Informationen zum Befehl `cf app push` finden Sie unter [Anwendung hochladen](/docs/starters/upload_app.html).

  ```
  cf push <app_name>
  ```
  {: pre}

6.  Greifen Sie durch Navigieren zu `https://<app_url>.<AppDomainName>` auf die Anwendung zu.

## Bereitgestellte Anwendungen in Benutzerschnittstelle anzeigen
{: #view_apps}

Sie können in der CFEE-Umgebung bereitgestellte Anwendungen entweder im Kontext eines bestimmten Bereichs oder global für alle CFEE-Instanzen anzeigen.

### In einem bestimmten CFEE-Bereich bereitgestellte Anwendungen anzeigen
{: #view_specific}

Gehen Sie wie folgt vor, um Anwendungen anzuzeigen, die in einem bestimmten Bereich einer bestimmten CFEE-Instanz bereitgestellt werden:
1. Wechseln Sie zum [{{site.data.keyword.Bluemix_notm}}-Dashboard](https://console.bluemix.net/dashboard/apps/) und öffnen Sie die {{site.data.keyword.cfee_full_notm}}-Umgebung, in der Sie die Organisationen erstellen möchten.
2. Wechseln Sie in der {{site.data.keyword.cfee_full_notm}}-Benutzerschnittstelle im Navigationsbereich zum Eintrag **Organisationen**, um die Seite _Organisationen_ zu öffnen.
3. Wechseln Sie ganz oben auf der Seite zur Registerkarte **Bereiche**.
4. Klicken Sie in der Registerkarte __Bereiche__ auf einen Bereich in der Tabelle, um die Seite des Bereichs zu öffnen.
5. Wechseln Sie auf der Seite __Bereich__ zur Registerkarte **Anwendungen**.
6. In der Registerkarte _Anwendungen_ werden alle Anwendungen angezeigt, die in diesem Bereich bereitgestellt werden. Optional können Sie eine Anwendung über das Menü ganz rechtes in der Zeile für die Anwendung starten, erneut starten, stoppen oder löschen.

Sie können die Zeile für eine Anwendung auch erweitern, um die Serviceinstanzen anzuzeigen, an die die Anwendung gebunden ist.

### Für alle CFEE-Instanzen bereitgestellte Anwendungen anzeigen
{: #view_global}

Gehen Sie wie folgt vor, um alle Anwendungen anzuzeigen, die für alle CFEE-Instanzen bereitgestellt werden:
1. Klicken Sie auf das Menüsymbol ![Kontoüberprüfung](img/HamburgerMenu.png "Screenshot des Menüsymbols") > **Cloud Foundry**, um das Cloud Foundry-Dashboard zu öffnen.
2. Klicken Sie im linken Navigationsbereich auf **Unternehmen > Anwendungen**. In der Tabelle in der Ansicht werden die folgenden Informationen angezeigt:

| Element   | Beschreibung |
|-----------|---------------|
| Name | Der Name der Anwendung. |
| Instanzen | Die Anzahl der Instanzen der Anwendung. |
| Umgebung | Die {{site.data.keyword.cfee_full}}-Umgebung, in der die Anwendung bereitgestellt wird. |
| Organisation | Die Organisation, in der die Anwendung bereitgestellt wird. |
| Bereich | Die Organisation in der CFEE-Instanz, in der sich der Alias befindet. |
| Hauptspeicher | Die Speicherkapazität, die von der Anwendung verwendet wird. |
| Status | Der Status der Anwendung. |
{:caption="Tabelle 1. Beschreibung von Schlüsselelementen" caption-side="top"}

Optional können Sie eine Anwendung über das Menü ganz rechtes in der Zeile für die Anwendung starten, erneut starten, stoppen oder löschen. Sie können auf beliebige Anwendungen, Umgebungen, Organisationen oder Bereiche klicken, um zur entsprechenden Seite in der CFEE-Benutzerschnittstelle zu navigieren.

In dieser Ansicht haben Sie die Möglichkeit, Anwendungen nach Organisation, Bereich und/oder Anwendungsname zu gruppieren. Diese Funktion ermöglicht es Ihnen, Anwendungen zu einer einzigen Einheit zu verbinden, die möglicherweise über unterschiedliche Namen verfügen und/oder in verschiedenen CFEE-Organisationen oder -Bereichen bereitgestellt werden, aber derselben logischen Anwendungsentität zugeordnet sind. Sie können zum Beispiel über verschiedene Anwendungen verfügen, die Komponenten eines größeren Projekts darstellen oder in verschiedenen Bereitstellungsstufen (zum Beispiel Entwicklung, Tests, Produktion) bereitgestellt werden, die Sie jedoch als Teil derselben logischen Entität gruppiert anzeigen möchten.

Wechseln Sie zum Gruppieren von Anwendungen zum Dropdown-Menü **Gruppe** in der rechten oberen Ecke der Seite. Wenn Sie Anwendungen gruppieren, wird jede so entstehende Gruppe als einzelner Eintrag in der Tabelle angezeigt. Sie können diese Zeile erweitern, um die Anwendungen anzuzeigen, die in dieser Gruppe zusammengefasst sind.

In dieser Ansicht können Sie die folgenden Aktionen ausführen:
* Elemente in der Tabelle nach einer der Eigenschaften sortieren, die als Tabellenspalten angezeigt werden.
* Anwendungen an einen bestimmten Alias durch Zugriff auf das Aliasüberlaufmenü des Aliasnamens binden, der sich in der Zeile ganz rechts befindet.
* Einen Alias (eine Zeile) erweitern, um alle Anwendungen anzuzeigen, an die der Aliasname gebunden ist.
* Anwendungen durch Zugriff auf das Anwendungsüberlaufmenü des Aliasnamens starten und stoppen, der sich in der Zeile ganz rechts befindet.
* Durch Klicken auf den Link zur entsprechenden CFEE-Instanz, CFEE-Organisation oder entsprechenden CFEE-Bereich zu einer CFEE-Instanz, CFEE-Organisation oder einem CFEE-Bereich navigieren.

## Anwendungsmanifest
{: #appmanifest}

Anwendungsmanifeste enthalten Optionen, die auf den Befehl `cf push` angewendet werden. Durch die Verwendung eines Anwendungsmanifests können Sie die Anzahl der Bereitstellungsdetails reduzieren, die Sie jedes Mal angeben müssen, wenn Sie für eine Anwendung eine Push-Operation an {{site.data.keyword.Bluemix_notm}} durchführen.

In Anwendungsmanifesten können Sie Optionen wie beispielsweise die Anzahl der zu erstellenden Anwendungsinstanzen, die Speicherkapazität, das zuzuordnende Datenträgerkontingent sowie weitere Umgebungsvariablen angeben. Darüber hinaus können Sie Anwendungsmanifeste verwenden, um Anwendungsbereitstellungen zu automatisieren. Der Standardname einer Manifestdatei lautet `manifest.yml`.

### Unterstützte Optionen in der Manifestdatei

Die nachstehende Tabelle zeigt die unterstützten Optionen, die Sie in einer Anwendungsmanifestdatei verwenden können. Wenn Sie einen anderen Dateinamen als `manifest.yml` verwenden möchten, müssen Sie die Option **-f** mit dem Befehl `cf push` verwenden. Im folgenden Beispiel wird `appManifest.yml` als Dateiname verwendet:

```
cf push -f appManifest.yml
```

| Optionen | Beschreibung | Verwendung oder Beispiel |
|:----------|:--------------|:---------------|
| **buildpack** | Die URL oder der Name des angepassten Buildpacks.	| `buildpack:` *buildpack_URL* |
| **disk_quota** | Das Datenträgerkontingent, das einer Anwendung zugeordnet ist. Der Standardwert ist 1 GB.	| `disk_quota: 500M` |
| **domain** | Der Domänenname der Anwendung in {{site.data.keyword.Bluemix_notm}}.	| `domain:` ng.bluemix.net |
| **host** | Der Hostname der Anwendung in {{site.data.keyword.Bluemix_notm}}. Dieser Wert muss in der {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.	| `host:` *host_name* |
| **name** | Der Anwendungsname in {{site.data.keyword.Bluemix_notm}}. Dieser Wert muss in der {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.	| `name:` *appname* |
| **path** | Die Position der Anwendung. Dieser Wert kann entweder ein relativer Pfad oder ein absoluter Pfad sein.	| `path:` *path_to_application* |
| **command** | Der angepasste Startbefehl für Ihre Anwendung oder der Befehl für die Ausführung von Scriptdateien.	| `command:` *custom_command* `command:` *bash ./run.sh* |
| **memory** | Die Speicherkapazität, die der Anwendung zugeordnet werden soll. Der Standardwert ist 1 GB.	| `memory: 512M` |
| **instances** | Die Anzahl der Instanzen, die für Ihre Anwendung erstellt werden sollen.	| `instances: 2` |
| **timeout** | Die für den Start der Anwendung zulässige Höchstdauer in Sekunden. Der Standardwert ist 60 Sekunden.	| `timeout: 80` |
| **no-route** | Ein boolescher Wert, der verwendet wird, um zu verhindern, dass der Anwendung eine Route zugewiesen wird, wenn die Anwendung lediglich im Hintergrund ausgeführt wird. Der Standardwert ist **false**.	| `no-route: true` |
| **random-route** | Ein boolescher Wert, der verwendet wird, um der Anwendung eine beliebige Route zuzuweisen. Der Standardwert ist **false**.	| `random-route: true` |
| **services** | Die Services, die an die Anwendung gebunden werden sollen.	| `services: - mysql_maptest` |
| **env** | Die angepassten Umgebungsvariablen für die Anwendung.| `env: DEV_ENV: production` |
{: caption="Tabelle 2. Unterstützte Optionen in der YAML-Manifestdatei" caption-side="top"}

### Beispiel für die Datei 'manifest.yml'
{: #sample}

Das folgende Beispiel zeigt eine Manifestdatei für eine Node.js-Anwendung, die das integrierte Node.js-Community-Buildpack in {{site.data.keyword.Bluemix_notm}} verwendet.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
