---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Associazione delle applicazioni alle istanze dei servizi
{: #bind_services}

Per associare un'applicazione a un'istanza del servizio:

1. Nel tuo dashboard {{site.data.keyword.Bluemix}}, trova il Cloud Foundry Enterprise Environment che ospita la tua applicazione.
2. Vai a **Organizations** nel pannello di navigazione e apri l'organizzazione e lo spazio in cui si trova l'applicazione.
3. Passa alla scheda **Spaces** e individua lo spazio che contiene l'applicazione.
4. Nella pagina dello spazio di destinazione, vai alla scheda **Services**. 
5. Nella tabella **Service instances**, vai la menu Actions all'estrema destra della riga corrispondente all'istanza del servizio che vuoi associare e seleziona **Bind**.
6. Seleziona l'applicazione che vuoi associare all'istanza del servizio.

Per annullare l'associazione da un'istanza del servizio:

1. Nella scheda **Services** dello spazio, espandi l'istanza del servizio di destinazione per mostrare le applicazioni che sono associate ad essa.
2. Vai al menu Actions in una riga dell'applicazione e seleziona **Unbind service**.

Per ulteriori informazioni, consulta [{{site.data.keyword.cfee_full_notm}}](index.html) e la [documentazione Cloud Foundry](https://docs.cloudfoundry.org/adminguide/).
