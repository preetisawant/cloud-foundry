---

copyright:

  years: 2018
lastupdated: "2018-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Aggiornamento e ridimensionamento
{: #update-scale}

Aggiorna l'istanza del servizio {{site.data.keyword.cfee_full_notm}} all'ultima versione per ottenere le ultime correzioni e funzioni di CFEE. Gli aggiornamenti per ICDEE possono includere nuove versioni della piattaforma Cloud Foundry e del cluster Kubernetes che supportano l'infrastruttura CFEE.

Gli aggiornamenti della versione CFEE sono effettuati sul piano di controllo contenente i componenti CFEE e sulle celle. Puoi anche ridimensionare la capacità della tua istanza CFEE aggiungendo o eliminando le celle dell'applicazione.

**Nota:** durante un aggiornamento della versione o mentre le celle vengono aggiunte o eliminate, alcune metriche (ad esempio, Memoria e CPU) visualizzate nelle pagine _Overview_, _Resource Usage_ e _Update and Scaling_ potrebbero non essere disponibili.

## Aggiornamento della versione di CFEE
{: #update}

Gli utenti hanno bisogno delle seguenti autorizzazioni per poter aggiornare un'istanza CFEE a una nuova versione:
   * Ruolo di _Editor_ o superiore per un'istanza CFEE.
   * Ruolo di _Operatore_ o superiore al cluster Kubernetes in cui viene eseguito il provisioning della CFEE.

L'aggiornamento della versione di CFEE della tua istanza CFEE è un processo a due fasi. Prima, aggiorna il piano di controllo che ospita il componente CFEE. Poi, aggiorna le celle che ospitano le tue applicazioni.

I seguenti vincoli e regole vengono applicati durante l'aggiornamento di un CFEE a una nuova versione:
* Il piano di controllo deve essere aggiornato per primo. Una volta che il piano di controllo è stato aggiornato possono essere aggiornate le celle.
* Le celle dell'applicazione possono essere aggiornate solo alla versione del piano di controllo.  Cioè, le celle del piano di controllo possono essere ad un livello di versione CFEE superiore rispetto alle celle dell'applicazione, ma non viceversa.

Per aggiornare la versione di CFEE della tua istanza CFEE:
1. Vai al [Dashboard {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) e apri il {{site.data.keyword.cfee_full_notm}} che vuoi aggiornare.
2. In {{site.data.keyword.cfee_full_notm}}, vai alla voce **Celle** nel pannello di navigazione per aprire la pagina delle celle.
3. (Facoltativo) Nella tabella _Piano di controllo_ puoi espandere la riga per visualizzare i nodi di lavoro nel piano di controllo.
4. Fai clic su **Aggiorna**.
5. Nella finestra di dialogo Aggiorna il _Piano di controllo_, seleziona una delle versioni CFEE disponibili e fai clic su **Aggiorna**. L'aggiornamento dura circa 5 minuti.  La descrizione della versione illustra le versioni dei componenti inclusi nel pacchetto di versione CFEE selezionato, insieme a un link al documento _Novità_ che descrive il contenuto fornito in tale versione.
6. La colonna _Stato nodi_ mostra l'avanzamento dell'aggiornamento. Una volta che l'aggiornamento è completo, la colonna _Versione_ riflette la nuova versione CFEE.
7. Una volta completato l'aggiornamento delle celle del piano di controllo, trova la tabella _Celle_ e fai clic su **Aggiorna**.
8. Nella finestra di dialogo _Aggiorna piano di controllo_ seleziona la versione CFEE e fai clic su *Aggiorna*. È presente solo la versione disponibile per le celle da aggiornare perché le celle possono essere aggiornate solo alla versione del piano di controllo. Una sola azione di aggiornamento aggiorna tutte le celle.
9. Le celle vengono aggiornate in sequenza. La colonna _Stato nodi_ indica l'avanzamento dell'aggiornamento di ogni cella. Come le celle vengono aggiornate, la loro nuova versione si riflette nella colonna _Versione_.

## Interruzioni durante l'aggiornamento della versione
{: #update-disruption}

L'aggiornamento del piano di controllo Cloud Foundry non comporta interruzioni.  Tuttavia, l'aggiornamento delle celle Cloud Foundry a una nuova versione CFEE può interrompere il funzionamento dell'ambiente CFEE.  L'aggiornamento viene eseguito una cella alla volta, in modo che le istanze dell'applicazione in esecuzione in una cella vengano riattivate una volta completato l'aggiornamento mentre le altre celle vengono disattivate durante il proprio aggiornamento. Tuttavia, alcuni servizi e applicazioni in esecuzione in CFEE potrebbero diventare indisponibili in alcune circostanze. Ad esempio, se il CFEE dispone di due celle Cloud Foundry a piena capacità, un'applicazione con una sola istanza verrà disattivata durante l'aggiornamento della versione perché l'istanza dell'applicazione non può essere spostata in un'altra cella mentre la cella è in fase di aggiornamento e, di conseguenza, l'applicazione non sarà disponibile.  

Durante l'aggiornamento della versione potrebbe esserci una discrepanza nelle metriche di Memoria e CPU riportate nei misuratori dei nodi della cella mostrati nella pagina CFEE _Overview_ (che sono generati dal cluster Kubernetes) e le stesse metriche mostrate nel dashboard _Nodes_ in Grafana (che sono generate a livello del sistema operativo).

Lo stato dei componenti CFEE mentre l'aggiornamento è in corso si rifletterà nella pagina Health Check.  Il riavvio richiede circa 45 minuti. 

## Politica del ciclo di versione e supporto
{: #version-cycle}

Il servizio Cloud Foundry Enterprise Environment normalmente rilascia una nuova versione su base regolare. La versione del servizio segue il formato delle versioni semantiche _**Major.Minor.Patch**_ (https://semver.org/)

La versione _minore_ viene incrementata regolarmente (normalmente, in modo mensile). Anche la versione _maggiore_ viene incrementata, ma meno frequentemente, normalmente quando c'è una modifica significativa.  L'aggiornamento ad una versione _maggiore_ potrebbe causare delle interruzioni durante l'aggiornamento. Le _patch_ forniscono una correzione e vengono applicate alla versione disponibile più recente. 

Per evitare un'interruzione del sistema, le istanza CFEE possono essere aggiornate solo a 2 versioni _maggiori_ in più rispetto alla loro versione corrente. Utilizzando l'esempio precedente, se la versione corrente dell'istanza CFEE è 3.1.2 e la versione di destinazione è 7.0.0, l'istanza CFEE deve essere aggiornata prima alla versione 5.x.x e quindi alla versione di destinazione 7.0.0.

Nuove funzionalità e miglioramenti alle funzionalità esistenti vengono fornite regolarmente e diventano disponibili solo nella versione più recente. Le correzioni critiche vengono fornite nell'ultima release solo per le ultime 3 versioni _maggiori_ (l'ultima versione e le due versioni precedenti). Ad esempio, se le versioni 4.x.x, 3.x.x e 2.x.x sono disponibili, le versioni 1.x.x non saranno supportate (ad esempio, le patch non verranno fornite con correzioni per le versioni 1.x.x).  

Le patch vengono fornite per la versione _maggiore_ più recente disponibile. Ad esempio, se un'istanza CFEE è in esecuzione con la versione 3.1.2 ma l'ultima versione _maggiore_ disponibile in 3.x.x è la versione 3.3.4, tutte le patch saranno fornite sulla base di codice della versione 3.3.x, il che significa che la patch sarà fornita in una (nuova) versione 3.3.5. L'istanza CFEE con versione 3.1.2 deve essere aggiornata alla versione 3.3.5 per ricevere la nuova patch (cioè, il solo aggiornamento alla versione 3.3.4 non risolverà il problema risolto nella patch, che viene fornita solo nella versione 3.3.5).

## Ridimensionamento dell'infrastruttura CFEE
{: #scale}

Gli utenti hanno bisogno delle seguenti autorizzazioni per poter aggiungere o rimuovere le celle Cloud Foundry a un'istanza CFEE:
* Ruolo di _Amministratore_ o superiore per un'istanza CFEE.
* Ruolo di _Operatore_ o superiore al cluster Kubernetes in cui viene eseguito il provisioning della CFEE.

Per aggiungere le celle dell'applicazione nella tua istanza CFEE:
1. Passa al [Dashboard {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) e apri il {{site.data.keyword.cfee_full_notm}} in cui vuoi aggiungere le celle.
2. Fai clic su **Aggiungi cella** vicino alla tabella _Celle_, che apre la pagina _Aggiungi celle di Foundry Foundry_.
3. Nella pagina _Aggiungi celle di Foundry Foundry_, seleziona il numero di celle da aggiungere. La pagina mostra anche la geografia e l'ubicazione dell'istanza CFEE in cui le celle saranno aggiunte. Mostra inoltre il numero corrente di celle e la capacità delle celle da aggiungere (che è la stessa capacità delle celle correnti). Il pannello destro della pagina mostra il costo stimato delle celle aggiunte insieme al nuovo costo totale stimato dell'ambiente.
4. Fai clic su **Aggiungi cella**.  
5. Vai alla pagina _Nodi_. Una nuova riga viene aggiunta nella tabella _Celle_ per ogni nuovo nodo. La colonna _Stato nodo_ indica l'avanzamento dell'aggiunta e della distribuzione della cella al tuo ambiente CFEE.
