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

# Struktur der {{site.data.keyword.Bluemix_notm}}-Umgebung entwerfen
{: #bpimplementation}

Anstelle der traditionellen, streng definierten Entwicklungs-, Test- und Produktionsmethodik haben Sie die Möglichkeit, eine Umgebung zu implementieren, in der Entwickler und Tester mit anderen Teammitgliedern zusammenarbeiten können. Wenn Sie die Art und Weise gestalten, in der Sie Ihre Anwendungen entwickeln und liefern möchten, erstellen Sie {{site.data.keyword.Bluemix}}-Bereiche, um diese Methodik umzusetzen. Ziehen Sie in Betracht, beim Entwurf der {{site.data.keyword.Bluemix_notm}}-Umgebung nicht von der Organisationsebene aus abwärts, sondern von der Bereichsebene an aufwärts vorzugehen.

Berücksichtigen Sie die Größenordnung und den Geltungsbereich der Anwendungen, wenn Sie die Entwicklung und Bereitstellung planen. Ein {{site.data.keyword.Bluemix_notm}}-Bereich kann als Entwicklungsumgebung für eine oder mehrere Anwendungen verwendet werden, die eng miteinander verbunden oder zusammenhängend definiert sind. Abgesehen von einem Entwicklungsbereich können Sie zum Beispiel Bereiche für Komponententests, Leistungstests und Integrationstests erstellen. Außerdem können Bereiche für Build, Staging und Produktion eingesetzt werden. Jeder der Bereiche, die Sie erstellen, kann von verschiedenen Teammitgliedern innerhalb derselben Organisation gemeinsam genutzt werden.

Erstellen Sie separate Cloud Foundry-Organisationen, wenn Sie Mitarbeiter haben, die in verschiedenen Geschäftsbereichen tätig sind und sich die Tätigkeiten nicht überschneiden. Wenn zwei voneinander unabhängige Gruppen vorhanden sind, lassen sich durch die Erstellung je einer Organisation für jede Gruppe klare Abgrenzungen für die Bereitstellung sowie für das Management von Teampartnern und Ressourcen definieren. Für die Kommunikation zwischen den Organisationen können Sie eine API definieren.

Cloud Foundry-Organisationen können so erstellt werden, dass sie nicht so sehr die Struktur innerhalb eines Unternehmens als viel mehr die gewünschten Arbeitsweisen abbilden. Unternehmensorganisationen können sich im Lauf der Zeit ändern, während die Entwicklung und Verwaltung einer Anwendung davon meist völlig unabhängig fortgeführt wird. Entwerfen Sie die {{site.data.keyword.Bluemix_notm}}-Umgebung also im Hinblick auf die Lebensdauer der Anwendungen und nicht mit Blick auf die Organisationsstruktur Ihres Unternehmens.

Die iterative Entwicklung und Bereitstellung kann dazu führen, dass Anwendungen rasch sehr viel Platz benötigen. Der Entwurf für Ihren Bereitstellungsprozess muss sich schnell und einfach vertikal skalieren lassen. Sie möchten eine kontinuierliche Entwicklung mit hoher Bereitstellungsrate. Wenn Ihre Entwicklungs- und Produktionsbereiche in derselben {{site.data.keyword.Bluemix_notm}}-Organisation enthalten sind, haben sie Zugriff auf dieselben Ressourcen. Die Verwaltung unterschiedlicher Bereiche innerhalb einer Organisation verringert den Verwaltungsaufwand. Das Personal für Entwicklung, Tests und Betrieb kann problemlos zusammenarbeiten, wenn sie innerhalb derselben {{site.data.keyword.Bluemix_notm}}-Organisation arbeiten.

Implementieren Sie einen Benennungsstandard, um die Organisation und die Speicherbelegung klar zu kennzeichnen. Sie können zum Beispiel den Cloudtyp, die geografische Region, den Nutzungstyp (zum Beispiel dev, test oder prod), den Anwendungsnamen und die Versions- oder Revisionsnummer in die Namen einschließen. Die Organisationen und Bereiche sind dadurch leicht bei Verwaltung und Zugriff zu identifizieren.  

Die Anzahl der Bereiche kann sich aufgrund der iterativen Entwicklung rasch erhöhen. Sie können Bereiche innerhalb einer Organisation nach Bedarf definieren. Wenn Sie planen, viele Bereiche zu definieren, kann es sinnvoll sein, eine Anwendung zu erstellen, die bei der Verwaltung der Bereiche hilft. Überschreiten die Bereiche die Anzahl von 60, empfiehlt es sich vielleicht, eine weitere Organisation zu definieren.

Lassen Sie nur eine Person eine Organisation erstellen und verwalten, Bereiche definieren und Teammitgliedern Zugriffsberechtigungen erteilen. Eine zweite Person könnte dieselben Zugriffsberechtigungen erhalten, um die Umgebung zu verwalten, wenn der Organisationsmanager inaktiviert ist.  

Ermitteln Sie alle Personen, die Zugriff auf die einzelnen Bereiche und Organisationen benötigen. Legen Sie Rollen für diese Personen fest. Durch die Tätigkeitsrolle eines Teammitglieds wird die entsprechende Berechtigung festgelegt. Beispiel: Ein leitender Entwickler benötigt die Berechtigung zum Anzeigen und Aktualisieren der gesamten {{site.data.keyword.Bluemix_notm}}-Entwicklungsumgebung. Mitarbeitende Entwickler können hingegen einen eingeschränkten Zugriff auf Komponenten haben, die sie anzeigen und aktualisieren können.
