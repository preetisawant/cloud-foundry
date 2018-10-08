---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Mit Services arbeiten
{: #workingwith-services}

Anwendungen, die in {{site.data.keyword.cfee_full_notm}} bereitgestellt werden, können an zwei Typen von Serviceinstanzen gebunden werden:
1. Öffentliche Serviceinstanzen, die mithilfe des {{site.data.keyword.Bluemix}}-Katalogs erstellt werden und im {{site.data.keyword.Bluemix}}-Konto verfügbar sind.  
Öffentliche Serviceinstanzen, die im {{site.data.keyword.Bluemix}}-Konto verfügbar sind, sind ohne eine weitere Aktion nicht für CFEE-Umgebungen verfügbar.  Damit eine öffentliche Serviceinstanz (im {{site.data.keyword.Bluemix}}-Konto verfügbar) für Bereiche in einer CFEE-Umgebung verfügbar wird, muss sie explizit zum Ziel-CFEE-Bereich hinzugefügt werden. Nachdem die {{site.data.keyword.Bluemix}}-Serviceinstanz zum CFEE-Bereich hinzugefügt wurde, kann sie an Anwendungen in diesem CFEE-Bereich gebunden werden.  Dies ermöglicht es Entwicklern, den umfangreichen Katalog der {{site.data.keyword.Bluemix}}-Services in ihren Anwendungen, die in CFEE-Umgebungen bereitgestellt sind, zu nutzen, während die Zugriffssteuerung für diese {{site.data.keyword.Bluemix}}-Services zugelassen wird.

   Zusätzlich zum Hinzufügen vorhandener {{site.data.keyword.Bluemix}}-Serviceinstanzen zu einem CFEE-Bereich können Sie eine neue {{site.data.keyword.Bluemix}}-Serviceinstanz aus einem CFEE-Bereich heraus erstellen, wodurch sie ebenfalls automatisch zu diesem CFEE-Bereich hinzufügt wird.

2. Serviceinstanzen, die von einem lokalen Cloud Foundry-Service-Broker verwaltet werden (lokal für die CFEE-Umgebung). Diese können wiederum zwei Typen aufweisen:
   *  2a. Eine Instanz eines Serviceangebots, das im Cloud Foundry-Marktplatz der aktuellen {{site.data.keyword.cfee_full_notm}}-Instanz erstellt wurde. Für diesen Serviceinstanztyp muss ein registrierter Service-Broker in der Umgebung verfügbar sein. Von einem Service-Broker wird ein Katalog mit Serviceangeboten und -plänen angezeigt; außerdem ermöglicht er es, Instanzen dieser Serviceangebote zu erstellen, zu entfernen, zu binden und Bindungen zu ihnen aufzuheben. Weitere Informationen hierzu finden Sie unter [Service-Broker verwalten](https://docs.cloudfoundry.org/services/managing-service-brokers.html) in der Dokumentation zu Cloud Foundry.
   * 2b. Eine vom Benutzer bereitgestellte Serviceinstanz. Die Erstellung dieses Typs wird über die Befehlszeilenschnittstelle (CLI) unterstützt, aber nicht über die Benutzerschnittstelle. Dennoch werden vom Benutzer bereitgestellte Serviceinstanzen in der Benutzerschnittstelle aufgelistet.
   

## {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen für alle CFEE-Umgebungen anzeigen
{: #viewing-services_across}

Rufen Sie das [Cloud Foundry-Service-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) auf, um eine konsolidierte Ansicht aller {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen (auf die Sie Zugriff haben) im {{site.data.keyword.Bluemix_notm}}-Konto anzuzeigen und zu prüfen, welche Serviceinstanzen zu welchen CFEE-Bereichen hinzugefügt wurden.

Diese Ansicht zeigt alle im Konto verfügbaren {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen an und gibt an, welche (mit Aliasnamen versehen) zu welchen CFEE-Bereichen hinzugefügt wurden. Erweitern Sie eine Serviceinstanz, um die CFEE-Bereiche anzuzeigen, in denen sie hinzugefügt wurde.  Sie können diese nochmals erweitern, um die Anwendungen in denjenigen CFEE-Bereichen anzuzeigen, an die diese Serviceinstanzen gebunden wurden.  

In dieser Ansicht können Sie auch Anwendungen binden, die in den CFEE-Bereichen bereitgestellt wurden, zu denen diese Serviceinstanzen hinzugefügt wurden. Wechseln Sie in das Menü ganz rechts in der Tabellenzeile für den entsprechenden Service (für einen bestimmten CFEE-Bereich verfügbar) und wählen Sie **An Anwendungen binden** aus.

## Vorhandene {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen zu einem CFEE-Bereich hinzufügen
{: #adding-services_inspace}

Sie können {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen an Anwendungen binden, die in einem CFEE-Bereich bereitgestellt sind.  Damit eine IBM Cloud-Serviceinstanz an eine Anwendung gebunden werden kann, die in einer CFEE bereitgestellt ist, muss sie einem CFEE-Bereich hinzugefügt werden, in dem die Anwendung bereitgestellt ist. Folgendes ist erforderlich, bevor Sie eine {{site.data.keyword.Bluemix_notm}}-Serviceinstanz zu einem CFEE-Bereich hinzufügen können:
* Der {{site.data.keyword.Bluemix_notm}}-Service muss in demselben {{site.data.keyword.Bluemix_notm}}-Konto verfügbar sein, in dem sich die CFEE-Instanz befindet.
* Sie müssen über Zugriff auf die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz selbst verfügen. Weitere Informationen zum Überprüfen Ihrer aktuellen Kontozugriffsrichtlinien finden Sie auf der Seite 'Identität & Zugang' im Menü **Verwalten > Benutzer** im {{site.data.keyword.Bluemix_notm}}-Header.

Gehen Sie wie folgt vor, um eine vorhandene {{site.data.keyword.Bluemix_notm}}-Serviceinstanz zu einem CFEE-Bereich hinzufügen:
1. Rufen Sie das [Cloud Foundry-Service-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) auf.  
2. Suchen Sie die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz in der Liste und rufen Sie das Menü ganz rechts in der entsprechenden Tabellenzeile auf.
3. Wählen Sie **Service hinzufügen** aus.
4. Wählen Sie im Dialog _ Service hinzufügen _ die CFEE, die Organisation und den Bereich aus, denen Sie den Service hinzufügen möchten, und klicken Sie auf **Hinzufügen**.
5. Erweitern Sie den {{site.data.keyword.Bluemix_notm}}-Zielservice, um den neuen CFEE zu suchen, dem der Service hinzugefügt wurde.


Alternativ können Sie die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz aus dem CFEE-Bereich heraus hinzufügen, dem sie hinzugefügt werden soll:
1. Suchen Sie in Ihrem {{site.data.keyword.Bluemix_notm}} [-Dashboard](https://console.bluemix.net/dashboard) oder [Cloud Foundry-Service-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) nach der Cloud Foundry Enterprise-Umgebung, die Ihre Anwendung hostet.
2. Wechseln Sie im Navigationsbereich zu **Organisationen** und öffnen Sie die Organisation und den Bereich, in dem sich die Anwendung befindet.
3. Wechseln Sie zur Registerkarte **Bereiche** und suchen Sie den Bereich, in dem die Anwendung enthalten ist.
4. Wechseln Sie auf der Seite des Zielbereichs zur Registerkarte **Services** und klicken Sie auf **Service hinzufügen**.  Dadurch wird der Dialog __Service hinzufügen__ geöffnet.  Auf der Seite werden die Serviceinstanzen aufgeführt, die im {{site.data.keyword.Bluemix_notm}}-Konto verfügbar sind.
5. Suchen Sie eine verfügbare Serviceinstanz, die Sie zum CFEE-Bereich hinzufügen möchten, und wählen Sie sie aus. 
6. Die Serviceinstanz wird der Liste der Services hinzugefügt, die im CFEE-Bereich verfügbar sind.

   **Hinweis:** Wenn Sie einem CFEE-Bereich einen {{site.data.keyword.Bluemix_notm}}-Service hinzufügen, wird in diesem Bereich ein Alias zu dieser Serviceinstanz erstellt. Wenn Sie mit **Entfernen** die Serviceinstanz aus einem CFEE-Bereich entfernen (aus dem Menü ganz rechts in der entsprechenden Serviceinstanz-Zeile der Tabelle), wird der Service nicht aus dem öffentlichen Konto gelöscht.  Mit der Aktion wird er aus dem jeweiligen CFEE-Konto entfernt und ist für das Binden an Anwendungen in diesem CFEE-Bereich nicht mehr verfügbar.  Wenn Sie zudem die Serviceinstanz selbst aus dem {{site.data.keyword.Bluemix_notm}}-Konto löschen, ist der Service für keinen CFEE-Bereich mehr verfügbar. 

## {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen über eine Benutzerschnittstelle für den CFEE-Bereich erstellen
{: #creating-services_inspace}
Sie können {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen aus einem CFEE-Bereich heraus erstellen.  Das Erstellen einer {{site.data.keyword.Bluemix_notm}}-Serviceinstanz führt zu folgenden Ergebnissen:
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird in der IBM Cloud erstellt.  Dies ist äquivalent zum Erstellen der Serviceinstanz aus dem {{site.data.keyword.Bluemix_notm}} [-Katalog ](https://console.bluemix.net/catalog).
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird (mit Aliasnamen versehen) in den CFEE-Bereich eingefügt, von dem aus die Erstellungsaktion initiiert wurde.


Gehen Sie wie folgt vor, um eine Serviceinstanz aus einem CFEE-Bereich zu erstellen:
1. Wechseln Sie auf der Seite des Zielbereichs zur Registerkarte **Services** und klicken Sie auf **Service erstellen**.  Dadurch wird die Ansicht **Marketplace** für {{site.data.keyword.cfee_full_notm}} geöffnet.  In der Ansicht werden Serviceangebote aus zwei Quellen aufgelistet (siehe Spalte __Quelle__):
   * Angebote aus dem {{site.data.keyword.Bluemix_notm}}-Katalog.
   * Angebote aus dem lokalen {{site.data.keyword.cfee_full_notm}}-Marktplatz.
5. Suchen Sie ein verfügbares Serviceangebot, das Sie instanziieren möchten, und wählen Sie es aus. 
6. Je nach der Quelle des Serviceangebots (IBM Cloud-Katalog oder lokaler CFEE-Marktplatz) fahren Sie mit einem der folgenden Schritte fort:
   * Wenn es sich bei dem ausgewählten Serviceangebot um ein {{site.data.keyword.Bluemix_notm}}-Katalogangebot handelt, wird eine Schaltfläche **Weiter** auf der Seite für die Erstellung des IBM Cloud-Serviceangebots angezeigt.  Dies ist dieselbe Seite, die über den {{site.data.keyword.Bluemix_notm}}-Katalog zur Verfügung steht.  Auf dieser Seite geben Sie den Namen der neuen Serviceinstanz, der Region, des Plans und anderer Eigenschaften an, die erforderlich sind, um den Service in der IBM Cloud zu erstellen.  Nachdem Sie die Serviceinstanz erstellt haben, wird sie in der IBM Cloud erstellt und automatisch zum aktuellen CFEE-Bereich hinzugefügt.
   * Wenn das ausgewählte Serviceangebot aus dem lokalen CFEE-Katalog stammt, wird Ihnen die Schaltfläche **Erstellen** für die Serviceinstanz angezeigt. Sie werden aufgefordert, eine Organisation und einen Bereich in dem aktuellen CFEE anzugeben, in dem die Serviceinstanz erstellt wird.

## {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen aus einem CFEE-Bereich über die CLI erstellen
{: #creating-services_cli}

Sie können eine Serviceinstanz über die CLI aus einem Bereich in einer CFEE erstellen.  Das Erstellen eines Service über die CLI in einem CFEE-Bereich ist äquivalent zu seiner Erstellung über die Benutzerschnittstelle in diesem Bereich. Das Erstellen eines Service hat also folgende doppelte Auswirkung:
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird in der IBM Cloud erstellt.  Dies ist äquivalent zum Erstellen der Serviceinstanz aus dem {{site.data.keyword.Bluemix_notm}} [-Katalog ](https://console.bluemix.net/catalog).
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird (mit Aliasnamen versehen) in den CFEE-Bereich eingefügt, von dem aus die Erstellungsaktion initiiert wurde.

Der Unterschied zwischen der Erstellung einer Serviceinstanz aus einem CFEE-Bereich und ihrer Erstellung über die CLI liegt im Lebenszyklus der erstellten Serviceinstanz.  Wenn Sie die Serviceinstanz in der Benutzerschnittstelle des CFEE-Bereichs erstellen, wird der Lebenszyklus der erstellten Serviceinstanz von der Serviceinstanz selbst im {{site.data.keyword.Bluemix_notm}}-Konto gesteuert.  Dies bedeutet, dass Aktualisierungen am Serviceplan über die Instanz im {{site.data.keyword.Bluemix_notm}}-Konto und nicht über den CFEE-Bereich gesteuert werden.  Wird die Serviceinstanz hingegen über die CLI erstellt, wird der Servicelebenszyklus über den CFEE-Bereich gesteuert (der Service wird über den CFEE-Bereich aktualisiert).

Serviceinstanzen, die über die CLI erstellt werden, werden auch in der Benutzerschnittstelle angezeigt und durch einen Stern `*` neben dem Namen der Serviceinstanz angezeigt.

Führen Sie die folgenden Schritte aus, um Serviceinstanzen über die CLI zu erstellen:

1. Laden Sie die {{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunter und installieren Sie sie, wenn noch nicht geschehen. [Laden Sie die Cloud Foundry-CLI herunter](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").

2. Wechseln Sie auf die {{site.data.keyword.cfee_full}}-Übersichtsseite und suchen Sie den API-Endpunkt der Umgebung.

3. Legen Sie in der Befehlszeilenschnittstelle den API-Endpunkt für den Endpunkt Ihrer CFEE-Umgebung fest:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Melden Sie sich bei der CFEE-Umgebung an:

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Wenn Sie eine eingebundene ID verwenden, verwenden Sie die Option `-sso`:

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. Erstellen Sie den Service:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  Optional können Sie eine Datei bereitstellen, die Parameter in einem gültigen JSON-Objekt enthält, das zur Erstellung eines bestimmten Service notwendig ist.
  Der Pfad zu der Parameterdatei kann ein absoluter oder relativer Pfad zu einer Datei sein:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  Nachfolgend ein Beispiel für ein gültiges JSON-Objekt:
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   Wenn Sie bei der Erstellung eines Service über die CLI Hilfe benötigen, geben Sie Folgendes ein:
  
  ```
  cf cs -help
  ```
  Weitere Informationen finden Sie unter [Serviceinstanzen mit der Cloud Foundry-CLI erstellen](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") in der Cloud Foundry-Dokumentation.
  
## Services an Anwendungen binden
{: #bind_services}

Sie können eine Serviceinstanz, die in einer CFEE bereitgestellt ist, entweder über das [Cloud Foundry-Service-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) oder über die Registerkarte 'Services' einer Seite des CFEE-Bereichs an eine Anwendung binden.  

Gehen Sie wie folgt vor, um eine Serviceinstanz über das [Cloud Foundry-Service-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) an eine Anwendung zu binden:
1. Rufen Sie das [Cloud Foundry-Service-Dashboard](https://console.bluemix.net/dashboard/cloudfoundry/services) auf, um eine konsolidierte Ansicht aller {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen anzuzeigen, die Ihnen im {{site.data.keyword.Bluemix_notm}}-Konto zur Verfügung stehen.  Die Ansicht soll auch zeigen, welche {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen (mit Alias versehen) in welchen CFEE-Bereichen verfügbar sind. Sie können eine Serviceinstanz erweitern, um die CFEE-Bereiche anzuzeigen, denen sie hinzugefügt wurde.  Sie können diese nochmals erweitern, um die Anwendungen in denjenigen CFEE-Bereichen anzuzeigen, an die diese Serviceinstanzen gebunden wurden. 
2. Suchen Sie die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz, die Sie binden möchten.
3. Erweitern Sie die entsprechende Ansicht, um alle CFEE-Bereiche anzuzeigen, in denen diese Serviceinstanz hinzugefügt wurde. Wenn diese Serviceinstanz nicht zu dem CFEE-Bereich hinzugefügt wurde, in dem die Anwendung bereitgestellt ist, wählen Sie **Hinzufügen** aus dem Menü in der Zeile ganz rechts aus, um die Serviceinstanz im Ziel-CFEE-Bereich verfügbar zu machen.
4. Wechseln Sie in das Menü ganz rechts in der Zeile für die CFEE/den Bereich, in dem die Serviceinstanz verfügbar ist, und wählen Sie **Anwendung binden** aus.
5. Wählen Sie im Dialog __Anwendung binden__ die Anwendung aus, die Sie binden möchten.
6. Die Anwendung wird jetzt an die Serviceinstanz in dem CFEE-Bereich gebunden, in dem die Anwendung bereitgestellt ist.  Sie können die Zeile für die entsprechende Zeile in der Tabelle erweitern, um die gebundenen Anwendungen im CFEE-Bereich anzuzeigen.


Gehen Sie wie folgt vor, um eine Anwendung über die Seite __Services__ eines CFEE-Bereichs an eine Serviceinstanz zu binden:

1. Öffnen Sie die Benutzerschnittstelle der CFEE, in der die Anwendung bereitgestellt ist.
2. Rufen Sie im linken Navigationsfenster **Organisationen** auf und öffnen Sie die Organisation und den Bereich, wo die Anwendung bereitgestellt ist.
3. Wechseln Sie zur Registerkarte **Bereiche** und suchen Sie den Bereich, in dem die Anwendung enthalten ist.
4. Wechseln Sie auf der Seite des Zielbereichs zur Registerkarte **Services**.
5. Rufen Sie in der Tabelle **Serviceinstanzen** das Menü __Aktionen__ ganz rechts in der Zeile entsprechend der zu bindenden Serviceinstanz auf und wählen Sie **Binden** aus.
6. Wählen Sie die Anwendung aus, die Sie an die Serviceinstanz binden möchten.

Gehen Sie wie folgt vor, um die Bindung einer Anwendung an eine Serviceinstanz aufzuheben:

1. Erweitern Sie in der Registerkarte **Services** des Bereichs die Zielserviceinstanz, um die Apps anzuzeigen, die an sie gebunden sind.
2. Öffnen Sie das Aktionsmenü in der Zeile einer Anwendung und wählen Sie **Bindung für Service aufheben** aus.

Weitere Informationen zum Binden von Anwendungen über die CLI finden Sie im Abschnitt [Eine Serviceinstanz binden](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") der Cloud Foundry-Dokumentation.


