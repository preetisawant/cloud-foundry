---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Esercitazione introduttiva
{: #getting-started}

{{site.data.keyword.cfee_full}} è una piattaforma cloud per ospitare applicazioni e servizi nel cloud. {{site.data.keyword.cfee_full_notm}} rende più semplice ridimensionare le applicazioni man mano che il consumo cresce, semplificando il runtime, il middleware e l'infrastruttura in modo che ti puoi concentrare sullo sviluppo delle applicazioni.
{: shortdesc}

Questa esercitazione introduttiva mostra come creare un {{site.data.keyword.cfee_full_notm}}, aggiungere utenti, creare un'organizzazione e gli spazi, distribuire le applicazioni e associare queste applicazioni ai servizi.

## Informazioni sulle autorizzazioni
{: #permissions}

Per gestire le istanze di {{site.data.keyword.cfee_full_notm}}, gli utenti del servizio devono disporre delle autorizzazioni corrette. Per ulteriori informazioni, consulta [Autorizzazioni](/docs/cloud-foundry/permissions.html).

## Passo 1: assicurati che l'account {{site.data.keyword.Bluemix_notm}} possa creare le risorse dell'infrastruttura
{: #accountprep-environment}

Le istanze CFEE vengono distribuite sulle risorse dell'infrastruttura, che sono nodi di lavoro Kubernetes dal servizio IBM Container.  [Prepara il tuo account IBM Cloud](/docs/cloud-foundry/prepare-account.html) per verificare di poter creare le risorse dell'infrastruttura necessarie per un'istanza CFEE.

## Passo 2: crea la tua istanza CFEE 
{: #creating-environment}

Prima di creare la tua CFEE, assicurarti di essere nell'account {{site.data.keyword.Bluemix_notm}} IBM Cloud in cui vuoi creare l'ambiente e di disporre delle politiche di accesso necessarie (per il passo 1 sopra riportato).

1. Apri il {{site.data.keyword.Bluemix_notm}}Catalogo [ ](https://console.bluemix.net/catalog).
2. Individua il servizio {{site.data.keyword.cfee_full_notm}} nel catalogo e fai clic su di esso per aprirne la pagina della panoramica.
3. La prima pagina della pagina di creazione fornisce una panoramica delle funzioni principali del servizio. Fai clic su **Continue**.
4. Configura l'istanza che deve essere creata fornendo quanto segue:
    * Seleziona un piano (la disponibilità del piano può essere limitata durante Beta).
    * Immetti un **Name** per l'istanza del servizio.
    * Seleziona una **Location** in cui deve essere eseguito il provisioning dell'istanza del servizio.
    * Seleziona il **Number of cells** per l'ambiente Cloud Foundry.
    * Seleziona il **Machine type**, che determina la dimensione delle celle Cloud Foundry (CPU e memoria).
    * Seleziona un **Resource group** nel quale viene raggruppato l'ambiente. Solo i gruppi di risorse a cui hai accesso nell'account IBM Cloud corrente verranno elencati nell'elenco a discesa _Resourouce groups_, il che significa che devi disporre dell'autorizzazione per accedere ad almeno un gruppo di risorse nell'account per poter creare una CFEE.
5. Facoltativamente, apri la sezione **Infrastructure** per visualizzare le proprietà del cluster Kubernetes che supporta l'istanza CFEE. Tieni presente che il **Number of worker nodes** è uguale al numero di celle più 2 (due dei nodi di lavoro Kubernetes forniti supportano il piano di controllo CFEE).
6. L'**Order Summary** nella parte destra della pagina riflette il costo dell'istanza CFEE e il totale stimato.
7. Fai clic su **Create**, che apre il dashboard dell'ambiente e indica lo stato e l'avanzamento della creazione.
8. Una volta avviato il provisioning, l'ambiente viene visualizzato nel dashboard {{site.data.keyword.Bluemix_notm}}, così come nel [Dashboard Ambienti Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments).  Lo stato indica quando il provisioning è completato.

Il processo automatizzato che crea l'ambiente distribuisce l'infrastruttura in un cluster Kubernetes e la configura per renderla pronta per l'uso. Il processo dura 90 - 120 minuti.

**Nota:** il cluster Kubernetes su cui l'ambiente viene distribuito viene visualizzato nel {{site.data.keyword.Bluemix_notm}} [ dashboard](https://console.bluemix.net/dashboard/apps/). Per ulteriori informazioni, consulta [ {{site.data.keyword.Bluemix_notm}} Container Service documentation](/docs/containers/cs_why.html#cs_ov).

## Passo 3: creazione di organizzazioni e spazi

Dopo aver creato il {{site.data.keyword.cfee_full_notm}}, consulta [Creazione di organizzazioni e spazi](/docs/cloud-foundry/orgs-spaces.html) per informazioni su come strutturare l'ambiente creando le organizzazioni e gli spazi. Le applicazioni in un {{site.data.keyword.cfee_full_notm}} vengono indirizzate all'interno di spazi specifici. A sua volta, uno spazio si trova all'interno di un'organizzazione specifica. I membri di un'organizzazione condividono un piano di quota, le applicazioni, le istanze dei servizi e i domini personalizzati.

**Nota:** la pagina _Cloud Foundry organizations_ disponibile dal menu **_Manage > Account > Cloud Foundry orgs_** situata nella parte superiore dell'intestazione di IBM Cloud è destinata esclusivamente alle organizzazioni pubbliche di IBM Cloud, **non alle organizzazioni CFEE**. Le organizzazioni CFEE vengono gestite all'interno della pagina _Organizations_ di un'istanza CFEE.  Apri l'interfaccia utente CFEE e fai clic sulla pagina **_Organizations_** per creare e gestire le organizzazioni per tale CFEE.

## Passo 4: aggiunta di utenti a organizzazioni e spazi

[Aggiungi gli utenti](/docs/cloud-foundry/add-users.html) a tali organizzazioni e spazi in specifiche assegnazioni di ruoli che controllano il loro livello di accesso.  Prima che gli utenti possano essere aggiunti come membri di organizzazioni e spazi in una CFEE, è necessario che tali utenti abbiano un accesso precedente all'istanza CFEE. Consulta [Autorizzazioni](/docs/cloud-foundry/permissions.html).

## Passo 5: distribuzione e visualizzazione delle applicazioni

Quando sei pronto, puoi [distribuire l'applicazione](/docs/cloud-foundry/deploy-apps.html) con l'interfaccia riga di comando (CLI) {{site.data.keyword.Bluemix_notm}}.  Visualizza l'elenco delle applicazioni distribuite nell'interfaccia utente, nel contesto di uno spazio CFEE specifico o globalmente in tutte le istanze CFEE.  Puoi anche avviare, arrestare o eliminare le applicazioni da quelle viste.

## Passo 6: creazione degli alias e delle istanze del servizio

Crea gli [alias del servizio](/docs/cloud-foundry/add-serv-inst.html) dalle istanze del servizio disponibili nell'account IBM Cloud per utilizzarli nelle applicazioni CFEE.

## Passo 7: associazione delle applicazioni alle istanze del servizio

[Associa la tua applicazione](/docs/cloud-foundry/binding.html) a un alias dell'istanza del servizio per poter utilizzare le funzioni del servizio.

## Passo 8: installazione della console Stratos per gestire le applicazioni (facoltativo)

La console Stratos è uno strumento open source basato sul web per lavorare con Cloud Foundry. L'applicazione della console Stratos può essere facoltativamente installata e utilizzata in un ambiente CFEE specifico per gestirne le organizzazioni, gli spazi e le applicazioni.

Gli utenti con i ruoli di editor e amministratore IBM Cloud nell'istanza CFEE possono installare l'applicazione della console Stratos in tale istanza CFEE.

Per installare l'applicazione della console Stratos:

1. Apri l'istanza CFEE in cui vuoi installare la console Stratos.
2. Fai clic su **Install Stratos Console** nella pagina della panoramica. Il pulsante è visibile solo agli utenti con autorizzazioni di amministratore o di editor per tale istanza CFEE.
3. Nella finestra di dialogo Install Stratos Console, seleziona un'opzione di installazione. Puoi installare l'applicazione della console Stratos sul piano di controllo CFEE o in una delle celle. Seleziona una versione della console Stratos e il numero di istanze dell'applicazione da installare. Se installi l'applicazione della console Stratos in una cella, ti vengono richiesti l'organizzazione e lo spazio in cui distribuire l'applicazione.
4. Fai clic su **Install**.

Per installare l'applicazione sono necessari circa 5 minuti. Una volta completata l'installazione, viene visualizzato il pulsante **Stratos Console** al posto del pulsante _Install Stratos Console_ nella pagina della panoramica. Il pulsante _Stratos Console_ avvia la console ed è disponibile per tutti gli utenti con accesso all'istanza CFEE. Le assegnazioni di appartenenza all'organizzazione e allo spazio possono limitare ciò che un utente può visualizzare e gestire nella console Stratos.

Per avviare la console Stratos:

1. Apri l'istanza CFEE in cui è stata installata la console Stratos.
2. Fai clic su **Stratos Console** nella pagina della panoramica. 
3. La console Stratos viene aperta in una scheda del browser separata. Quando apri la console per la prima volta, ti viene richiesto di accettare due avvertenze consecutive per via dei certificati autofirmati.
4. Fai clic su **Login** per aprire la console. Non è richiesta alcuna credenziale poiché l'applicazione utilizza le tue credenziali {{site.data.keyword.Bluemix_notm}}.

Ciò che puoi visualizzare e gestire è limitato dai tuoi ruoli e dalla tua appartenenza alle organizzazioni e agli spazi.
