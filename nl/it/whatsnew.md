---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Novità in IBM Cloud Foundry Enterprise Environment

Questo documento descrive le novità in ogni versione rilasciata fino a questa data del servizio {{site.data.keyword.cfee_full_notm}}.


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
