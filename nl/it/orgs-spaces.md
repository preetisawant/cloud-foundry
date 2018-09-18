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

# Creazione di organizzazioni e spazi
{: #create_orgs}

Le applicazioni in un {{site.data.keyword.cfee_full}} vengono indirizzate all'interno di spazi specifici. A sua volta, uno spazio si trova all'interno di un'organizzazione specifica. I membri di un'organizzazione condividono un piano di quota, le applicazioni, le istanze dei servizi e i domini personalizzati. Dopo aver creato le organizzazioni e gli spazi, gli utenti possono essere aggiunti ad essi con ruoli specifici che determinano il livello di accesso e di controllo a tali organizzazioni e spazi. Per creare le organizzazioni ed assegnare i gestori ad esse, devi avere un ruolo di amministratore per il servizio {{site.data.keyword.cfee_full_notm}} e per l'istanza dell'ambiente specifica a cui stanno venendo aggiunti gli utenti. Queste autorizzazioni sono impostate nella pagina _Identity & Access_ nel menu **Manage > Users** nell'intestazione {{site.data.keyword.Bluemix}}.
{: shortdesc}

## Creazione delle organizzazioni
{: #create-org}

Per creare le organizzazioni in {{site.data.keyword.cfee_full_notm}}:

1. Vai al [Dashboard Ambienti Cloud Foundry {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments){: new_window} e apri il {{site.data.keyword.cfee_full_notm}} in cui vuoi creare le organizzazioni.
2. Nell'interfaccia utente di {{site.data.keyword.cfee_full_notm}}, vai alla voce **Organizations** nel pannello di navigazione per aprire la pagina _organizations_.
3. Fai clic su **Add new**.
4. Immetti un **Name** per la nuova organizzazione.
5. In **Managers**, identifica almeno un utente. Solo gli utenti con un ruolo di gestore possono aggiungere i membri a tale organizzazione.
6. In **Quota plan**, seleziona un piano disponibile. Un piano di quota limita la memoria disponibile per le applicazioni nell'organizzazione, il numero massimo di istanze di applicazioni ospitate e il numero massimo di rotte.

Oltre alla gestione dell'appartenenza all'organizzazione, i gestori dell'organizzazione possono creare, visualizzare, modificare o eliminare gli spazi all'interno dell'organizzazione. I gestori dell'organizzazione possono anche visualizzare l'utilizzo e la quota dell'organizzazione, invitare gli utenti nell'organizzazione, gestire l'appartenenza e i ruoli nell'organizzazione e gestire i domini personalizzati dell'organizzazione.

Per creare spazi all'interno di un'organizzazione, nella pagina _Organizations_, vai alla scheda **Spaces** e fai clic su **Add new**. I membri di un'organizzazione possono anche creare e gestire i propri spazi all'interno di un'organizzazione. Per ulteriori informazioni sui ruoli Cloud Foundry, vedi [Accesso Cloud Foundry](https://console.bluemix.net/docs/iam/cfaccess.html#cfroles){: new_window}.

**Nota**: l'accesso alle organizzazioni e agli spazi all'interno di un {{site.data.keyword.cfee_full_notm}} richiede che gli utenti abbiano l'autorizzazione ad accedere all'ambiente stesso. Senza l'autorizzazione per accedere a {{site.data.keyword.cfee_full_notm}}, gli utenti non possono accedere alle organizzazioni e agli spazi all'interno dell'ambiente, indipendentemente dalla loro appartenenza e ruolo in tali organizzazioni e spazi.
