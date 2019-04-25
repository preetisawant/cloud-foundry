---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Creazione di un ambiente
{: #create-environment}

## Prerequisiti
* Assicurati di essere nell'account {{site.data.keyword.Bluemix_notm}} in cui vuoi creare l'ambiente.
* Assicurati di disporre delle [autorizzazioni](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html) corrette prima di creare le istanze di {{site.data.keyword.cfee_full_notm}}. 
* [Prepara il tuo account IBM Cloud](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html) per garantire che possa creare le risorse dell'infrastruttura necessarie per un'istanza CFEE (le istanze CFEE vengono distribuite nei nodi di lavoro Kubernetes dal servizio Kubernetes).  

## Creazione di un'istanza CFEE
1.  Apri il {{site.data.keyword.Bluemix_notm}} catalogo [](https://cloud.ibm.com/catalog).

2.  Individua il servizio {{site.data.keyword.cfee_full_notm}} nel catalogo e fai clic su di esso per aprirne la pagina della panoramica.  Tale prima pagina fornisce una panoramica delle funzioni principali del servizio. Fai clic su **Continue**.

3.  Configura l'istanza CFEE da creare:
    * Seleziona un piano. Vedi la sezione [Anteprima tecnica Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) per una descrizione delle limitazioni di questo piano.
    * Immetti un **Nome** per l'istanza CFEE.
    * Seleziona un **Gruppo di risorse** nel quale viene raggruppato l'ambiente. Solo i gruppi di risorse a cui hai accesso nell'account IBM Cloud corrente verranno elencati nell'elenco a discesa _Gruppi di risorse_, il che significa che devi disporre dell'autorizzazione per accedere ad almeno un gruppo di risorse nell'account per poter creare un CFEE.
    * Seleziona l'**Area geografica** e l'**Ubicazione** in cui deve essere eseguito il provisioning dell'istanza del servizio. Vedi l'elenco di [data center e ubicazioni di provisioning disponibili](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") in base all'area geografica per CFEE e i servizi di supporto. 

4. Viene eseguito il provisioning delle istanze CFEE su un cluster Kubernetes. Viene eseguito il provisioning delle celle Cloud Foundry all'interno delle zone di lavoro nel cluster Kuberentes. Puoi configurare l'ubicazione, l'hardware e la crittografia del cluster:
    * Seleziona l'isolamento hardware per il cluster Kubernetes:   
      * _Condiviso virtuale_: le risorse dell'infrastruttura nel cluster, ad esempio l'hypervisor e l'hardware fisico, vengono distribuite tra te e gli altri clienti IBM, ma ogni nodo di lavoro è un tuo singolo tenant.
      * _Dedicato virtuale_: i nodi di lavoro nel cluster sono ospitati sull'infrastruttura dedicata al tuo account.
    * I dati nel cluster sono crittografati per impostazione predefinita. Hai la possibilità di disattivare la _Crittografa disco locale_.
    * Seleziona l'**Area geografica** e la **Regione** in cui sarà eseguito il provisioning del cluster Kubernetes.
    * Seleziona le **Zone** in cui saranno distribuiti i nodi di lavoro Kubernetes. Hai la possibilità di eseguire il provisioning dei nodi di lavoro nella stessa zona (**Zona singola**) o in più zone (**Multizona**).  **Tieni presente** che la creazione di un CFEE multizona richiede lo [Spanning della VLAN](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning), che è supportato anche quando l'account {{site.data.keyword.Bluemix_notm}} è [abilitato VRF](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).
    
    Le VLAN disponibili vengono automaticamente richiamate per le zone selezionate. Se non è disponibile alcuna VLAN, saranno create automaticamente.
    
    **Nota: provisioning su una rete isolata:** puoi selezionare le VLAN in una rete isolata. Quando l'istanza CFEE viene creata in una rete isolata, le politiche nella rete isolata (ad es. le politiche calico o le regole VRA) devono consentire TUTTO l'accesso in uscita dall'istanza CFEE in modo che venga correttamente eseguito il provisioning del CFEE. Dopo aver creato il CFEE, possono essere ripristinate le limitazioni dell'accesso in uscita, ad eccezione dell'accesso in uscita ad alcuni servizi e microservizi in IBM Cloud.  Per ulteriori informazioni, vedi la documentazione [Utilizzo di una rete isolata](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network).
    
    Dopo aver creato il CFEE, verrà visualizzato il cluster Kubernetes in cui è stato eseguito il provisioning dell'ambiente, (come qualsiasi altra risorsa nel tuo account IBM Cloud) nel [dashboard](https://https://cloud.ibm.com/catalog/dashboard/apps/) {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi la [documentazione del servizio Kubernetes](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov).

5.  Configura la capacità del CFEE:
    * Seleziona il **Numero di celle** per il CFEE. Queste sono le celle dell'applicazione che ospiteranno le applicazioni distribuite nel CFEE.  
    * Seleziona la **Dimensione del nodo**, che determina la capacità delle celle Cloud Foundry (CPU e memoria).
    
    Oltre alle celle dell'applicazione che hai precedentemente specificato, vengono create e riservate ulteriori _celle del piano di controllo_ per l'operatività e il controllo della piattaforma Cloud Foundry nel tuo CFEE. 

    **Nota:** ti consigliamo che lo spanning della VLAN sia abilitato se viene eseguito il provisioning dei nodi di lavoro nel cluster Kubernetes su sottoreti diverse.  I nodi di lavoro su sottoreti differenti potrebbero impedire l'interconnettività se lo spanning della VLAN è disabilitato.  Per ulteriori informazioni, vedi la documentazione dello [spanning della VLAN](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning).

6.  Nei campi **Compose for PostgreSQL**, seleziona una delle organizzazioni pubbliche e seleziona quindi uno degli spazi disponibili in tale organizzazione. Verrà eseguito il provisioning dell'istanza di Compose for PostgreSQL nello spazio selezionato. Il servizio Compose for PostgreSQL è una dipendenza obbligatoria del servizio CFEE.

    **Nota:** in _Compose for PostgreSQL_ solo le organizzazioni nell'ubicazione in cui intendi eseguire il provisioning dell'istanza CFEE (passo 4 in alto) e a cui hai accesso sono disponibili per la selezione.  All'interno di una specifica organizzazione, sono disponibili per la selezione solo gli spazi a cui hai un accesso di _sviluppatore_. 

7.  Il **Riepilogo ordine** sul lato destro della pagina riflette il costo dell'istanza CFEE e dei servizi ausiliari insieme al totale mensile stimato.

8.  Fai clic su **Crea**, che apre il dashboard dell'ambiente e indica lo stato e l'avanzamento della creazione.

**Nota:** una volta avviato il processo di creazione, viene visualizzata una riga tabella per il CFEE nel dashboard {{site.data.keyword.Bluemix_notm}}, nell'_Elenco risorse_ e nel [dashboard Ambienti Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments).  Lo stato nella riga tabella indica quando è completata la creazione.

Il processo automatizzato che crea l'ambiente distribuisce l'infrastruttura in un cluster Kubernetes e la configura per renderla pronta per l'uso. Il processo dura 90 - 120 minuti.

Dopo che il CFEE è stato creato, riceverai diverse email che confermano il provisioning del CFEE e dei servizi di supporto, nonché delle email che ti informano dello stato degli ordini corrispondenti.

Quando crei un'istanza CFEE, nello stesso account IBM Cloud vengono create tre istanze del servizio di supporto aggiuntive. Tali istanze del servizio di supporto prendono il nome da quello dell'istanza CFEE. Pertanto, la creazione di un CFEE determina la creazione di un totale di quattro istanze del servizio nell'account IBM Cloud:
* Istanza CFEE ("_cfeename_").
* Cluster Kubernetes ("_cfeename_-cluster"). Il cluster fornisce l'infrastruttura in cui viene eseguito il provisioning dell'istanza CFEE.
* Istanza Cloud Object Storage ("_cfeename_-cos"). L'istanza viene utilizzata per archiviare i dati generati durante la creazione dei contenitori dell'applicazione CFEE (ad esempio, pacchetti di applicazioni caricati, pacchetti di build ed eseguibili compilati).
* Istanza Compose for PostgreSQL ("_cfeename_-postgres"). L'istanza viene utilizzata per archiviare i dati Cloud Foundry nell'istanza CFEE (ad esempio controllo della distribuzione delle applicazioni e degli avvii e arresti degli eventi, conservazione dei record di connessioni di servizi, applicazioni, spazi, organizzazioni e appartenenze degli utenti CFEE). 

## Il piano dell'anteprima tecnica Eirini
{: #eirini}

 Il piano dell'anteprima tecnica Eirini ti consente di esplorare un CFEE utilizzando Kubernetes nativo come programma di pianificazione del contenitore (invece di Diego). Il programma di pianificazione Kubernetes viene utilizzato nel CFEE per distribuire ed eseguire le applicazioni nel runtime dell'applicazione Cloud Foundry, aggiungere gli utenti, creare un'organizzazione e gli spazi, distribuire le applicazioni e associare tali applicazioni ai servizi. Vedi la documentazione del [progetto Eirini](https://www.cloudfoundry.org/project-eirini/) per ulteriori informazioni sul progetto incubatore Eirini dalla Cloud Foundry Foundation.
 Le seguenti limitazioni si applicano alle istanze CFEE create dal piano dell'anteprima tecnica Eirini:
 
* Kubernetes con `containerd` non è supportato. Sono supportate solo le versioni di Kuberetes che utilizzano Docker invece di `containerd`. La versione più recente di IBM Container Service (IKS) che supporta Docker è la v1.10.
* L'SSH di Cloud Foundry non è supportato.
* `cf push` delle immagini Docker non è supportato.
* La preparazione Eirini nativa Kubernetes non è supportata. Le istanze CFEE create dal piano dell'anteprima tecnica Eirini utilizzano Eirini per eseguire le applicazioni, ma non per prepararle. Le celle Diego vengono ancora utilizzate per la preparazione delle applicazioni.
* Il riavvio di istanze dell'applicazione specifiche (`cf restart-app-instance`) non è supportato.

 
