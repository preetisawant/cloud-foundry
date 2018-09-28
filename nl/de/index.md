---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Informationen zu {{site.data.keyword.cfee_full_notm}}
{: #creating}

Mit {{site.data.keyword.cfee_full}} (CFEE) können Sie mehrere isolierte und auf Unternehmen abgestimmte Cloud Foundry-Plattformen bedarfsgesteuert instanziieren. Instanzen des {{site.data.keyword.Bluemix_notm}} Foundry Enterprise Environment-Service werden im eigenen Konto in {{site.data.keyword.Bluemix_notm}} ausgeführt. Die Umgebung wird auf isolierter Hardware (Kubernetes-Cluster) bereitgestellt. Sie haben volle Kontrolle über die Umgebung, einschließlich Zugriffssteuerung, Kapazitätsmanagement, Änderungsmanagement, Überwachung und Services.{:shortdesc}

{{site.data.keyword.cfee_full}} befindet sich derzeit in der Beta-Phase und jedes Feedback ist eine wertvolle Hilfe. Erstellen Sie als Erstes eine eigene Instanz von {{site.data.keyword.cfee_full}} unter [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) und [fordern Sie Zugriff](http://ibm.biz/cfee-forum-signup) auf das [IBM CFEE Slack-Forum](https://ibm-cfee.slack.com) an, um Ihr Feedback zu teilen, Fragen zu stellen und mit dem Produktteam in Kontakt zu treten.{:tip}

Für den Erfolg eines Projekts ist es wichtig, sich Zeit zum Planen und Entwerfen zu nehmen, um die erforderlichen Ressourcen und die Anforderungen Ihres Unternehmens zu klären. Beginnen Sie für den Einstieg mit den folgenden Fragen:

* Wie viele und welche Art von Anwendungen entwickeln Sie?
* Auf welche Services müssen die Anwendungen zugreifen können?
* Welche Personen arbeiten am Entwicklungsprozess mit und welche Rolle spielen sie?
* Welcher Grad an Isolierung ist für jede Phase des Projekts erforderlich?
* Werden die Infrastrukturressourcen von Ihrem Unternehmen bereitgestellt?
* Wie kommuniziert Ihr Unternehmen?
* Gibt es einen Benennungsstandard, den Sie implementieren können, um die Organisation und die Speicherplatzbelegung eindeutig kenntlich zu machen?

Planen Sie bei der Entscheidung, welcher Typ von Cloudumgebung benötigt wird, die Struktur Ihrer Konten, Organisationen, Bereiche, Ressourcen und Teammitglieder.

Ein einziges {{site.data.keyword.Bluemix_notm}}-Konto ist für die meisten Organisationen ausreichend. Wenn eine Organisation über mehrere Geschäftsbereiche verfügt, können Sie für jede Geschäftsdomäne ein getrenntes {{site.data.keyword.Bluemix_notm}}-Konto erstellen; ein großes Bankunternehmen kann zum Beispiel separate Konten für den Einzelhandel und für den gewerblichen Sektor erstellen.

Die folgende Tabelle enthält eine Zusammenfassung einiger Schlüsselelemente.

| Element   | Beschreibung |
|-----------|---------------|
| IBM Cloud-Konto | CFEE-Instanzen werden unter einem bestimmten IBM Cloud-Konto erstellt, wodurch es Benutzern in diesem Konto entsprechend den Rollen und Zugriffsrichtlinien zur Verfügung steht, die für diese Benutzer definiert sind. |
|| Das Konto, unter dem die CFEE-Instanzen erstellt werden, muss ein nutzungsabhängiges Konto oder ein Abonnementkonto sein (kein Testkonto). |
| CFEE | IBM Cloud Foundry Enterprise Environment-Service für Hostanwendungen. |
|| Ist im IBM Cloud-Katalog verfügbar. |
| CFEE-Instanz | Eine Instanz des IBM Cloud Foundry Enterprise Environment-Service, die in einem IBM Cloud-Konto von einem Benutzer erstellt wurde, der in diesem Konto über eine Administrator- oder Bearbeiterrolle verfügt. |
|| In einem IBM Cloud-Konto können mehrere CFEE-Instanzen vorhanden sein. |
|| Es kann auch mindestens eine Organisation vorhanden sein. |
| Organisation | Besteht aus mindestens einem Bereich. |
|| Enthält mindestens einen Organisationsmanager. |
|| Enthält mindestens ein Teammitglied. Jedem Teammitglied kann mindestens eine Rolle erteilt werden. |
|| Die Nutzungsgebühren, die durch eine bereitgestellte Anwendung in einem Bereich generiert werden, werden auf Organisationsebene gemeldet. |
| Bereich | Besteht aus mindestens einer Ressource. |
|| Besteht aus mindestens einer Anwendung. |
|| Enthält mindestens einem Bereichsmanager. |
|| Enthält mindestens ein Teammitglied. Jeder Benutzer muss bereits ein Teammitglied in der Eignerorganisation sein. Jedem Teammitglied kann mindestens eine Rolle erteilt werden. |
| Teammitglied | Kann mindestens einer Organisation und mindestens einem Bereich über verschiedene Konten hinweg hinzugefügt werden. |
|| Kann mehrere Rollen innerhalb derselben Organisation und/oder desselben Bereichs innehaben. |
| Servicealias | Ein Alias einer Serviceinstanz in der IBM Cloud. |
|| Ermöglicht Entwicklern das Binden vorhandener Serviceinstanzen, die in ihrem IBM Cloud-Konto verfügbar sind, an Anwendungen, die in einem Bereich innerhalb einer CFEE-Umgebung bereitgestellt werden.|
{:caption="Tabelle 1. Beschreibung von Schlüsselelementen" caption-side="top"}

