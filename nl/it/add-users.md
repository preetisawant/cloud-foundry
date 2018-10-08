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

# Aggiunta di utenti a organizzazioni e spazi
{: #adding_users}

I membri di un'organizzazione con un ruolo di gestore possono aggiungere membri a tale organizzazione. Prima che gli utenti possano essere aggiunti a un'organizzazione, devono avere almeno il ruolo di visualizzatore sia per il servizio {{site.data.keyword.cfee_full}} che per il gruppo di risorse a cui appartiene l'istanza di {{site.data.keyword.cfee_full_notm}}. Queste autorizzazioni sono impostate nella pagina _Identity & Access_ in **Gestisci > Utenti** nell'intestazione {{site.data.keyword.Bluemix}}.

Per aggiungere gli utenti come membri di un'organizzazione in un'istanza {{site.data.keyword.cfee_full_notm}}:

1. Vai alla voce **Organizzazioni** nel riquadro di navigazione. Individua l'organizzazione a cui vuoi aggiungere un membro. Vai al menu _Azioni_ nella riga della tabella e seleziona **Aggiungi membro**. In alternativa, puoi fare clic sull'organizzazione per aprire la pagina dell'organizzazione, andare alla scheda **Membri** e fare clic su **Aggiungi membro**.
2. Nella finestra _Aggiungi membro_, trova l'utente, seleziona un **Ruolo organizzazione** e fai clic su **Aggiungi**.

**Nota:** se vuoi aggiungere un utente che è stato recentemente invitato nel tuo account {{site.data.keyword.Bluemix_notm}}, possono servire diversi minuti perché l'utente venga riconosciuto nella finestra in cui aggiungi gli utenti a un'organizzazione o a uno spazio. Se l'utente non viene riconosciuto quando immetti il nome utente, inserisci l'indirizzo email dell'utente e premi l'icona più (+) per aggiungere l'utente.

Solo i gestori dello spazio (o i gestori dell'organizzazione principale) possono aggiungere i membri a uno spazio. Per aggiungere gli utenti come membri di uno spazio in un'organizzazione in un'istanza di {{site.data.keyword.cfee_full_notm}}:

1. Vai alla voce **Organizzazioni** nel riquadro di navigazione, individua l'organizzazione in cui si trova lo spazio di destinazione e fai clic su di essa per aprire la pagina dell'organizzazione.
2. Nella pagina dell'organizzazione, vai alla scheda **Spazi**.
3. Individua lo spazio di destinazione nella tabella degli spazi, vai al menu _Azioni_ nella riga della tabella e seleziona **Aggiungi membro**. In alternativa, puoi fare clic sullo spazio di destinazione nella tabella per aprire la pagina dello spazio, quindi fai clic su **Aggiungi membro**.
4. Nella finestra _Aggiungi membro_, trova l'utente, seleziona un **Ruolo spazio** e fai clic su **Aggiungi**.

**Nota**: i gestori dell'organizzazione possono aggiungere i membri direttamente a uno spazio senza aggiungerli prima all'organizzazione principale. Quando un gestore dell'organizzazione aggiunge i membri a uno spazio, tali membri diventano anche membri dell'organizzazione principale.
