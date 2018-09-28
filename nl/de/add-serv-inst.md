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

# Serviceinstanzen erstellen und anzeigen
{: #creating-services}

Anwendungen, die in {{site.data.keyword.cfee_full_notm}} bereitgestellt werden, können an zwei Typen von Serviceinstanzen gebunden werden:
1. Serviceinstanzen, die von einem lokalen Cloud Foundry-Service-Broker verwaltet werden (lokal für die CFEE-Umgebung). Diese können wiederum zwei Typen aufweisen:
   *  1a. Eine Instanz eines Serviceangebots, das im Cloud Foundry-Marktplatz der aktuellen {{site.data.keyword.cfee_full_notm}}-Instanz erstellt wurde. Für diesen Serviceinstanztyp muss ein registrierter Service-Broker in der Umgebung verfügbar sein. Von einem Service-Broker wird ein Katalog mit Serviceangeboten und -plänen angezeigt; außerdem ermöglicht er es, Instanzen dieser Serviceangebote zu erstellen, zu entfernen, zu binden und Bindungen zu ihnen aufzuheben. Weitere Informationen hierzu finden Sie unter [Service-Broker verwalten](https://docs.cloudfoundry.org/services/managing-service-brokers.html) in der Dokumentation zu Cloud Foundry.
   * 1b. Eine vom Benutzer bereitgestellte Serviceinstanz. Die Erstellung dieses Typs wird über die Befehlszeilenschnittstelle (CLI) unterstützt, aber nicht über die Benutzerschnittstelle. Dennoch werden vom Benutzer bereitgestellte Serviceinstanzen in der Benutzerschnittstelle aufgelistet.
2. Öffentliche Serviceinstanzen, die mithilfe des {{site.data.keyword.Bluemix}}-Katalogs erstellt werden und im {{site.data.keyword.Bluemix}}-Konto verfügbar sind. Öffentliche Serviceinstanzen, die im {{site.data.keyword.Bluemix}}-Konto verfügbar sind, sind ohne eine weitere Aktion nicht für CFEE-Umgebungen verfügbar. Damit eine öffentliche Serviceinstanz (im {{site.data.keyword.Bluemix}}-Konto verfügbar) für Bereiche in einer CFEE-Umgebung verfügbar ist, muss ein Aliasname für die Serviceinstanz im CFEE-Bereich erstellt werden. Der Aliasname fungiert als Verweis auf die tatsächliche öffentliche Serviceinstanz. Sobald der Aliasname für den Service in einem CFEE-Bereich erstellt wurde, kann er an Anwendungen in diesem CFEE-Bereich gebunden werden. Die Aliasnamenumsetzung für den Service ermöglicht Entwicklern das Nutzen des umfangreichen Katalogs der {{site.data.keyword.Bluemix}}-Services in den Anwendungen, die in CFEE-Umgebungen bereitgestellt werden.


## Aliasnamen für Services in einem CFEE-Bereich erstellen und anzeigen
{: #creating-services_inspace}

Ein Aliasname für eine vorhandene öffentliche Serviceinstanz, die in Ihrem IBM Cloud-Konto verfügbar ist, ermöglicht Ihnen das Binden dieser Serviceinstanz an Anwendungen, die in einem CFEE-Bereich bereitgestellt werden. Zum Erstellen eines Aliasnamens für eine vorhandene {{site.data.keyword.Bluemix_notm}}-Serviceinstanz ist der Benutzerzugriff auf die Instanz selbst erforderlich. Weitere Informationen zum Überprüfen Ihrer aktuellen Kontozugriffsrichtlinien finden Sie auf der Seite 'Identität & Zugang' im Menü **Verwalten > Benutzer** im {{site.data.keyword.Bluemix_notm}}-Header.

Gehen Sie wie folgt vor, um einen Aliasnamen für eine Serviceinstanz innerhalb eines Bereichs in einer CFEE-Umgebung zu erstellen:

1. Suchen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard nach der Cloud Foundry Enterprise Environment-Umgebung, in der die Anwendung gehostet wird.
2. Wechseln Sie im Navigationsbereich zu **Organisationen** und öffnen Sie die Organisation und den Bereich, in dem sich die Anwendung befindet.
3. Wechseln Sie zur Registerkarte **Bereiche** und suchen Sie den Bereich, in dem die Anwendung enthalten ist.
4. Wechseln Sie auf der Seite des Zielbereichs zur Registerkarte **Services** und klicken Sie auf **Service erstellen**. Daraufhin wird die Seite **Katalog** für {{site.data.keyword.cfee_full_notm}} geöffnet. Auf der Seite werden Serviceangebote aus zwei Quellen aufgelistet (siehe Spalte _Quelle_):
   * Angebote aus dem IBM Cloud-Katalog.
   * Angebote aus dem lokalen {{site.data.keyword.cfee_full_notm}}-Marktplatz.
5. Suchen Sie ein verfügbares Serviceangebot, das Sie instanziieren möchten, und wählen Sie es aus.
6. Fahren Sie abhängig von der Quelle des Serviceangebots (IBM Cloud oder lokale CFEE-Umgebung) mit einem der folgenden Schritte fort:
   * **Fahren fort**, auf der Seite zum Erstellen von IBM Cloud-Serviceangeboten den Namen der neuen Serviceinstanz, die Region, den Plan und die weiteren Eigenschaften bereitzustellen, die zum Erstellen des Service in IBM Cloud erforderlich sind. Sobald Sie auf *Erstellen* klicken, wird die Serviceinstanz in IBM Cloud erstellt. Außerdem wird ein Aliasname für die Serviceinstanz in {{site.data.keyword.cfee_full_notm}} erstellt. Der Aliasname steht zum Binden von Anwendungen in {{site.data.keyword.cfee_full_notm}} zur Verfügung.
   **Hinweis:** Wenn eine {{site.data.keyword.Bluemix_notm}}-Instanz auf diese Weise erstellt wird, wird zusätzlich zur Erstellung einer öffentlichen und für Benutzer über das IBM Cloud-Konto verfügbaren Instanz ein Aliasname für diesen Service in der {{site.data.keyword.cfee_full_notm}}-Umgebung erstellt, in der dieser erstellt wurde.
   * **Erstellen** Sie die Serviceinstanz im lokalen Cloud Foundry-Marktplatz. Daraufhin wird ein Dialog geöffnet, in dem Sie den Namen der neuen Serviceinstanz und des Plans angeben können. Sobald Sie auf *Erstellen* klicken, wird die Serviceinstanz in {{site.data.keyword.cfee_full_notm}} erstellt und zum Binden an Anwendungen in {{site.data.keyword.cfee_full_notm}} verfügbar.

Nach der Erstellung der Serviceinstanz wird die Serviceinstanz (falls sie im lokalen Cloud Foundry-Marktplatz erstellt wurde) oder der Aliasname (falls die Serviceinstanz über den IBM Cloud-Katalog erstellt wurde) in der Registerkarte **Services** aufgelistet.


## Servicealiasnamen in allen CFEE-Umgebungen im globalen Cloud Foundry-Dashboard erstellen und anzeigen
{: #creating-services_across}

Sie können eine konsolidierte Ansicht aller Serviceinstanzaliasnamen (für alle CFEE-Instanzen) im globalen Cloud Foundry-Dashboard anzeigen.

1. Klicken Sie auf das Menüsymbol ![Kontoüberprüfung](img/HamburgerMenu.png "Screenshot des Menüsymbols") > **Cloud Foundry**, um das Cloud Foundry-Dashboard zu öffnen.
2. Klicken Sie im linken Navigationsbereich auf **Unternehmen > Services**. In der Tabelle in der Ansicht werden die folgenden Informationen angezeigt:

| Element   | Beschreibung |
|-----------|---------------|
| Servicealias | Der Name des Serviceinstanzalias. |
| Serviceinstanz | Die öffentliche IBM Cloud-Serviceinstanz, mit deren Hilfe der Aliasname erstellt wird. |
| Angebot | Das Serviceangebot aus dem IBM Cloud-Katalog, von dem die Serviceinstanz erstellt wurde. |
| CFEE | Die {{site.data.keyword.cfee_full}}-Umgebung, in der sich der Alias befindet. |
| Organisation | Die Organisation in der CFEE-Instanz, in der sich der Alias befindet. |
| Bereich | Der Bereich in der Organisation in der CFEE-Instanz, in der sich der Alias befindet. |
{:caption="Tabelle 1. Beschreibung von Schlüsselelementen" caption-side="top"}

In dieser Ansicht können Sie die folgenden Aktionen ausführen:
* Elemente in der Tabelle nach einer der Eigenschaften sortieren, die als Tabellenspalten angezeigt werden.
* Anwendungen an einen bestimmten Alias durch Zugriff auf das Aliasüberlaufmenü des Aliasnamens binden, der sich in der Zeile ganz rechts befindet.
* Einen Alias (eine Zeile) erweitern, um alle Anwendungen anzuzeigen, an die der Aliasname gebunden ist.
* Anwendungen durch Zugriff auf das Anwendungsüberlaufmenü des Aliasnamens starten und stoppen, der sich in der Zeile ganz rechts befindet.
* Durch Klicken auf den Link zur entsprechenden CFEE-Instanz, CFEE-Organisation oder dem entsprechenden CFEE-Bereich zur CFEE-Instanz, zur CFEE-Organisation oder zu einem CFEE-Bereich navigieren.

Gehen Sie wie folgt vor, um einen Servicealias im globalen Cloud Foundry-Dashboard zu erstellen:
1. Klicken Sie ganz oben auf der Seite auf die Schaltfläche **Servicealias erstellen**. Daraufhin wird der Dialog _Servicealias erstellen_ geöffnet. In diesem Dialog werden alle öffentlichen Serviceinstanzen aufgelistet, die im aktuellen IBM Cloud-Konto verfügbar sind.
2. Wählen Sie eine der öffentlichen Serviceinstanzen aus.
3. Klicken Sie auf **Erstellen**. Nach der Erstellung wird der neue Aliasname der Serviceinstanz zur Liste hinzugefügt. Der Servicealias wird auch in der Liste der Services in dem CFEE-Bereich angezeigt, in dem er an Anwendungen in diesem Bereich gebunden werden kann (CFEE > Organisationen > Bereich > Services).


