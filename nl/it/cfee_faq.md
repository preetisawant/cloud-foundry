---



copyright:

  years: 2018

lastupdated: "2019-01-08"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# Domande frequenti (FAQ)
{: #cfeefaq}

## Qual è la differenza tra IBM Cloud Foundry Enterprise Environment (CFEE) e Cloud Foundry pubblico?
{: #cfee_diff}

Puoi utilizzare {{site.data.keyword.cloud}} Foundry pubblico per eseguire le applicazioni native cloud che stanno utilizzando Cloud Foundry per una semplice configurazione, una potente scalabilità e la gestione del traffico. Puoi anche avere un facile accesso a tutti i servizi {{site.data.keyword.cloud}}.

Puoi utilizzare {{site.data.keyword.cfee_full}} per tutto quello che faresti con Cloud Foundry pubblico, ma anche per creare e gestire ambienti isolati per ospitare le applicazioni Cloud Foundry esclusivamente per la tua azienda.


## Come si differenzia la nuova offerta dalla precedente offerta di IBM Cloud Foundry?
{: #cfOfferings_diff}

Per quanto riguarda il multitenant pubblico la differenza più degna di nota riguarda sicuramente le proprietà di isolamento. Per quanto riguarda l'offerta esistente a singolo tenant sull'infrastruttura IBM Cloud, le due principali differenze sono il footprint dell'infrastruttura ridotto (e quindi il costo) così come il modello di integrazione del servizio in un ambiente a singolo tenant.

## Dove posso trovare il servizio CFEE?
{: #where}

Puoi trovare e istanziare il servizio {{site.data.keyword.cfee_full}} nel [catalogo](https://console.stage1.bluemix.net/catalog) {{site.data.keyword.Bluemix_notm}}.

## Posso avere più di un ambiente CFEE all'interno di un data center regionale?
{: #multiple-cfees}

Sì, puoi creare le istanze CFEE su richiesta, quante ne desideri in [queste regioni](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

## Dovrò iniziare con una certa capacità minima?
{: #minimum-capacity}

Sì. La creazione di un'istanza CFEE richiede un minimo di due celle Cloud Foundry, ciascuna con 4 core di RAM da 16GB, disco primario SSD da 25GB, disco secondario SSD da 100GB e velocità di rete di 1000Mbps.

## Qual è l'IaaS di base in cui è distribuito CFEE?
{: #why-kubs}

Il servizio CFEE viene eseguito su contenitori Kubernetes, che consentono di ridurre i costi dell'infrastruttura e operazioni più efficienti, poiché Kubernetes è un IaaS molto intelligente che automatizza molte attività operative. 

## Quali sono le mie opzioni di isolamento quando creo un CFEE?
{: #isolation}

Hai due opzioni hardware sul tipo di infrastruttura Kubernetes in cui viene distribuita l'istanza CFEE: hardware _Virtual shared_ o _Virtual dedicated_. Con l'hardware _Virtual shared_, i nodi di lavoro (in cui viene distribuito il contenitore della piattaforma Cloud Foundry) vengono distribuiti tra te e gli altri clienti IBM.  Con _Virtual dedicated_ i nodi di lavoro sono ospitati sull'hardware dedicato in modo esclusivo al tuo account.  Nota che in entrambi i casi, _Virtual shared_ e _Virtual dedicated_, ogni nodo di lavoro è a singolo tenant per il cliente.  Ciò significa che le celle Cloud Foundry in cui vengono eseguite le applicazioni non sono condivise con altri clienti.

## Posso ridimensionare la capacità di un CFEE?
{: #scaling}

Sì, puoi aumentare o diminuire la capacità del tuo CFEE come cambiano i tuoi bisogni, aggiungendo o rimuovendo le celle Cloud Foundry.

## Posso eseguire l'upgrade del mio CFEE a una nuova versione? Come funziona?
{: #upgrading}
Sì. L'interfaccia utente di CFEE ti avvisa quando sono presenti nuove versioni di CFEE.  Controlli quando aggiornare a una nuova versione. L'aggiornamento della versione CFEE viene richiamato dagli amministratori CFEE nell'interfaccia utente. Gli aggiornamenti della versione CFEE possono impacchettare nuove versioni dei suoi componenti o servizi di supporto (ad esempio, Cloud Foundry, Kubernetes, ecc.).  Aggiorna prima il piano di controllo CFEE e poi le celle Cloud Foundry.  Il processo di aggiornamento è ottimizzato per minimizzare l'interruzione.

## Cosa c'è da fare per creare un'istanza CFEE?
{: #create}

Puoi trovare il servizio CFEE elencato nel catalogo {{site.data.keyword.Bluemix_notm}}.  Devi disporre di un account {{site.data.keyword.Bluemix_notm}} aggiornato e delle autorizzazioni al servizio CFEE e ai relativi servizi supportati (Kubernetes, Cloud Object Storage e Compose for PostgreSQL).  Una volta che hai tali autorizzazioni, fornisci un nome all'ambiente e fai clic su _Create_.  La creazione richiede circa 90 minuti.

## Posso utilizzare i servizi {{site.data.keyword.Bluemix_notm}} nel mio CFEE?
{: #Services-ibmcloud}

Assolutamente!  Essendo integrati in {{site.data.keyword.Bluemix_notm}}, gli sviluppatori in un CFEE possono creare le istanze del servizio {{site.data.keyword.Bluemix_notm}} (o utilizzare istanze esistenti) e associarle alle applicazioni distribuite negli spazi CFEE.

## Posso disporre dei miei servizi nel mio CFEE?
{: #Services-ibmcloud}

Sì.  Un amministratore può registrare un broker di servizi in CFEE e rendere i piani di servizi personalizzati disponibili agli utenti in tale CFEE.  Il marketplace MCFEE locale include i servizi dal catalogo {{site.data.keyword.Bluemix_notm}} più tutti i servizi del cliente gestiti dal broker di servizi locale di CFEE.

## Come posso controllare l'accesso dell'utente a un CFEE?
{: #Services}

Come per qualsiasi altro servizio {{site.data.keyword.Bluemix_notm}}, l'accesso a un CFEE viene controllato tramite _Identity & Access Management_ (IAM). L'assegnazione di politiche di accesso utente (sia individualmente che tramite gruppi di accesso) con ruoli specifici fornisce livelli specifici di accesso a un CFEE.  Oltre all'accesso al servizio CFEE, l'accesso alle organizzazioni e agli spazi di Cloud Foundry viene controllato tramite l'appartenenza a Cloud Foundry e ai ruoli assegnati agli utenti in organizzazioni e spazi specifici.

