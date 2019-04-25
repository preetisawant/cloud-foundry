---

copyright:
  years: 2018
lastupdated: "2019-04-03"

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
Im {{site.data.keyword.Bluemix}}-Konto verfügbare öffentliche Serviceinstanzen sind an sich nicht automatisch für CFEE-Umgebungen verfügbar. Damit eine (im {{site.data.keyword.Bluemix}}-Konto verfügbare) öffentliche Serviceinstanz für Bereiche in einer CFEE-Umgebung verfügbar wird, muss sie explizit dem CFEE-Zielbereich hinzugefügt werden. Wenn Sie eine öffentliche Serviceinstanz über die CFEE-Benutzerschnittstelle einer CFEE-Instanz _hinzufügen_, wird ein Alias der öffentlichen Serviceinstanz in die CFEE-Instanz gestellt. Nachdem die {{site.data.keyword.Bluemix}}-Serviceinstanz dem CFEE-Bereich (über einen Alias) hinzugefügt wurde, kann sie an Anwendungen in diesem CFEE-Bereich gebunden werden. Dies ermöglicht es Entwicklern, den umfangreichen Katalog der {{site.data.keyword.Bluemix}}-Services in ihren Anwendungen, die in CFEE-Umgebungen bereitgestellt sind, zu nutzen, während die Zugriffssteuerung für diese {{site.data.keyword.Bluemix}}-Services zugelassen wird.

   Zusätzlich zum Hinzufügen vorhandener {{site.data.keyword.Bluemix}}-Serviceinstanzen zu einem CFEE-Bereich können Sie eine neue {{site.data.keyword.Bluemix}}-Serviceinstanz aus einem CFEE-Bereich heraus erstellen, wodurch sie ebenfalls automatisch zu diesem CFEE-Bereich hinzufügt wird.
  
2. Serviceinstanzen, die von einem lokalen Cloud Foundry-Service-Broker verwaltet werden (lokal für die CFEE-Umgebung). Diese können wiederum zwei Typen aufweisen:
   *  2a. Eine Instanz eines Serviceangebots, das im Cloud Foundry-Marktplatz der aktuellen {{site.data.keyword.cfee_full_notm}}-Instanz erstellt wurde. Für diesen Serviceinstanztyp muss ein registrierter Service-Broker in der Umgebung verfügbar sein. Von einem Service-Broker wird ein Katalog mit Serviceangeboten und -plänen angezeigt; außerdem ermöglicht er es, Instanzen dieser Serviceangebote zu erstellen, zu entfernen, zu binden und Bindungen zu ihnen aufzuheben. Weitere Informationen hierzu finden Sie unter [Service-Broker verwalten](https://docs.cloudfoundry.org/services/managing-service-brokers.html) in der Dokumentation zu Cloud Foundry.
   * 2b. Eine vom Benutzer bereitgestellte Serviceinstanz. Die Erstellung dieses Typs wird über die Befehlszeilenschnittstelle (Command Line Interface, CLI) unterstützt, aber nicht über die Benutzerschnittstelle. Dennoch werden vom Benutzer bereitgestellte Serviceinstanzen in der Benutzerschnittstelle aufgelistet.
   
Sie können eine Serviceinstanz auch aus einem CFEE-Bereich erstellen. Verwenden Sie dazu die CFEE-Benutzerschnittstelle oder die CLI (siehe die folgenden Abschnitte). Das Erstellen einer Serviceinstanz aus einer CFEE-Instanz mit diesem Befehl hat ein doppeltes Ergebnis: 
* Eine Serviceinstanz wird in der öffentlichen {{site.data.keyword.Bluemix}} erstellt. 
* Ein Alias dieser öffentlichen Serviceinstanz wird innerhalb des CFEE-Bereichs erstellt, aus dem die Serviceinstanz erstellt wurde. 
    
In den folgenden Abschnitten wird beschrieben, wie Sie Serviceinstanzen über die Benutzerschnittstelle und über die Cloud Foundry-CLI hinzufügen, erstellen und binden und wie Sie den Zugriff auf diese Serviceinstanzen steuern können. 
   

## {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen für alle CFEE-Umgebungen anzeigen
{: #viewing-services_across}

Rufen Sie das [Cloud Foundry-Service-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/services) auf, um eine konsolidierte Ansicht aller {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen (auf die Sie Zugriff haben) im {{site.data.keyword.Bluemix_notm}}-Konto anzuzeigen und zu prüfen, welche Serviceinstanzen zu welchen CFEE-Bereichen hinzugefügt wurden.

Diese Ansicht zeigt alle im Konto verfügbaren {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen an und gibt an, welche (mit Aliasnamen versehen) zu welchen CFEE-Bereichen hinzugefügt wurden. Erweitern Sie eine Serviceinstanz, um die CFEE-Bereiche anzuzeigen, in denen sie hinzugefügt wurde.  Sie können diese nochmals erweitern, um die Anwendungen in denjenigen CFEE-Bereichen anzuzeigen, an die diese Serviceinstanzen gebunden wurden.  

In dieser Ansicht können Sie auch Anwendungen binden, die in den CFEE-Bereichen bereitgestellt wurden, zu denen diese Serviceinstanzen hinzugefügt wurden. Wechseln Sie in das Menü ganz rechts in der Tabellenzeile für den entsprechenden Service (für einen bestimmten CFEE-Bereich verfügbar) und wählen Sie **An Anwendungen binden** aus.

## Vorhandene {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen zu einem CFEE-Bereich hinzufügen
{: #adding-services-inspace}

Sie können {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen an Anwendungen binden, die in einem CFEE-Bereich bereitgestellt sind.  Damit eine IBM Cloud-Serviceinstanz an eine Anwendung gebunden werden kann, die in einer CFEE bereitgestellt ist, muss sie einem CFEE-Bereich hinzugefügt werden, in dem die Anwendung bereitgestellt ist. Folgendes ist erforderlich, bevor Sie eine {{site.data.keyword.Bluemix_notm}}-Serviceinstanz zu einem CFEE-Bereich hinzufügen können:
* Beim Service, dessen Instanz hinzugefügt werden soll, darf es sich nicht um einen Cloud Foundry-Service handeln.  Nur {{site.data.keyword.Bluemix_notm}}-Services, die Ressourcengruppen und IAM unterstützen, können (über einen Alias) zu einer CFEE hinzugefügt werden. Services, die in öffentlichen Cloud Foundry-Organisationen, -Bereichen und -Rollen instanziiert werden, können nicht (über einen Alias) zu einer CFEE hinzugefügt werden.  {{site.data.keyword.Bluemix_notm}}-Services nutzen in immer höherem Maß die Vorteile von Ressourcengruppen.  Sobald ein Service Ressourcengruppen anstelle von Cloud Foundry-Organisationen und -Bereichen verwendet, können bereits vorhandene Instanzen dieses Service in eine Ressourcengruppe migriert werden. Nun kann der Service zu einer CFEE hinzugefügt werden.  Weitere Informationen hierzu finden Sie in [Cloud Foundry-Serviceinstanzen in eine Ressourcengruppe migrieren](https://cloud.ibm.com/docs/resources/instance_migration.html#migrate).
* Der {{site.data.keyword.Bluemix_notm}}-Service muss in demselben {{site.data.keyword.Bluemix_notm}}-Konto verfügbar sein, in dem sich die CFEE-Instanz befindet.
* Sie benötigen die Plattformrolle eines _Operators_ (oder eine Rolle mit umfassenderen Berechtigungen) für die eigentliche {{site.data.keyword.Bluemix_notm}}-Serviceinstanz. Weitere Informationen zum Überprüfen Ihrer aktuellen Kontozugriffsrichtlinien finden Sie auf der Seite 'Identität & Zugang' im Menü **Verwalten > Benutzer** im {{site.data.keyword.Bluemix_notm}}-Header.

Gehen Sie wie folgt vor, um eine vorhandene {{site.data.keyword.Bluemix_notm}}-Serviceinstanz zu einem CFEE-Bereich hinzufügen:
1. Rufen Sie das [Cloud Foundry-Service-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/services) auf.  
2. Suchen Sie die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz in der Liste und rufen Sie das Menü ganz rechts in der entsprechenden Tabellenzeile auf.
3. Wählen Sie **Service hinzufügen** aus.
4. Wählen Sie im Dialog _ Service hinzufügen _ die CFEE, die Organisation und den Bereich aus, denen Sie den Service hinzufügen möchten, und klicken Sie auf **Hinzufügen**.
5. Erweitern Sie den {{site.data.keyword.Bluemix_notm}}-Zielservice, um den neuen CFEE zu suchen, dem der Service hinzugefügt wurde.


Alternativ können Sie die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz aus dem CFEE-Bereich heraus hinzufügen, dem sie hinzugefügt werden soll:
1. Suchen Sie in Ihrem {{site.data.keyword.Bluemix_notm}} [-Dashboard](https://cloud.ibm.com/dashboard) oder [Cloud Foundry-Service-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/services) nach der Cloud Foundry Enterprise-Umgebung, die Ihre Anwendung hostet.
2. Wechseln Sie im Navigationsbereich zu **Organisationen** und öffnen Sie die Organisation und den Bereich, in dem sich die Anwendung befindet.
3. Wechseln Sie zur Registerkarte **Bereiche** und suchen Sie den Bereich, in dem die Anwendung enthalten ist.
4. Wechseln Sie auf der Seite des Zielbereichs zur Registerkarte **Services** und klicken Sie auf **Service hinzufügen**.  Dadurch wird der Dialog __Service hinzufügen__ geöffnet.  Auf der Seite werden die Serviceinstanzen aufgeführt, die im {{site.data.keyword.Bluemix_notm}}-Konto verfügbar sind.
5. Suchen Sie eine verfügbare Serviceinstanz, die Sie zum CFEE-Bereich hinzufügen möchten, und wählen Sie sie aus. 
6. Die Serviceinstanz wird der Liste der Services hinzugefügt, die im CFEE-Bereich verfügbar sind.

   **Hinweis:** Wenn Sie einem CFEE-Bereich einen {{site.data.keyword.Bluemix_notm}}-Service hinzufügen, wird in diesem Bereich ein Alias zu dieser Serviceinstanz erstellt. Wenn Sie mit **Entfernen** die Serviceinstanz aus einem CFEE-Bereich entfernen (aus dem Menü ganz rechts in der entsprechenden Serviceinstanz-Zeile der Tabelle), wird der Service nicht aus dem öffentlichen Konto gelöscht.  Mit der Aktion wird er aus dem jeweiligen CFEE-Konto entfernt und ist für das Binden an Anwendungen in diesem CFEE-Bereich nicht mehr verfügbar. Wenn Sie zudem die Serviceinstanz selbst aus dem {{site.data.keyword.Bluemix_notm}}-Konto löschen, ist der Service für keinen CFEE-Bereich mehr verfügbar. 

## {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen über eine Benutzerschnittstelle für den CFEE-Bereich erstellen
{: #creating-services-inspace}

Sie können {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen aus einem CFEE-Bereich heraus erstellen.  Das Erstellen einer {{site.data.keyword.Bluemix_notm}}-Serviceinstanz führt zu folgenden Ergebnissen:
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird in der IBM Cloud erstellt.  Dies ist äquivalent zum Erstellen der Serviceinstanz aus dem {{site.data.keyword.Bluemix_notm}} [-Katalog ](https://cloud.ibm.com/catalog).
* Ein Alias für die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird (mit Aliasnamen versehen) zum CFEE-Bereich hinzugefügt, von dem aus die Erstellungsaktion initiiert wurde. Eine Aliasserviceinstanz (in einem CFEE-Bereich) ist ein Verweis auf die tatsächliche Serviceinstanz (im IBM Cloud-Konto). Der Aliasname der Serviceinstanz ermöglicht Entwicklern die Interaktion mit der Serviceinstanz (zum Beispiel die Bindung an Anwendungen), indem alle Berechtigungsnachweise automatisch für die Interaktion mit der Serviceinstanz verarbeitet werden. .

Gehen Sie wie folgt vor, um eine Serviceinstanz aus einem CFEE-Bereich zu erstellen:
1. Wechseln Sie auf der Seite des Zielbereichs zur Registerkarte **Services** und klicken Sie auf **Service erstellen**.  Dadurch wird die Ansicht **Marketplace** für {{site.data.keyword.cfee_full_notm}} geöffnet.  In der Ansicht werden Serviceangebote aus zwei Quellen aufgelistet (siehe Spalte __Quelle__):
   * Angebote aus dem {{site.data.keyword.Bluemix_notm}}-Katalog.
   * Angebote aus dem lokalen {{site.data.keyword.cfee_full_notm}}-Marktplatz.
5. Suchen Sie ein verfügbares Serviceangebot, das Sie instanziieren möchten, und wählen Sie es aus. 
6. Je nach der Quelle des Serviceangebots (IBM Cloud-Katalog oder lokaler CFEE-Marktplatz) fahren Sie mit einem der folgenden Schritte fort:
   * Wenn es sich bei dem ausgewählten Serviceangebot um ein {{site.data.keyword.Bluemix_notm}}-Katalogangebot handelt, wird eine Schaltfläche **Weiter** auf der Seite für die Erstellung des IBM Cloud-Serviceangebots angezeigt.  Dies ist dieselbe Seite, die über den {{site.data.keyword.Bluemix_notm}}-Katalog zur Verfügung steht.  Auf dieser Seite geben Sie den Namen der neuen Serviceinstanz, der Region, des Plans und anderer Eigenschaften an, die erforderlich sind, um den Service in der IBM Cloud zu erstellen.  Nachdem Sie die Serviceinstanz erstellt haben, wird sie in der IBM Cloud erstellt und automatisch zum aktuellen CFEE-Bereich hinzugefügt.
   * Wenn das ausgewählte Serviceangebot aus dem lokalen CFEE-Katalog stammt, wird Ihnen die Schaltfläche **Erstellen** für die Serviceinstanz angezeigt. Sie werden aufgefordert, eine Organisation und einen Bereich in dem aktuellen CFEE anzugeben, in dem die Serviceinstanz erstellt wird.

## {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen aus einem CFEE-Bereich über die Cloud Foundry-CLI erstellen
{: #creating-services_cli}

Sie können eine Serviceinstanz über die CLI aus einem Bereich in einer CFEE erstellen.  Das Erstellen eines Service über die CLI in einem CFEE-Bereich ist äquivalent zu seiner Erstellung über die Benutzerschnittstelle in diesem Bereich. Das Erstellen eines Service hat also folgende doppelte Auswirkung:
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird in der IBM Cloud erstellt.  Dies ist äquivalent zum Erstellen der Serviceinstanz aus dem {{site.data.keyword.Bluemix_notm}} [-Katalog ](https://cloud.ibm.com/catalog).
* Die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz wird (mit Aliasnamen versehen) in den CFEE-Bereich eingefügt, von dem aus die Erstellungsaktion initiiert wurde.

Der Unterschied zwischen der Erstellung einer Serviceinstanz aus einem CFEE-Bereich und ihrer Erstellung über die CLI liegt im Lebenszyklus der erstellten Serviceinstanz.  Wenn Sie die Serviceinstanz in der Benutzerschnittstelle des CFEE-Bereichs erstellen, wird der Lebenszyklus der erstellten Serviceinstanz von der Serviceinstanz selbst im {{site.data.keyword.Bluemix_notm}}-Konto gesteuert.  Dies bedeutet, dass Aktualisierungen am Serviceplan über die Instanz im {{site.data.keyword.Bluemix_notm}}-Konto und nicht über den CFEE-Bereich gesteuert werden.  Wird die Serviceinstanz hingegen über die Befehlszeilenschnittstelle (CLI) erstellt, wird der Servicelebenszyklus über den CFEE-Bereich gesteuert (der Service wird über den CFEE-Bereich aktualisiert).

Serviceinstanzen, die über die Befehlszeilenschnittstelle erstellt werden, werden auch in der Benutzerschnittstelle angezeigt und durch einen Stern `*` neben dem Namen der Serviceinstanz angezeigt.

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
Sie können einen Befehl `cf create-service` ausgeben, um eine Serviceinstanz in dem CFEE-Bereich zu erstellen, in dem der Befehl ausgegeben wird. Das Erstellen einer Serviceinstanz aus einer CFEE-Instanz mit diesem Befehl hat ein doppeltes Ergebnis: 
    * Eine Serviceinstanz wird in der öffentlichen {{site.data.keyword.Bluemix}} erstellt, wobei der Name durch den Parameter `instance_name` angegeben wird. Wird der Parameter `instance_name` im Befehl nicht angegeben, vergibt der {{site.data.keyword.Bluemix}}-Ressourcencontroller einen Namen.   
    * Ein Alias dieser öffentlichen Serviceinstanz wird innerhalb des CFEE-Bereichs erstellt, aus dem die Serviceinstanz erstellt wurde, wobei der Name durch `SERVICE_INSTANCE` angegeben wird. Beachten Sie, dass der Name der öffentlichen Serviceinstanz nicht automatisch mit dem Namen der Serviceinstanz in der CFEE-Instanz identisch ist. Wenn der Name der öffentlichen Serviceinstanz und der Name der Serviceinstanz in der CFEE-Instanz (der Alias der öffentlichen Serviceinstanz) übereinstimmen sollen, müssen Sie daher beide Parameter `instance_name` und `SERVICE_INSTANCE` (mit demselben Wert) in dem folgenden Befehl angeben: 

  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"instance_name":"value", "resource_group":"value", "target":"value"}'
  ```
  {: pre}
  
Mit dem folgenden Beispiel wird eine Instanz des Cloudant-Service (Standardplan) mit dem Namen "myCloudant" (mit übereinstimmendem Namen der öffentlichen Instanz und des CFEE-Alias) in der Region "bluemix-us-south" erstellt und in einer bestimmten Ressourcengruppe gruppiert: 

  ```
  cf create-service cloudant standard myCloudant -c '{"instance_name":"myCloudant", "resource_group":"b0daaf6c3ccd4392a266da916cce2e8c", "target":"bluemix-us-south"}'
  ```
  {: pre}

 Der Befehl `create-service` kann mit optionalen Parametern für bestimmte Anwendungsfälle ausgegeben werden: 
 
   * Instanzname (`instance_name`): Ermöglicht Ihnen die Angabe eines angepassten Namens für die Serviceinstanz, die in der öffentlichen {{site.data.keyword.Bluemix}} erstellt wird. Wird kein Wert für `instance_name` angegeben, unterscheidet sich der Standardname der öffentlichen Serviceinstanz vom Wert für `SERVICE_INSTANCE` (dem Namen der Instanz in der CFEE-Instanz). Es wird empfohlen, diesen Parameter zu verwenden, um den Namen der öffentlichen Serviceinstanz zu steuern oder wenn dieser Name mit dem Namen der Serviceinstanz in der CFEE-Instanz (Alias der öffentlichen Instanz) übereinstimmen soll. 
   * Ressourcengruppe (`resource_group`). Ermöglicht Ihnen die Angabe einer Ressourcengruppe, unter der die neue Instanz platziert werden soll. Die "Ressourcengruppe" (`resource_group`). Beachten Sie, dass der Wert dieses Parameters in der ID der Ressourcengruppe (_Ressourcengruppen-ID_), nicht im Namen der Ressourcengruppe (_Ressourcengruppenname_) enthalten sein muss. Die _Ressourcengruppen-ID_ einer bestimmten Ressourcengruppe ermitteln Sie mit dem Befehl `ibmcloud resource groups`. 
   * Zielbereitstellungsregion(`target`). Die Region, in der die Serviceinstanz bereitgestellt werden soll. Beachten Sie, dass einige Services keine Spezifikation eines Ziels erfordern. Der Befehl schlägt jedoch fehl, wenn kein Ziel angegeben wird und der Service, der gerade erstellt wird, dies erfordert. 

Optional können Sie eine JSON-Datei bereitstellen, die diese Parameter enthält. Beispiel: 
  ```
  {
    "NewCloudant": 
        {  
        "instance_name":"myCloudant",
        "resource_group": "b0daaf6c3ccd4392a266da916cce2e8c",
        "target": "bluemix-us-south"
        }
   }
  ```
  {: pre}
  
Die JSON-Datei kann dann als Teil des Befehls `cf create-service` aufgerufen werden. Der Pfad zu der JSON-Datei kann ein absoluter oder relativer Pfad sein: 
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
Wenn Sie weitere Details wünschen, können Sie den folgenden Befehl ausgeben: 
  ```
  cf create-service -help
  ```
<br>
Weitere Informationen finden Sie unter [Serviceinstanzen mit der Cloud Foundry-CLI erstellen](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") in der Cloud Foundry-Dokumentation.
  
## Services über die CFEE-Benutzerschnittstelle an Anwendungen binden
{: #bind-services-ui}

Benutzer, die über die Plattformrolle eines _Operators_ (oder eine Rolle mit umfassenderen Berechtigungen) und über die Servicerolle eines _Schreibberechtigten_ (oder eine Rolle mit umfassenderen Berechtigungen) für eine {{site.data.keyword.Bluemix_notm}}-Serviceinstanz verfügen, können diese Instanz an eine Anwendung binden, die in einem CFEE-Bereich bereitgestellt ist. Dies ist entweder über das [Cloud Foundry-Service-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/services) oder über die Serviceregisterkarte in der Benutzerschnittstelle eines CFEE-Bereichs möglich.   

Gehen Sie wie folgt vor, um eine Serviceinstanz über das [Cloud Foundry-Service-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/services) an eine Anwendung zu binden:
1. Rufen Sie das [Cloud Foundry-Service-Dashboard](https://cloud.ibm.com/dashboard/cloudfoundry/services) auf, um eine konsolidierte Ansicht aller {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen anzuzeigen, die Ihnen im {{site.data.keyword.Bluemix_notm}}-Konto zur Verfügung stehen.  Die Ansicht soll auch zeigen, welche {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen (mit Alias versehen) in welchen CFEE-Bereichen verfügbar sind. Sie können eine Serviceinstanz erweitern, um die CFEE-Bereiche anzuzeigen, denen sie hinzugefügt wurde.  Sie können diese nochmals erweitern, um die Anwendungen in denjenigen CFEE-Bereichen anzuzeigen, an die diese Serviceinstanzen gebunden wurden. 
2. Suchen Sie die {{site.data.keyword.Bluemix_notm}}-Serviceinstanz, die Sie binden möchten.
3. Erweitern Sie die entsprechende Ansicht, um alle CFEE-Bereiche anzuzeigen, in denen diese Serviceinstanz hinzugefügt wurde. Wenn diese Serviceinstanz nicht zu dem CFEE-Bereich hinzugefügt wurde, in dem die Anwendung bereitgestellt ist, wählen Sie **Hinzufügen** aus dem Menü in der Zeile ganz rechts aus, um die Serviceinstanz im Ziel-CFEE-Bereich verfügbar zu machen.
4. Wechseln Sie in das Menü ganz rechts in der Zeile für die CFEE/den Bereich, in dem die Serviceinstanz verfügbar ist, und wählen Sie **Anwendung binden** aus.
5. Wählen Sie im Dialog __Anwendung binden__ die Anwendung aus, die Sie binden möchten. 

   **Hinweis:** Wenn der zu bindende Service sowohl öffentliche (externe) als auch private (interne) Endpunkte (siehe [IBM Cloud-Serviceendpunkte](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about)) und/oder mehrere [Servicezugriffsrollen](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am) unterstützt (diese geben die zulässigen Aktionen für die Serviceinstanz an, die über die Bindung ausgeführt werden können), wird ein Dialog mit mehreren Schritten angezeigt. In diesem Dialog werden Sie aufgefordert, einen Endpunkttyp (öffentlich oder privat) und/oder eine bestimmte Servicerolle auszuwählen. 
6. Die Anwendung ist jetzt an die Serviceinstanz gebunden.  Sie können eine Serviceinstanz in der Tabelle erweitern, um die Anwendungen anzuzeigen, die an sie gebunden sind (in einem bestimmten CFEE-Bereich).


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

## Services über die Cloud Foundry-CLI an Anwendungen binden
{: #bind-services-cli}

Sie können den Befehl `cf bind-service` verwenden, um eine Serviceinstanz an eine Anwendung in einer CFEE-Instanz zu binden: 

 ```
  cf bind-service APP_NAME SERVICE_INSTANCE -c '{"parameter": "value"}' 
  ```
  {: pre}

In den folgenden Fällen erfordert der Befehl besondere Parameter: 

* Wenn Sie mit dem Befehl `cf bind-service` eine App an eine Serviceinstanz binden, die [IBM Cloud Service Endpoints](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about) unterstützt. Diese stellen über das private IBM Cloud-Netz Verbindungen zu IBM Cloud-Services her. Zum Binden einer (in einer CFEE-Instanz bereitgestellten) Anwendung an einen Service, der sowohl öffentliche (externe) als private (interne) Endpunkte unterstützt, müssen Sie angeben, welche Endpunkte für die Bindungen verwendet werden sollen. Im folgenden Beispiel wird der Service unter Verwendung der "internen" Endpunkte gebunden: 

  ```
  cf bind-service myApplication myServiceInstance -c '{"service-endpoints":"internal"}' 
  ```
  {: pre}

* Wenn der Service über mehrere [Servicezugriffsrollen](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am) verfügt. Servicezugriffsrollen geben die zulässigen Aktionen für die Serviceinstanz an, die über die Bindung ausgeführt werden können. Sie können eine bestimmte Servicezugriffsrolle über den Parameter `role` angeben. Im folgenden Beispiel gibt die Bindung die Servicezugriffsrolle "writer" (Schreibberechtigter) an: 

  ```
  cf bind-service myApplication myServiceInstance -c '{"role": "writer"}' 
  ```
  {: pre}
<br>
Unter [Serviceinstanz binden](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") in der Cloud Foundry-Dokumentation finden Sie weitere Informationen zum Binden von Anwendungen mit dem CLI-Befehl `cf bind-service`. 

## Sichtbarkeit von Services
{: #service_visibility}

Kunden können steuern, wer neue IBM Cloud-Services in einer CFEE-Umgebung erstellen kann.  Sie können auch steuern, wer vorhandene IBM Cloud-Services zu einem CFEE-Bereich hinzufügen kann.  Diese Steuerung wird durch das Steuern der Sichtbarkeit von Serviceangeboten (und/oder Instanzen dieser Serviceangebote) für den Benutzer ausgeübt.

### Erstellung von Serviceinstanzen steuern
{: #control_servicecreation}

Die Steuerung der Serviceerstellung kann durch das Steuern der Sichtbarkeit von Serviceangeboten im IBM Cloud-Katalog für alle Benutzer im IBM Cloud-Konto oder für Benutzer in bestimmten Cloud-Foundry-Organisationen durchgeführt werden.

#### Sichtbarkeit für Benutzer in einem IBM Cloud-Konto im IBM Cloud-Katalog steuern
{: #creation_accountvisibility}

IBM Cloud-Kontoadministratoren (Benutzer mit der Rolle _Administrator_ für alle für IAM aktivierten Services) können verhindern, dass ein Service oder Serviceplan im Katalog für alle Benutzer in einem bestimmten **IBM Cloud-Konto** anzeigt wird.  Kontoadministratoren können verhindern, dass alle Kontenbenutzer einen Service verwenden, indem sie den Service bzw. Serviceplan für alle Benutzer in einem Konto in die Blacklist aufnehmen. Durch das Blacklisting eines Service wird sogar verhindert, dass Benutzer in diesem Konto diesen Service (oder Serviceplan) im IBM Cloud-Katalog anzeigen können.  Dazu wird der Befehl `ibmcloud catalog blacklist` mit der folgenden Syntax ausgeführt:

  ```
  ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]
  ```

In seiner einfachsten Form kann der Befehl `catalog backlist` dazu verwendet werden, ein Serviceangebot (alle zugehörigen Pläne) für alle Benutzer im aktuellen Konto auszublenden:

  ```
  Ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]

  ```
  {: pre}

Sie können die Sichtbarkeit aber nicht nur generell für ein ganzes Serviceangebot durch Blacklisting verhindern, sondern auch für einen bestimmten Plan in einer bestimmten Region.  Hierfür benötigen Sie jedoch die ID für den entsprechenden Eintrag im globalen Katalog und nicht den Namen.   Wenn Sie verhindern möchten, dass Benutzern ein bestimmter Plan in einer bestimmten Region angezeigt wird, können Sie folgenden Befehl absetzen:

  ```
  Ibmcloud catalog blacklist -add <catalogEntryID>
  ```
  {: pre}
  
 Gehen Sie wie folgt vor, um Services aus der Blacklist zu entfernen:
 ```
  Ibmcloud catalog blacklist -remove <catalogEntryID>
  ```
  {: pre}
 
Die ID eines bestimmten Katalogeintrags (zum Beispiel eines Serviceplans und der zugehörigen Bereitstellungsregion) können Sie mit dem folgenden Befehl suchen. Nach dem Absetzen des Befehls werden alle Pläne und ihre Bereitstellungsregionen für einen bestimmten Service zurückgegeben:

  ```
  ibmcloud catalog service <thisService>
  ```
  {: pre}

Weitere Details zum Befehl `ibmcloud catalog blacklist` erhalten Sie, wenn Sie den folgenden Befehl absetzen:

  ```
  Ibmcloud catalog blacklist -help
  ```
  {: pre}


#### Sichtbarkeit für Benutzer in einer Cloud-Foundry-Organisation steuern
{: #creation_orgvisibility}

Mit den Befehlen `cf enable-service-access` und `cf disable-service-access` können Sie den Zugriff auf Services für bestimmte **Cloud Foundry-Organisationen** steuern.  Der Steuerpunkt für den Zugriff ist in diesem Fall Cloud Foundry (nicht das IBM Cloud-Konto).  Beachten Sie, dass es sich hierbei um einen nativen `cf`-Befehl handelt (nicht um einen `ibmcloud`-Befehl). 

Beachten Sie Folgendes, wenn Sie die Servicesichtbarkeit über die Befehlszeilenschnittstelle `cf` festlegen:

*  Mit `cf`-Befehlen werden Serviceangebote (optional auch Pläne von Serviceangeboten) für alle Benutzer bestimmter Cloud Foundry-Organisationen aktiviert bzw. inaktiviert.
* Die Aktivierung wird durch die Erstellung einer Whitelist für die Organisation durchgeführt. Diese Whitelist ist eine Einschlussliste der Cloud Foundry-Organisationen, die über Zugriff auf einen Service verfügen (im Gegensatz zum Konzept der Blacklist des vorher beschriebenen `ibmcloud`-Befehls, durch den ein Service in eine Liste aus Services aufgenommen wird, die von den Kontobenutzern nicht angezeigt werden können). Dies bedeutet, dass für die Zugriffssteuerung auf einen Katalogservice bei diesem Konzept nicht definiert wird, welche Organisationen einen Service nicht anzeigen können (Blacklisting), sondern dass definiert wird, welche Organisationen einen Service anzeigen können (Whitelisting).
*  Wenn Sie einer Organisation Zugriff auf einen Service (oder Serviceplan) gewähren, indem Sie diese Organisation einer Whitelist hinzufügen, inaktivieren Sie dadurch faktisch den Zugriff aller anderen Organisationen auf den Service (schließen diese vom Zugriff aus).  Dies bedeutet, dass Sie durch das Aufnehmen einer Organisation in die Whitelist den Zugriff aller anderen Organisationen auf diesen Service (oder Serviceplan) inaktivieren.
*  Bevor Sie Organisationen zu der Liste der Organisationen hinzufügen, die einen Service anzeigen können, müssen Sie die Sichtbarkeit für alle Organisationen inaktivieren.  Sie können den Zugriff auf einen Serviceplan nicht inaktivieren, wenn der Plan derzeit für alle Organisationen verfügbar ist.

In Übereinstimmung mit dem oben beschriebenen allgemeinen Verhalten wird empfohlen, den Zugriff der Organisationen auf Services durch das Absetzen der folgenden Befehle zu steuern:

  * **Inaktivieren** des Zugriffs auf einen Serviceplan für alle Organisationen:
  ```
  cf disable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}
  
  Im folgenden Beispiel wird der Zugriff auf den Standardplan des Cloudant-Service für alle Mitglieder von MyOrg inaktiviert: 
  ```
  cf disable-service-access cloudant -p standard -o MyOrg
  ```
  {: pre}

  
  * **Aktivieren** des Zugriffs auf den Serviceplan für bestimmte CFEE-Organisationen.  Dadurch wird der Serviceplan für aller anderen Organisationen inaktiviert, für die der im Befehl nicht ausdrücklich aktiviert wird. 
  ```
  cf enable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}

<br>  
**Anmerkung:** Es wird empfohlen, die Cloud Foundry-Befehle zum Aktivieren und Inaktivieren des Service für den gesamten Service und nicht für bestimmte Pläne auszuführen.


### Zugriff auf vorhandene Serviceinstanzen steuern
{: #control_serviceaddition}

Entwickler in einem CFEE-Bereich können vorhandene Serviceinstanzen verwenden, die im IBM Cloud-Konto verfügbar sind.  Innerhalb eines bestimmten Bereichs einer CFEE können Benutzer eine Serviceinstanz zu diesem Bereich **hinzufügen** (siehe [Vorhandene Serviceinstanzen hinzufügen](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) weiter oben). Durch das Hinzufügen einer Serviceinstanz zu einem CFEE-Bereich wird ein Aliasname (eine Referenz) für die Serviceinstanz erstellt, der es einem Entwickler ermöglicht, die Serviceinstanz so an eine Anwendung zu binden, die in diesem CFEE-Bereich bereitgestellt wird, als wäre sie die tatsächliche Serviceinstanz.

Kontoadministratoren können die Verwendung von Serviceinstanzen über [IAM-Zugriffsrichtlinien](https://cloud.ibm.com/docs/iam/iamusermanage.html#iamusermanage) steuern.  Über die Benutzerschnittstelle oder die ibmcloud-Befehlszeilenschnittstelle können Sie die Rollen entweder den Serviceinstanzen selbst oder den Ressourcengruppen zuordnen, in denen sich diese Instanzen befinden.  Damit ein Entwickler eine Instanz zu einem Bereich hinzufügen kann, benötigt er für die Serviceinstanz die Rolle _Anzeigeberechtigter_ oder eine höhere Rolle.

Videos mit umfassenden Diskussionen und Vorführungen zu CFEE-Services finden Sie in der [CFEE-Videowiedergabeliste](https://ibm.biz/CFEE-Playlist){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
{:tip}
