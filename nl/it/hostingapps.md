---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Host delle applicazioni in {{site.data.keyword.Bluemix_notm}}
{: #hosting_apps}

Con {{site.data.keyword.Bluemix}}, puoi creare applicazioni e ospitare le tue applicazioni esistenti. Purché pronta per il cloud, puoi spostare la tua applicazione in {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.Bluemix_notm}} offre molti modi per eseguire le tue applicazioni, ad esempio Cloud Foundry, IBM Containers e Virtual Machines.

## Come far sì che le tue applicazioni siano pronte per il cloud
{: #cloud-readyapps}

Se per la tua applicazione vengono osservati tutti i seguenti principi, essa è pronta per il cloud e può essere migrata in {{site.data.keyword.Bluemix_notm}}. Se un principio viene violato nella tua applicazione, di solito puoi [modificare l'applicazione](../apps/cloud-ready.html) per far sì che rispetti tutti i principi.

## Migrazione delle tue applicazioni
{: #ht_hostapp}

Puoi migrare le tue applicazioni in {{site.data.keyword.Bluemix_notm}} in modo incrementale, invece di spostare completamente l'applicazione nell'ambiente cloud. Puoi migrare prima una parte della tua applicazione e connetterla al system of record o ai dati esistenti attraverso il servizio Cloud Integration.

Nelle tue applicazioni cloud, potresti dover accedere ai dati o ai servizi di backend, ad esempio un system of record. In {{site.data.keyword.Bluemix_notm}},
puoi utilizzare il servizio Secure Gateway per stabilire un tunnel protetto
tra un'organizzazione {{site.data.keyword.Bluemix_notm}}
e la rete backend aziendale. Il servizio consente alle applicazioni su {{site.data.keyword.Bluemix_notm}} di accedere ai dati e ai servizi della rete di back-end. Per i dettagli, vedi [Reaching enterprise backend with {{site.data.keyword.Bluemix_notm}} Secure Gateway via console ![Icona link esterno](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}.

Per distribuire la tua applicazione a {{site.data.keyword.Bluemix_notm}} come applicazione Cloud Foundry, seleziona un runtime dal catalogo {{site.data.keyword.Bluemix_notm}}. Il runtime contiene un'applicazione starter Hello World che puoi sostituire con la tua propria applicazione. Se non riesci a trovare uno starter con il runtime desiderato, puoi portare un pacchetto di build personalizzato compatibile con Cloud Foundry in {{site.data.keyword.Bluemix_notm}} utilizzando l'opzione –b con il comando cf push. Per i dettagli, vedi [Utilizzo dei pacchetti di build della community](byob.html).

Puoi usare i seguenti servizi e strumenti forniti da {{site.data.keyword.Bluemix_notm}}:

| Strumento | Metodo |
|:------|:--------|
| Interfaccia riga di comando Cloud Foundry (cf cli) | Gestisci il tuo codice sul client locale e utilizza l'interfaccia riga di comando Cloud Foundry per distribuire manualmente la tua applicazione a {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [Caricamento delle tue applicazioni](../starters/upload_app.html). |
| Eclipse | Gestisci il tuo codice in Eclipse e utilizza IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} per distribuire la tua applicazione. |
| Integrazione di Git | Gestisci il tuo codice su GitHub e integra Git
in {{site.data.keyword.Bluemix_notm}}. Puoi collaborare con altri sviluppatori. La tua applicazione viene distribuita automaticamente a {{site.data.keyword.Bluemix_notm}} quando esegui il commit delle modifiche nel codice. Non devi eseguire manualmente la distribuzione dell'applicazione. |
| {{site.data.keyword.Bluemix_notm}} DevOps
Delivery Pipeline | Gestisci il tuo codice sul repository DevOps GitHub e distribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando DevOps Delivery Pipeline. |
{: caption="Tabella 1. Strumenti {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Se la piattaforma Cloud Foundry non risponde ai requisiti della tua applicazione, puoi utilizzare un contenitore o una VM in cui il runtime sia impostato, configurato e gestito con più opzioni personalizzate.

## Sviluppo e distribuzione delle tue applicazioni utilizzando le toolchain in Continuous Delivery
{:ht_cd}

Aggiungi una [toolchain alla tua applicazione](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app) e quindi utilizza l'[IU della toolchain Continuous Delivery](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using) per sviluppare e distribuire la tua applicazione.

## Caricamento delle tue applicazioni attraverso la CLI cf
{: #ht_cfcli}

Puoi gestire il tuo codice sul client locale e utilizzare l'interfaccia riga di comando Cloud Foundry per caricare manualmente la tua applicazione in {{site.data.keyword.Bluemix_notm}}. Se modifichi il codice, devi distribuire di nuovo la tua applicazione a {{site.data.keyword.Bluemix_notm}} per eseguire il codice aggiornato.

Per effettuare la migrazione della tua applicazione, attieniti alla seguente procedura:

Installa l'interfaccia riga di comando Cloud Foundry. Assicurati
di usare la versione più recente dell'interfaccia riga di comando cf.
  1. Scarica il programma di installazione per il tuo sistema
operativo.
  2. Segui la procedura guidata di installazione della riga di comando.
  3. Utilizza il seguente comando per verificare la versione dell'interfaccia riga di comando cf: `cf -v`

Facoltativo: se desideri specificare e salvare i dettagli di distribuzione prima di distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}}, puoi aggiungere il manifest dell'applicazione utilizzando la seguente procedura:

  1. Passa alla directory di lavoro della tua applicazione e crea un file denominato manifest.yml, che è il nome predefinito.</li>
  2. Specifica i dettagli di distribuzione nel file manifest. Il seguente esempio mostra un file manifest per un'applicazione Java™.

  ```
  applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

Per ulteriori informazioni sulle opzioni supportate che puoi utilizzare in questo file, vedi [Manifest dell'applicazione](depapps.html#appmanifest).

### Distribuisci la tua applicazione

Puoi caricare la tua applicazione utilizzando il comando `cf push`.
  1. Connettiti ed accedi a {{site.data.keyword.Bluemix_notm}} eseguendo
il seguente comando. Quando richiesto, seleziona la tua organizzazione
e il tuo spazio.
  ```
  cf login -a https://api.ng.bluemix.net
  ```
  Se la tua organizzazione utilizza il Single Sign On, aggiugni l'indicatore `-sso`.

  2. Dalla directory della tua applicazione, immetti il comando cf push seguito dal nome dell'applicazione. Il nome dell'applicazione deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.

  ```
  cf push nomeapplicazione
  ```

  3. Facoltativo: se utilizzi un pacchetto di build esterno, devi utilizzare l'opzione -b con il comando cf push. Ad esempio:

  ```
  cf push nomeapplicazione -b buildpack_URL
  ```

  Per i dettagli, vedi [Utilizzo dei pacchetti di build della community](byob.html).

Facoltativo: se modifichi la tua applicazione, devi caricare queste modifiche immettendo di nuovo il comando `cf push command`. L'interfaccia riga di comando cf utilizza le tue opzioni precedenti e le tue risposte ai prompt per aggiornare con i nuovi bit di codice tutte le istanze dell'applicazione in esecuzione.

#### Note:

* Quando utilizzi il comando cf push, l'interfaccia riga di comando cf copia tutti i file e tutte le directory dalla tua directory corrente a {{site.data.keyword.Bluemix_notm}}. Assicurati di avere solo i file richiesti nella directory della tua applicazione.
* Assicurati che la tua organizzazione abbia memoria sufficiente per tutte le istanze della tua applicazione. Per visualizzare la quota di memoria per la tua organizzazione, utilizza cf org org_name.
* Per ulteriori informazioni su cf push, vedi [comandi cf](../cli/reference/cfcommands/index.html).

## Migrazione dei tuoi dati e utilizzo dei servizi
{: #ht_service}

Dopo aver caricato la tua applicazione in {{site.data.keyword.Bluemix_notm}}, seleziona il servizio a cui è connessa l'applicazione dal catalogo {{site.data.keyword.Bluemix_notm}}, crea un'istanza del servizio, esegui il bind dell'istanza all'applicazione e quindi riavvia l'applicazione.

La variabile di ambiente VCAP_SERVICES della tua applicazione è un oggetto JSON che contiene informazioni su come interagire con un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}. Tali informazioni includono il nome dell'istanza di servizio, le credenziali e
l'URL di connessione all'istanza di servizio.

Per eseguire il codice su {{site.data.keyword.Bluemix_notm}},
devi aggiungere la logica del codice per l'analisi della variabile VCAP_SERVICES,
al fine di ottenere informazioni sulla connessione al servizio. Modifica la tua applicazione per ottenere attraverso le variabili di ambiente la porta e l'host dell'istanza del servizio assegnati dinamicamente. Il seguente esempio mostra come ottenere le credenziali di un'istanza del servizio Postgre SQL in un'applicazione Ruby:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

Per garantire che la tua applicazione possa essere eseguita in un ambiente locale dopo aver modificato l'applicazione per {{site.data.keyword.Bluemix_notm}}, verifica che sia presente la variabile di ambiente VCAP_SERVICES, che viene impostata per tutte le applicazioni {{site.data.keyword.Bluemix_notm}} Cloud Foundry.


# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [Virtual Machine](/docs/virtualmachines/vm_index.html)
* [Introduzione a Delivery Pipeline](/docs/services/DeliveryPipeline/index.html)
* [Distribuzione di applicazioni con IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html)
* [The twelve-factor app ![Icona link esterno](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console ![Icona link esterno](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
