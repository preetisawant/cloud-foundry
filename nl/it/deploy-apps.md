---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Distribuzione e visualizzazione delle applicazioni
{: #deploy_apps}

Puoi distribuire le applicazioni a {{site.data.keyword.Bluemix}} con l'interfaccia della riga di comando o con gli IDE (integrated development environment). Puoi anche utilizzare i manifest dell'applicazione per distribuire le applicazioni. Quando utilizzi un manifest dell'applicazione, riduci il numero di dettagli della distribuzione che devi specificare ogni volta che distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Distribuzione delle applicazioni con il comando Cloud Foundry
{: #dep_apps}

Scarica e installa l'interfaccia della riga di comando {{site.data.keyword.Bluemix}}. [Scarica la CLI {{site.data.keyword.Bluemix_notm}}](https://clis.ng.bluemix.net){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

Dopo aver installato l'interfaccia della riga di comando, effettua le seguenti operazioni:

1. Passa alla directory in cui si trova il codice. `cd <your_directory>`
2. Vai alla pagina {{site.data.keyword.cfee_full}} Overview e individua l'endpoint API dell'ambiente.
3. Nell'interfaccia riga di comando (CLI), imposta l'endpoint API sull'endpoint dell'ambiente:

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Accedi all'ambiente

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Se stai utilizzando un ID federato, utilizza l'opzione `-sso`.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **Nota**: devi aggiungere virgolette singole o doppie intorno a `username`, `org_name` e `space_name` se il valore include uno spazio, ad esempio `-o "my org"`.

5.  Da `<your_new_directory>`, ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando il comando `bluemix app push`. Per ulteriori informazioni relative al comando `cf app push`, vedi [Caricamento della tua applicazione](/docs/starters/upload_app.html).

  ```
  cf push <app_name>
  ```
  {: pre}

6.  Accedi alla tua applicazione selezionando ` https://<app_url>.<AppDomainName>`.

## Visualizzazione delle applicazioni distribuite nell'interfaccia utente
{: #view_apps}

Puoi visualizzare le applicazioni distribuite a CFEE nel contesto di uno spazio specifico o globalmente in tutte le istanze CFEE.

### Visualizzazione delle applicazioni distribuite in uno spazio CFEE specifico
{: #view_specific}

Per visualizzare le applicazioni distribuite in uno spazio specifico di un'istanza CFEE specifica:
1. Passa al [Dashboard {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) e apri il {{site.data.keyword.cfee_full_notm}} in cui vuoi creare le organizzazioni.
2. Nell'interfaccia utente di {{site.data.keyword.cfee_full_notm}}, vai alla voce **Organizations** nel pannello di navigazione per aprire la pagina _organizations_.
3. Vai alla scheda **Spaces** all'inizio della pagina.
4. Nella scheda __Spaces__, fai clic su uno spazio nella tabella per aprire la pagina dello spazio.
5. Nella pagina __Space__, vai alla scheda **Applications**.
6. La scheda __Applications_)_ mostra tutte le applicazioni distribuite in tale spazio.
Facoltativamente, puoi avviare, riavviare, arrestare o eliminare un'applicazione accedendo al menu all'estrema destra della riga che rappresenta l'applicazione.

Puoi anche espandere la riga di un'applicazione per visualizzare le istanze del servizio a cui è associata l'applicazione.

### Visualizzazione delle applicazioni distribuite su tutte le istanze CFEE
{: #view_global}

Per visualizzare tutte le applicazioni distribuite su tutte le istanze CFEE:
1. Fai clic sull'icona Menu ![Account Checking](img/HamburgerMenu.png "Acquisizione schermo che mostra l'icona menu") > **Cloud Foundry** per aprire il dashboard Cloud Foundry.
2. Fai clic su **Enterprise > Applications** nel pannello di navigazione di sinistra.
La tabella nella vista mostra le seguenti informazioni:

| Elemento   | Descrizione |
|-----------|---------------|
| Nome | Il nome dell'applicazione. |
| Istanze | Il numero di istanze dell'applicazione. |
| Ambiente | L'ambiente {{site.data.keyword.cfee_full}} in cui viene distribuita l'applicazione. |
| Organizzazione | L'organizzazione in cui è distribuita l'applicazione. |
| Spazio | L'organizzazione nell'istanza CFEE in cui si trova l'alias. |
| Memoria | La quantità di memoria utilizzata dall'applicazione. |
| Stato | Lo stato dell'applicazione. |
{:caption="Tabella 1. Descrizione degli elementi chiave" caption-side="top"}

Facoltativamente, puoi avviare, riavviare, arrestare o eliminare un'applicazione accedendo al menu all'estrema destra della riga che rappresenta l'applicazione.
Puoi fare clic su un qualsiasi ambiente, applicazione, organizzazione o spazio per passare alla pagina corrispondente nell'interfaccia utente CFEE.

In questa vista, disponi dell'opzione per raggruppare le applicazioni per organizzazione, spazio e/o nome dell'applicazione.  Questa funzione ti consente di unire in un'unica entità le applicazioni che possono avere nomi diversi e/o essere distribuite in organizzazioni o spazi CFEE differenti, ma che corrispondono alla stessa entità di applicazione logica.  Ad esempio, puoi avere applicazioni diverse che rappresentano i componenti di un progetto più ampio o che sono distribuite in diverse fasi di consegna (ad esempio, sviluppo, verifica, produzione) ma che vuoi visualizzare raggruppate come parte della stessa entità logica.

Per raggruppare le applicazioni, vai all'elenco a discesa **Group** situato nella parte superiore destra della pagina.
Quando raggruppi le applicazioni, ogni gruppo risultante è rappresentato da una sola voce nella tabella. Puoi espandere quella riga per visualizzare le applicazioni in quel gruppo.

In questa vista puoi eseguire le seguenti azioni:
* Ordinare gli elementi nella tabella per una qualsiasi delle proprietà visualizzate come colonne della tabella.
* Eseguire il bind delle applicazioni a un alias specifico accedendo al menu di overflow dell'alias ubicato all'estrema destra della riga.
* Espandere un alias (riga) per visualizzare tutte le applicazioni associate a tale alias.
* Avviare, arrestare le applicazioni accedendo al menu di overflow dell'applicazione dell'alias ubicato all'estrema destra della riga.
* Passare ad un CFEE, a un'organizzazione CFEE o a uno spazio CFEE facendo clic sul collegamento al corrispondente CFEE, organizzazione o spazio.

## Manifest dell'applicazione
{: #appmanifest}

I manifest dell'applicazione includono le opzioni che vengono applicate al comando `cf push`. Puoi utilizzare un manifest dell'applicazione per ridurre il numero di dettagli di distribuzione che devi specificare ogni volta che distribuisci un'applicazione in {{site.data.keyword.Bluemix_notm}}.

Nei manifest dell'applicazione, puoi specificare opzioni quali il numero di istanze dell'applicazione da creare, la quantità di memoria e la quota di disco da assegnare e altre variabili di ambiente. Inoltre, puoi utilizzare i manifest dell'applicazione per automatizzare le distribuzioni dell'applicazione. Il nome predefinito di un file manifest è `manifest.yml`.

### Opzioni supportate nel file manifest

La seguente tabella mostra le opzioni supportate che puoi utilizzare in un file manifest dell'applicazione. Se scegli di utilizzare un nome file diverso da `manifest.yml`, devi utilizzare l'opzione **-f** con il comando `cf push`.
Nel seguente esempio, `appManifest.yml` è il nome file:

```
cf push -f appManifest.yml
```

| Opzioni | Descrizione | Utilizzo o esempio |
|:----------|:--------------|:---------------|
| **buildpack** | L'URL o il nome del pacchetto di build personalizzato. | `buildpack:` *buildpack_URL* |
| **disk_quota** | La quota di disco assegnata per un'applicazione. Il valore predefinito è 1 G.| `disk_quota: 500M` |
| **domain** | Il nome dominio dell'applicazione in {{site.data.keyword.Bluemix_notm}}.| `domain:` ng.bluemix.net |
| **host** | Il nome host dell'applicazione in {{site.data.keyword.Bluemix_notm}}. Questo valore deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.| `host:` *host_name* |
| **name** | Il nome applicazione in {{site.data.keyword.Bluemix_notm}}. Questo valore deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.| `name:` *appname* |
| **path** | L'ubicazione della tua applicazione. Questo valore può essere un percorso relativo o percorso assoluto.| `path:` *path_to_application* |
| **command** | Il comando di avvio personalizzato per la tua applicazione o il comando per eseguire i file di script.| `command:` *custom_command* `command:` *bash ./run.sh* |
| **memory** | La quantità di memoria da assegnare per l'applicazione. Il valore predefinito è 1G.| `memory: 512M` |
| **instances** | Il numero di istanze da creare per la tua applicazione.| `instances: 2` |
| **timeout** | La quantità massima di tempo (in secondi) impiegata per l'avvio dell'applicazione. Il valore predefinito è 60 secondi.| `timeout: 80` |
| **no-route** | Un valore booleano che impedisce l'assegnazione di una rotta all'applicazione se l'applicazione è solo in esecuzione in background. Il valore predefinito è **false**.| `no-route: true` |
| **random-route** | Un valore booleano per assegnare una rotta casuale all'applicazione. Il valore predefinito è **false**.| `random-route: true` |
| **services** | I servizi di cui eseguire il bind all'applicazione.| `services: - mysql_maptest` |
| **env** | Le variabili di ambiente personalizzate per l'applicazione.| `env: DEV_ENV: production` |
{: caption="Tabella 2. Opzioni supportate nel file YAML manifest" caption-side="top"}

### Un file manifest.yml di esempio
{: #sample}

Il seguente esempio mostra un file manifest per un'applicazione Node.js che utilizza il pacchetto di build Node.js community integrato in {{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
