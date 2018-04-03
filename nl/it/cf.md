---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Funzionamento di Cloud Foundry con {{site.data.keyword.cloud_notm}}
{: #howwork}

Quando distribuisci un'applicazione a Cloud Foundry, devi configurare {{site.data.keyword.cloud_notm}} con una quantità sufficiente di informazioni per supportare l'applicazione.

* Per un'applicazione mobile, {{site.data.keyword.cloud_notm}} contiene una risorsa che rappresenta il back-end dell'applicazione mobile, ad esempio i servizi utilizzati dall'applicazione mobile per comunicare con un server.
* Per un'applicazione web, devi assicurarti che le informazioni sul runtime e sul framework siano comunicate a {{site.data.keyword.cloud_notm}}, in modo che {{site.data.keyword.cloud_notm}} possa configurare l'ambiente di esecuzione appropriato per eseguire l'applicazione.

Ogni ambiente di esecuzione, compresi sia quello mobile sia quello web, è isolato dall'ambiente di esecuzione di altre applicazioni. Gli ambienti di esecuzione sono isolati anche se tali applicazioni si trovano sulla stessa macchina fisica. La seguente figura mostra il flusso di base del modo in cui Cloud Foundry gestisce la distribuzione di applicazioni in {{site.data.keyword.cloud_notm}}:

![Distribuzione di un'applicazione](images/deploy.png)

Figura 1. Distribuzione di un'applicazione

Quando crei un'applicazione e la distribuisci a Cloud Foundry, l'ambiente {{site.data.keyword.cloud_notm}} determina un server virtuale appropriato a cui inviare l'applicazione o le risorse da essa rappresentate. Per un'applicazione mobile, su {{site.data.keyword.cloud_notm}} viene creata una proiezione di back-end mobile. Tutto il codice per l'applicazione mobile in esecuzione nel cloud alla fine viene eseguito nell'ambiente {{site.data.keyword.cloud_notm}}. Per un'applicazione web, il codice in esecuzione nel cloud è l'applicazione stessa che lo sviluppatore distribuisce a {{site.data.keyword.cloud_notm}}. La determinazione del server virtuale si basa su diversi fattori, tra cui:

* Il carico già sulla macchina
* I runtime o i framework supportati da tale server virtuale.

Una volta selezionato un server virtuale, su ciascun server virtuale un gestore dell'applicazione installa il framework e il runtime appropriati per l'applicazione. L'applicazione può quindi essere distribuita in tale framework. Una volta completata la distribuzione, le risorse dell'applicazione vengono avviate.

La seguente figura mostra la struttura di un server virtuale, nota anche come DEA (Droplet Execution Agent), su cui sono distribuite più applicazioni:

![Progetto di un server virtuale](images/container-diego.png)

Figura 2. Progetto di un server virtuale

In ciascun server virtuale, un gestore dell'applicazione comunica con il resto dell'infrastruttura {{site.data.keyword.cloud_notm}} e gestisce le applicazioni distribuite a tale server. Ogni server virtuale dispone di contenitori per separare e proteggere le applicazioni. In ogni contenitore, {{site.data.keyword.cloud_notm}} installa il framework e il runtime appropriati richiesti per ogni applicazione.

Quando l'applicazione viene distribuita, se ha un'interfaccia web (come per un'applicazione web Java), o altri servizi basati su REST (come i servizi mobili presentati pubblicamente all'applicazione mobile), gli utenti dell'applicazione possono comunicare con essa utilizzando normali richieste HTTP.

![Richiamo di un'applicazione {{site.data.keyword.cloud_notm}}](images/execute.png)

Figura 3. Richiamo di un'applicazione {{site.data.keyword.cloud_notm}}

A ogni applicazione può essere associato uno o più URL, ma tutti devono puntare all'endpoint {{site.data.keyword.cloud_notm}}. Quando viene ricevuta una richiesta, {{site.data.keyword.cloud_notm}} la esamina, determina qual è l'applicazione a cui è destinata, quindi seleziona un'istanza dell'applicazione per ricevere la richiesta.


## Architettura di Cloud Foundry in {{site.data.keyword.cloud_notm}}
{: #architecture}

In generale, non devi preoccuparti dei livelli di infrastruttura e sistema operativo durante l'esecuzione delle applicazioni su {{site.data.keyword.cloud_notm}} in Cloud Foundry. I livelli
quali, ad esempio, i file system root e i componenti middleware vengono astratti e pertanto puoi concentrarti sul
codice della tua applicazione. Tuttavia, se hai bisogno di specifiche su dove è in esecuzione
la tua applicazione, puoi consultare ulteriori informazioni su questi livelli.

Per i dettagli, vedi [Visualizzazione dei livelli dell'infrastruttura {{site.data.keyword.cloud_notm}}](cf.html#infralayers).

In qualità di sviluppatore, puoi interagire con l'infrastruttura {{site.data.keyword.cloud_notm}} utilizzando un'interfaccia utente basata sul browser. Puoi anche utilizzare un'interfaccia riga di comando Cloud Foundry, denominata cf, per distribuire applicazioni
web.

I client, che possono essere applicazioni mobili, applicazioni che vengono eseguite esternamente, applicazioni basate su {{site.data.keyword.cloud_notm}} o sviluppatori che stanno utilizzando dei browser, interagiscono con le applicazioni ospitate da {{site.data.keyword.cloud_notm}}. I client utilizzano API REST o HTTP per instradare le richieste tramite {{site.data.keyword.cloud_notm}} a una delle istanze dell'applicazione o ai servizi compositi.

La seguente figura mostra l'architettura di alto livello di Cloud Foundry in {{site.data.keyword.cloud_notm}}.

![{{site.data.keyword.cloud_notm}} architettura](images/arch.png)

Figura 4. Architettura di Cloud Foundry in {{site.data.keyword.cloud_notm}}

Puoi distribuire le
tue applicazioni a regioni {{site.data.keyword.cloud_notm}} differenti, per
considerazioni di sicurezza o di latenza. Puoi scegliere di effettuare la distribuzione su una singola regione o tra più regioni.


![Sviluppo di applicazioni a più regioni](images/multi-region.png)

Figura 5. Distribuzione di applicazioni a più regioni

Livelli dell'infrastruttura {{site.data.keyword.Bluemix_notm}}
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} astrae e nasconde i
livelli di sistema operativo e infrastruttura in modo che tu non debba occuparti della loro gestione. Tuttavia, potrebbe capitare che
tu voglia saperne di più sul sistema operativo e sul middleware per la tua applicazione.
{:shortdesc}

### Visualizzazione dei livelli dell'infrastruttura {{site.data.keyword.Bluemix_notm}}
{: #viewinfra}

Puoi eseguire il comando **bluemix app stacks** per visualizzare gli stack disponibili, o filesystem root, a cui devono essere distribuite le tue applicazioni. Puoi anche specificare lo stack quando utilizzi il comando **bluemix app push** con l'opzione *-s* e il *nome_stack*, dove il nome_stack è il filesystem root, ad esempio `lucid64` o `cflinuxfs2`:

```
bluemix app push appName -s nome_stack
```

Puoi utilizzare il comando `cf buildpacks` per visualizzare i componenti middleware, come il profilo WebSphere Liberty ed SDK for Node.js, disponibili come runtime in cui eseguire la tua applicazione. Puoi anche specificare l'ambiente di runtime per la tua applicazione utilizzando il seguente comando:

```
bluemix app push appName -b buildpackname
```
