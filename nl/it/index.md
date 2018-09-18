---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Informazioni su {{site.data.keyword.cfee_full_notm}}
{: #creating}

Con il {{site.data.keyword.cfee_full}} (CFEE), puoi avviare più piattaforme Cloud Foundry a livello aziendale e isolate su richiesta. Le istanze del servizio {{site.data.keyword.Bluemix_notm}} Foundry Enterprise vengono eseguite all'interno del tuo account in {{site.data.keyword.Bluemix_notm}}. L'ambiente viene distribuito su hardware isolato (cluster Kubernetes). Hai il controllo completo sull'ambiente, incluso il controllo dell'accesso, la gestione delle capacità, la gestione delle modifiche, il monitoraggio e i servizi.
{:shortdesc}

{{site.data.keyword.cfee_full}} è attualmente nella fase beta e stiamo cercando feedback! Per iniziare, crea la tua istanza di {{site.data.keyword.cfee_full}} all'indirizzo [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) e [richiedi l'accesso](http://ibm.biz/cfee-forum-signup) al [IBM CFEE Slack forum](https://ibm-cfee.slack.com) per condividere il feedback, fare domande e interagire con il team del prodotto.
{:tip}

Per il buon esito di un progetto, ti occorre del tempo per pianificare e progettare quali siano le risorse di cui hai bisogno e i requisiti della tua azienda. Per aiutarti a iniziare, considera le seguenti domande: 

* Quante e quali tipi di applicazioni verranno sviluppate? 
* A quali servizi devono accedere le applicazioni? 
* Chi collabora nel processo di sviluppo e quale è il suo ruolo? 
* Che grado di isolamento è richiesto per ogni fase del progetto? 
* La tua azienda fornisce le risorse dell'infrastruttura? 
* In che modo comunica la tua azienda? 
* Esiste una denominazione standard che puoi implementare per identificare chiaramente l'utilizzo dell'organizzazione e dello spazio? 

Quando devi decidere quale tipo di ambiente cloud ti serve, pianifica la struttura dei tuoi account, organizzazioni, spazi, risorse e membri del team. 

Un solo account {{site.data.keyword.Bluemix_notm}} è sufficiente per la maggior parte delle organizzazioni. Se la tua organizzazione ha più di un'area di business, puoi creare un account {{site.data.keyword.Bluemix_notm}} separato per ciascun dominio di business, ad esempio, una grande società bancaria potrebbe creare account separati per i settori del dettaglio e commerciale.

La seguente tabella fornisce un riepilogo di alcuni degli elementi chiave. 

| Elemento   | Descrizione |
|-----------|---------------|
| Account IBM Cloud | Le istanze CFEE vengono create in un account IBM Cloud specifico, rendendole disponibili agli utenti in tale account in base ai ruoli e alle politiche di accesso definite per tali utenti. |
|| L'account con cui vengono create le istanze CFEE deve essere un tipo di account Sottoscrizione o Pagamento a consumo (non un account di prova).  |
| CFEE | Il servizio IBM Cloud Foundry Enterprise Environment per ospitare le applicazioni. |
|| È disponibile nel catalogo di IBM Cloud. |
| Istanza CFEE | Un'istanza del servizio IBM Cloud Foundry Enterprise Environment creata in un account IBM Cloud da un utente con un ruolo di amministratore o di editor in tale account. |
|| Ci possono essere più istanze CFEE in un account IBM Cloud. |
|| Puoi avere una o più organizzazioni. |
| Organizzazione | Include uno o più spazi. |
|| Include uno o più gestori dell'organizzazione. |
|| Include uno o più membri del team. A ciascun membro del team può essere concesso uno o più ruoli. |
|| I costi di utilizzo, generati da un'applicazione distribuita all'interno di uno spazio, vengono riportati a livello dell'organizzazione. |
| Spazio | Include una o più risorse. |
|| Include una o più applicazioni. |
|| Include uno o più gestori dello spazio. |
|| Include uno o più membri del team. Ogni utente deve già essere un membro del team nell'organizzazione di appartenenza. A ciascun membro del team può essere concesso uno o più ruoli. |
| Membro del team | Può essere aggiunto a una o più organizzazioni e spazi in diversi account. |
|| Puoi assegnare più di un ruolo all'interno della stessa organizzazione, spazio o entrambi. |
| Alias del servizio | Un alias di un'istanza del servizio in IBM Cloud. |
|| Consente agli sviluppatori di assegnare le istanze del servizio esistenti disponibili nel proprio account IBM Cloud alle applicazioni distribuite in uno spazio all'interno di una CFEE.|
{:caption="Tabella 1. Descrizione degli elementi chiave" caption-side="top"}

