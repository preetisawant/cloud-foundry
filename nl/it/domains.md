---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Gestione dei domini
{: #domains}

Ci sono due tipi di domini Cloud Foundry:
* Domini condivisi disponibili per qualsiasi applicazione in qualsiasi spazio all'interno di {{site.data.keyword.cfee_full_notm}}.  Per accedere ai domini condivisi vai alla pagina **Domains** nel pannello di navigazione a sinistra dell'IU (sotto *Operations*).
* Domini privati disponibili solo alle applicazioni e agli spazi all'interno di un'organizzazione specifica.  Per accedere ai domini all'interno di un'organizzazione, vai alla pagina **Organizations** nel pannello di navigazione a sinistra dell'IU, apri l'organizzazione e vai alla scheda **Domains**.

## Creazione ed eliminazione dei domini
{: #create-domains}

Per creare un dominio condiviso, vai a **Domains** nel pannello di navigazione di sinistra di {{site.data.keyword.cfee_full_notm}}.  

Per creare un dominio privato, vai alla pagina **Organizations** nel pannello di navigazione a sinistra dell'IU, apri l'organizzazione e vai alla scheda **Domains**.

Una volta nella pagina _Domains_ (per i domini condivisi) o nella scheda _Domains_ di un'organizzazione specifica (per i domini privati) fai clic su **Create domain** per creare un dominio e immettere un nome univoco.

**Nota:** i nomi di dominio devono essere univoci nell'ambito completo di {{site.data.keyword.cfee_full_notm}}.  Questo perché, un dominio privato non può prendere il nome di uno dei domini condivisi o privati all'interno di un dato {{site.data.keyword.cfee_full_notm}}

Puoi anche creare un dominio condiviso dalla CLI Cloud Foundry immettendo il seguente comando:
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
Puoi creare un dominio privato dalla CLI Cloud Foundry immettendo il seguente comando:
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**Nota:** i domini creati dalla CLI Cloud Foundry si rifletteranno nell'IU immediatamente ma potrebbe essere necessaria fino a 1 ora perché diventino effettivi.

Per eliminare un dominio, vai al menu ubicato all'estrema destra della riga della tabella corrispondente al dominio che vuoi eliminare e seleziona **Delete domain**.
  
Puoi anche eliminare un dominio condiviso dalla CLI Cloud Foundry immettendo il seguente comando:
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## Caricamento dei certificati SSL
 {: #upload-certificates}
 
Puoi caricare un certificato SSL per un dominio (condiviso o privato). Fai clic su **Upload** nella riga della tabella corrispondente al dominio a cui stai aggiungendo il certificato, seleziona il file contenente il certificato e quello contenente la chiave privata.
  
