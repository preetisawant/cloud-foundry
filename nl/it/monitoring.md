---

copyright:
  years: 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Monitoraggio 
{: #monitoring}

Il monitoraggio di un'istanza {{site.data.keyword.cfee_full}} e delle relative infrastrutture supportate è supportato da un insieme di strumenti open-source composto da Prometheus e Grafana.  La soluzione ti consente di analizzare, visualizzare e gestire gli avvisi per le metriche nell'ambiente Cloud Foundry.  Ci sono tre console web da cui si verifica il monitoraggio: una console Grafana, una console Prometheus e una console Prometheus Alert Manager.

A partire da CFEE v2.2.0, gli strumenti di monitoraggio non sono abilitati per impostazione predefinita quando viene creato un ambiente.  Gli amministratori possono abilitare il monitoraggio dopo la creazione dell'ambiente.  Nell'interfaccia utente CFEE, vai alla pagina _Monitoraggio_ nel pannello di navigazione di sinistra e fai clic su **Abilita**. L'abilitazione del monitoraggio esegue automaticamente il provisioning di ulteriori nodi di lavoro Kubernetes (nello stesso account IBM Cloud) e installa gli strumenti di monitoraggio in tali nodi di lavoro.

**Nota:** l'accesso alla funzionalità di monitoraggio in un'istanza {{site.data.keyword.cfee_full}} richiede un ruolo di _Amministratore_ o _Editor_ nel CFEE e un ruolo _Operatore_ nel cluster Kubernetes che supporta l'istanza CFEE (in aggiunta al ruolo _Visualizzatore_ nel gruppo di risorse in cui viene raggruppato il CFEE).  Il nome predefinito del cluster Kubernetes che supporta un'istanza CFEE è _`<CFEEname>`-cluster_. 

## Prometheus
{: #prometheus}

Prometheus è un toolkit open-source di monitoraggio e avviso di sistemi. Fin dalla sua istituzione nel 2012, molte aziende e organizzazioni hanno utilizzato Prometheus e il progetto ha una community di utenti e sviluppatori molto attiva. 
Si tratta di un progetto open source autonomo e gestito indipendentemente da qualsiasi azienda. Per sottolineare questo punto e per chiarire la struttura di governance del progetto, Prometheus si è unito alla Cloud Native Computing Foundation nel 2016 come secondo progetto ospitato, dopo Kubernetes. Per ulteriori informazioni, consulta la [Documentazione di Prometheus](https://prometheus.io/docs/introduction/overview/).

L'ecosistema Prometheus è costituito da più componenti, molti dei quali sono facoltativi:

* Il server Prometheus principale che conserva e archivia i dati delle serie temporali.</li>
* [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) per gestire gli avvisi.</li>
* Vari esportatori a scopo specifico, quali l'esportatore di nodi, l'esportatore di black box, ecc.</li>
* Un gateway push per supportare i lavori di breve durata.</li>

Prometheus raccoglie le metriche dai lavori strumentati, direttamente o tramite un gateway push intermediario per i lavori di breve durata. Archivia tutti gli esempi raccolti localmente ed esegue le regole su questi dati per aggregare e registrare nuove serie temporali da dati esistenti o per generare avvisi. 

## Grafana
{: #grafana}

Grafana è una piattaforma di analisi open-source per tutte le metriche raccolte da Prometheus. La versione Grafana distribuita sul tuo cluster è già configurata per utilizzare il database Prometheus sottostante. Contiene anche alcuni dashboard Grafana importanti.  Per ulteriori informazioni, consulta la [Documentazione di Grafana](http://docs.grafana.org/guides/getting_started/).

## Introduzione al monitoraggio
{: #gettingStarted_monitor}

I componenti Prometheus e Grafana che comprendono la soluzione di monitoraggio sono preinstallati nell'infrastruttura Kubernetes che supporta l'istanza CFEE.  Per accedere agli strumenti di monitoraggio devi inoltrare le porte dei server Prometheus, Prometheus AlertManager e Grafana.  Questa operazione viene eseguita tramite la CLI Kubernetes. 
Di seguito vengono riportate le istruzioni per l'installazione delle CLI richieste, l'inoltro delle porte del server e l'avvio delle console.

**Nota:** le seguenti istruzioni sono disponibili anche nell'interfaccia utente di {{site.data.keyword.cfee_full}}.  Apri l'interfaccia utente dell'istanza CFEE, fai clic su **Monitoraggio** nel riquadro di navigazione di sinistra e passa alla scheda **Accesso** per vedere le istruzioni visualizzate.

### Prerequisiti

1. Spunta [Politiche di accesso](https://console.bluemix.net/iam/#/users) per assicurarti di avere almeno un ruolo di visualizzatore nel cluster Kubernetes che supporta l'ambiente.
2. Installa la [CLI IBM Cloud](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
3. Installa la [CLI Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  Se hai una CLI Kubernetes esistente, ti consigliamo di installare la versione più recente.
4. Installa il plug-in del servizio contenitore:
```
    ibmcloud plugin install container-service -r Bluemix
```
 
### Personalizzazione della configurazione di Alertmanager

Alertmanager dispone di un file [configurazione Alertmanager](https://prometheus.io/docs/alerting/configuration/) predefinito che definisce le politiche per la gestione, il raggruppamento e l'instradamento delle notifiche degli avvisi Alertmanager. Puoi scaricare il file di configurazione predefinito e caricare una configurazione personalizzata nella scheda **Configurazione** della pagina _Monitoraggio_.
 
### Accedi al cluster Kubernetes

1. Accedi al tuo account di IBM Cloud:

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}
  
  Se hai un ID federato, utilizza __ibmcloud login -sso__ per accedere alla CLI di IBM Cloud.

2. Seleziona la regione del servizio IBM Cloud Container che vuoi utilizzare (ad esempio, us-south):

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}
    
3. Configura il contenuto del cluster nella tua CLI: 

  a. Richiama il comando per impostare la variabile di ambiente e scarica i file di configurazione Kubernetes:

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}
    
  b. Imposta la variabile di ambiente KUBECONFIG. Copia l'output dal comando precedente e incollalo nel tuo terminale. L'output del comando dovrebbe essere simile a quanto segue:
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### Inoltra le porte del server
4. Imposta l'inoltro della porta nel cluster Kubernetes per i pod che eseguono Prometheus, AlertManager e Grafana. In tal modo, ti sarà possibile ospitare le metriche di monitoraggio per il proxy sulla macchina locale (localhost):

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000 &''
  ```
  {: pre}
  
### Avvia le console di monitoraggio sul tuo proxy web locale

5. Avvia la console Grafana per visualizzare le analisi sulle metriche selezionate.  Esistono dashboard Grafana predefiniti inclusi nell'istanza CFEE. Questi dashboard predefiniti sono interattivi e ti forniscono una vista dell'infrastruttura utilizzata per ospitare l'istanza CFEE. (Cluster Kubernetes). Una volta avviata la console Grafana, fai clic sul pulsante **Home** nella parte superiore della console Grafana per selezionare uno dei dashboard pre-distribuiti (consulta il seguente elenco), che rappresenterà graficamente le metriche corrispondenti:

   Per CFEE v2.1.0 o precedenti esiste un utente `admin` predefinito in Grafana, la cui password predefinita è impostata su `admin`. Ti consigliamo di accedere con il nome utente e la password `admin/admin` e di modificarli con delle nuove credenziali. Per utenti CFEE v2.2.0 o successiva, gli utenti vengono autenticati automaticamente con le proprie credenziali ID IBM.

     [Avvia la console Grafana](https://localhost:3000)

   I seguenti dashboard predefiniti sono forniti con l'istanza CFEE e sono disponibili dall'elenco a discesa _Home_.

    Dashboard Cloud Foundry:
   - _CF: Cells Capacity_ 
        - Mostra lo stato generale delle celle Cloud Foundry in cui sono distribuite le applicazioni Cloud Foundry.
   - _CF: Diego Cell dashboard_ 
        - Mostra lo stato delle celle Cloud Foundry e dei componenti di Diego.
   - _CF: Router_ 
        - Mostra lo stato del router Cloud Foundry in esecuzione sul tuo ambiente CFEE.
  
   I dashboard per l'infrastruttura Kubernetes che supporta l'ambiente CFEE:
   - _Deployment_ 
        - Mostra lo stato delle tue distribuzioni Kubernetes.
   - _Kubernetes Cluster Health_ 
        - Mostra l'integrità del cluster Kubernetes.
   - _Kubernetes Cluster Status_ 
        - Mostra lo stato del cluster Kubernetes.
   - _Kubernetes Resource Requests_ 
        - Mostra la CPU, la memoria e altri parametri utilizzati nel cluster Kubernetes.
   - _Pods_ 
        - Mostra i dettagli di ogni pod in esecuzione nel cluster Kubernetes.
   - _Replica Set_ 
        - Mostra lo stato delle serie di repliche Kubernetes.       
   - _Worker Nodes_ 
        - Mostra i dettagli di ogni nodo di lavoro del cluster Kubernetes.
   - _Worker Nodes Overview_ 
        - Mostra l'utilizzo di CPU e memoria dell'infrastruttura Kubernetes, insieme al suo traffico di rete.
        
6. Facoltativamente, puoi anche avviare la console Prometheus per visualizzare i dati non elaborati raccolti dai server Prometheus e Prometheus Alertmanager per gestire gli avvisi inviati dal server Prometheus:

     [Avvia il server Prometheus](https://localhost:9090)

     [Avvia il server Prometheus Alertmanager](https://localhost:9093)

