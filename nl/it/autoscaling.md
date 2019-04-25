---

copyright:
  years: 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Ridimensionamento automatico delle applicazioni
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} dispone di un supporto di ridimensionamento automatico integrato per le applicazioni Cloud Foundry per modificare il numero di istanze dell'applicazione tramite  
  * Ridimensionamento dinamico basato sulle metriche delle prestazioni dell'applicazione.
  * Ridimensionamento pianificato basato sul tempo.

Questa funzionalità viene offerta in base al progetto open source Cloud Foundry [App-Autoscaler][autoscaler_project]. Per iniziare, fai riferimento alla [guida utente][autoscaler_user_guide]. 

## Gestione del ridimensionamento automatico tramite la CLI

Puoi utilizzare il plugin dell'interfaccia riga di comando App Autoscaler (anche noto come CLI AutoScaler) per gestire la politica, le metriche di query e la cronologia del ridimensionamento. 

### Installazione della CLI AutoScaler
Utilizza il seguente comando per installare l'`AutoScaler CLI` che è un plugin della CLI Cloud Foundry.  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

Lo stesso comando può essere utilizzato per aggiornare il plugin `AutoScaler CLI` alla versione più recente se si dispone di una precedente installazione. 

### Utilizzo della CLI AutoScaler

Se hai già eseguito l'accesso a un ambiente Cloud Foundry su {{site.data.keyword.Bluemix}} e disponi di applicazioni in esecuzione nel tuo spazio come descritto nella [guida di distribuzione delle applicazioni][deploy_app], utilizza la seguente procedura per creare una politica di ridimensionamento per la tua applicazione e le metriche di query e la cronologia di ridimensionamento. 

 *  (facoltativo) Conferma che l'endpoint API App-Autoscaler sia impostato correttamente per impostazione predefinita.  

    Se l'endpoint API Cloud Foundry viene presentato come `api.<DOMAIN>`, l'endpoint API App-Autoscaler dovrebbe essere `autoscaler.<DOMAIN>`.  
    Utilizza il seguente comando per controllare l'impostazione dell'endpoint API App-Autoscaler.

    ```
    cf asa
    ```
    {:codeblock} 

    Se l'endpoint API App-Autoscaler non è corretto, devi reimpostarlo con il comando:

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  Crea un file JSON della politica sulla tua macchina locale. 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    La precedente politica viene utilizzata per attivare il ridimensionamento in base all'utilizzo di memoria quando viene superata la soglia definita per almeno 120 secondi (`120    seconds`).  Fai riferimento alla [guida utente di Cloud Foundry App-Autoscaler][autoscaler_user_guide] su come creare la tua politica di ridimensionamento.

*  Collega la politica alla tua applicazione

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (facoltativo) Inoltre, puoi eseguire la query delle metriche aggregate più recenti della tua applicazione. App-Autoscaler supporta più [tipi di metrica][metric_type], ma possono essere richiamate solo le metriche che hai definito nella tua politica, ad es. `memoryutil` nel precedente esempio.  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (facoltativo) Utilizza il seguente comando per eseguire la query della cronologia di ridimensionamento:

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    Fai riferimento alla [guida plugin CLI Cloud Foundry App Autoscaler][autoscaler_cli] per ulteriori opzioni di utilizzo della riga di comando. 


## Gestione del ridimensionamento automatico tramite la console Stratos 

Oltre che con l'interfaccia riga di comando, puoi gestire le impostazioni di ridimensionamento automatico tramite la console Stratos. 

Se hai installato [stratos][stratos] su {{site.data.keyword.cfee_full}} (CFEE), vai alla scheda **"Auto scaling**" nel dashboard dell'applicazione per visualizzare una panoramica della politica di ridimensionamento automatico e gli eventi di ridimensionamento più recenti.
Fai clic su una delle icone in uno qualsiasi dei tile per avviare l'editor della politica e modificarla.

Se non è stata definita alcuna politica di ridimensionamento automatico, la pagina della panoramica non conterrà alcuna informazione.  Fai clic su **Create policy** per avviare l'editor della politica e creare una politica.

Ti consigliamo di utilizzare la [guida utente di Cloud Foundry App-Autoscaler][autoscaler_user_guide] per comprendere i concetti di base in modo da configurare correttamente una politica di ridimensionamento automatico. 

### Statistiche delle metriche

Una volta che hai definito una politica basata su uno o più tipi di metrica selezionati, puoi visualizzare i valori della metrica più recenti e la cronologia delle metriche negli ultimi 30 minuti. 

**Nota:** le metriche rappresentano i dati calcolati come media di tutte le istanze dell'applicazione, non i dati non elaborati da ogni istanza dell'applicazione.
    
### Cronologia del ridimensionamento

La scheda **History** nell'editor della politica, mostra le azioni di ridimensionamento effettuate sulla tua applicazione che sono state attivate dalla politica di ridimensionamento automatico. Vengono mostrati anche tutti i messaggi di errore risultanti da errori di ridimensionamento. Puoi eseguire la query della cronologia del ridimensionamento durante gli ultimi 30 giorni. 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]: https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
