---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Determina i tuoi spazi
{: #determinespaces}

All'interno di un'organizzazione, gli spazi forniscono un ulteriore livello di applicazione di limiti e astrazione.

Uno spazio è un'area riservata dell'organizzazione in cui gli utenti possono sviluppare ed eseguire applicazioni e servizi. Puoi creare un numero qualsiasi di spazi all'interno di un'organizzazione e puoi controllare gli utenti che hanno accesso a uno spazio. Per ulteriori dettagli, vedi [Spazi](/docs/account/orgs_spaces.html#orgsspacesusers).

Se intendi definire un numero elevato di spazi, potresti creare un'applicazione per facilitare la gestione di tali spazi. Se il numero di spazi supera sessanta, puoi valutare la possibilità di definire un'altra organizzazione.

## Spazi per singola organizzazione contro multi organizzazioni
{: #spaceconsiderations}

Quando utilizzi un'architettura a singola organizzazione, il livello di separazione e astrazione viene fornito dagli spazi da te definiti all'interno dell'organizzazione. Tieni conto delle seguenti indicazioni quando definisci gli spazi:

* Definisci uno spazio per ospitare un servizio che richieda di effettuare una sola volta il provisioning e la configurazione nell'organizzazione.
* Definisci gli spazi in base al ciclo di vita della distribuzione.
  Ad esempio, puoi definire uno o più spazi per le applicazioni da sviluppare, uno o più spazi per le applicazioni che si trovano già in fase di test e uno o più
  spazi per le applicazioni che sono in produzione.
* Se il limite del ciclo di vita della distribuzione non è sufficiente, puoi ottenere ulteriore separazione definendo uno o più spazi per ogni LOB e fase di distribuzione.
* Stabilisci se hai bisogno di applicare dei limiti per i diversi gruppi di utenti.
  Ad esempio, gli sviluppatori non possono sviluppare l'applicazione e testarla. Hai bisogno di un insieme di utenti diverso per testare l'applicazione. In questo scenario crei due spazi, uno per
  gli sviluppatori dell'applicazione e uno per i tester. Ad ogni insieme di utenti concedi quindi l'accesso allo spazio corretto.

Quando implementi un'architettura a più organizzazioni, puoi separare ogni organizzazione in base alla LOB e/o al ciclo di vita della distribuzione. Puoi quindi definire più spazi che si basano sul numero di applicazioni o progetti forniti dallo stesso reparto nell'azienda. Tieni conto delle seguenti indicazioni quando pianifichi gli spazi in un'organizzazione:

* Definisci uno spazio per ospitare un servizio che richieda di effettuare una sola volta il provisioning e la configurazione nell'organizzazione.
* Definisci uno spazio per ogni applicazione, per ogni gruppo di applicazioni correlate o per uno specifico progetto.
* Se hai bisogno di applicare dei limiti per i diversi utenti, definisci uno spazio per ogni insieme di utenti. Quando a un utente viene concesso il ruolo di sviluppatore in uno spazio, tale utente ha accesso completo a tutte le risorse e ai servizi {{site.data.keyword.Bluemix_notm}} forniti e in esecuzione in questo spazio. Se hai bisogno di applicare una maggiore sicurezza per impedire agli utenti di controllare ogni risorsa, valuta la possibilità di definire più spazi. In tutti questi spazi, puoi fornire i servizi {{site.data.keyword.Bluemix_notm}} utilizzati dalle applicazioni in esecuzione in tale spazio.

## Denominazione, limitazioni e gestione dello spazio
{: #spaceadmin}

Per definire i diversi spazi per la tua organizzazione cloud, tieni presenti le seguenti indicazioni:

* Definisci e applica una convenzione di denominazione. Ad esempio, definisci una convenzione di denominazione in cui il nome dello spazio include informazioni sulla posizione dell'organizzazione e sul tipo di cloud. Puoi modificare il nome di uno spazio dopo che è stato creato. Se un nome spazio viene modificato, avvisa tutti i membri del team dello spazio in merito alla modifica.
* Definisci le restrizioni applicabili allo spazio. Ad esempio, definisci il tipo di applicazione che è possibile sviluppare, gestire e distribuire in ciascuno spazio.
* Identifica il gestore dello spazio. Potresti voler delegare l'amministrazione dello spazio a più di una persona.
