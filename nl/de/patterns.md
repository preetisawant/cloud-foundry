---

copyright:

  years: 2015, 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Strukturelle Übersicht
{: #patterns}

Für den Erfolg eines Projekts ist es wichtig, sich Zeit zum Planen und Entwerfen zu nehmen, um die erforderlichen Ressourcen und die Anforderungen Ihres Unternehmens zu klären. Beginnen Sie zunächst mit den folgenden Fragen:
{:shortdesc}

* Wie viele und welche Art von Anwendungen entwickeln Sie?
* Auf welche Services müssen die Anwendungen zugreifen können?
* Welche Personen arbeiten am Entwicklungsprozess mit und welche Rolle spielen sie?
* Welcher Grad an Isolierung ist für jede Phase des Projekts erforderlich?
* Werden die Infrastrukturressourcen von Ihrem Unternehmen bereitgestellt?
* Wie kommuniziert Ihr Unternehmen?
* Gibt es einen Benennungsstandard, den Sie implementieren können, um die Organisation und die Speicherplatzbelegung eindeutig kenntlich zu machen?

Planen Sie bei der Entscheidung, welcher Cloudumgebungstyp benötigt wird, die Struktur Ihrer Konten, Organisationen, Bereiche, Ressourcen und Teammitglieder.

Für die meisten Unternehmen reicht ein einzelnes {{site.data.keyword.Bluemix_notm}}-Konto aus. Für größere Unternehmen mit mehreren Geschäftsbereichen kann sich ein separates {{site.data.keyword.Bluemix_notm}}-Konto für jeden Geschäftsbereich sinnvoll sein. In einem großen Finanzunternehmen kann es zum Beispiel separate Konten für den Einzelhandelssektor und den Großkundensektor geben.

Die folgende Tabelle enthält eine Zusammenfassung einiger Schlüsselelemente.

| Element   | Beschreibung |
|-----------|---------------|
|| Enthält mindestens eine Organisation. Sie müssen ein nutzungsabhängiges Konto haben, um mehr als eine Organisation erstellen zu können. |
|| Kann nur Eigner eines Kontos sein. |
|| Kann einen oder mehrere Organisationsmanager zur Delegierung des Organisationsmanagements hinzufügen, das Lese- und Schreibberechtigungen für die Organisationen umfasst. |
|| Kann ein Teammitglied in Organisationen und Bereichen in anderen {{site.data.keyword.Bluemix_notm}}-Konten sein. |
| Organisation   | Enthält mindestens einen Bereich. |
|| Enthält mindestens einen Organisationsmanager. |
|| Enthält mindestens ein Teammitglied. Jedem Teammitglied kann mindestens eine Rolle erteilt werden. |
|| Die Nutzungsgebühren, die durch eine bereitgestellte Anwendung in einem Bereich generiert werden, werden auf Organisationsebene gemeldet. |
| Bereich   | Enthält mindestens eine Ressource. |
|| Enthält mindestens eine App. |
|| Enthält mindestens einen Bereichsmanager. |
|| Enthält mindestens ein Teammitglied. Jeder Benutzer muss bereits ein Teammitglied in der Eignerorganisation sein. Jedem Teammitglied kann mindestens eine Rolle erteilt werden. |
| Teammitglied   | Kann mindestens einer Organisation und mindestens einem Bereich über verschiedene Konten hinweg hinzugefügt werden. |
|| Kann mehrere Rollen innerhalb derselben Organisation und/oder desselben Bereichs innehaben. |
{:caption="Tabelle 1. Beschreibung von Schlüsselelementen" caption-side="top"}

