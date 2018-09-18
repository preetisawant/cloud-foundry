---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Autorizzazioni
{: #permissions}

Prima di iniziare a creare ed utilizzare le istanze del servizio {{site.data.keyword.cfee_full}}, le autorizzazioni dell'amministratore e del resto del team devono essere impostate correttamente.

## Autorizzazioni necessarie per creare un nuovo ambiente
{: #perm-creating}

Per creare nuove istanze del servizio {{site.data.keyword.cfee_full_notm}}, agli utenti devono essere concesse le politiche di accesso dall'amministratore dell'account in cui deve essere creata l'istanza:

* Accedi ad almeno un gruppo di risorse nell'account {{site.data.keyword.Bluemix}}. I gruppi di risorse consentono di organizzare le risorse in raggruppamenti personalizzati per facilitare il controllo dell'accesso a tali risorse. Ti viene richiesto di creare un gruppo di risorse quando crei una nuova istanza dell'ambiente.

* Il ruolo di amministratore o di editor per il servizio {{site.data.keyword.cfee_full_notm}} nel gruppo di risorse a cui è assegnato l'ambiente. Gli utenti con i ruoli di amministratore o di editor nel servizio {{site.data.keyword.cfee_full_notm}} possono creare ed eliminare gli ambienti. Ma solo gli utenti con un ruolo di amministrazione possono assegnare gli utenti a un'istanza {{site.data.keyword.cfee_full_notm}} o modificare i ruoli assegnati agli utenti in tale istanza.

* Il ruolo di amministratore o di editor per il servizio IBM Cloud Object Storage, che è una dipendenza richiesta del servizio CFEE.  Un'istanza del servizio IBM Cloud Object Storage viene utilizzata per archiviare i dati generati durante la creazione dei contenitori dell'applicazione ICFEE (ad esempio, pacchetti di applicazioni caricati, pacchetti di build ed eseguibili compilati).

* Un'istanza del servizio Compose for PostgreSQL è una dipendenza necessaria del servizio CFEE.  Compose for PostgreSQL viene utilizzato per archiviare i dati Cloud Foundry nella tua istanza CFEE (ad esempio, controllo della distribuzione dell'applicazione, avvio o arresto degli eventi; conservando i record di appartenenza dell'utente CFEE, delle organizzazioni, degli spazi, delle applicazioni e delle connessioni al servizio).  L'istanza del servizio Compose for PostgreSQL viene distribuita in un'organizzazione Cloud Foundry pubblica (non correlata alle organizzazioni CFEE). L'organizzazione Cloud Foundry pubblica in cui viene distribuita l'istanza Compose for PostgresSQL ha un nome specifico: **_cfee-`<accountId>`_**, dove "accountId" è l'ID dell'account IBM Cloud in cui deve essere eseguito il provisioning di CFEE (insieme all'istanza del servizio Compose for PostgreSQL).  L'organizzazione Cloud Foundry pubblica viene creata automaticamente quando il proprietario dell'account crea un'istanza CFEE.  L'organizzazione non viene creata automaticamente quando un utente che non è il proprietario dell'account tenta di creare l'istanza CFEE (quindi, il tentativo di creazione della CFEE avrà esito negativo).  Pertanto, qualsiasi utente dell'account IBM Cloud che crea istanze CFEE ma non è il proprietario dell'account deve essere aggiunto all'organizzazione Cloud Foundry pubblica **_cfee-`<accountId>`_** con un **ruolo di gestore**.   

   Per aggiungere un utente dall'account IBM Cloud all'organizzazione pubblica _cfee-`<accountId>`_:
    * Vai a [**Manage > Account > Cloud Foundry Orgs**](https://console.bluemix.net/account/organizations).
    * Fai clic sull'organizzazione **_cfee-`<accountId>`_**.
    * Vai alla scheda **Users** all'inizio della pagina.
    * Trova l'utente che deve creare le istanze CFEE e fai clic sulla casella di spunta **Manager** per tale utente. Se l'utente che vuoi sia in grado di creare le istanze CFEE non è presente nell'elenco, fai clic su **Add or invite user** sopra la tabella per aggiungere o invitare gli utenti nell'organizzazione **_cfee-`<accountId>`_**.

   **Nota**: sebbene l'organizzazione pubblica **_cfee-`<accountId>`_** venga creata automaticamente e in modo implicito quando il proprietario dell'account IBM Cloud crea un'istanza CFEE, il proprietario dell'account (e soltanto lui) potrebbe invece creare l'organizzazione Cloud Foundry manualmente, senza dover creare un'istanza CFEE. Il proprietario dell'account IBM Cloud può creare l'organizzazione pubblica _cfee-`<accountId>`_ manualmente nella pagina **Manage > Account > Cloud Foundry Orgs**. Se sei il proprietario dell'account e crei l'organizzazione pubblica _cfee-`<accountId>`_, assicurati di denominarla esattamente con _cfee-`<accountId>`_. Per trovare l'ID dell'account IBM Cloud, vai alla pagina [**Manage > Account > Cloud Foundry Orgs**](https://console.bluemix.net/account/organizations) e cerca l'URL della pagina disponibile nel tuo browser.  L'ID dell'account IBM Cloud è la serie di valori alfanumerici che segue `=` nell'URL della pagina. In alternativa, puoi andare a __Manage > Account > Users__ e passare con il mouse sul suggerimento a sinistra del nome _Account_ situato nell'angolo in alto a destra della pagina.
   
* Il ruolo di amministratore o di editor per il servizio {{site.data.keyword.Bluemix_notm}} Container nel gruppo di risorse a cui è assegnato l'ambiente. Le istanze di {{site.data.keyword.cfee_full_notm}} vengono distribuite sull'infrastruttura del cluster di contenitori, fornita dal servizio {{site.data.keyword.Bluemix_notm}} Container. Quando crei un'istanza del servizio {{site.data.keyword.cfee_full_notm}}, il servizio crea automaticamente un cluster Kubernetes in cui viene distribuito {{site.data.keyword.cfee_full_notm}}. L'accesso al servizio IBM Container, in particolare al gruppo di risorse a cui è assegnato l'ambiente, è necessario per la creazione di tale infrastruttura del cluster.

Per confermare che disponi delle politiche di accesso richieste per creare un'istanza {{site.data.keyword.cfee_full_notm}}:
1. Vai al menu [**Manage > Account > Users**](https://console.bluemix.net/iam/#/users) nell'intestazione {{site.data.keyword.Bluemix_notm}} per aprire la pagina **Identity & Access**.
2. Nella scheda Access policies, fai clic sull'utente che sta creando l'ambiente.
3. Conferma che le politiche di accesso dell'utente che sta creando l'ambiente siano coerenti con le politiche descritte in precedenza.

La seguente schermata illustra le politiche di accesso come vengono visualizzate nella pagina Identity & Access di {{site.data.keyword.Bluemix_notm}} che consentono a un utente di creare un'istanza {{site.data.keyword.cfee_full_notm}}.

![Politiche di accesso](img/AccessPolicies_Creator.png)

## Autorizzazioni necessarie per utilizzare un ambiente
{: #perm-working}

Per utilizzare un'istanza di {{site.data.keyword.cfee_full_notm}}, gli utenti devono essere:
1. Membri dell'account {{site.data.keyword.Bluemix_notm}} in cui è stata creata l'istanza {{site.data.keyword.cfee_full_notm}}.
2. Avere le seguenti _Politiche di accesso_ concesse dall'amministratore dell'account (consulta la pagina _Identity & Access_ nel menu [**Manage > Account > Users**](https://console.bluemix.net/iam/#/users) nell'intestazione {{site.data.keyword.Bluemix_notm}} per controllare le tue politiche di accesso correnti):
  - Accedi ad almeno un gruppo di risorse nell'account {{site.data.keyword.Bluemix_notm}}. I gruppi di risorse consentono di organizzare le risorse in raggruppamenti personalizzati per facilitare il controllo dell'accesso a tali risorse. Ti viene richiesto di creare un gruppo di risorse quando crei una nuova istanza dell'ambiente.
  - Agli utenti deve essere assegnato l'accesso al servizio {{site.data.keyword.cfee_full_notm}} nel gruppo di risorse in cui è stata creata l'istanza dell'ambiente. Il livello di accesso e di controllo che gli utenti hanno in un'istanza {{site.data.keyword.cfee_full_notm}} dipende dal ruolo che viene concesso nella politica di accesso:
     - Gli utenti assegnati ai ruoli di amministratore o di editor possono creare organizzazioni, assegnare gestori alle organizzazioni e agli spazi, disporre di autorizzazioni complete per tutti gli spazi e le organizzazioni all'interno dell'ambiente ed eseguire le azioni operative utilizzando l'API controller Cloud. A questi utenti viene concesso automaticamente l'_ambito cloud_controller.admin_ nell'_ambito Account utente e autenticazione_ Cloud Foundry.
     - Gli utenti a cui è assegnato un ruolo di visualizzatore possono vedere tale ambiente nel dashboard principale {{site.data.keyword.Bluemix_notm}} e possono aprire la relativa interfaccia utente. Gli utenti che accedono a specifiche organizzazioni e spazi all'interno dell'ambiente sono regolati dai ruoli specifici dell'organizzazione e degli spazi assegnati dai gestori di tali organizzazioni e spazi. Per ulteriori informazioni, consulta [Aggiunta di utenti a organizzazioni](add-users.html).

L'immagine illustra le politiche di accesso minime (come vengono visualizzate nella pagina {{site.data.keyword.Bluemix_notm}} _Identity & Access_) necessarie per accedere a un {{site.data.keyword.cfee_full_notm}}.

![Politiche di accesso](img/AccessPolicies_User.png)

