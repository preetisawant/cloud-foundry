---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Novità in IBM Cloud Foundry Enterprise Environment

Questo documento descrive le novità in ogni versione rilasciata fino a questa data del servizio {{site.data.keyword.cfee_full_notm}}.

## Versione 1.1.0
{: #v101}

_Data di release:_ 16-11-2018

Le seguenti modifiche sono state rilasciate nella versione 1.1.0 del servizio {{site.data.keyword.cfee_full_notm}}:

* Nuove funzionalità:
   * [Aggiornamento](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) di un'istanza CFEE a una nuova versione.
   * [Ridimensionamento](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale)  della capacità di un'istanza CFEE aggiungendo o eliminando le celle Cloud Foundry.
   * [Controllo](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) delle attività Cloud Foundry tramite l'integrazione con un'istanza del servizio Programma di traccia dell'attività IBM Cloud configurata automaticamente.
   * Persistenza degli [eventi di log](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) Cloud Foundry tramite un'istanza del servizio IBM Cloud Log Analysis configurata automaticamente.
   * Nuovi comandi `ibmcloud cfee`  [](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) per richiamare e impostare le autorizzazioni per creare le istanze CFEE. I comandi aggregano e semplificano l'impostazione delle autorizzazioni per il servizio CFEE e per i servizi di supporto richiesti.
   * Nuovo comando `ibmcloud catalog blacklist` per semplificare il [controllo della visibilità](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) dei servizi di IBM Cloud per gli utenti in un account di IBM Cloud.

* Problemi risolti:
   *  Problema risolto: errore intermittente durante l'accesso alle metriche della cella
   
Guarda una dimostrazione delle novità in CFEE v1.1.0 in questo [breve video](https://ibm.biz/CFEE-V110){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

Puoi trovare altri video su vari argomenti CFFE in [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
