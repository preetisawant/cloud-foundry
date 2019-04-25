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

# Esercitazione introduttiva
{: #getting-started}

CFEE ({{site.data.keyword.cfee_full}}) è una piattaforma cloud per ospitare applicazioni e servizi nel cloud. {{site.data.keyword.cfee_full_notm}} rende più semplice ridimensionare le applicazioni man mano che il consumo cresce, semplificando il runtime, il middleware e l'infrastruttura in modo che ti puoi concentrare sullo sviluppo delle applicazioni.
{: shortdesc}

Questa esercitazione introduttiva mostra come creare un {{site.data.keyword.cfee_full_notm}}, aggiungere utenti, creare un'organizzazione e gli spazi, distribuire le applicazioni e associare queste applicazioni ai servizi.

**Nota:** la seguente procedura può essere applicata ai CFEE creati dal piano **Standard**.  Se questo CFEE è stato creato dal piano **Anteprima tecnica Eirini**, segui **solo i passi da 1 a 6** e il passo **11**. Le funzionalità descritte nei passi da 8 a 11 non sono supportate nel piano _Anteprima tecnica Eirini_.  Vedi [Introduzione all'anteprima tecnica Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).
Il piano _Anteprima tecnica Eirini_ ti consente di esplorare un CFEE utilizzando Kubernetes nativo come programma di pianificazione del contenitore (invece di Diego). Il programma di pianificazione Kubernetes viene utilizzato nel CFEE per distribuire ed eseguire le applicazioni nel runtime dell'applicazione Cloud Foundry, aggiungere gli utenti, creare un'organizzazione e gli spazi, distribuire le applicazioni e associare tali applicazioni ai servizi. 

## Passo 1: crea la tua istanza CFEE
{: #create-environment}

Puoi creare un'istanza di {{site.data.keyword.cfee_full_notm}} (CFEE) dal catalogo {{site.data.keyword.Bluemix_notm}}. Prima di creare l'istanza CFEE visita la documentazione [Crea l'ambiente](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment) per le istruzioni sulla preparazione del tuo account {{site.data.keyword.Bluemix_notm}}, la verifica delle autorizzazioni corrette e i passi per la creazione dell'istanza CFEE.


## Passo 2: crea organizzazioni e spazi
{: #create-orgsandspaces}

Dopo aver creato l'{{site.data.keyword.cfee_full_notm}}, consulta [Creazione di organizzazioni e spazi](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) per informazioni su come strutturare l'ambiente creando le organizzazioni e gli spazi. Le applicazioni in un {{site.data.keyword.cfee_full_notm}} vengono indirizzate all'interno di spazi specifici. A sua volta, uno spazio si trova all'interno di un'organizzazione specifica. I membri di un'organizzazione condividono un piano di quota, le applicazioni, le istanze dei servizi e i domini personalizzati.

Quando crei un'organizzazione assegni una quota ad essa.  La quota imposta i limiti sulle risorse (memoria, cpu, ecc.) disponibili per tale organizzazione. Puoi assegnare una quota differente in un momento successivo. Esiste una serie di quote preconfigurate disponibili in ogni CFEE, ma puoi anche creare le tue quote personalizzate nella pagina **Quote** dell'interfaccia utente CFEE.  Puoi rendere una quota personalizzata la quota _Predefinita_ richiamando l'azione _Copia come predefinita_ dal menu delle quote, che copia i valori della quota personalizzata in quella predefinita.

**Nota:** la pagina _Organizzazioni Cloud Foundry_ disponibile dal menu **_Gestisci > Account > Organizzazioni Cloud Foundry_** situata nella parte superiore dell'intestazione di IBM Cloud è destinata esclusivamente alle organizzazioni pubbliche di IBM Cloud, **non alle organizzazioni CFEE**. Le organizzazioni CFEE vengono gestite all'interno della pagina _Organizzazioni_ di un'istanza CFEE.  Apri l'interfaccia utente CFEE e fai clic sulla pagina **_Organizzazioni_** per creare e gestire le organizzazioni per tale CFEE.

## Passo 3: aggiungi utenti a organizzazioni e spazi
{: #add-users}

[Aggiungi gli utenti](https://console.bluemix.net/docs/cloud-foundry/add-users.html) a tali organizzazioni e spazi in specifiche assegnazioni di ruoli che controllano il loro livello di accesso.  Prima che gli utenti possano essere aggiunti come membri di organizzazioni e spazi in un CFEE, è necessario che tali utenti abbiano un accesso precedente all'istanza CFEE. Consulta [Autorizzazioni](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Passo 4: distribuisci e visualizza applicazioni
{: #deploy-apps}

Quando sei pronto, puoi [distribuire l'applicazione](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html) con l'interfaccia riga di comando (CLI) {{site.data.keyword.Bluemix_notm}}.  Visualizza l'elenco delle applicazioni distribuite nell'interfaccia utente, nel contesto di uno spazio CFEE specifico o globalmente in tutte le istanze CFEE.  Puoi anche avviare, arrestare o eliminare le applicazioni da quelle viste.

## Passo 5: crea o aggiungi istanze del servizio IBM Cloud a spazi CFEE
{: #service-instances}

[Crea i servizi](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) oppure [Aggiungi dei servizi esistenti](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) disponibili nell'account IBM Cloud.  Una volta che un'istanza del servizio è disponibile in uno spazio CFEE, puoi eseguirne il bind (associazione) alle applicazioni CFEE distribuite in tale spazio.

## Passo 6: associa mediante bind applicazioni a istanze del servizio
{: #bind-apps}

[Associa la tua applicazione](https://cloud.ibm.com/docs/cloud-foundry/binding.html) a un alias dell'istanza del servizio per poter utilizzare le funzioni del servizio.

Nel [dashboard Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") puoi vedere una vista consolidata di tutte le applicazioni e tutti i servizi, sia quelli *pubblici* che quelli *aziendali*.  Una volta all'interno del dashboard Cloud Foundry, fai clic su *Pubblico* nel riquadro di navigazione a sinistra per visualizzare le applicazioni e i servizi pubblici disponibili nell'account IBM Cloud.  Fai clic su *Azienda* per visualizzare tutti gli ambienti CFEE, le applicazioni distribuite negli spazi CFEE e i servizi disponibili agli spazi CFEE.
{:tip}

## Passo 7: abilita controllo e persistenza della registrazione (facoltativo)
{: #enable-auditingandlogging}

Abilita l'ambiente per [eventi di controllo](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) e [persistenza della registrazione](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging).

## Passo 8: Abilita gli strumenti di monitoraggio (facoltativo)
{: #enable-monitoring}

Il provisioning degli strumenti di monitoraggio non viene eseguito automaticamente sulle istanze CFEE v2.2.0 o successiva. Gli amministratori CFEE possono [abilitare gli strumenti di monitoraggio](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring) dopo che è stata creata l'istanza CFEE. Il set di strumenti di monitoraggio include Prometheus, Grafana e Alertmanager.

## Passo 9: crea e proteggi domini Cloud Foundry (facoltativo)
{: #create-domains}

Crea [domini](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains) per tutte le applicazioni nel CFEE (domini condivisi) o per una specifica organizzazione (domini privati) e proteggili con certificati SSL.

## Passo 10: configura l'ordine di priorità dei pacchetti di build Cloud Foundry
{: #create-buildpacks}

I pacchetti di build forniscono il supporto di runtime per le applicazioni distribuite in un ambiente Cloud Foundry, configurando automaticamente il runtime per un'applicazione e gestendone le dipendenze.  Cloud Foundry include una serie di pacchetti di build per i linguaggi e i framework comuni.  [Ulteriori informazioni](https://docs.cloudfoundry.org/buildpacks/) sui pacchetti di build Cloud Foundry.  

Puoi creare e caricare dei pacchetti di build personalizzati nella pagina **Pacchetti di build** dell'interfaccia utente CFEE. I pacchetti di build hanno una posizione ordinale nell'elenco di priorità.  Durante la preparazione di un'applicazione, Cloud Foundry verifica la compatibilità dell'applicazione con la serie di pacchetti di build a partire dalla posizione 1. I controlli di compatibilità procedono verso il basso nell'elenco di priorità finché non viene trovato un pacchetto di build compatibile. Assicurati che la sequenza di priorità della serie di pacchetti di build soddisfi le esigenze dei tuoi team di sviluppo.  Puoi modificare la posizione di un pacchetto di build nella sequenza di priorità trascinando e rilasciando il nome del pacchetto di build in una posizione diversa.  Puoi inoltre gestire i pacchetti di build tramite la [CLI Cloud Foundry](https://docs.cloudfoundry.org/adminguide/buildpacks.html).

## Passo 11: installa la console Stratos per gestire le applicazioni (facoltativo)
{: #install-stratos}

La console Stratos è uno strumento open source basato sul web per lavorare con Cloud Foundry. L'applicazione della console Stratos può essere facoltativamente installata e utilizzata in un ambiente CFEE specifico per gestirne le organizzazioni, gli spazi e le applicazioni.

Gli utenti con i ruoli di editor e amministratore IBM Cloud nell'istanza CFEE possono installare l'applicazione della console Stratos in tale istanza CFEE.

Per installare l'applicazione della console Stratos:

1. Apri l'istanza CFEE in cui vuoi installare la console Stratos.
2. Fai clic su **Installa Stratos Console** nella pagina della panoramica. Il pulsante è visibile solo agli utenti con autorizzazioni di amministratore o di editor per tale istanza CFEE.
3. Nella finestra di dialogo Installa Stratos Console, seleziona un'opzione di installazione. Puoi installare l'applicazione Stratos in una cella Cloud Foundry o nel cluster Kubernetes. Seleziona una versione della console Stratos e il numero di istanze dell'applicazione da installare. Se installi l'applicazione della console Stratos in una cella Cloud Foundry, ti vengono richiesti l'organizzazione e lo spazio in cui distribuire l'applicazione.
4. Fai clic su **Installa**.

Per installare l'applicazione sono necessari circa 5 minuti. Una volta completata l'installazione, viene visualizzato il pulsante **Stratos Console** al posto del pulsante _Installa Stratos Console_ nella pagina della panoramica. Il pulsante _Stratos Console_ avvia la console ed è disponibile per tutti gli utenti con accesso all'istanza CFEE. Le assegnazioni di appartenenza all'organizzazione e allo spazio possono limitare ciò che un utente può visualizzare e gestire nella console Stratos.

Per avviare la console Stratos:

1. Apri l'istanza CFEE in cui è stata installata la console Stratos.
2. Fai clic su **Stratos Console** nella pagina della panoramica.
3. La console Stratos viene aperta in una scheda del browser separata. Quando apri la console per la prima volta, ti viene richiesto di accettare due avvertenze consecutive per via dei certificati autofirmati.
4. Fai clic su **Login** per aprire la console. Non è richiesta alcuna credenziale poiché l'applicazione utilizza le tue credenziali {{site.data.keyword.Bluemix_notm}}.

## Risorse aggiuntive
{: #additional-resources}

Puoi eseguire alcune attività di gestione in un CFEE utilizzando i comandi CLI `ibmcloud CFEE`. I comandi ti consentono di ottenere informazioni su un'istanza CFEE, così come di gestire le tue organizzazioni e i tuoi spazi. Consulta i [Riferimenti ai comandi IBM Cloud CLI CFEE](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

Puoi trovare i video su discussioni e dimostrazioni approfondite su vari argomenti CFEE in [CFEE video playlist](https://ibm.biz/CFEE-Playlist){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

Le informazioni sull'API CFEE sono disponibili nella [documentazione dell'API](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
