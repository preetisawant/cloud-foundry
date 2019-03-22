---

copyright:

  years: 2018
lastupdated: "2018-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Progetta la struttura del tuo IBM Cloud Foundry Enterprise Environment
{: #bpimplementation}

Invece della rigorosa metodologia di sviluppo, test e produzione tradizionale, puoi implementare un ambiente in cui sviluppatori e tester siano in grado di collaborare con gli altri membri del team. Se progetti il modo in cui vuoi sviluppare e distribuire le applicazioni, crea gli spazi per soddisfare tale metodologia. Anziché progettare il tuo ambiente dal livello dell'organizzazione a scendere, prova a progettare il tuo {{site.data.keyword.cfee_full}} (CFEE) dal livello dello spazio a salire.

Considera la dimensione e l'ambito delle applicazioni che intendi sviluppare e distribuire. Uno spazio Cloud Foundry può essere utilizzato come ambiente di sviluppo per una o più applicazioni strettamente connesse o definite. Oltre a uno spazio di sviluppo, ad esempio, puoi creare degli spazi per i test di unità, test delle prestazioni e test di integrazione. Inoltre, gli spazi possono essere definiti per le fasi di creazione, preparazione e produzione. Ogni spazio creato può esser condiviso con diversi membri del team all'interno della stessa organizzazione.

Crea delle organizzazioni Cloud Foundry separate per le persone che lavorano in diverse aree di business e in cui le loro attività non si sovrappongano. Se ci sono due gruppi indipendenti, la creazione di un'organizzazione per ognuno di questi definisce chiaramente i limiti per la distribuzione e gestione dei gruppi e delle risorse. Puoi definire un'API per la comunicazione tra le organizzazioni.

Le organizzazioni Cloud Foundry possono essere create per soddisfare il modo in cui vuoi lavorare anziché la struttura all'interno di un'azienda. Di norma, le organizzazioni aziendali possono cambiare, ma lo sviluppo e la manutenzione di un'applicazione continuano a prescindere. Progetta la tua istanza di {{site.data.keyword.cfee_full}} per tutta la durata delle applicazioni e non in base alla struttura dell'organizzazione aziendale.

Lo sviluppo e la distribuzione iterativa possono comportare una rapida espansione delle applicazioni. La progettazione del tuo processo di distribuzione deve potersi incrementare in modo rapido e veloce. Vuoi uno sviluppo continuo con un tasso di distribuzione elevato. Con gli spazi di sviluppo e produzione presenti nella stessa organizzazione CFEE, fornisci l'accesso alle stesse risorse. La gestione di spazi diversi all'interno di una singola organizzazione riduce i carichi di lavoro amministrativi. Il personale addetto allo sviluppo, al test e alle operazioni può collaborare facilmente se lavorano tutti all'interno della stessa organizzazione CFEE.

Implementa una denominazione standard per identificare chiaramente l'utilizzo dell'organizzazione e dello spazio. Ad esempio, potresti includere il tipo di cloud, la regione geografica, il tipo di utilizzo (ad esempio, sviluppo, test, produzione), il nome dell'applicazione e il numero di versione o revisione. Le organizzazioni e gli spazi possono essere facilmente identificati per scopi di amministrazione e accesso.  

Il numero di spazi può moltiplicarsi rapidamente per via dello sviluppo iterativo. All'interno di un'organizzazione, puoi definire il numero di spazi desiderato. Se intendi definire un numero elevato di spazi, potresti creare un'applicazione per facilitare la gestione di tali spazi. Se il numero di spazi supera sessanta, puoi valutare la possibilità di definire un'altra organizzazione.

Scegli una persona che crei e gestisca un'organizzazione, definisca gli spazi e conceda l'accesso ai membri del team. A una seconda persona può essere fornito lo stesso accesso per mantenere l'ambiente quando il gestore dell'organizzazione non è disponibile.  

Identifica tutte le persone che hanno bisogno dell'accesso a ogni spazio e organizzazione. Determina i loro ruoli. Il ruolo lavorativo di un membro del team ne determina l'autorità. Ad esempio, uno sviluppatore senior ha bisogno dell'autorità per visualizzare e aggiornare l'intero ambiente di sviluppo {{site.data.keyword.cfee_full}}. Tuttavia, uno sviluppatore junior è limitato su ciò che può visualizzare e aggiornare.
