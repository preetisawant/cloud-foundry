---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Autorizzazioni
{: #permissions}

Prima che gli utenti inizino a creare e utilizzare istanze del servizio {{site.data.keyword.cfee_full}}, le loro autorizzazioni devono essere impostate correttamente da un amministratore dell'account dove deve essere creata l'istanza. 

## Autorizzazioni necessarie per creare un nuovo ambiente
{: #perm-creating}

Per creare delle nuove istanze del servizio CFEE, agli utenti devono essere concesse le politiche di accesso da un amministratore dell'account, non solo al servizio CFEE stesso ma anche ai servizi di supporto creati anch'essi automaticamente quando viene creato il CFEE.

Le seguenti politiche di accesso IAM (Identity & Access Management) sono richieste affinché gli utenti possano creare un'istanza di {{site.data.keyword.cfee_full_notm}}:

* Accesso _visualizzatore_ (o superiore) al **gruppo di risorse** **_Predefinito_** nell'account {{site.data.keyword.Bluemix}}. I gruppi di risorse consentono di organizzare le risorse in raggruppamenti personalizzati per facilitare il controllo dell'accesso a tali risorse. Ti viene richiesto di creare un gruppo di risorse quando crei una nuova istanza dell'ambiente. L'accesso al gruppo di risorse _Predefinito_ è richiesto perché questo è sempre il gruppo di risorse in cui è richiesto il cluster Kubernetes.  Gli utenti possono eseguire il provisioning dell'istanza CFEE in un gruppo di risorse differente, ma il provisioning del cluster Kubernetes verrà comunque eseguito nel gruppo di risorse _Predefinito_.  Se un utente esegue il provisioning del CFEE in un gruppo utenti differente, a tale utente verrà richiesto l'accesso visualizzatore in tale gruppo di risorse.

* Ruolo _amministratore_ o _editor_ alle risorse **del servizio {{site.data.keyword.cfee_full_notm}}**. Nel gruppo di risorse a cui viene assegnato l'ambiente. Gli utenti con i ruoli di amministratore o di editor nel servizio {{site.data.keyword.cfee_full_notm}} possono creare ed eliminare gli ambienti. Ma solo gli utenti con un ruolo di amministrazione possono assegnare gli utenti a un'istanza di {{site.data.keyword.cfee_full_notm}} o modificare i ruoli assegnati agli utenti in tale istanza.
   
* Ruolo _amministratore_ alle risorse del **Servizio Kubernetes**. Le istanze di {{site.data.keyword.cfee_full_notm}} sono distribuite sull'infrastruttura del cluster di contenitori, fornita dal servizio Kubernetes. Quando crei un'istanza del servizio {{site.data.keyword.cfee_full_notm}}, il servizio crea automaticamente un cluster Kubernetes. L'accesso al servizio Kubernetes è richiesto per la creazione di tale infrastruttura cluster. Puoi definire l'ambito dell'accesso per la politica del servizio Kubernetes a una specifica regione dove intendi eseguire il provisioning dell'istanza CFEE oppure definire l'ambito dell'accesso a tutte le regioni.

* Un ruolo della piattaforma _amministratore_ o _editor_ e il ruolo di accesso di gestore del servizio al **servizio IBM Cloud Object Storage**, che è una dipendenza richiesta del servizio CFEE. Un'istanza del servizio IBM Cloud Object Storage viene utilizzata per archiviare i dati generati durante la creazione dei contenitori dell'applicazione ICFEE (ad esempio, pacchetti di applicazioni caricati, pacchetti di build ed eseguibili compilati).

* Un'istanza del servizio Compose for PostgreSQL è una dipendenza necessaria del servizio CFEE.  Compose for PostgreSQL viene utilizzato per archiviare i dati Cloud Foundry nella tua istanza CFEE (ad esempio, controllo della distribuzione dell'applicazione, avvio o arresto degli eventi; conservando i record di appartenenza dell'utente CFEE, delle organizzazioni, degli spazi, delle applicazioni e delle connessioni al servizio).  L'istanza del **servizio Compose for PostgreSQL** è distribuita in uno spazio in un'organizzazione Cloud Foundry pubblica (non correlata all'organizzazione CFEE) che selezioni in fase di creazione di un'istanza {{site.data.keyword.cfee_full_notm}}.  Questo significa che, quando crei un'istanza {{site.data.keyword.cfee_full_notm}}, devi avere l'accesso di _gestore_ ad almeno un'organizzazione nell'ubicazione dove intendi eseguire il provisioning dell'istanza CFEE. Devi anche disporre dell'accesso di _sviluppatore_ ad almeno uno spazio in tale organizzazione. 

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
1. Vai al menu [**Gestisci > Account > Utenti**](https://console.bluemix.net/iam/#/users) nell'intestazione {{site.data.keyword.Bluemix_notm}} per aprire la pagina **Identity & Access**.
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

Per utilizzare un'istanza di {{site.data.keyword.cfee_full_notm}}, gli utenti devono essere:
1. Membri dell'account {{site.data.keyword.Bluemix_notm}} in cui è stata creata l'istanza di {{site.data.keyword.cfee_full_notm}}.
2. Disporre delle seguenti _Politiche di accesso_ IAM concesse dall'amministratore dell'account (consulta la pagina _Identity & Access_ nel menu [**Gestisci > Account > Utenti**](https://console.bluemix.net/iam/#/users) nell'intestazione {{site.data.keyword.Bluemix_notm}} per controllare le tue politiche di accesso correnti):

    Tutti gli utenti hanno bisogno di un accesso da _visualizzatore_ o superiore per l'istanza {{site.data.keyword.cfee_full_notm}} nel gruppo di risorse in cui è stata creata l'istanza dell'ambiente. Il livello di accesso e di controllo che gli utenti hanno in un'istanza di {{site.data.keyword.cfee_full_notm}} dipende dal ruolo che viene concesso nella politica di accesso:
  - Gli utenti assegnati ai ruoli di _amministratore_ o _editor_ possono creare organizzazioni, assegnare gestori alle organizzazioni e agli spazi, disporre di autorizzazioni complete per tutti gli spazi e le organizzazioni all'interno dell'ambiente ed eseguire le azioni operative tramite l'API controller Cloud. A questi utenti viene concesso automaticamente l'_ambito cloud_controller.admin_ nell'_ambito Account utente e autenticazione_ Cloud Foundry.
  - Gli utenti con il ruolo di _visualizzatore_ per un CFEE, possono vederlo elencato nel dashboard {{site.data.keyword.Bluemix_notm}} principale e aprirne l'interfaccia utente. Gli utenti che accedono a specifiche organizzazioni e spazi all'interno dell'ambiente sono regolati dai ruoli specifici dell'organizzazione e degli spazi assegnati dai gestori di tali organizzazioni e spazi. Per ulteriori informazioni, consulta [Aggiunta di utenti a organizzazioni](add-users.html).

     **Nota:** l'accesso da _visualizzatore_ al gruppo di risorse in cui viene raggruppata un'istanza CFEE non è sufficiente, di per se, a rendere visibile il CFEE a un utente.  Gli utenti hanno bisogno di un accesso esplicito all'istanza CFEE (con ruolo di visualizzatore o superiore) per avere la visibilità in quella istanza.

  - Gli utenti hanno bisogno di un ruolo di _editor_ o superiore a un servizio {{site.data.keyword.Bluemix_notm}} per poter **associare** un'istanza di tale servizio a un'applicazione distribuita in uno spazio CFEE.

  - Gli utenti hanno bisogno di un ruolo di _editor_ o superiore a un'istanza CFEE e di un ruolo di _operatore_ o superiore al cluster Kubernetes in cui viene eseguito il provisioning del CFEE per poter **aggiornare il CFEE a una nuova versione**.

  - Gli utenti hanno bisogno di un ruolo di _amministratore_ a un'istanza CFEE e un ruolo di _operatore_ o superiore al cluster di Kubernetes in cui viene eseguito il provisioning del CFEE per poter **modificare la capacità** di un CFEE (aggiungendo o rimuovendo le celle).

