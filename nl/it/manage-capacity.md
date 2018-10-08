---

copyright:
  years: 2018
lastupdated: "2018-08-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Utilizzo delle risorse

Gli amministratori e gli sviluppatori possono vedere in che modo la capacità delle risorse (memoria e CPU) di un CFEE viene utilizzata dalle applicazioni e dalle celle. Per monitorare l'utilizzo delle risorse in un ambiente CFEE:

1. Vai al [dashboard Ambienti Cloud Foundry {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments) e apri {{site.data.keyword.cfee_full_notm}} in cui vuoi gestire l'utilizzo delle risorse.
2. Nell'interfaccia utente di {{site.data.keyword.cfee_full_notm}}, vai alla voce **Utilizzo risorsa** nel riquadro di navigazione di sinistra per aprire la pagina _Utilizzo risorsa_. Nella pagina _Utilizzo risorsa_ puoi andare alle voci secondarie _Applicazioni_ o _Celle_ per aprire le pagine corrispondenti.  Le informazioni visualizzate nelle pagine _Applicazioni_ e _Celle_ possono essere considerate come due modi per scomporre l'utilizzo delle risorse:
   * La pagina **Applicazioni** analizza l'utilizzo delle risorse da parte delle applicazioni aggregate nelle istanze.
   * La pagina **Celle** mostra l'utilizzo delle risorse delle istanze dell'applicazione in esecuzione su celle specifiche. Il modello di utilizzo delle risorse tra le celle può fornire informazioni approfondite sulla capacità e sulla distribuzione del carico.  Ad esempio, potrebbe aiutare a identificare i problemi con il bilanciamento del carico delle applicazioni (ad esempio, grandi differenze nelle risorse utilizzate da un'applicazione nelle celle) o l'utilizzo delle risorse che si avvicina alla capacità totale (ad esempio, grandi percentuali di utilizzo delle risorse in tutte le celle).

**Nota:** i dati sull'utilizzo delle risorse rappresentano l'utilizzo delle risorse durante l'ultimo ciclo di raccolta di 5 minuti. I dati di utilizzo delle risorse possono essere aggiornati facendo clic su **Aggiorna dati** all'inizio della pagina.

## Applicazioni
{: #usage_apps}

La pagina Applicazioni contiene due sezioni:
1. Grafici a barre orizzontali che mostrano l'utilizzo della memoria fisica e riservata
   * Memoria riservata e fisica utilizzata dalle **applicazioni selezionate** nella tabella riportata di seguito.
   * Memoria riservata e fisica utilizzata da **tutte le applicazioni** nell'istanza CFEE.
   * La memoria fisica utilizzata dal **sistema**, che include la memoria utilizzata dal piano di controllo Cloud Foundry e la memoria applicazione memorizzata in cache dal piano di controllo Cloud Foundry.
   * **Totale disponibile** di memoria riservata e fisica nell'istanza CFEE.
   
   **Nota:** quando le applicazioni riservano più memoria di quanta ne sia fisicamente disponibile, viene visualizzato un contorno rosso punteggiato nel grafico a barre della memoria riservata per rappresentare la quantità di memoria riservata in accesso dall'applicazione o dalle applicazioni selezionate.

   Per visualizzare la percentuale di memoria e CPU utilizzata da tutte le applicazioni o da quelle selezionate nella tabella, passa con il mouse sulla parte corrispondente del grafico.  Passando con il mouse sulla parte *tutte le applicazioni* del grafico, viene visualizzata la percentuale di memoria e CPU relativa al totale disponibile. Passando con il mouse sulla parte *applicazioni selezionate* del grafico, viene visualizzata la percentuale di memoria e CPU relativa al totale disponibile.

2. Una tabella che elenca tutte le applicazioni.  Ogni riga nella tabella visualizza le informazioni sulle risorse per tale applicazione.  L'espansione di una riga mostra le informazioni sull'utilizzo delle risorse per le varie istanze di tale applicazione.

  La prima colonna nella tabella è una casella di spunta che determina se l'applicazione corrispondente deve essere inclusa nella serie di *Applicazioni selezionate* da includere nel grafico nella parte superiore della pagina. Per includere (o escludere) un'applicazione nella serie selezionata, fai clic sulla casella di spunta corrispondente.  Quando un'applicazione viene selezionata o deselezionata per l'inclusione nella serie, il grafico viene aggiornato.  La legenda _Applicazioni selezionate_ a destra del grafico a barre indica (tra parentesi) il numero di applicazioni attualmente selezionate per l'inclusione nel grafico.

  Le seguenti informazioni vengono visualizzate come colonne nella tabella delle applicazioni:
   * **Nome applicazione**: il nome dell'istanza dell'applicazione o dell'applicazione. Se l'utente non dispone dell'autorizzazione per accedere all'applicazione, viene invece visualizzato il GUID dell'applicazione.
   * **Istanze**: per un'applicazione rappresenta il numero di istanze in esecuzione.  Per un'istanza dell'applicazione (mostrata al di sotto del nome dell'applicazione quando la riga dell'applicazione viene espansa) rappresenta il nome della cella in cui viene eseguita l'istanza dell'applicazione.
   * **Memoria totale-Fisica**: i MB di memoria fisica utilizzata da tutte le istanze di un'applicazione.  La memoria fisica utilizzata da un'applicazione è uguale alla somma della memoria fisica utilizzata da tutte le istanze dell'applicazione.
   * **Memoria totale-Riservata**: i MB di memoria riservata da tutte le istanze di un'applicazione.  La memoria riservata da un'applicazione è uguale alla somma della memoria riservata da tutte le istanze dell'applicazione.
   * **CPU media (% della cella)**: per le istanze dell'applicazione, la metrica rappresenta la CPU media **all'interno della cella in cui viene eseguita**.  Per un'applicazione, rappresenta la media dell'utilizzo della CPU tra le medie dell'istanza.
   * **CPU massima (% della cella)**: per le istanze dell'applicazione, la metrica rappresenta la CPU massima utilizzata da tale istanza **all'interno della cella in cui viene eseguita**.  Per un'applicazione, rappresenta il valore più alto dell'utilizzo della CPU massimo delle proprie istanze.
   * **CPU (% del sistema)**: la percentuale di CPU totale disponibile nella CFEE utilizzata da un'applicazione e dalle relative istanze.  La CPU utilizzata da un'applicazione è uguale alla somma della CPU utilizzata da tutte le istanze dell'applicazione.
   * **Richieste**: il numero di richieste a un'applicazione durante l'ultimo ciclo di raccolta dati (cinque minuti).
   * **Organizzazione**: l'organizzazione in cui viene distribuita l'applicazione. Se l'utente non è un membro dell'organizzazione, viene invece visualizzato il GUID dell'organizzazione.

Espandi una riga dell'applicazione nella tabella per visualizzare l'elenco delle istanze dell'applicazione e le relative metriche di utilizzo delle risorse corrispondenti.

### Filtro delle applicazioni
Puoi utilizzare il filtro del contenuto della tabella mediante gli elenchi a discesa dei filtri **Applicazioni** e **Organizzazioni** che si trovano sopra la tabella.

Inoltre, puoi utilizzare il campo di immissione del filtro sopra la tabella per visualizzare solo le applicazioni corrispondenti alla stringa che hai immesso nel campo del filtro.  Il filtro si riflette in entrambi, la tabella e il grafico sopra di essa.

**Nota:** i filtri funzionano in modo indipendente dalle righe della tabella selezionate (tramite la casella di spunta nella prima colonna della tabella) per l'inclusione nella serie di _Applicazioni selezionate_ incluse nel grafico sopra visualizzato. Ad esempio, se è presente un totale di dieci applicazioni nell'ambiente CFEE e cinque di esse sono selezionate per l'inclusione nel grafico, quando applichi un filtro che corrisponde a una sola istanza dell'applicazione, solo tale istanza dell'applicazione verrà visualizzata nella tabella.  Inoltre, la serie di _Applicazioni selezionate_ includerà solo tale applicazione corrispondente e il grafico verrà aggiornato di conseguenza.  Quando rimuovi il filtro, tutte e dieci le applicazioni verranno visualizzate di nuovo nella tabella e la serie di _Applicazioni selezionate_ verrà reimpostata per includere tutte le applicazioni.


## Celle
{: #usage_cells}

La pagina Celle contiene due sezioni:
1. Grafici a barre verticali che mostrano:
   * *Totale disponibile* di memoria e CPU disponibili nell'istanza CFEE.
   * Memoria e CPU utilizzate dalle **Istanze dell'applicazione selezionate** nell'istanza CFEE.
   * Memoria e CPU utilizzate da **Tutte le istanze dell'applicazione** nell'istanza CFEE.
   * Memoria e CPU utilizzate dal **Sistema** nella tabella riportata di seguito.  L'utilizzo del sistema rappresenta la risorsa utilizzata dal componente del servizio CFEE più la cache dell'applicazione.
   * Memoria totale e CPU disponibili nella cella.Il **Totale cella** è uguale al totale (memoria o CPU) disponibile nel nodo di lavoro Kubernetes (dove è eseguito il provisioning della cella) meno quanto utilizzato dal sistema.

   Per visualizzare la percentuale di memoria o CPU utilizzata da tutte le istanze dell'applicazione o da quelle selezionate nella tabella, passa con il mouse sulla parte corrispondente del grafico.  Passando con il mouse sulla barra del grafico viene visualizzata la memoria o la CPU assoluta disponibile, la memoria o la CPU utilizzata da tutte le applicazioni e la memoria o la CPU utilizzata da sistema+cache.  Mostra anche la percentuale di memoria o CPU utilizzata da tutte le applicazioni e da sistema+cache rispetto al totale disponibile.

2. Una tabella che elenca tutte le celle e le istanze delle applicazioni in esecuzione in esse.  Ogni riga nella tabella visualizza le informazioni sulle risorse per tale istanza dell'applicazione.

  La prima colonna nella tabella è una casella di spunta che determina se l'istanza dell'applicazione corrispondente deve essere inclusa nella serie di *Istanze dell'applicazione selezionate* da includere nel grafico nella parte superiore della pagina. Per includere (o escludere) un'istanza dell'applicazione nella serie selezionata, fai clic sulla casella di spunta corrispondente.  Quando un'istanza dell'applicazione viene selezionata o deselezionata per l'inclusione nella serie, il grafico viene aggiornato.

  Le seguenti informazioni vengono visualizzate come colonne nella tabella:
   * **Nome cella**: il nome della cella.
   * **Nome applicazione**: il nome dell'applicazione in esecuzione sulla cella. Se l'utente non dispone dell'autorizzazione per accedere all'applicazione, viene invece visualizzato il GUID dell'applicazione.
   * **Istanze**: il numero di istanze dell'applicazione in esecuzione sulla cella.
   * **Memoria-Fisica**: i MB di memoria fisica utilizzata dall'istanza dell'applicazione in esecuzione nella cella.
   * **Memoria-Riservata**: i MB di memoria riservata dall'istanza dell'applicazione in esecuzione nella cella.
   * **CPU (% )**: la percentuale di CPU totale disponibile nella CFEE utilizzata dall'istanza dell'applicazione in esecuzione sulla cella.

### Filtro delle celle e delle istanze dell'applicazione
Puoi utilizzare il filtro del contenuto della tabella tramite l'elenco a discesa del filtro **Celle** che si trova sopra la tabella e selezionando le celle da visualizzare nella tabella.

Inoltre, puoi utilizzare il campo di immissione del filtro sopra la tabella per visualizzare solo le istanze dell'applicazione corrispondenti alla stringa che hai immesso nel campo del filtro.  Il filtro si riflette in entrambi, la tabella e il grafico sopra di essa.

**Nota:** i filtri funzionano in modo indipendente dalle righe della tabella selezionate (tramite la casella di spunta nella prima colonna della tabella) per l'inclusione nella serie di _Istanze dell'applicazione selezionate_ incluse nel grafico sopra visualizzato. Ad esempio, se è presente un totale di dieci istanze dell'applicazione nell'ambiente CFEE e cinque di esse sono selezionate per l'inclusione nel grafico, quando applichi un filtro che corrisponde a una sola istanza dell'applicazione, solo tale istanza dell'applicazione verrà visualizzata nella tabella.  Inoltre, la serie di _Istanze dell'applicazione selezionate_ includerà solo tale istanza dell'applicazione e il grafico verrà aggiornato di conseguenza.  Quando rimuovi il filtro, tutte e dieci le istanze dell'applicazione verranno visualizzate di nuovo nella tabella e la serie di _Istanze dell'applicazione selezionate_ verrà reimpostata per includere tutte le istanze dell'applicazione.
