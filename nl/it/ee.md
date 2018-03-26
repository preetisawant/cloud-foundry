---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Scenario: sviluppo end-to-end
{: #ee}


Puoi utilizzare la console, la piattaforma e una selezione di strumenti {{site.data.keyword.Bluemix}} per la creazione, esecuzione e distribuzione delle tue applicazioni. Per iniziare, segui questo scenario di sviluppo
end-to-end.
{:shortdesc}

## Registrazione
{: #ee_start}

Per iniziare, vai alla [console IBM Cloud ![Icona link esterno](../icons/launch-glyph.svg)](https://bluemix.net){: new_window}. Registra un ID IBM e accedi a {{site.data.keyword.Bluemix_notm}} per iniziare la tua prova gratuita di 30 giorni. {{site.data.keyword.Bluemix_notm}} fornisce
una franchigia di 2 GB di memoria di runtime e 10 istanze del servizio per la tua prova
gratuita.

## Sviluppo della tua applicazione
{: #develop}

Esistono tre modi per sviluppare la tua applicazione:

* Con il [servizio Continuous Delivery](#ee_cd)
* Nel dashboard dell'[interfaccia utente IBM Cloud](#ee_appui)
* Attraverso la [riga di comando Cloud Foundry](#ee_cf)

## Sviluppo e distribuzione delle tue applicazioni attraverso le toolchain e il servizio {{site.data.keyword.contdelivery_short}}
{: #ee_cd}

<a href="/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app">Aggiungi una toolchain</a> che include il servizio {{site.data.keyword.contdelivery_full}} nella tua applicazione. Quindi, <a href="/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using">utilizza la toolchain</a> per sviluppare e distribuire la tua applicazione.

## Creazione della tua applicazione web con l'interfaccia utente {{site.data.keyword.Bluemix_notm}}
{: #ee_appui}

Dopo la registrazione, inizia a creare la tua prima applicazione utilizzando il catalogo e il dashboard {{site.data.keyword.Bluemix_notm}}.

In {{site.data.keyword.Bluemix_notm}},
le applicazioni sono associate a organizzazioni e spazi. Un'organizzazione
appartiene ed è utilizzata da più collaboratori. Inizialmente, ottieni
un'organizzazione predefinita che prende il nome dal tuo nome utente e di cui
sei l'unico collaboratore. All'interno di questa organizzazione ottieni anche uno spazio. Lo spazio è un ambiente per l'esecuzione delle tue applicazioni; ad esempio, puoi
avere uno spazio di sviluppo come un ambiente di sviluppo, uno spazio di test come un ambiente di test
e uno spazio di produzione come un ambiente di produzione. iascuno degli ambienti appartiene a una regione. Con {{site.data.keyword.Bluemix_notm}},
puoi distribuire le applicazioni a una specifica regione geografica
per una bassa latenza di rete, riservatezza dei dati e maggiore disponibilità.

Per questo scenario, vuoi distribuire un'applicazione Web che utilizza Node.js. Supponiamo che ti trovi negli Stati Uniti così come la maggior parte degli utenti della
tua applicazione. Decidi di creare ed eseguire la tua applicazione vicino alla base
dei tuoi utenti, in modo da poter usufruire di una più bassa latenza di rete. Dopo che ti sei collegato a {{site.data.keyword.Bluemix_notm}}, fai clic sul link delle preferenze dell'account utente e seleziona la regione **Stati Uniti Sud**. Puoi quindi attenerti alla seguente procedura per creare un'applicazione:

  1. Fai clic su **Catalogo** nella barra degli strumenti {{site.data.keyword.Bluemix_notm}}.
  2. Seleziona **Applicazioni Cloud Foundry**.
  3. Seleziona **SDK for Node.js**.
  4. Immetti un nome univoco per la tua applicazione e fai clic su **Crea**. Il nome dell'applicazione deve essere univoco
nell'intero ambiente {{site.data.keyword.Bluemix_notm}}.

Adesso, puoi visualizzare l'**Esercitazione introduttiva**. Segui le istruzioni per scaricare il codice starter della tua applicazione, modificarlo e distribuirlo.

All'applicazione viene assegnata 1 istanza e 512 MB di quota di memoria
per impostazione predefinita. Puoi aumentare la memoria o aggiungere più istanze per
garantire la disponibilità elevata della tua applicazione; ad esempio 3 istanze con 1 GB
di memoria per ciascuna istanza. Fai clic su **Visualizza panoramica dell'applicazione** per
specificare le istanze della tua applicazione e la quota di memoria. Ad esempio, immetti 3 per
istanze e 1 GB per quota di memoria e fai clic su **Salva**. Puoi inoltre visualizzare file, log e variabili di ambiente per la risoluzione
dei problemi.

### Esecuzione del bind di un servizio utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}}
{: #ee_bindui}

Dopo aver creato la tua applicazione, connetti a un database con l'applicazione. Puoi memorizzare ed esaminare i dati dell'applicazione utilizzando il linguaggio di query del database. In questo scenario, decidi di
utilizzare il servizio {{site.data.keyword.cloudant}}
fornito da {{site.data.keyword.Bluemix_notm}}.

Per utilizzare i servizi all'interno dell'applicazione, crea un'istanza del servizio ed esegui il bind della tua applicazione all'istanza del servizio completando la seguente procedura:

  1. Nel catalogo {{site.data.keyword.Bluemix_notm}}, seleziona il servizio {{site.data.keyword.cloudant}}. Aggiungi un nome univoco per il tuo servizio Cloudant e fai clic su **Crea**. Nel pannello di gestione Cloudant, avvia il servizio facendo clic su **Avvia**.
  2. Fai clic su **Connessioni** e quindi su **Crea connessione**.
  3. Fai clic su **Connetti** accanto alla tua applicazione.
  4. Viene visualizzata la finestra Riprepara applicazione. Fai clic su **Riprepara**.

La tua applicazione è ora associata al servizio {{site.data.keyword.cloudant}}. Puoi trovare tutti i dati necessari perché l'applicazione comunichi con l'istanza del servizio nella variabile di ambiente VCAP_SERVICES. Ad esempio, poiché {{site.data.keyword.Bluemix_notm}}
ospita diverse applicazioni sulla stessa macchina virtuale, le applicazioni
non possono utilizzare lo stesso numero di porta HTTP per ricevere le richieste
in entrata. Per evitare conflitti, a ciascuna applicazione viene dato un
numero di porta univoco. Questo numero di porta è disponibile nella variabile di ambiente VCAP_APP_PORT.

Puoi visualizzare l'intero elenco di variabili VCAP_SERVICES associate alla tua applicazione nel dashboard. Per visualizzare l'elenco, fai clic sul Menu nella barra degli strumenti IBM Cloud e seleziona **Dashboard**. Fai clic sulla tua applicazione, quindi seleziona **Runtime** e fai clic sulla scheda **Variabili di ambiente**.

**Nota:** questa variabile di ambiente è la serializzazione di un oggetto JSON con una singola voce per ogni istanza del servizio a cui è associata l'applicazione. La quantità e il tipo di dati forniti da ciascuna istanza del servizio
sono specifici per il servizio. Se l'applicazione non utilizza alcun servizio, VCAP_SERVICES è un oggetto JSON vuoto. Questa variabile di ambiente viene utilizzata solo
quando aggiungi un servizio alla tua applicazione.

## Creazione della tua applicazione utilizzando la CLI cf
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}} fornisce
diversi strumenti che ti consentono di iniziare a scrivere codice con la tua applicazione, ad esempio l'interfaccia riga di comando cf
e gli strumenti Eclipse. Puoi scegliere l'interfaccia riga di comando cf per iniziare a scrivere codice con la tua applicazione.

  1. Innanzitutto, scarica e sviluppa il tuo codice applicativo.

    1. Fai clic su Introduzione nel dashboard della tua applicazione. Fai clic sul link **Scarica il codice di esempio** per scaricare il codice della tua applicazione.
    2. Estrai il file scaricato in una directory, ad esempio `C:\test`.
    3. Sviluppa il codice con il tuo ambiente di sviluppo
integrato locale.

  2. Installa l'interfaccia riga di comando **cf**
(CLI).

    1. Scarica il programma di installazione dello strumento riga di comando cf per il tuo sistema operativo.
    2. Segui la procedura guidata dello strumento per completare l'installazione.
    3. Utilizza il comando `cf -v` per verificare la versione dell'interfaccia riga di comando cf.

    **Requisito:** assicurati di usare sempre la versione più recente dello strumento riga di comando cf.

  3. Dopo che hai installato l'interfaccia riga di comando **cf**,
devi specificare qual è la regione {{site.data.keyword.Bluemix_notm}} che
desideri gestire utilizzando il comando **cf api**. L'interfaccia riga di comando **cf** utilizza *https://api.[Bluemix_URL]*, dove *Bluemix_URL* è l'URL della regione. L'endpoint API per la regione Stati Uniti Sud è `ng.bluemix.net`. Immetti il seguente comando per
stabilire una connessione a {{site.data.keyword.Bluemix_notm}}:

  ```
  cf api https://api.ng.bluemix.net
  ```

  Per trovare altri endpoint API, vedi [Regioni](/docs/overview/cf.html#ov_intro_reg). Dopo che hai specificato la regione {{site.data.keyword.Bluemix_notm}},
le informazioni sull'ubicazione da te specificate vengono salvate.

  4. Successivamente, accedi a {{site.data.keyword.Bluemix_notm}} utilizzando il comando `cf login`.

  ```
  cf login -u your_user_ID -p ***** -o your_org_name -s your_space_name
  ```

  Se la tua organizzazone utilizza il single sign on, usa `cf login -sso`.

  5. Dopo che hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}},
sei pronto a ridistribuire l'applicazione a {{site.data.keyword.Bluemix_notm}}. Dalla directory dell'applicazione `C:\test`, immetti il seguente
comando:

  ```
  cf push [your_appname]
  ```

  Per ulteriori informazioni sul comando **cf
push**, vedi [Caricamento della tua applicazione](/docs/cfapps/hostingapps.html#ht_cfcli).

  6. Puoi ora accedere all'applicazione immettendo il seguente URL
in un browser:
  ```
  http://your_app.stage1.mybluemix.net
  ```

Per creare la tua applicazione puoi scegliere anche altri strumenti, ad esempio
gli strumenti Eclipse. Per ulteriori informazioni, consulta la pagina Introduzione della tua applicazione nel dashboard {{site.data.keyword.Bluemix_notm}}.

### Esecuzione del bind di un servizio utilizzando la CLI cf
{: #ee_cfbind}

Puoi anche eseguire il bind di un servizio utilizzando l'interfaccia riga di comando **cf**. Supponiamo che tu voglia aggiungere il servizio {{site.data.keyword.cloudant}} alla tua applicazione con l'interfaccia riga di comando cf.

Per utilizzare il servizio {{site.data.keyword.cloudant}} all'interno dell'applicazione, crea un'istanza del servizio Cloudant, esegui il bind della tua applicazione all'istanza del servizio e quindi utilizza l'istanza. La stessa procedura si applica a tutti gli altri servizi.

  1. Crea un'istanza del servizio Cloudant NoSQL DB.

  Usa il comando cf create-service per creare una nuova istanza di un servizio. In questo esempio, *Lite* è il nome del piano. Ad
esempio:

  ```
  cf create-service cloudantNoSQLDB Lite [your_name_for_your_cloudant_service]
  ```

  Puoi anche usare il comando cf services per visualizzare l'elenco di istanze del servizio da te create.

  ```
  cf services
  ```

  Dopo essere stata creata, un'istanza del servizio è a disposizione di tutte le
tue applicazioni che possono eseguirne il bind e farne uso.

  2. Esegui il bind dell'istanza del servizio alla tua applicazione.

  Per utilizzare un'istanza del servizio, devi eseguirne il bind alla
tua applicazione. Usa il comando cf bind-service per eseguire il bind di un'istanza del servizio a un'applicazione specificando il nome applicazione e l'istanza del servizio da te creata.

  ```
  cf bind-service [your_app_name] [your_name_for_your_cloudant_service]
  ```

  L'esecuzione del bind di un'istanza del servizio a un'applicazione abilita {{site.data.keyword.Bluemix_notm}} a
comunicare con il servizio e a specificare che una nuova applicazione comunicherà con tale
istanza del servizio. Per servizi differenti, {{site.data.keyword.Bluemix_notm}} può
elaborare l'applicazione e l'istanza del servizio in modo differente, durante il bind. Ad esempio, alcuni servizi possono creare un nuovo
tenant per ciascuna applicazione che comunica con l'istanza del servizio. Il servizio risponde a
sua volta a {{site.data.keyword.Bluemix_notm}} con
delle informazioni, come le credenziali, che devono essere passate all'applicazione
per le comunicazioni tra l'applicazione e il servizio.

  **Nota:** se l'applicazione è in esecuzione quando è associata a un'istanza del servizio, la variabile di ambiente VCAP_SERVICES viene aggiornata solo dopo il riavvio dell'applicazione. Per riavviare la tua applicazione, usa il comando cf restart.

  3. Usa l'istanza del servizio.

  In questo scenario, la variabile di ambiente VCAP_SERVICES include delle informazioni, come i seguenti elementi, che un'applicazione può utilizzare per stabilire una connessione a questa istanza di {{site.data.keyword.cloudant}}:

  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>segreto</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dl>

  Ad esempio, la tua applicazione Node.js potrebbe accedere a queste
informazioni nel seguente modo:
  ```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```

  **Nota:** come mostrato dal codice di esempio, per stabilire una connessione a un'istanza del servizio {{site.data.keyword.cloudant}}, puoi prima controllare se la variabile di ambiente VCAP_SERVICES esiste. Se esiste, l'applicazione può utilizzare le proprietà della variabile cloudant per accedere al database. Tuttavia, se la variabile di ambiente VCAP_SERVICES non è presente, l'istanza del servizio {{site.data.keyword.cloudant}} locale viene utilizza valori predefiniti forniti.

  4. Interagisci con l'istanza del servizio.

  Puoi interagire con l'istanza del servizio utilizzando le informazioni delle credenziali. Le azioni che puoi eseguire includono la lettura, la scrittura e l'aggiornamento. Il
seguente esempio illustra come inserire un oggetto JSON nell'istanza del servizio
{{site.data.keyword.cloudant}}:

  ```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```

  5. **Facoltativo:** annulla il bind di un'istanza del servizio oppure eliminala.

  È possibile che tu voglia annullare il bind di un'istanza del servizio oppure eliminarla qualora
non sia più utilizzata o per liberare dello spazio. Per annullare il bind di un'istanza del servizio alla tua applicazione, usa il **comando cf unbind-service**; per eliminare un'istanza del servizio, usa il comando **cf delete-service**.

  Per ulteriori informazioni sui servizi, vedi Servizi. Per ulteriori informazioni sulle opzioni **cf** che puoi utilizzare per gestire le tue applicazioni nell'ambiente {{site.data.keyword.Bluemix_notm}}, immetti il comando **cf --help** nell'interfaccia riga di comando **cf**.

  **Nota:** assicurati di non avere più bisogno di un'istanza del servizio, prima di eliminarla. L'eliminazione di un'istanza del servizio elimina tutti i dati a essa associati. È possibile aggiornare la variabile di ambiente VCAP_SERVICES di un'applicazione associata a un servizio eliminato solo dopo il riavvio dell'applicazione.

## Calcolo del costo della tua applicazione
{: #ee_billing}

Il tuo periodo di prova gratuito di 30 giorni è scaduto ma vuoi continuare
a utilizzare {{site.data.keyword.Bluemix_notm}}. Per continuare a utilizzare {{site.data.keyword.Bluemix_notm}}
dovrai aggiungere le informazioni della tua carta di credito per un account Pagamento a consumo o per un account Sottoscrizione. Tuttavia, {{site.data.keyword.Bluemix_notm}} continua a offrire una franchigia per la
maggior parte dei servizi e dei framework di runtime anche se passi a un account a pagamento. {{site.data.keyword.Bluemix_notm}}
non ti addebita niente a meno che l'utilizzo non superi le franchigie concesse.

{{site.data.keyword.Bluemix_notm}} fornisce
una funzione di stima e un calcolatore per consentirti di visualizzare il costo della tua applicazione. Puoi visualizzare il costo della tua applicazione nei seguenti modi:

  * Nel tuo dashboard, fai clic sulla tua applicazione. Quindi, nella pagina Panoramica, fai clic su **Stima il costo di questa applicazione** per vedere il prezzo del runtime e del supporto **SDK for Node.js** e il prezzo totale mensile della tua applicazione.

  * In alternativa, nella pagina Listino prezzi, immetti l'utilizzo mensile del runtime e dei servizi della tua applicazione. Ad esempio 3 istanze di **SDK for Node.js** con 1 GB
di memoria per ciascuna istanza. Il prezzo mensile viene calcolato e visualizzato.

Puoi anche calcolare il costo della tua applicazione manualmente sommando i prezzi dei tuoi runtime e servizi
e sottraendo la franchigia. Per ulteriori informazioni, vedi Calcolo manuale dei tuoi costi.

## Rimozione di applicazioni
{: #ee_removing}

Man mano che crei ulteriori applicazioni, la quota potrebbe avvicinarsi al limite. Tuttavia, delle applicazioni
che tu potresti non utilizzare più continuano a consumare una parte della quota. È facile eliminare delle applicazioni per liberare dello
spazio in {{site.data.keyword.Bluemix_notm}} in qualsiasi momento.

Nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}, vai alla pagina Panoramica dell'applicazione, fai clic sull'icona **Menu** ed elimina l'applicazione che non utilizzi più. Per eliminare le applicazioni puoi anche utilizzare il comando **cf delete**.
