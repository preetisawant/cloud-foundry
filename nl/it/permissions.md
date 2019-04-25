---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2019-02-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Autorizzazioni
{: #permissions}

Prima che gli utenti inizino a creare e utilizzare un servizio {{site.data.keyword.cfee_full}} (CFEE), le loro autorizzazioni devono essere impostate correttamente da un amministratore dell'account dove deve essere creata l'istanza CFEE. 

## Panoramica delle autorizzazioni
{: #perm-summary}

Il seguente è un riepilogo delle assegnazioni di ruoli [IAM](https://cloud.ibm.com/iam#/users) e [Cloud Foundry](https://cloud.ibm.com/account/cloud-foundry) minime richieste per eseguire varie attività in un'istanza CFEE. La restante sezione descrive tali autorizzazioni in modo più dettagliato.

|  **Attività** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|  **Ruoli di accesso IAM** &nbsp; &nbsp; &nbsp; |**Ruolo Cloud Foundry** &nbsp; &nbsp; &nbsp; |
|----------------------------------------|-------------------|-------------------|
|Crea un CFEE |  <ul><li>Ruolo di visualizzatore nel gruppo di risorse dove deve essere creato il CFEE.</li> <li>Ruolo di editor nel servizio CFEE.</li> <li>Ruolo di amministratore nel servizio Kubernetes.</li> <li>Ruolo della piattaforma editor e il ruolo di accesso al servizio gestore nel servizio IBM Cloud Object Storage.</li> </ul> | <ul><li>Ruolo di utente in un'organizzazione pubblica.</li> <li>Ruolo di sviluppatore in uno spazio in tale organizzazione pubblica. </li></ul>|
|Aggiorna versione CFEE |  <ul><li>Ruolo di visualizzatore nel gruppo di risorse CFEE.</li> <li>Ruolo della piattaforma di editor nel servizio CFEE.</li></li> <li>Ruolo di operatore nel servizio Kubernetes.</li> <li>Ruolo di editor nel servizio Cloud Object Storage.</li> </ul> | <ul><li>Ruolo di utente in un'organizzazione pubblica.</li> <li>Ruolo di sviluppatore in uno spazio in tale organizzazione pubblica. </li></ul>|
|Scala capacità CFEE (aggiungi/rimuovi celle)|  <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE.</li> <li>Ruolo di amministratore nell'istanza CFEE.</li> <li>Ruolo di operatore nel servizio Kubernetes.</li> <li>Ruolo di editor nel servizio Cloud Object Storage.</li> </ul> | |
|Monitora CFEE |  <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE</li> <li>Ruolo di editor nell'istanza CFEE.</li> <li>Ruolo di operatore nel cluster Kubernetes di CFEE.</li></ul> |  |
|Visualizza utilizzo risorse CFEE. |  <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE.</li> <li>Ruolo di visualizzatore nell'istanza CFEE.</li></ul> |  |
|Abilita controllo CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE.</li> <li>Ruolo di editor nell'istanza CFEE.</li></ul> | <ul><li>Ruolo di revisore nello spazio Cloud Foundry pubblico dove è distribuita l'istanza del servizio Programma di traccia dell'attività.</li></ul>  |
|Visualizza eventi di controllo CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE.</li> <li>Ruolo di editor nell'istanza CFEE.</li></ul> | <ul><li>Ruolo di revisore nello spazio Cloud Foundry pubblico dove è distribuita l'istanza del servizio Programma di traccia dell'attività.</li></ul>  |
|Abilita persistenza log CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE</li> <li>Ruolo di editor nell'istanza CFEE.</li></ul> |<ul><li>Ruolo di revisore nello spazio Cloud Foundry pubblico dove è distribuita l'istanza del servizio Analisi log dell'attività.</li></ul>  |
|Visualizza log indicati come persistenti CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE</li> <li>Ruolo di editor nell'istanza CFEE.</li></ul> | <ul><li>Ruolo di revisore nello spazio Cloud Foundry pubblico dove è distribuita l'istanza del servizio Analisi log dell'attività.</li></ul> |
|Crea organizzazioni CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE</li> <li>Ruolo di editor nell'istanza CFEE.</li></ul> |  |
|Crea spazi CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE</li> <li>Ruolo di visualizzatore nell'istanza CFEE.</li></ul> | <ul><li>Gestore nell'organizzazione dove deve essere creato lo spazio.</li></ul> |
|Gestisci domini condivisi|<ul><li>Visualizzatore nel gruppo di risorse dell'istanza CFEE. </li><li>Ruolo di editor nell'istanza CFEE. </li></ul>|  |
|Visualizza domini condivisi|<ul><li>Visualizzatore nel gruppo di risorse dell'istanza CFEE. </li><li>Ruolo di visualizzatore nell'istanza CFEE. </li></ul>|  |
|Gestisci domini privati|<ul> <li>Visualizzatore nel gruppo di risorse dell'istanza CFEE. </li><li>Ruolo di visualizzatore nell'istanza CFEE. </li></ul>| <ul><li>Ruolo di gestore nell'organizzazione proprietaria del dominio. </li></ul>|
|Visualizza domini privati|<ul> <li>Visualizzatore nel gruppo di risorse dell'istanza CFEE </li><li>Ruolo di visualizzatore nell'istanza CFEE. </li></ul>|<ul><li>Ruolo di visualizzatore nell'organizzazione proprietaria del dominio. </li></ul>|
|Crea/elimina un'istanza del servizio IBM Cloud in uno spazio CFEE| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dove deve essere creato il CFEE.</li> <li>Ruolo di visualizzatore nell'istanza CFEE.</li> <li>Editor nel gruppo di risorse in cui deve essere creata l'istanza del servizio o per il servizio gestito da IAM da istanziare.</li> </ul>| <ul><li>Ruolo di sviluppatore nello spazio CFEE da dove viene creata l'istanza del servizio (e dove verrà aggiunta/aggiunta con alias automaticamente).</li></ul> |
|Aggiungi/rimuovi un'istanza del servizio IBM Cloud a/da uno spazio CFEE (ossia, crea/elimina un alias a un servizio IBM Cloud in uno spazio CFEE)| <ul><li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE.</li><li>Ruolo di visualizzatore nell'istanza CFEE. </li><li>Ruolo della piattaforma di operatore e ruolo del servizio di lettore per l'istanza del servizio da aggiungere. </li></ul>|<ul><li>Ruolo di sviluppatore nello spazio CFEE in cui deve essere aggiunta l'istanza del servizio (aggiunta con alias).</li></ul> |
|Associa mediante bind o annulla l'associazione mediante bind di un'istanza del servizio IBM Cloud in uno spazio CFEE|<ul> <li>Editor nel gruppo di risorse dell'istanza del servizio da associare mediante bind o di cui annullare l'associazione mediante bind.</li><li>Ruolo di visualizzatore nell'istanza CFEE. </li><li>Ruolo della piattaforma di operatore e ruolo del servizio di scrittore per l'istanza del servizio da associare mediante bind.</li></ul> | <ul><li>Ruolo di sviluppatore nello spazio CFEE in cui associare mediante bind l'istanza del servizio.</li></ul> |
|Immetti comandi cli `cf`|<ul> <li>Ruolo di visualizzatore nel gruppo di risorse dell'istanza CFEE. </li><li>Ruolo di visualizzatore nell'istanza CFEE.</li></ul> | <ul><li>Ruoli Cloud Foundry nell'organizzazione/nello spazio richiesti per eseguire il comando.</li></ul> |
{: caption="Tabella 1. Autorizzazioni richieste per eseguire le attività in un CFEE" caption-side="top"}

## Autorizzazioni necessarie per creare un nuovo ambiente
{: #perm-creating}

Per creare delle nuove istanze del servizio CFEE, agli utenti devono essere concesse le politiche di accesso da un amministratore dell'account, non solo al servizio CFEE stesso ma anche ai servizi di supporto creati anch'essi automaticamente quando viene creato il CFEE.

Le seguenti politiche di accesso IAM (Identity & Access Management) sono richieste affinché gli utenti possano creare un'istanza di {{site.data.keyword.cfee_full_notm}}:

* Accesso _visualizzatore_ (o superiore) al **gruppo di risorse** **_Predefinito_** nell'account {{site.data.keyword.Bluemix}}. I gruppi di risorse consentono di organizzare le risorse in raggruppamenti personalizzati per facilitare il controllo dell'accesso a tali risorse. Ti viene richiesto di creare un gruppo di risorse quando crei una nuova istanza dell'ambiente. L'accesso al gruppo di risorse _Predefinito_ è richiesto perché questo è sempre il gruppo di risorse in cui è richiesto il cluster Kubernetes.  Gli utenti possono eseguire il provisioning dell'istanza CFEE in un gruppo di risorse differente, ma il provisioning del cluster Kubernetes verrà comunque eseguito nel gruppo di risorse _Predefinito_.  Se un utente esegue il provisioning del CFEE in un gruppo utenti differente, a tale utente verrà richiesto l'accesso visualizzatore in tale gruppo di risorse.

* Ruolo di _amministratore_ o _editor_ alle risorse **del servizio {{site.data.keyword.cfee_full_notm}}**. Nel gruppo di risorse a cui viene assegnato l'ambiente. Gli utenti con i ruoli di amministratore o di editor nel servizio {{site.data.keyword.cfee_full_notm}} possono creare ed eliminare gli ambienti. Ma solo gli utenti con un ruolo di amministrazione possono assegnare gli utenti a un'istanza di {{site.data.keyword.cfee_full_notm}} o modificare i ruoli assegnati agli utenti in tale istanza.
   
* Ruolo di _amministratore_ alle risorse del **Servizio Kubernetes**.  Le istanze di {{site.data.keyword.cfee_full_notm}} sono distribuite sull'infrastruttura del cluster di contenitori, fornita dal servizio Kubernetes. Quando crei un'istanza del servizio {{site.data.keyword.cfee_full_notm}}, il servizio crea automaticamente un cluster Kubernetes. L'accesso al servizio Kubernetes è richiesto per la creazione di tale infrastruttura cluster. Puoi definire l'ambito dell'accesso per la politica del servizio Kubernetes a una specifica regione dove intendi eseguire il provisioning dell'istanza CFEE oppure definire l'ambito dell'accesso a tutte le regioni.

* Un ruolo della piattaforma di _amministratore_ o di _editor_ e il ruolo di accesso di gestore del servizio al **servizio IBM Cloud Object Storage**, che è una dipendenza richiesta del servizio CFEE.  Un'istanza del servizio IBM Cloud Object Storage viene utilizzata per archiviare i dati generati durante la creazione dei contenitori dell'applicazione ICFEE (ad esempio, pacchetti di applicazioni caricati, pacchetti di build ed eseguibili compilati).

* Un'istanza del servizio Compose for PostgreSQL è una dipendenza necessaria del servizio CFEE.  Compose for PostgreSQL viene utilizzato per archiviare i dati Cloud Foundry nella tua istanza CFEE (ad esempio, controllo della distribuzione dell'applicazione, avvio o arresto degli eventi; conservando i record di appartenenza dell'utente CFEE, delle organizzazioni, degli spazi, delle applicazioni e delle connessioni al servizio).  L'istanza del **servizio Compose for PostgreSQL** è distribuita in uno spazio in un'organizzazione Cloud Foundry pubblica (non correlata all'organizzazione CFEE) che selezioni in fase di creazione di un'istanza {{site.data.keyword.cfee_full_notm}}.  Questo significa che, quando crei un'istanza {{site.data.keyword.cfee_full_notm}}, devi avere l'accesso di _gestore_ ad almeno un'organizzazione nell'ubicazione dove intendi eseguire il provisioning dell'istanza CFEE.  Devi anche disporre dell'accesso di _sviluppatore_ ad almeno uno spazio in tale organizzazione. 

  Se non sei un membro di almeno un'organizzazione pubblica nell'ubicazione dove intendi creare un'istanza CFEE, chiedi a un amministratore di IBM Cloud di invitarti a una. Se ha il ruolo di amministratore nell'account, puoi aggiungere utenti alle organizzazioni e agli spazi pubblici nell'account attenendoti alla seguente procedura:

     * Vai a [**Gestisci > Account > Organizzazioni Cloud Foundry**](https://console.bluemix.net/account/organizations) e fai clic su **Aggiungi un'organizzazione** oppure seleziona un'organizzazione esistente.
     * Vai alla scheda **Utenti** nella parte superiore della pagina dell'organizzazione.
     * Trova l'utente che ha bisogno di creare le istanze CFEE. Se l'utente che vuoi sia in grado di creare le istanze CFEE non è presente nell'elenco, fai clic su **Aggiungi o invita utente** sopra la tabella per aggiungere o invitare gli utenti all'organizzazione.
     * Vai alla scheda **Spazi** nella parte superiore della pagina dell'organizzazione.
     * Trova lo spazio dove verrà eseguito il provisioning dell'istanza di Compose for PostgreSQL e seleziona la casella di spunta del ruolo **Sviluppatore**.

La seguente schermata illustra le politiche di accesso come vengono visualizzate nella pagina Identity & Access di {{site.data.keyword.Bluemix_notm}} che consentono a un utente di creare un'istanza di {{site.data.keyword.cfee_full_notm}}.

![Politiche di accesso](img/AccessPolicies_Creator.png)

Puoi concedere le autorizzazioni utente utilizzando la riga di comando {{site.data.keyword.Bluemix}}.  Puoi anche definire una politica di accesso per un utente specificando i parametri della politica (cioè, servizi, ruoli, regioni, ecc.) in un file formattato JSON richiamato dal comando che crea la politica.  Consulta [Assegnazione a un utente di una politica IAM utilizzando la riga di comando](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline) per ulteriori informazioni o immetti `ibmcloud iam -help` nella riga di comando. Nota che questo richiede l'installazione della [CLI IBM Cloud](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
{:tip}

Per confermare che disponi delle politiche di accesso richieste per creare un'istanza di {{site.data.keyword.cfee_full_notm}}:
1. Vai al menu [**Gestisci > Accesso (IAM) > Utenti**](https://console.bluemix.net/iam/#/users) nell'intestazione {{site.data.keyword.Bluemix_notm}} per aprire la pagina **Identity & Access**.
2. Nella scheda Politiche di accesso, fai clic sull'utente che sta creando l'ambiente per assegnare e visualizzare le politiche di accesso per tale utente.

Per ulteriori informazioni sulla gestione degli utenti e dell'accesso in {{site.data.keyword.Bluemix}}, incluso come organizzare una serie di utenti e ID servizio per facilitare l'assegnazione dell'accesso a più utenti contemporaneamente, consulta [Gestione di utenti e accesso](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage).

### Velocizza l'impostazione delle autorizzazioni per creare un ambiente utilizzando la CLI
{: #permcli-creating}

Puoi velocizzare l'impostazione delle autorizzazioni per la creazione di istanze CFEE tramite `ibmcloud cfee create-permission-set`.  Il comando consente a un amministratore CFEE di impostare in un unico comando le politiche di accesso richieste per la creazione di un'istanza CFEE e di tutti i suoi servizi ausiliari. 

Il comando imposta le autorizzazioni a un _Gruppo di accesso_ IAM e aggiunge un utente a quel _Gruppo di accesso_.  L'amministratore che immette il comando può includere nel comando un _Gruppo di accesso_ esistente.  Se non viene fornito alcun _Gruppo di accesso_, viene creato automaticamente un _cfee-provision-access-group_ predefinito.

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

Il comando imposta le seguenti politiche di accesso per l'utente selezionato:

*  Ruoli di editor ai servizi Cloud Object Storage e CFEE nell'account IBM Cloud corrente.
*  Ruolo di amministratore al servizio Kubernetes nell'account IBM Cloud corrente.
*  Ruolo di sviluppatore nello spazio e nell'organizzazione correnti per il provisioning di Compose for PostgreSQL.

Per ulteriori dettagli sul comando immetti quanto segue:

```
cfee create-permission-set -help
```
{: pre}

Puoi utilizzare `ibmcloud cfee create-permission-get` per individuare o convalidare le politiche di accesso al posto di un utente:

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## Autorizzazioni necessarie per utilizzare un ambiente
{: #perm-working}

Per utilizzare un'istanza di {{site.data.keyword.cfee_full_notm}}, gli utenti devono:
1. Essere membri dell'account {{site.data.keyword.Bluemix_notm}} in cui è stata creata l'istanza di {{site.data.keyword.cfee_full_notm}}.
2. Disporre delle seguenti _Politiche di accesso_ IAM concesse dall'amministratore dell'account (consulta la pagina _Identity & Access_ nel menu [**Gestisci > Accesso (IAM) > Utenti**](https://console.bluemix.net/iam/#/users) nell'intestazione {{site.data.keyword.Bluemix_notm}} per controllare le tue politiche di accesso correnti):

    Qualsiasi utente che lavora in un'istanza CFEE ha bisogno di un ruolo della piattaforma di _visualizzatore_ (o superiore) per:
  - Il gruppo di risorse nel quale è stata creata l'istanza CFEE.
  - L'istanza CFEE stessa. 
  
   Il livello di accesso e controllo di cui gli utenti dispongono in un'istanza CFEE dipende dal ruolo concesso nelle loro politiche di accesso:

  - Gli utenti con il ruolo di _visualizzatore_ per un'istanza CFEE, possono vederlo elencato nel dashboard {{site.data.keyword.Bluemix_notm}} principale e aprirne l'interfaccia utente. Gli utenti che accedono a specifiche organizzazioni e spazi all'interno dell'ambiente sono regolati dai ruoli specifici dell'organizzazione e degli spazi assegnati dai gestori di tali organizzazioni e spazi. Per ulteriori informazioni, consulta [Aggiunta di utenti a organizzazioni](add-users.html).
  
  - Gli utenti a cui sono assegnati i ruoli di _amministratore_ o _editor_ per un'istanza CFEE possono creare organizzazioni, assegnare gestori alle organizzazioni e agli spazi, disporre di autorizzazioni complete per tutti gli spazi e le organizzazioni all'interno dell'ambiente ed eseguire le azioni operative tramite l'API controller cloud. A questi utenti viene concesso automaticamente l'_ambito cloud_controller.admin_ nell'_ambito Account utente e autenticazione_ Cloud Foundry.

  - Gli utenti hanno bisogno di un ruolo della piattaforma di _editor_ o superiore a un'istanza CFEE e di un ruolo di _operatore_ o superiore al cluster Kubernetes in cui viene eseguito il provisioning del CFEE per poter **aggiornare il CFEE a una nuova versione**.

  - Gli utenti hanno bisogno di un ruolo della piattaforma di _amministratore_ a un'istanza CFEE e di un ruolo di _operatore_ o superiore al cluster di Kubernetes in cui viene eseguito il provisioning del CFEE per poter **modificare la capacità** di un CFEE (aggiungendo o rimuovendo le celle).
 
  - Gli utenti hanno bisogno del ruolo della piattaforma di _operatore_ (o superiore) per un'istanza del servizio IBM Cloud per poter **aggiungere** tale *istanza del servizio* a uno spazio CFEE (ossia, aggiungere come alias un'istanza del servizio in uno spazio CFEE).
 
  - Gli utenti hanno bisogno del ruolo della piattaforma di _operatore_ (o successiva) e del ruolo del servizio di _scrittore_ (o superiore) per un'istanza del servizio IBM Cloud per poter **associare mediante bind** tale istanza del servizio a un'applicazione distribuita in uno spazio CFEE.


## Prassi ottimali: gruppi di accesso
{: #access-groups}

Prendi in considerazione l'utilizzo dei gruppi di accesso per gestire e semplificare il controllo dell'accesso per il tuo CFEE.  I gruppi di accesso ti consentono di definire dei gruppi arbitrari a cui puoi assegnare politiche di accesso.  A qualsiasi utente aggiunto a un gruppo di accesso viene automaticamente assegnata la politica di accesso del gruppo. 

Puoi creare e gestire i gruppi di accesso dall'interfaccia utente IBM Cloud oppure tramite la cli `ibmcloud`. 

Dall'interfaccia utente, vai alla barra dei menu, fai clic su **Gestisci > Accesso (IAM)** e seleziona [Gruppi di accesso](https://cloud.ibm.com/iam#/groups).

In alternativa, puoi utilizzare la cli `ibmcloud`:

1. Crea un gruppo di accesso:

  ```
  ibmcloud iam access-group-create NOME_GRUPPO [-d, --description DESCRIZIONE]
```
  {: pre}

2. Crea una politica di accesso per tale gruppo di accesso:

  ```
  ibmcloud iam access-group-policy-create NOME_GRUPPO
  ```
  {: pre}

3. Aggiungi gli utenti al gruppo di accesso:

  ```
  ibmcloud iam access-group-user-add <user-name> [<user-name2...]
  ```
  {: pre}

<br>
Per ulteriori informazioni, vedi [Configurazione dei gruppi di accesso](https://cloud.ibm.com/docs/iam/groups.html#groups).
