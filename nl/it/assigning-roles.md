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

# Assegna i ruoli
{: #roles}

Puoi concedere più ruoli ai membri del team in un account {{site.data.keyword.Bluemix_notm}}. Questi ruoli definiscono le autorizzazioni dell'utente per gestire le risorse dell'account e dell'organizzazione:
Puoi concedere i [ruoli utente](/docs/iam/users_roles.html#userroles) ai membri di un'organizzazione. Questi ruoli definiscono il livello di accesso all'interno dell'organizzazione e limitano gli utenti che possono accedere a uno spazio e alle relative risorse. Ad esempio, puoi concedere agli utenti autorizzazioni diverse per spazi differenti.

## Proprietario dell'account
{: #accountowner}

Sia che progetti un'architettura con più organizzazioni o un'architettura con una sola organizzazione, il proprietario dell'account è il super utente dell'ambiente cloud.

Le attività principali del proprietario dell'account includono:

* Gestione delle risorse dell'account globale.
* Creazione delle organizzazioni.
* Aggiunta dei membri del team all'account.

Il proprietario dell'account può anche aggiungere uno o più utenti come gestori di un'organizzazione, assegnando a questi utenti il ruolo di **Gestore**. Valuta l'aggiunta di due utenti come gestori dell'organizzazione. Il primo utente funge da gestore principale dell'organizzazione. Il secondo utente agisce come vice gestore, nel caso in cui il gestore principale non sia disponibile.

## Ruoli dell'utente
{: #userroles}

I ruoli dell'utente definiscono le autorizzazioni che puoi assegnare a un membro del team in un'organizzazione e definiscono il livello di accesso a disposizione di un membro del team all'interno dell'organizzazione e di ogni spazio.

In un'architettura a più organizzazioni o in un'architettura con una sola organizzazione, definisci i membri del team e le autorizzazioni necessarie a ciascun utente per completare il proprio lavoro:

1. Identifica la serie di utenti che necessita dell'accesso a un'organizzazione.
2. Definisci le autorizzazioni di ogni membro del team nell'organizzazione e in uno spazio dell'organizzazione.
3. Seleziona il ruolo che concede ad un utente le autorizzazioni necessarie.

   * Gestore organizzazione
   * Revisore organizzazione
   * Gestore fatturazione dell'organizzazione
   * Gestore spazio
   * Sviluppatore spazio
   * Revisore spazio

### Gestore organizzazione
{: #bporgmgr}

Le attività di cui un gestore dell'organizzazione è responsabile includono la creazione di spazi, la distribuzione della quota tra gli spazi, l'invito dei membri del team e, facoltativamente, la concessione di ruoli specifici e la definizione dei domini personalizzati.

### Revisore organizzazione
{: #bporgauditor}

I membri del team con il ruolo **Revisore** dell'organizzazione possono monitorare la quota, l'utilizzo delle risorse e i membri del team per tutti gli spazi in un'organizzazione.
I revisori possono quindi notificare l'efficienza dell'organizzazione ed evidenziare eventuali problemi potenziali.

* Quando utilizzi un'architettura con più organizzazioni, potresti voler concedere il ruolo di revisore agli stessi membri del team per ogni organizzazione che fa parte dell'account.
Quindi, questi membri del team possono monitorare la quota in tutte le organizzazioni nel tuo ambiente cloud e ottenere una vista globale dell'account.
* Quando utilizzi un'architettura con una sola organizzazione, assegna il ruolo di revisore ai membri del team con la responsabilità di monitorare l'utilizzo della quota e l'efficienza complessiva
dell'organizzazione.

### Gestore fatturazione dell'organizzazione
{: #bporgbillingmgr}

I membri del team con il ruolo **Gestore fatturazione** possono monitorare i costi di un'organizzazione.

* Quando utilizzi un'architettura con più organizzazioni, potresti voler concedere il ruolo di fatturazione alla stessa serie di membri del team per ogni organizzazione che fa parte dell'account. Quindi, questi membri del team possono monitorare i costi di ogni organizzazione e ottenere una vista globale dell'account.
* In un'architettura con una sola organizzazione, identifica gli utenti che sono responsabili del monitoraggio dei costi.

### Gestore spazio
{: #bpspacemgr}

Il **Gestore** dello spazio è responsabile di tutto il lavoro effettuato all'interno dello spazio che gestisce e controlla. Il gestore dello spazio può eseguire le seguenti attività:

* Monitoraggio della quota allocata allo spazio.
* Richiesta di più risorse al gestore dell'organizzazione.
* Notifica al gestore dell'organizzazione di risorse non necessarie.
* Aggiunta di membri del team allo spazio con il ruolo **Sviluppatore**.
* Facoltativamente, assegna il ruolo **Gestore** dello spazio a un membro del team che agisce come vice gestore dello spazio in sua assenza.

### Sviluppatore spazio
{: #bpspacedev}

Uno sviluppatore dello spazio può eseguire le seguenti attività:

* Gestire le applicazioni Cloud Foundry.
* Eseguire il provisioning e configurare i servizi {{site.data.keyword.Bluemix_notm}}.
* Associare i domini alle applicazioni.

### Revisore spazio
{: #bpspaceauditor}

Per ogni spazio, potresti voler concedere il ruolo **Revisore** dello spazio agli stessi membri del team con il ruolo **Revisore** dell'organizzazione. Nella tua azienda, questo ruolo potrebbe essere concesso a una serie specifica di utenti.

