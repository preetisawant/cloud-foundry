---

copyright:

  years: 2015, 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Panoramica strutturale 
{: #patterns}

Per il buon esito di un progetto, ti occorre del tempo per pianificare e progettare quali siano le risorse di cui hai bisogno e i requisiti della tua azienda. Per aiutarti a iniziare, considera le seguenti domande:
{:shortdesc}

* Quante e quali tipi di applicazioni verranno sviluppate?
* A quali servizi devono accedere le applicazioni?
* Chi collabora nel processo di sviluppo e quale è il suo ruolo?
* Che grado di isolamento è richiesto per ogni fase del progetto?
* La tua azienda fornisce le risorse dell'infrastruttura?
* In che modo comunica la tua azienda?
* Esiste una denominazione standard che puoi implementare per identificare chiaramente l'utilizzo dell'organizzazione e dello spazio?

Quando devi decidere quale tipo di ambiente cloud ti serve, pianifica la struttura dei tuoi account, organizzazioni, spazi, risorse e membri del team.

Per la maggior parte delle aziende, un account {{site.data.keyword.Bluemix_notm}} è sufficiente. Per le aziende più grandi in cui c'è più di un'area di business, potresti voler un account {{site.data.keyword.Bluemix_notm}} separato per ogni dominio di business. Ad esempio, all'interno di una grande azienda bancaria potrebbero esserci account separati per i settori vendita al dettaglio e commerciale. 

La seguente tabella fornisce un riepilogo di alcuni degli elementi chiave.

| Elemento   | Descrizione |
|-----------|---------------|
|| Contiene una o più organizzazioni. Per creare più di un'organizzazione, devi disporre di un account con pagamento a consumo. |
|| Puoi essere proprietario di un solo account. |
|| Puoi aggiungere uno o più gestori dell'organizzazione per delegarne la gestione, che comprende le autorizzazioni di lettura e scrittura per le organizzazioni. |
|| Puoi essere un membro del team in organizzazioni e spazi di altri account {{site.data.keyword.Bluemix_notm}}. |
| Organizzazione | Contiene uno o più spazi. |
|| Contiene uno o più gestori organizzazione. |
|| Contiene uno o più membri del team. A ciascun membro del team può essere concesso uno o più ruoli. |
|| I costi di utilizzo, generati da un'applicazione distribuita all'interno di uno spazio, vengono riportati a livello dell'organizzazione. |
| Spazio   | Contiene una o più risorse. |
|| Contiene una o più applicazioni. |
|| Contiene uno o più gestori spazio. |
|| Contiene uno o più membri del team. Ogni utente deve già essere un membro del team nell'organizzazione di appartenenza. A ciascun membro del team può essere concesso uno o più ruoli. |
| Membro del team   | Può essere aggiunto a una o più organizzazioni e spazi in diversi account. |
|| Puoi assegnare più di un ruolo all'interno della stessa organizzazione, spazio o entrambi. |
{:caption="Tabella 1. Descrizione degli elementi chiave" caption-side="top"}

