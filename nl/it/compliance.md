---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Conformità e normative
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) è un PaaS (platform-as-a-service). In quanto tale, il cliente è libero di utilizzare l'istanza del servizio per tutto ciò che è in grado di supportare. I servizi CFEE e dipendenti hanno accesso al minor numero possibile di dati personali.

Dovrebbe essere chiaro, però, che anche se il piano di controllo CFEE (tramite IU/API/CLI) non elaborerà i dati sensibili (ad es. dati HIPAA), è responsabilità del cliente assicurarsi che utilizzino responsabilmente il proprio CFEE, poiché tutte le dipendenze sono gestite e di proprietà dei clienti nel loro account {{site.data.keyword.Bluemix_notm}}. 

Consigliamo le seguenti procedure ottimali:
*  Non modificare i servizi dipendenti creati con un CFEE (Kubernetes, Cloud Object Storage e Compose for PostgreSQL).
*  Aggiornare e gestire CFEE tramite il servizio CFEE stesso (interfaccia utente o interfaccia riga di comando), piuttosto che tramite il servizio Kubernetes.

Il cluster Kubernetes viene utilizzato per ospitare la maggior parte dell'infrastruttura CFEE, così come tutte le applicazioni in esecuzione su CFEE, dal momento che le celle Cloud Foundry sono distribuite sui nodi Kubernetes. Questo cluster è di proprietà e gestito dall'account SoftLayer del cliente.

Il database Compose for PostgreSQL viene utilizzato da CFEE per ospitare i metadati sulle organizzazioni, gli spazi, gli utenti e i ruoli. Se l'istanza CFEE viene utilizzata come consigliato, non ci saranno dati sensibili esposti. Tuttavia, se un cliente decide di nominare le proprie organizzazioni e spazi con informazioni personali o sensibili sui propri clienti, il database PostgreSQL potrebbe contenere HIPAA o un altro tipo di informazioni sensibili.

L'istanza di Cloud Object Storage viene utilizzata da CFEE per ospitare i droplet dell'applicazione, in modo che possano essere distribuite, arrestate, avviate, ecc. Ciò significa che l'istanza di Cloud Object Storage non sta eseguendo l'applicazione, ne sta solo ospitando l'immagine. Pertanto, se l'istanza di Cloud Object Storage viene utilizzata seguendo le procedure consigliate, non ospiterà alcuna informazione sensibile HIPAA. Il cliente ha la responsabilità di garantire che nessun dato personale sia codificato in nessuna delle proprie applicazioni (dati di test, ecc.).
