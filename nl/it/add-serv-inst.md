---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Creazione e visualizzazione delle istanze del servizio
{: #creating-services}

Le applicazioni distribuite in {{site.data.keyword.cfee_full_notm}} possono essere associate a due tipi di istanze del servizio:
1. Le istanze del servizio gestite da un broker dei servizi Cloud Foundry locale (locale per la CFEE). A loro volta, possono essere di due tipi:
   *  1a. Un'istanza di un'offerta di servizi creata dal marketplace Cloud Foundry dell'istanza {{site.data.keyword.cfee_full_notm}} corrente. Questo tipo di istanza del servizio richiede un broker dei servizi registrato disponibile nell'ambiente. Un broker dei servizi mostra un catalogo di offerte e piani del servizio, oltre a consentire la creazione, la rimozione, il bind e l'annullamento del bind delle istanze da tali offerte di servizi. Per ulteriori informazioni, consulta [Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html) nella documentazione Cloud Foundry.
   * 1b. Un'istanza del servizio fornita dall'utente. La creazione di questo tipo è supportata tramite la CLI, ma non tramite l'interfaccia utente. Tuttavia, le istanze del servizio fornite dall'utente verranno elencate nell'interfaccia utente.
2. Le istanze del servizio pubbliche create dal catalogo {{site.data.keyword.Bluemix}} e disponibili nell'account {{site.data.keyword.Bluemix}}.
Le istanze del servizio pubbliche disponibili nell'account {{site.data.keyword.Bluemix}} non possono essere disponibili, da sole, agli ambienti CFEE. Affinché un'istanza del servizio pubblica (disponibile nell'account {{site.data.keyword.Bluemix}}) diventi disponibile per gli spazi in un ambiente CFEE, è necessario creare un alias per l'istanza del servizio nello spazio CFEE di destinazione. L'alias funziona come riferimento all'istanza del servizio pubblica effettiva.  Una volta che l'alias del servizio viene creato in uno spazio CFEE, può essere associato alle applicazioni in tale CFEE.  L'aliasing del servizio consente agli sviluppatori di sfruttare l'ampio catalogo dei servizi {{site.data.keyword.Bluemix}} nelle proprie applicazioni distribuite negli ambienti CFEE.


## Creazione e visualizzazione degli alias in uno spazio CFEE 
{: #creating-services_inspace}

Un alias a un'istanza del servizio pubblica esistente disponibile nel tuo account IBM Cloud ti consente di eseguire il bind di tale istanza del servizio alle applicazioni distribuite in uno spazio CFEE. La creazione di un alias per un'istanza del servizio {{site.data.keyword.Bluemix_notm}} esistente richiede l'accesso da parte dell'utente all'istanza stessa. Per ulteriori informazioni, consulta la pagina Identity & Access nel menu**Manage > Users** nell'intestazione {{site.data.keyword.Bluemix_notm}} per controllare le tue politiche di accesso all'account correnti.

Per creare un alias dell'istanza del servizio all'interno di uno spazio in una CFEE:

1. Nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, trova l'ambiente Cloud Foundry Enterprise che ospita la tua applicazione.
2. Vai a **Organizations** nel pannello di navigazione e apri l'organizzazione e lo spazio in cui si trova l'applicazione.
3. Passa alla scheda **Spaces** e individua lo spazio che contiene l'applicazione.
4. Nella pagina dello spazio di destinazione, vai alla scheda **Services** e fai clic su **Create service**.  Si aprirà la pagina **Catalog** per il {{site.data.keyword.cfee_full_notm}}.  La pagina elenca le offerte di servizi da due origini (consulta la colonna _Source_):
   * Offerte dal catalogo di IBM Cloud.
   * Le offerte dal marketplace {{site.data.keyword.cfee_full_notm}} locale.
5. Trova e seleziona un'offerta di servizi disponibile che vuoi istanziare.
6. A seconda dell'origine dell'offerta di servizi (IBM Cloud o CFEE locale) procedi con una delle seguenti operazioni:
   * **Continua** alla pagina di creazione dell'offerta di servizi IBM Cloud per fornire il nome della nuova istanza del servizio, della regione, del piano e delle altre proprietà richieste per creare il servizio in IBM Cloud.  Dopo aver fatto clic su *Create* l'istanza del servizio sarà creata in IBM Cloud.  Inoltre, un alias di tale istanza del servizio verrà creato in {{site.data.keyword.cfee_full_notm}}. L'alias sarà disponibile per il bind con le applicazioni in {{site.data.keyword.cfee_full_notm}}.
**Nota:** quando crei un {{site.data.keyword.Bluemix_notm}} in questa fase, oltre alla creazione di un'istanza pubblica disponibile agli utenti nell'account IBM Cloud, viene creato un alias per tale istanza del servizio nel {{site.data.keyword.cfee_full_notm}} da cui è stata creata.
   * **Crea** l'istanza del servizio nel marketplace Cloud Foundry locale. In questo modo verrà aperta una finestra di dialogo in cui fornire il nome della nuova istanza del servizio e il piano. Dopo aver fatto clic su *Create* l'istanza del servizio sarà creata in {{site.data.keyword.cfee_full_notm}} e sarà disponibile per il bind con le applicazioni in {{site.data.keyword.cfee_full_notm}}.

Dopo che l'istanza del servizio è stata creata, l'istanza del servizio (se viene creata nel marketplace Cloud Foundry locale) o l'alias (se l'istanza del servizio è stata creata dal catalogo IBM Cloud) è elencata nella scheda **Services**.


## Creazione e visualizzazione degli alias del servizio in tutti gli ambienti CFEE nel dashboard Cloud Foundry globale
{: #creating-services_across}

Puoi visualizzare una vista consolidata di tutti gli alias dell'istanza del servizio (tra tutte le istanze CFEE) nel dashboard Cloud Foundry globale.

1. Fai clic sull'icona Menu ![Account Checking](img/HamburgerMenu.png "Acquisizione schermo che mostra l'icona menu") > **Cloud Foundry** per aprire il dashboard Cloud Foundry.
2. Fai clic su **Enterprise > Services** nel pannello di navigazione di sinistra.
La tabella nella vista mostra le seguenti informazioni:

| Elemento   | Descrizione |
|-----------|---------------|
| Alias del servizio | Il nome dell'alias dell'istanza del servizio. |
| Istanza del servizio | L'istanza del servizio IBM Cloud pubblica da cui viene creato l'alias. |
| Offerta | L'offerta di servizi dal catalogo IBM Cloud da cui è stata creata l'istanza del servizio. |
| CFEE | Il {{site.data.keyword.cfee_full}} in cui si trova l'alias. |
| Organizzazione | L'organizzazione nell'istanza CFEE in cui si trova l'alias. |
| Spazio | Lo spazio nell'organizzazione nell'istanza CFEE in cui si trova l'alias. |
{:caption="Tabella 1. Descrizione degli elementi chiave" caption-side="top"}

In questa vista puoi eseguire le seguenti azioni:
* Ordinare gli elementi nella tabella per una qualsiasi delle proprietà visualizzate come colonne della tabella.
* Eseguire il bind delle applicazioni a un alias specifico accedendo al menu di overflow dell'alias ubicato all'estrema destra della riga.
* Espandere un alias (riga) per visualizzare tutte le applicazioni associate a tale alias.
* Avviare, arrestare le applicazioni accedendo al menu di overflow dell'applicazione dell'alias ubicato all'estrema destra della riga.
* Passare ad un CFEE, a un'organizzazione CFEE o a uno spazio CFEE facendo clic sul collegamento al corrispondente CFEE, organizzazione o spazio.

Per creare un alias del servizio dal dashboard Cloud Foundry globale:
1. Fai clic sul pulsante **Create service alias** all'inizio della pagina. Verrà visualizzata la finestra di dialogo _Create Service Alias_.  La finestra di dialogo elenca tutte le istanze del servizio pubbliche disponibili nell'account IBM Cloud corrente.
2. Seleziona una delle istanze del servizio pubbliche.
3. Fai clic su **Create**. Una volta creato, il nuovo alias dell'istanza del servizio verrà aggiunto all'elenco.
L'alias del servizio verrà visualizzato anche nell'elenco dei servizi nello spazio CFEE, in cui può essere associato alle applicazioni in tale spazio (CFEE > Organizations > Space > Services).


