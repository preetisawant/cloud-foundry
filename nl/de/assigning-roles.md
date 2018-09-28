---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Rollen zuweisen
{: #roles}

In einem {{site.data.keyword.Bluemix_notm}}-Konto können Teammitgliedern mehrere Rollen zugewiesen werden. Diese Rollen definieren die Berechtigungen der Benutzer im Hinblick auf die Verwaltung von Konto- und Organisationsressourcen: Sie können den Mitgliedern einer Organisation [Benutzerrollen](/docs/iam/users_roles.html#userroles) erteilen. Diese Rollen definieren die Zugriffsebene innerhalb der Organisation und beschränken den Zugriff von Benutzern auf einen Bereich und seine Ressourcen. Sie können Benutzern zum Beispiel unterschiedliche Berechtigungen für unterschiedliche Bereiche erteilen.

## Kontoeigner
{: #accountowner}

Der Kontoeigner ist unabhängig davon, ob die Architektur eine oder mehrere Organisationen umfasst, der Superuser der Cloudumgebung.

Zu den Kernaufgaben des Kontoeigners gehören die folgenden Tasks:

* Verwaltung der Ressourcen des globalen Kontos
* Erstellung von Organisationen
* Hinzufügen von Teammitgliedern zum Konto

Der Kontoeigner kann auch einen oder mehrere Benutzer als Manager einer Organisation hinzufügen, indem er diesen Benutzern die Rolle **Manager** zuweist. Ziehen Sie in Betracht, zwei Benutzer als Organisationsmanager hinzuzufügen. Der erste Benutzer ist der Hauptmanager der Organisation. Der zweite Benutzer fungiert als stellvertretender Manager, falls der Hauptmanager nicht verfügbar ist.

## Benutzerrollen
{: #userroles}

Benutzerrollen definieren die Berechtigungen, die Sie einem Teammitglied in einer Organisation zuweisen können, und die Zugriffsebene, über die ein Teammitglied innerhalb der Organisation und in den einzelnen Bereichen verfügt.

Definieren Sie in einer Architektur mit mehreren Organisationen oder mit einer Einzelorganisation die Teammitglieder und die Berechtigungen, die jeder einzelne Benutzer zur Ausführung seiner Arbeit benötigt:

1. Geben Sie die Benutzergruppe an, für die Zugriff auf eine Organisation erforderlich ist.
2. Definieren Sie die Berechtigungen für jedes Teammitglied in der Organisation und in einem Bereich der Organisation.
3. Wählen Sie die Rolle aus, die einem Benutzer die erforderlichen Berechtigungen erteilt.

   * Organisationsmanager
   * Organisationsauditor
   * Abrechnungsmanager der Organisation
   * Bereichsmanager
   * Bereichsentwickler
   * Bereichsauditor

### Organisationsmanager
{: #bporgmgr}

Ein Organisationsmanager ist unter anderem für Tasks wie die Erstellung von Bereichen, die Verteilung des Kontingents auf die Bereiche, die Einladung von Teammitgliedern, die optionale Erteilung besonderer Rollen sowie die Definition angepasster Domänen verantwortlich.

### Organisationsauditor
{: #bporgauditor}

Die Teammitglieder mit der Organisationsrolle **Auditor** können das Kontingent, die Ressourcennutzung und die Teammitglieder für alle Bereiche in einer Organisation überwachen. Die Auditoren können anschließend Berichte zur Organisationseffizienz erstellen und auf potenzielle Probleme hinweisen.

* Wenn Sie eine Architektur mit mehreren Organisationen einrichten, kann es sinnvoll sein, die Auditorrolle den gleichen Teammitgliedern für jede Organisation zu erteilen, die Teil des Kontos ist. Diese Teammitglieder können dann das Kontingent für alle Organisationen in Ihrer Cloudumgebung überwachen und sich einen umfassenden Überblick über das Konto verschaffen.
* Wenn Sie eine Architektur mit einer Einzelorganisation einrichten, erteilen Sie die Auditorrolle den Teammitgliedern, die für die Überwachung der Kontingentnutzung und der allgemeinen Effizienz der Organisation zuständig sind.

### Abrechnungsmanager der Organisation
{: #bporgbillingmgr}

Die Teammitglieder mit der Rolle eines **Abrechnungsmanagers** können die Kosten einer Organisation überwachen.

* Wenn Sie eine Architektur mit mehreren Organisationen einrichten, kann es sinnvoll sein, die Abrechnungsrolle der gleichen Gruppe von Teammitgliedern für jede Organisation zu erteilen, die Teil des Kontos ist. Diese Teammitglieder können dann die Kosten für jede Organisation überwachen und sich einen umfassenden Überblick über das Konto verschaffen.
* Geben Sie in einer Architektur mit einer Einzelorganisation die Benutzer an, die für die Kostenüberwachung zuständig sind.

### Bereichsmanager
{: #bpspacemgr}

Ein **Bereichsmanager** ist für alle Arbeiten zuständig, die innerhalb des Bereichs ausgeführt werden, den er verwaltet und steuert. Ein Bereichsmanager kann die folgenden Tasks ausführen:

* Überwachen des Kontingents, das dem Bereich zugeordnet ist.
* Anfordern weiterer Ressourcen vom Organisationsmanager.
* Benachrichtigen des Organisationsmanagers über Ressourcen, die nicht erforderlich sind.
* Hinzufügen von Teammitgliedern zum Bereich mit der **Entwicklerrolle**.
* Optional: Zuweisen der Rolle **Bereichsmanager** zu einem Teammitglied, sodass dieses als stellvertretender Bereichsmanager in Abwesenheit des Bereichsmanagers fungieren kann.

### Bereichsentwickler
{: #bpspacedev}

Ein Bereichsentwickler kann die folgenden Tasks ausführen:

* Verwalten von Cloud Foundry-Anwendungen
* Bereitstellen und Konfigurieren von {{site.data.keyword.Bluemix_notm}}-Services
* Zuordnen von Domänen zu Anwendungen

### Bereichsauditor
{: #bpspaceauditor}

Es kann sinnvoll sein, für jeden Bereich denselben Teammitgliedern die Rolle des **Bereichsauditors** mit der Rolle des **Organisationsauditors** zu erteilen. In Ihrem Unternehmen muss diese Rolle möglicherweise einer bestimmten Gruppe von Benutzern erteilt werden.

