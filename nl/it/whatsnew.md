---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Novità in IBM Cloud Foundry Enterprise Environment

Questo documento descrive le novità in ogni versione rilasciata fino a questa data del servizio {{site.data.keyword.cfee_full_notm}}.

## Versione 2.2.0
{: #v220}

_Data di release:_ 01-04-2019

CFEE v2.2.0 include le seguenti versioni dei suoi componenti costituenti:
* Cloud Foundry: v2.7.1.15.5
* API Cloud Foundry: v2.115.0
* Pacchetti di build CFEE: v0.1.5
* Servizio IBM Kubernetes: nessun aggiornamento della versione fornito.  **Importante:** ti consigliamo di aggiornare il cluster Kubernetes CFEE alla v1.13 prima dell'aggiornamento a CFEE v2.2.0 (obbligatorio quando l'istanza CFEE opera in una rete isolata).

Le seguenti modifiche sono state rilasciate nella versione 2.2.0 del servizio {{site.data.keyword.cfee_full_notm}} (CFEE). Per aggiornare la versione del tuo CFEE, vai alla pagina **Aggiornamenti e ridimensionamento** nell'interfaccia utente del CFEE e fai clic su **Aggiorna**:

* Nuova opzione per **creare** un'istanza CFEE in un cluster Kubernetes **multizona**. Le istanze CFEE create su un cluster multizona distribuiscono le istanze dell'applicazione non solo tra i nodi di lavoro all'interno di un data center, ma anche tra i data center, rendendo le tue applicazioni più resilienti rispetto a delle interruzioni dell'infrastruttura. Inoltre, i CFEE multizona possono essere **ridimensionati** aggiungendo ulteriori celle o rimuovendone di esistenti dalle zone correnti.  Tieni presente che non puoi aggiungere o rimuovere delle zone da un CFEE multizona una volta che viene creata l'istanza CFEE.
* Le istanze CFEE v2.2.0 possono ora [operare all'interno di una **rete isolata**](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). Tieni presente che se l'istanza CFEE viene distribuita nelle VLAN da una rete isolata, alcuni endpoint (indirizzi IP) [devono essere identificati ed instradati correttamente](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points) in modo che l'istanza CFEE diventi operativa. Un'istanza CFEE richiede un cluster Kubernetes v1.13 per operare in una rete isolata.
* Nuova funzionalità per associare le applicazioni (distribuite in uno spazio CFEE) alle istanze del servizio tramite la rete IBM interna. La funzionalità consente l'utilizzo dei servizi che supportano l'endpoint del servizio IBM Cloud senza dover accedere a internet pubblico.
* Strumenti di **monitoraggio**:
    * Non viene più eseguito per impostazione predefinita il provisioning degli strumenti di monitoraggio (Prometheus, Grafana e Alertmanager) quando crei un CFEE.  Viene eseguito il provisioning degli strumenti di monitoraggio CFEE v2.2.0 solo quando abilitati in modo esplicito dagli amministratori CFEE.  Inoltre, quando abilitati, non viene più eseguito il provisioning degli strumenti di monitoraggio nei nodi di lavoro del piano di controllo CFEE. Ne viene eseguito il provisioning nei rispettivi nodi di lavoro, al di fuori del piano di controllo. Per abilitare ed eseguire il provisioning degli strumenti di monitoraggio, vai alla pagina _Monitoraggio_ CFEE (nel pannello di navigazione di sinistra) e fai clic su **Abilita monitoraggio**. 
    * Quando aggiorni un CFEE esistente alla versione 2.2.0, gli strumenti di monitoraggio esistenti vengono eliminati dal piano di controllo. Tutte le configurazioni personalizzate esistenti degli strumenti di monitoraggio andranno perse. 
    *  Nuova funzionalità per sostituire la [configurazione Alertmanager](https://prometheus.io/docs/alerting/configuration/) predefinita con una personalizzata che ti consente di personalizzare la gestione, il raggruppamento e l'instradamento della notifica degli avvisi. Nella pagina _Monitoraggio_ potrai _Scaricare_ il file di configurazione predefinito e _Caricare_ un file di configurazione dal tuo file system locale.  Vedi un [esempio](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml) di un file di configurazione.
* Nuova funzionalità per contrassegnare con tag le istanze CFEE nell'[_Elenco risorse_](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}} e nell'interfaccia utente CFEE.
* Miglioramenti generali all'esperienza utente del [**dashboard Cloud Foundry** {{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/dashboard/cloudfoundry/overview). Il _dashboard Cloud Foundry_ mostra le viste globali dei servizi pubblici, delle applicazioni e delle istanze CFEE aggiunti come alias negli spazi CFEE. 

**Nota:** è disponibile un nuovo piano **Anteprima tecnica Eirini** quando crei una nuova istanza CFEE. Il piano è indipendente dalla v2.2.0 descritta in precedenza, che si applica solo al piano _Standard_.  Il piano Anteprima tecnica Eirini ti consente di esplorare un CFEE utilizzando Kubernetes nativo come programma di pianificazione del contenitore (invece di Diego). Per ulteriori informazioni, vedi [Introduzione all'anteprima tecnica Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).

Guarda una dimostrazione delle novità in CFEE v2.1.0 in questo [breve video](https://ibm.biz/CFEE-V220){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").  


## Versione 2.1.1
{: #v211}

_Data di release:_ 20-03-2019

Le seguenti modifiche sono state rilasciate nella versione 2.1.1 del servizio {{site.data.keyword.cfee_full_notm}} (CFEE). Per aggiornare la versione del tuo CFEE, vai alla pagina _Aggiornamenti e ridimensionamento_ nell'interfaccia utente del CFEE:

* Risolti i problemi che impedivano la corretta esecuzione del provisioning. 


## Versione 2.1.0
{: #v210}

_Data di release:_ 20-02-2019

**Nota:** puoi eseguire l'aggiornamento a questa versione solo dalla versione **2.0.2**. Esegui l'aggiornamento alla versione 2.0.2 prima di farlo alla v2.1.0.

Le seguenti modifiche sono state rilasciate nella versione 2.1.0 del servizio {{site.data.keyword.cfee_full_notm}} (CFEE). Per aggiornare la versione del tuo CFEE, vai alla pagina **Aggiornamenti e ridimensionamento** nell'interfaccia utente del CFEE e fai clic su **Aggiorna**:

* Nuova funzionalità di ridimensionamento automatico che ridimensiona automaticamente le istanze dell'applicazione Cloud Foundry in base a delle regole personalizzate. Il ridimensionamento automatico è accessibile dalla CLI e dalla console Stratos. La console Stratos può essere facoltativamente installata e avviata dalla pagina _Panoramica_ nell'interfaccia utente CFEE. Nella pagina _Applications_ della console Stratos, seleziona un'applicazione e cerca la scheda **Auto Scaling**. Fai clic su *Create Policy* per avviare l'editor di ridimensionamento automatico per definire la politica di ridimensionamento per l'applicazione di destinazione.
  Per ulteriori informazioni, vedi la [documentazione sul ridimensionamento automatico](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps).
* Nuova funzionalità per gestire i pacchetti di build dall'interfaccia utente CFEE, incluso il posizionamento tramite trascinamento e rilascio di un pacchetto di build nell'elenco di priorità. La funzionalità è disponibile nella nuova pagina **Pacchetti di build** dell'interfaccia utente CFEE (non la console Stratos). Nella release, solo i file zip del pacchetto di build della dimensione di 1 MB (o più piccoli) possono essere aggiunti o aggiornati tramite l'interfaccia utente. Puoi caricare file zip del pacchetto di build più grandi di 1 MB utilizzando i comandi `cf create-buildpack` e `cf update-buildpack`. 
* Nuova funzionalità per gestire le quote dell'organizzazione dall'interfaccia utente, inclusa la visualizzazione di quali organizzazioni stanno utilizzando una specifica quota. La funzionalità è disponibile nella nuova pagina **Quote** dell'interfaccia utente CFEE (non la console Stratos). Puoi creare delle nuove quote e modificarne di esistenti. Puoi anche aggiornare i valori della quota predefinita con i valori provenienti da tutte le quote esistenti richiamando **Copia come predefinita** dal menu della quota.
* Una nuova pagina **Introduzione** nell'interfaccia utente guida gli utenti alle attività più importanti per configurare ed utilizzare l'ambiente.
* Le **tag** possono essere aggiunte a un'istanza CFEE nell'elenco di risorse IBM Cloud.  Le tag aggiunte nell'elenco di risorse verranno visualizzate anche nell'intestazione della pagina di panoramica di CFEE.
* **Cloud Foundry** versione 2.7.21.
* Console **Stratos** versione 2.3.0, che include una patch di sicurezza. Tieni presente che aggiornare semplicemente la versione del CFEE non aggiornerà la versione della console Stratos. Devi eliminare e reinstallare la console Stratos (nella pagina Panoramica del CFEE), che sceglierà automaticamente la versione della console Stratos più recente.
* Gli utenti possono passare alla pagina **cluster** Kubernetes di CFEE dal menu di overflow nella pagina della panoramica di CFEE.

**Nota:** se esegui l'aggiornamento a CFEE v2.1.0 da una versione v2.0.x, l'aggiornamento viene eseguito con una sola azione _Aggiorna_ che aggiorna automaticamente sia il piano di controllo che le celle in sequenza. Se esegui l'aggiornamento da una versione v1.x.x, l'aggiornamento richiede due azioni _Aggiorna_ separate, una per l'aggiornamento del piano di controllo (prima azione) e una per l'aggiornamento delle celle.

Guarda una dimostrazione delle novità in CFEE v2.1.0 in questo [breve video](https://ibm.biz/CFEE-V210){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").  


## Versione 2.0.2
{: #v202}

_Data di release:_ 08-02-2019

Le seguenti modifiche sono state rilasciate nella versione 2.0.2 del servizio {{site.data.keyword.cfee_full_notm}} (CFEE). Per aggiornare la versione del tuo CFEE, vai alla pagina _Aggiornamenti e ridimensionamento_ nell'interfaccia utente del CFEE:

* Risolti i problemi che impedivano la corretta esecuzione degli aggiornamenti della versione. Questa versione è un prerequisito per l'aggiornamento alla versione **2.1.0**.


## Versione 2.0.1
{: #v201}

_Data di release:_ 10-01-2019

Le seguenti modifiche sono state rilasciate nella versione 2.0.1 del servizio {{site.data.keyword.cfee_full_notm}} (CFEE). Per aggiornare la versione del tuo CFEE, vai alla pagina _Aggiornamenti e ridimensionamento_ nell'interfaccia utente del CFEE:

* È stato risolto il problema che impedisce il corretto funzionamento dei domini personalizzati.
* È stato risolto il problema per cui le metriche dell'organizzazione non sono disponibili mentre vengono richiamate le nuove metriche.


## Versione 2.0.0
{: #v200}

_Data di release:_ 13-12-2018

Le seguenti modifiche sono state rilasciate nella versione 2.0.0 del servizio {{site.data.keyword.cfee_full_notm}} (CFEE). Per aggiornare la versione del tuo CFEE, vai alla pagina _Aggiornamenti e ridimensionamento_ nell'interfaccia utente del CFEE:

* Resilienza dell'aggiornamento della versione di CFEE migliorata.
* Miglioramenti a resilienza e disponibilità operativa delle istanze CFEE.
* Certificati lato client per un accesso più protetto alle applicazioni, consentendo al server di concedere l'accesso alle applicazioni solo ai client certificati.
* Quando viene creata un'istanza CFEE, il cluster Kubernetes di supporto e l'istanza del servizio Cloud Object Storage vengono ora creati nello stesso gruppo di risorse dell'istanza del servizio CFEE (invece che nel gruppo di risorse "Predefinito").
* Patch di sicurezza.
* Miglioramenti alla CLI `ibmcloud cfee`:
    * Nuovi comandi per creare un'istanza del servizio IBM Cloud da uno spazio CFEE e aggiungerla a tale spazio CFEE (`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`).
    * Nuovi comandi per ridimensionare la capacità di un CFEE (`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`).
    * Miglioramenti al comando per gestire le istanze CFEE (`ibmcloud cfee environments`).
    
      Aggiorna la CLI ibmcloud (`ibmcloud update`) per accedere a tali miglioramenti dei comandi e immetti `ibmcloud cfee -help` per ulteriori dettagli.
      
**Nota**: l'aggiornamento di un'istanza CFEE alla versione 2.0.0 richiede solo una singola azione _update_ che aggiorna sia il piano di controllo sia le celle. Non è richiesto alcun aggiornamento separato per le celle e il piano di controllo CFEE.


## Versione 1.1.2
{: #v112}

_Data di release:_ 07-12-2018

Le seguenti modifiche sono state rilasciate nella versione 1.1.2 del servizio {{site.data.keyword.cfee_full_notm}}:
* Dei nuovi data center a Chennai (che01) e Milano (mil01) sono ora disponibili per il provisioning di istanze CFEE.
* Patch di sicurezza.

## Versione 1.1.1
{: #v111}

_Data di release:_ 28-11-2018

Le seguenti modifiche sono state rilasciate nella versione 1.1.1 del servizio {{site.data.keyword.cfee_full_notm}}:
* Patch di sicurezza.
   
## Versione 1.1.0
{: #v110}

_Data di release:_ 16-11-2018

Le seguenti modifiche sono state rilasciate nella versione 1.1.0 del servizio {{site.data.keyword.cfee_full_notm}}:

* Nuove funzionalità:
   * È possibile eseguire il provisioning di istanze CFEE sui nodi di lavoro Kubernetes [virtuali-dedicati](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) ospitati sull'infrastruttura dedicata al tuo account IBM Cloud.
   * Un nuovo data center a Tokyo (tok05) è disponibile per eseguire il provisioning di istanze CFEE.
   * [Aggiornamento](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) di un'istanza CFEE a una nuova versione.
   * [Ridimensionamento](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) della capacità di un'istanza CFEE aggiungendo o eliminando le celle Cloud Foundry.
   * [Controllo](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) delle attività Cloud Foundry tramite l'integrazione con un'istanza del servizio Programma di traccia dell'attività IBM Cloud configurata automaticamente.
   * Persistenza degli [eventi di log](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) Cloud Foundry tramite un'istanza del servizio IBM Cloud Log Analysis configurata automaticamente.
   * Vista Controllo di integrità che indica lo stato operativo dei componenti CFEE.
   * Nuovi comandi per eseguire le azioni correlate a CFEE sull'interfaccia riga di comando (o CLI, Command Line Interface):
     * Comandi `ibmcloud cfee create`, `ibmcloud cfee create-locations` e `ibmcloud cfee create-status` per creare le istanze CFEE dall'interfaccia riga di comando, ottenere un elenco dei data center disponibili dove è possibile eseguire il provisioning di un CFEE e controllo dello stato di provisioning di un CFEE in fase di creazione.
     * [Comandi ](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) `ibmcloud cfee create-permission-get` e `ibmcloud cfee create-permission-set` per richiamare e impostare le autorizzazioni necessarie per creare istanze CFEE. I comandi aggregano e semplificano l'impostazione delle autorizzazioni per il servizio CFEE e per i servizi di supporto richiesti.
     * Comando `ibmcloud catalog blacklist` per semplificare il [controllo della visibilità](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) dei servizi IBM Cloud per gli utenti in un account IBM Cloud.

* Problemi risolti:
   *  Problema risolto: errore intermittente durante l'accesso alle metriche della cella
<br/>   
Guarda una dimostrazione delle novità in CFEE v1.1.0 in questo [breve video](https://ibm.biz/CFEE-V110){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").  Puoi anche trovare altri video su vari argomenti CFEE in [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
