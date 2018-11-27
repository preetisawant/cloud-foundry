---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Controllo e registrazione 
{: #auditing-logging}

Le funzioni di controllo e registrazione in {{site.data.keyword.cfee_full}} (CFEE) consentono agli amministratori di controllare gli eventi che si verificano in un'istanza CFEE e agli sviluppatori di tenere traccia degli eventi di log generati dalle relative applicazioni Cloud Foundry.

Il controllo e la registrazione in CFEE sono supportati tramite l'integrazione con i servizi Log Analysis e Programma di traccia dell'attività di IBM Cloud.

## Controllo
{: #auditing}

Il controllo consente agli amministratori CFEE di tenere traccia delle attività controllabili di Cloud Foundry che si verificano in un'istanza CFEE.  Tali attività includono l'accesso, la creazione di organizzazioni e spazi, l'appartenenza dell'utente e le assegnazioni del ruolo, le distribuzioni dell'applicazione, i bind al servizio e la configurazione del dominio. Il controllo è supportato tramite l'integrazione con il servizio Programma di traccia dell'attività in IBM Cloud. Un'istanza del servizio Programma di traccia dell'attività selezionata dall'amministratore CFEE viene configurata automaticamente per ricevere eventi che rappresentano le azioni eseguite all'interno del Cloud Foundry e sul piano di controllo CFEE.  L'utente può visualizzare e gestire quegli eventi nell'interfaccia utente dell'istanza del servizio Programma di traccia dell'attività.

Per abilitare il controllo di un'istanza CFEE:

1. Apri un'interfaccia utente CFEE e nella voce **Operations > Auditing** nel pannello di navigazione a sinistra apri la pagina Logging.
2. Fai clic su **Enable auditing** e seleziona una delle **Activity Tracker instances** disponibili nell'account IBM Cloud.  Se non sono disponibili istanze, l'utente visualizzerà un'opzione per creare una nuova istanza del Programma di traccia dell'attività nel catalogo IBM Cloud.
3.  Una volta che la persistenza della registrazione viene abilitata, i dettagli della configurazione vengono visualizzati nella pagina. I dettagli includono lo stato della configurazione e un link all'istanza del servizio Programma di traccia dell'attività stessa, dove l'utente può visualizzare e gestire gli eventi di controllo.

Puoi disabilitare il controllo facendo clic su **Disable auditing**, che rimuoverà l'istanza del servizio del Programma di traccia dell'attività precedentemente aggiunta e configurata. Questa azione non elimina l'istanza del servizio del Programma di traccia dell'attività.

## Persistenza della registrazione
{: #logging}

La registrazione degli eventi Cloud Foundry è supportata tramite l'integrazione con il servizio Log Analysis in IBM Cloud. Un'istanza del servizio Log Analysis selezionata dall'amministratore CFEE viene configurata automaticamente per ricevere e conservare gli eventi di registrazione Cloud Foundry generati dall'istanza CFEE.  L'utente può visualizzare e gestire quegli eventi di registrazione nell'interfaccia utente dell'istanza del servizio Log Analysis.

Per abilitare la registrazione di un'istanza CFEE:

1. Assicurati di disporre di una [politica di accesso IAM](https://console.bluemix.net/iam/#/users) che ti assegna il ruolo di editor, operatore o amministratore per l'istanza del servizio Log Analysis in cui vuoi conservare gli eventi di registrazione.
2. Apri un'interfaccia utente CFEE e nella voce **Operations > Logging** nel pannello di navigazione a sinistra apri la pagina Logging.
3. Fai clic su **Enable persistence** e seleziona una delle **Log Analysis instances** disponibili nell'account IBM Cloud.  Se non sono disponibili istanze, l'utente visualizzerà un'opzione per creare un'istanza nel catalogo IBM Cloud.
4. Una volta che la persistenza della registrazione viene abilitata, i dettagli della configurazione vengono visualizzati nella pagina. I dettagli includono lo stato della configurazione e un link all'istanza del servizio Log Analysis stessa, dove è possibile visualizzare e gestire gli eventi di registrazione.

**Avvertenza:** l'abilitazione della persistenza della registrazione richiede un riavvio con interruzione del servizio delle celle e del piano di controllo di CFEE.  Durante il riavvio, tutte le funzionalità di gestione saranno disponibili, ma alcune applicazioni e servizi in esecuzione in questa istanza CFEE potrebbero non essere disponibili. Lo stato dei componenti CFEE sarà visualizzato nella pagina Health Check durante il riavvio. Il riavvio richiede circa 20 minuti. 

Puoi disabilitare la persistenza del log facendo clic su **Disable log persistence**, che rimuoverà l'istanza del servizio precedentemente aggiunta e configurata. Questa azione non eliminerà l'istanza del servizio Log Analysis.

**Nota:** quando disabiliti la persistenza del log, gli eventi di registrazione di Cloud Foundry sono ancora in fase di generazione, non vengono conservati al di fuori dell'istanza CFEE.
