---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo dei pacchetti di build della community
{: #using_buildpacks}

Se nel catalogo {{site.data.keyword.Bluemix}} non riesci a trovare uno starter che ti fornisca il runtime desiderato, puoi portare tu un pacchetto di build esterno in {{site.data.keyword.Bluemix_notm}}. Puoi specificare un pacchetto di build personalizzato compatibile con Cloud Foundry quando distribuisci la tua applicazione utilizzando il comando cf push.
{:shortdesc}

I pacchetti di build esterni sono forniti dalla community di Cloud Foundry
e puoi usarli come tuoi pacchetti di build. Prima di
distribuire la tua applicazione a {{site.data.keyword.Bluemix_notm}},
assicurati di installare l'interfaccia riga di comando cf.

**Nota:** i pacchetti di build esterni non sono forniti da IBM. Per assistenza, contatta la community di Cloud Foundry.

## Pacchetti di build della community integrati

In {{site.data.keyword.Bluemix_notm}},
puoi utilizzare i pacchetti di build integrati forniti dalla community di
Cloud Foundry. Per visualizzare i pacchetti di build della community integrati, esegui il comando `cf
buildpacks`:

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}


Per lo stesso runtime o framework, i pacchetti di build creati da IBM hanno la precedenza su quelli della community. Se vuoi usare il pacchetto di build della community per sovrascrivere quello creato da IBM, devi specificare il pacchetto di build utilizzando l'opzione -b con il comando cf push.
Ad esempio, puoi usare il pacchetto di build della community per le applicazioni Web Java™:

```
cf push app_name -b java_buildpack -p app_path
```
{:pre}

Puoi anche usare il pacchetto di build della community per le applicazioni Node.js:

```
cf push app_name -b nodejs_buildpack -p app_path
```
{:pre}

Per un runtime o un framework non supportato da pacchetti di build creati da IBM ma supportato da pacchetti di build della community integrati, non devi necessariamente utilizzare l'opzione -b con il comando cf push. Ad esempio, per le applicazioni Ruby, non ci sono pacchetti di build creati da IBM. Puoi usare il pacchetto di build della community integrato immettendo il
seguente comando:

```
cf push app_name -p app_path
```
{:pre}

## Pacchetti di build esterni

Puoi utilizzare pacchetti di build esterni o personalizzati in {{site.data.keyword.Bluemix_notm}}. Devi specificare l'URL del pacchetto di build con l'opzione -b e specificare lo stack con l'opzione `-s` nel comando **cf push**. Ad esempio, per utilizzare un pacchetto di build della community esterno per i file statici, esegui questo comando

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/staticfile-buildpack.git
```
{:pre}

Se non vuoi utilizzare il pacchetto di build della community integrato per le applicazioni Ruby, puoi utilizzare un pacchetto di build esterno immettendo il seguente comando:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/ruby-buildpack.git
```
{:pre}

Puoi anche utilizzare un pacchetto di build personalizzato per la tua applicazione. Ad esempio, per utilizzare un pacchetto di build PHP open source fornito dalla community di Cloud Foundry, quando distribuisci la tua applicazione PHP a Bluemix, immetti il seguente comando per specificare l'URL del repository Git del pacchetto di build:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/php-buildpack.git
```
{:pre}

È anche possibile modificare il file `manifest.yml` del tuo progetto per aggiungere una riga `buildpack`:

```
buildpack: https://github.com/cloudfoundry/python-buildpack.git
```
{:pre}


## Specifica della versione del pacchetto di build Java

Utilizza il comando `cf set-env`. Ad esempio, immetti il seguente comando per impostare la versione Java su 1.7.0:
```
cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &apos;{jre: { version: 1.7.0_+ }}&apos;
```
{:pre}

Quindi, per rendere effettive
le modifiche, prepara di nuovo la tua applicazione:

```
cf restage app_name
```
{:pre}

Utilizza il file `manifest.yml`. Puoi aggiungere la
variabile di ambiente e il valore che vuoi specificare direttamente
nel file. Per informazioni dettagliate, vedi [Variabili di ambiente](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block)
