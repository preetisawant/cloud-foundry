---

copyright:
  years: 2018
lastupdated: "2018-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Gestione dei servizi
{: #workingwith-services}

Le applicazioni distribuite in {{site.data.keyword.cfee_full_notm}} possono essere associate a due tipi di istanze del servizio:
1. Le istanze del servizio pubbliche create dal catalogo {{site.data.keyword.Bluemix}} e disponibili nell'account {{site.data.keyword.Bluemix}}.  
Le istanze del servizio pubbliche disponibili nell'account {{site.data.keyword.Bluemix}} non possono essere disponibili, da sole, agli ambienti CFEE.  Affinché un'istanza del servizio pubblica (disponibile nell'account {{site.data.keyword.Bluemix}}) diventi disponibile per gli spazi in un ambiente CFEE, è necessario che venga specificamente aggiunta allo spazio CFEE di destinazione. Dopo che l'istanza del servizio {{site.data.keyword.Bluemix}} è aggiunta allo spazio CFEE, è possibile eseguirne il bind (associazione) alle applicazioni in tale spazio CFEE.  Ciò consente agli sviluppatori di avvalersi del vasto catalogo di servizi {{site.data.keyword.Bluemix}} nelle loro applicazioni distribuite in ambienti CFEE, consentendo al tempo stesso il controllo dell'accesso a tali servizi {{site.data.keyword.Bluemix}}.

   Oltre ad aggiungere le istanze del servizio {{site.data.keyword.Bluemix}} esistenti a uno spazio CFEE, puoi creare una nuova istanza del servizio {{site.data.keyword.Bluemix}} dall'interno di uno spazio CFEE, che ne esegue anche automaticamente l'aggiunta a tale spazio CFEE.
  
2. Le istanze del servizio gestite da un broker dei servizi Cloud Foundry locale (locale per la CFEE). A loro volta, possono essere di due tipi:
   *  2a. Un'istanza di un'offerta di servizi creata dal marketplace Cloud Foundry dell'istanza di {{site.data.keyword.cfee_full_notm}} corrente. Questo tipo di istanza del servizio richiede un broker dei servizi registrato disponibile nell'ambiente. Un broker dei servizi mostra un catalogo di offerte e piani del servizio, oltre a consentire la creazione, la rimozione, il bind (associazione) e l'annullamento del bind delle istanze da tali offerte di servizi. Per ulteriori informazioni, vedi il documento relativo alla [gestione dei broker dei servizi](https://docs.cloudfoundry.org/services/managing-service-brokers.html) nella documentazione Cloud Foundry.
   * 2b. Un'istanza del servizio fornita dall'utente. La creazione di questo tipo è supportata tramite l'interfaccia riga di comando (CLI), ma non tramite l'interfaccia utente. Tuttavia, le istanze del servizio fornite dall'utente verranno elencate nell'interfaccia utente.
   

## Visualizzazione delle istanze del servizio {{site.data.keyword.Bluemix_notm}} in tutti gli ambienti CFEE
{: #viewing-services_across}

Vai al [dashboard Servizi di Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) per visualizzare una vista consolidata di tutte le istanze del servizio {{site.data.keyword.Bluemix_notm}} (a cui hai accesso) nell'account {{site.data.keyword.Bluemix_notm}} e vedi quali sono state aggiunte ai diversi spazi CFEE.

Questa vista mostra tutte le istanze del servizio {{site.data.keyword.Bluemix_notm}} disponibili nell'account e indica quali sono state aggiunte (con alias) ai diversi spazi CFEE. Espandi un'istanza del servizio per visualizzare gli spazi CFEE dove è stata aggiunta.  Puoi eseguirne un'ulteriore espansione per visualizzare le applicazioni in tali spazi a cui è stato eseguito il bind (associazione) di tali istanze del servizio.  

Da questa vista, puoi anche eseguire il bind (associazione) delle applicazioni distribuite negli spazi CFEE a cui queste istanze del servizio sono state aggiunte. Vai al menu che si trova all'estrema destra della riga della tabella per il servizio corrispondente (disponibile per uno specifico spazio CFEE) e seleziona **Associa ad applicazioni**.

## Aggiunta delle istanze del servizio {{site.data.keyword.Bluemix_notm}} esistenti a uno spazio CFEE
{: #adding-services-inspace}

Puoi eseguire il bind (associazione) di istanze del servizio {{site.data.keyword.Bluemix_notm}} alle applicazioni distribuite in uno spazio CFEE.  Prima che sia possibile eseguirne il bind (associazione) a un'applicazione distribuita in CFEE, l'istanza del servizio deve essere aggiunta allo spazio CFEE in cui è distribuita l'applicazione. Prima di poter aggiungere un'istanza del servizio {{site.data.keyword.Bluemix_notm}} a uno spazio CFEE, è necessario quanto segue:
* Il servizio {{site.data.keyword.Bluemix_notm}} deve essere disponibile nello stesso account {{site.data.keyword.Bluemix_notm}} in cui si trova l'istanza CFEE.
* Devi disporre dell'accesso all'istanza del servizio {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, consulta la pagina Identity & Access nel menu**Gestisci > Utenti** nell'intestazione {{site.data.keyword.Bluemix_notm}} per controllare le tue politiche di accesso all'account correnti.

Per aggiungere un'istanza del servizio {{site.data.keyword.Bluemix_notm}} esistente a uno spazio CFEE:
1. Vai al [dashboard Servizi di Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services).  
2. Individua l'istanza del servizio {{site.data.keyword.Bluemix_notm}} dall'elenco e richiama il menu all'estrema destra della riga di tabella corrispondente.
3. Seleziona **Aggiungi servizio**.
4. Nella finestra di dialogo _Aggiungi servizio_, seleziona il CFEE, l'organizzazione e lo spazio dove vuoi aggiungere il servizio e fai clic su **Aggiungi**.
5. Espandi il servizio {{site.data.keyword.Bluemix_notm}} di destinazione per trovare il nuovo CFEE in cui è stato aggiunto il servizio.


In alternativa, puoi aggiungere un'istanza del servizio {{site.data.keyword.Bluemix_notm}} dall'interno dello spazio CFEE dove vuoi aggiungerlo:
1. Nel tuo [dashboard](https://console.bluemix.net/dashboard) {{site.data.keyword.Bluemix_notm}} o nel [dashboard Servizi di Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services), trova l'ambiente Cloud Foundry Enterprise che ospita la tua applicazione.
2. Vai a **Organizzazioni** nel riquadro di navigazione e apri l'organizzazione e lo spazio in cui si trova l'applicazione.
3. Passa alla scheda **Spazi** e individua lo spazio che contiene l'applicazione.
4. Nella pagina dello spazio di destinazione, vai alla scheda **Servizi** e fai clic su **Aggiungi servizio**.  Verrà visualizzata la pagina di dialogo __Aggiungi servizio__.  La pagina elenca le istanze del servizio disponibili nell'account {{site.data.keyword.Bluemix_notm}}.
5. Trova e seleziona un'istanza del servizio disponibile che vuoi aggiungere allo spazio CFEE. 
6. L'istanza del servizio verrà aggiunta all'elenco dei servizi disponibili nello spazio CFEE.

   **Nota:** quando aggiungi un servizio {{site.data.keyword.Bluemix_notm}} a uno spazio CFEE, viene creato un alias a tale istanza del servizio in tale spazio. Quando **Rimuovi** l'istanza del servizio da uno spazio CFEE (dal menu che si trova all'estrema destra della riga dell'istanza del servizio corrispondente nella tabella), il servizio non viene eliminato dall'account pubblico.  L'azione si limita a rimuoverlo dall'account CFEE specifico e non è più disponibile per il bind (associazione) ad applicazioni in tale spazio CFEE.  Inoltre, quando elimini l'istanza del servizio stessa dall'account {{site.data.keyword.Bluemix_notm}}, il servizio non è più disponibile per nessuno degli spazi CFEE. 

## Creazione di istanze del servizio {{site.data.keyword.Bluemix_notm}} da un'interfaccia utente dello spazio CFEE
{: #creating-services_inspace}
Puoi creare le istanze del servizio {{site.data.keyword.Bluemix_notm}} dall'interno di uno spazio CFEE.  La creazione di un'istanza del servizio {{site.data.keyword.Bluemix_notm}} determina quanto segue:
* L'istanza del servizio {{site.data.keyword.Bluemix_notm}} viene creata in IBM Cloud.  Questo è equivalente alla creazione dell'istanza del servizio dal {{site.data.keyword.Bluemix_notm}} [catalogo](https://console.bluemix.net/catalog).
* Un alias dell'istanza del servizio {{site.data.keyword.Bluemix_notm}} viene aggiunta (aggiunta con alias) nello spazio CFEE da cui è stata avviata l'azione di creazione. Un'istanza del servizio alias (in uno spazio CFEE) è un riferimento all'istanza del servizio reale (nell'account di IBM Cloud). L'alias dell'istanza del servizio consente agli sviluppatori di interagire con l'istanza del servizio (ad esempio, bind alle applicazioni) gestendo tutte le credenziali automaticamente per interagire con l'istanza del servizio. .

Per creare un'istanza del servizio dall'interno di uno spazio CFEE:
1. Nella pagina dello spazio di destinazione, vai alla scheda **Servizi** e fai clic su **Crea servizio**.  Verrà aperta la vista **Marketplace** per {{site.data.keyword.cfee_full_notm}}.  La vista elenca le offerte di servizi da due origini (vedi la colonna __Origine__):
   * Le offerte dal catalogo di {{site.data.keyword.Bluemix_notm}} .
   * Le offerte dal marketplace {{site.data.keyword.cfee_full_notm}} locale.
5. Trova e seleziona un'offerta di servizi disponibile che vuoi istanziare. 
6. A seconda dell'origine dell'offerta di servizi (catalogo di IBM Cloud o marketplace CFEE locale), procedi con una delle seguenti operazioni:
   * Se l'offerta di servizi selezionata è un'offerta del catalogo di {{site.data.keyword.Bluemix_notm}}, vedrai un pulsante **Continua** per continuare alla pagina di creazione dell'offerta di servizi IBM Cloud.  È la stessa pagina disponibile dal catalogo di {{site.data.keyword.Bluemix_notm}}.  In questa pagina, fornisci il nome della nuova istanza del servizio, la regione, il piano ed altre proprietà necessarie per creare il servizio in IBM Cloud.  Dopo che avrai creato l'istanza del servizio, essa verrà creata in IBM Cloud e aggiunta automaticamente allo spazio CFEE corrente.
   * Se l'offerta di servizi selezionata proviene dal catalogo CFEE locale, vedrai un pulsante **Crea** per creare l'istanza del servizio. Ti verranno richiesti un'organizzazione e uno spazio nel CFEE corrente dove verrà creata l'istanza del servizio.

## Creazione di istanze del servizio {{site.data.keyword.Bluemix_notm}} da uno spazio CFEE utilizzando la CLI
{: #creating-services_cli}

Puoi creare un'istanza del servizio dalla CLI da uno spazio in un CFEE.  La creazione di un servizio dalla CLI in uno spazio CFEE è equivalente a crearlo dall'IU in tale spazio. La creazione di un servizio ha, cioè, il seguente duplice risultato:
* L'istanza del servizio {{site.data.keyword.Bluemix_notm}} viene creata in IBM Cloud.  Questo è equivalente alla creazione dell'istanza del servizio dal {{site.data.keyword.Bluemix_notm}} [catalogo](https://console.bluemix.net/catalog).
* L'istanza del servizio {{site.data.keyword.Bluemix_notm}} viene aggiunta (aggiunta con alias) nello spazio CFEE da cui è stata avviata l'azione di creazione.

La differenza tra la creazione di un'istanza del servizio da uno spazio CFEE rispetto alla sua creazione dalla CLI consiste nel ciclo di vita dell'istanza del servizio creata. Quando crei l'istanza del servizio nell'IU dello spazio CFEE, il ciclo di vita dell'istanza del servizio creata è controllato dall'istanza del servizio stessa nell'account {{site.data.keyword.Bluemix_notm}}.  Ciò significa che gli aggiornamenti al piano di servizio sono controllati dall'istanza nell'account {{site.data.keyword.Bluemix_notm}}, non dallo spazio CFEE. In alternativa, se l'istanza del servizio viene creata dalla CLI, il ciclo di vita del servizio è controllato dallo spazio CFEE (il servizio viene aggiornato dallo spazio CFEE).

Le istanze del servizio create dalla CLI sono visualizzate anche nell'IU e sono indicate da un ` * ` accanto al nome dell'istanza del servizio.

Per creare le istanze del servizio utilizzando la CLI, attieniti alla seguente procedura:

1. Scarica e installa la CLI (command line interface) {{site.data.keyword.Bluemix}} (se non l'hai già fatto). [Scarica la CLI Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

2. Vai alla pagina Panoramica di {{site.data.keyword.cfee_full}} e individua l'endpoint API dell'ambiente.

3. Nella CLI (command line interface), imposta l'endpoint API sull'endpoint del tuo ambiente CFEE.

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Accedi all'ambiente CFEE:

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Se stai utilizzando un ID federato, utilizza l'opzione `-sso`:

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. Crea il servizio:
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  Facoltativamente, puoi fornire un file che contiene i parametri in un oggetto JSON valido richiesto per la creazione di uno specifico servizio.
  Il percorso al file dei parametri può essere un percorso assoluto o relativo a un file.
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  Il seguente è un esempio di un oggetto JSON valido:
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   Per una guida nella creazione di un servizio dalla CLI, immetti:
  
  ```
  cf cs -help
  ```
  Per ulteriori informazioni, vedi il documento relativo alla [gestione delle istanze del servizio con la CLI cf](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") nella documentazione di Cloud Foundry.
  
## Esecuzione del bind (associazione) di servizi alle applicazioni
{: #bind_services}

Gli utenti con ruolo _editor_ o superiori a un'istanza del servizio {{site.data.keyword.Bluemix_notm}} possono eseguire il bind di quell'istanza a un'applicazione distribuita in uno spazio CFEE, dal [dashboard Servizi cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) o dalla scheda Services di un'interfaccia utente di uno spazio CFEE.   

Per eseguire il bind (associazione) di un'istanza del servizio a un'applicazione dal [dashboard Servizi di Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services):
1. Vai al [dashboard Servizi di Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/services) per visualizzare una vista consolidata di tutte le istanze del servizio {{site.data.keyword.Bluemix_notm}} disponibili per te nell'account {{site.data.keyword.Bluemix_notm}}.  La vista è anche concepita per visualizzare quali istanze del servizio {{site.data.keyword.Bluemix_notm}} sono disponibili (con alias) nei diversi spazi CFEE. Puoi espandere un'istanza del servizio per visualizzare gli spazi CFEE dove è stata aggiunta.  Puoi eseguirne un'ulteriore espansione per visualizzare le applicazioni in tali spazi a cui è stato eseguito il bind (associazione) di tali istanze del servizio. 
2. Individua l'istanza del servizio {{site.data.keyword.Bluemix_notm}} di cui vuoi eseguire il bind (associazione).
3. Espandi la vista corrispondente per visualizzare tutti gli spazi CFEE dove è stata aggiunta tale istanza del servizio. Se tale istanza del servizio non è stata aggiunta allo spazio CFEE dove è distribuita l'applicazione, seleziona **Aggiungi** dal menu all'estrema destra della riga per rendere l'istanza del servizio disponibile nello spazio CFEE di destinazione.
4. Vai al menu che si trova all'estrema destra della riga corrispondente al CFEE e/o allo spazio dove l'istanza del servizio è disponibile e seleziona **Associa applicazione**.
5. Nella finestra di dialogo __Associa applicazione__, seleziona l'applicazione di cui vuoi eseguire il bind (associazione).
6. Per l'applicazione è stato ora eseguito il bind (associazione) all'istanza del servizio. Puoi espandere un'istanza del servizio nella tabella per visualizzare le applicazioni associate ad essa (in uno spazio CFEE specifico).


Per eseguire il bind (associazione) di un'applicazione a un'istanza del servizio dalla pagina __Servizi__ di uno spazio CFEE:

1. Apri l'interfaccia utente CFEE dove è distribuita l'applicazione.
2. Vai a **Organizzazioni** nel riquadro di navigazione a sinistra e apri l'organizzazione e lo spazio dove è distribuita l'applicazione.
3. Passa alla scheda **Spazi** e individua lo spazio che contiene l'applicazione.
4. Nella pagina dello spazio di destinazione, vai alla scheda **Servizi**.
5. Nella tabella di **Istanze del servizio**, vai al menu __Azioni__ all'estrema destra della riga corrispondente all'istanza del servizio di cui desideri eseguire il bind (associazione) e seleziona **Associa**.
6. Seleziona l'applicazione di cui vuoi eseguire il bind (associazione) all'istanza del servizio.

Per annullare l'associazione da un'istanza del servizio:

1. Nella scheda **Servizi** dello spazio, espandi l'istanza del servizio di destinazione per mostrare le applicazioni che sono associate ad essa.
2. Vai al menu Azioni in una riga dell'applicazione e seleziona **Annulla associazione del servizio**.

Vedi il documento relativo [al bind (associazione) di un'istanza del servizio](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") nella documentazione di Cloud Foundry per ulteriori informazioni sull'esecuzione del bind delle applicazioni utilizzando la CLI.

## Visibilità del servizio
{: #service_visibility}

I clienti possono controllare chi può creare nuovi servizi di IBM Cloud da un ambiente CFEE.  Possono anche controllare chi può aggiungere i servizi di IBM Cloud esistenti a uno spazio CFEE.  Questo controllo viene esercitato controllando la visibilità delle offerte di servizi (e/o le istanze di tali offerte di servizi) agli utenti.

### Controllo della creazione delle istanze del servizio
{: #control_servicecreation}

Il controllo della creazione dei servizi può essere realizzato controllando la visibilità delle offerte di servizi nel catalogo di IBM Cloud per tutti gli utenti nell'account IBM Cloud o per gli utenti in organizzazioni Cloud Foundry specifiche.

#### Controllo della visibilità agli utenti in un account IBM Cloud al catalogo IBM Cloud
{: #creation_accountvisibility}

Gli amministratori dell'account di IBM Cloud (utenti con ruolo _Amministratore_ a tutti i servizi abilitati IAM) possono impedire a un servizio o un piano del servizio di essere mostrato nel catalogo a tutti gli utenti in un dato **account IBM Cloud**.  Gli amministratori dell'account possono impedire a tutti gli utenti dell'account di utilizzare un servizio inserendo il servizio o il piano del servizio nella blacklist per tutti gli utenti in un account. L'inserimento nella blacklist di un servizio impedirà agli utenti in quell'account anche di visualizzare tale servizio (o piano del servizio) nel catalogo IBM Cloud.  Ciò viene effettuato tramite un comando `ibmcloud catalog blacklist` che ha la seguente sintassi:

  ```
  ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]
  ```

Nella sua forma più semplice, puoi inserire nella blacklist un'offerta di servizi (tutti i suoi piani) per renderla invisibile agli utenti nell'account corrente immettendo il seguente comando:

  ```
  Ibmcloud catalog blacklist <thisService>
  ```
  {: pre}

Potresti inserire nella blacklist la visibilità non solo generale per l'offerta di servizi completa, ma di un piano specifico in una regione specifica.  Per questo, devi utilizzare l'ID per la voce corrispondente nel catalogo globale, non il nome.   Se vuoi impedire agli utenti di vedere un piano specifico in una regione specifica puoi immettere quanto segue:

  ```
  Ibmcloud catalog blacklist -add <catalogEntryID>
  ```
  {: pre}
  
 Per rimuovere i servizi dalla blacklist:
 ```
  Ibmcloud catalog blacklist -remove <catalogEntryID>
  ```
  {: pre}
 
Puoi trovare l'ID di una voce del catalogo selezionata (ad esempio, il piano di un servizio e la sua regione di distribuzione) tramite il seguente comando. Il comando restituisce tutti i piani e le rispettive regioni di distribuzione per un determinato servizio:

  ```
  ibmcloud catalog service <thisService>
  ```
  {: pre}

Puoi trovare ulteriori dettagli per `ibmcloud catalog blacklist` immettendo le seguenti informazioni:

  ```
  Ibmcloud catalog blacklist -help
  ```
  {: pre}


#### Controllo della visibilità agli utenti in un'organizzazione Cloud Foundry
{: #creation_orgvisibility}

Puoi utilizzare i comandi `cf enable-service-access` e `cf disable-service-access` per controllare l'accesso si servizi di **organizzazioni Cloud Foundry** specifiche.  Qui il punto di controllo per l'accesso è Cloud Foundry (non l'account di IBM Cloud).  Nota che questo è un comando `cf` nativo (non un comando `ibmcloud`). 

Considera quanto segue quando imposti la visibilità del servizio tramite la CLI `cf`:

*  I comandi `cf` abilitano e/o disabilitano le offerte di servizi (facoltativamente, piani di offerta di servizi specifici) per tutti gli utenti di organizzazioni Cloud Foundry specifiche
* L'abilitazione funziona creando un'organizzazione “whitelist”. Cioè, un elenco di inclusione di organizzazioni Cloud Foundry che hanno accesso a un servizio (invece dell'approccio "blacklist" nel comando `ibmcloud` descritto in precedenza, che funziona definendo un elenco di servizi esclusi dalla visibilità per gli utenti dell'account). Ciò significa che il controllo dell'accesso a un servizio del catalogo con questo approccio funziona, non definendo quali organizzazioni non possono vedere un servizio (blacklist), ma definendo quali organizzazioni possono vederlo (whitelist).
*  Quando fornisci un accesso dell'organizzazione a un servizio (o piano di servizi) aggiungendo tale organizzazione a una whitelist, stai di fatto disabilitando (escludendo) tutte le altre organizzazioni dall'accedervi.  Cioè, una volta che inserisci nella whitelist un'organizzazione, stai disabilitando tutte le altre organizzazioni dall'accedere a quel servizio (o piano di servizi)
*  Prima di aggiungere le organizzazioni all'elenco "can see", devi disabilitare la visibilità di tutte le organizzazioni.  Non puoi disabilitare l'accesso a un piano di servizi se è al momento disponibile per tutte le organizzazioni.

In conformità al comportamento generale descritto in precedenza, ti consigliamo di controllare l'accesso all'organizzazione ai servizi immettendo i seguenti comandi:
1. **Disable** accesso a un piano di servizi per tutte le organizzazioni:
  ```
  cf disable-service-access <service name> -p <plan name>
  ```
  {: pre}
  
2. **Enable** accesso al piano di servizi per le organizzazioni CFEE specifiche.  Questo disabiliterà il piano di servizi per tutte le altre organizzazioni non specificatamente abilitate nel comando. 
  ```
  cf enable-service-access <service name> -p <plan name> -o <org name>
  ```
  {: pre}
  
**Nota:** ti consigliamo di eseguire i comandi del servizio enable e disable di Cloud Foundry per il servizio completo, non per piani specifici.


### Controllo dell'accesso alle istanze del servizio esistenti
{: #control_serviceaddition}

Gli sviluppatori in uno spazio CFEE possono utilizzare le istanze del servizio esistenti disponibili nell'account di IBM Cloud.  All'interno di uno spazio specifico di un CFEE, gli utenti possono **Aggiungere** un'istanza del servizio a tale spazio (consulta [Aggiunta di istanze del servizio esistenti](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) in precedenza). L'aggiunta di un'istanza del servizio a uno spazio CFEE crea un alias (un riferimento) all'istanza del servizio, che consente a uno sviluppatore di associare l'istanza del servizio a un'applicazione distribuita in quello spazio CFEE come se fosse l'istanza del servizio effettiva.

Gli amministratori dell'account possono controllare l'utilizzo delle istanze del servizio tramite le [Politiche di accesso IAM](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage).  Dall'IU o dalla CLI ibmcloud possono assegnare i ruoli alle istanze di servizio stesse e ai gruppi di risorse in cui si trovano tali istanze.  Uno sviluppatore ha bisogno del ruolo di _Visualizzatore_ o superiore a un'istanza del servizio (o al suo gruppo di risorse) prima di poter aggiungere quella istanza a uno spazio.

Puoi trovare i video su discussioni e dimostrazioni approfondite sui servizi CFEE in [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
{:tip}
