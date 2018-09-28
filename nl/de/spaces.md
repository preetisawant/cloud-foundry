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

# Bereiche festlegen
{: #determinespaces}

Innerhalb einer Organisation bieten Bereiche eine zusätzliche Abgrenzungs- und Abstraktionsebene.

Ein Bereich ist ein reservierter Teil in der Organisation, in dem Benutzer Apps und Services entwickeln und ausführen können. Sie können eine beliebige Anzahl von Bereichen in einer Organisation erstellen und die Benutzer steuern, die über Zugriff auf einen Bereich verfügen. Details hierzu finden Sie unter [Bereiche](/docs/account/orgs_spaces.html#orgsspacesusers).

Wenn Sie planen, viele Bereiche zu definieren, kann es sinnvoll sein, eine Anwendung zu erstellen, die Sie der Verwaltung der Bereiche unterstützt. Überschreiten die Bereiche die Anzahl von 60, empfiehlt es sich vielleicht, eine weitere Organisation zu definieren.

## Bereiche in einer Einzelorganisation und Bereiche in mehreren Organisationen
{: #spaceconsiderations}

Wenn Sie sich für eine Architektur mit Einzelorganisation entscheiden, wird die Abgrenzungs- und Abstraktionsebene durch die Bereiche bereitgestellt, die Sie innerhalb der Organisation definieren. Beachten Sie beim Definieren von Bereichen die folgenden Hinweise:

* Definieren Sie einen Bereich, um einen Service zu hosten, der nur eine einmalige Bereitstellung und Konfiguration in der Organisation erfordert.
* Definieren Sie Bereiche auf der Basis des Bereitstellungslebenszyklus. Beispiel: Sie können einen oder mehrere Bereiche für Anwendungen definieren, die entwickelt werden, einen oder mehrere Bereiche für Anwendungen, die in der Testphase sind, und einen oder mehrere Bereiche für Anwendungen, die in der Produktion eingesetzt werden.
* Wenn die Abgrenzung nach Bereitstellungslebenszyklus nicht ausreicht, können Sie eine weitere Abgrenzung erreichen, indem Sie einen oder mehrere Bereiche pro Geschäftsfeld (LOB) und Bereitstellungsphase definieren.
* Ermitteln Sie, ob Sie Abgrenzungen für verschiedene Benutzergruppen benötigen. Beispiel: Ihre Entwickler können die Anwendung nicht entwickeln und testen. Sie benötigen eine andere Benutzergruppe, die die Anwendung testet. In diesem Szenario erstellen Sie zwei Bereiche: einen für Entwickler der Anwendung und einen für Tester der Anwendung. Anschließend erteilen Sie jeder Benutzergruppe Zugriff auf den richtigen Bereich.

Wenn Sie eine Architektur mit mehreren Organisationen implementieren, können Sie jede Organisation nach Geschäftsfeld (LOB), nach Bereitstellungslebenszyklus oder nach beiden Kategorien abgrenzen. Anschließend können Sie mehrere Bereiche definieren, die auf der Anzahl der Apps oder Projekte basieren, die durch dieselbe Abteilung im Unternehmen bereitgestellt werden. Beachten Sie die folgenden Hinweise, wenn Sie die Bereiche in einer Organisation planen:

* Definieren Sie einen Bereich, um einen Service zu hosten, der nur eine einmalige Bereitstellung und Konfiguration in der Organisation erfordert.
* Definieren Sie einen Bereich pro Anwendung, pro Gruppe zusammengehöriger Apps oder für ein bestimmtes Projekt.
* Wenn Sie Abgrenzungen für verschiedene Benutzer benötigen, definieren Sie einen Bereich für jede Benutzergruppe. Wenn einem Benutzer eine Entwicklerrolle in einem Bereich erteilt wird, hat der Benutzer vollen Zugriff auf alle Ressourcen und {{site.data.keyword.Bluemix_notm}}-Services, die in diesem Bereich bereitgestellt und ausgeführt werden. Wenn Sie eine strengere Sicherheit einrichten müssen, um zu verhindern, dass Benutzer jede Ressource kontrollieren können, ziehen Sie in Betracht, mehrere verschiedene Bereiche zu definieren. Innerhalb aller dieser Bereiche können Sie {{site.data.keyword.Bluemix_notm}}-Services bereitstellen, die von den Apps verwendet werden, die im jeweiligen Bereich ausgeführt werden.

## Benennung, Einschränkungen und Verwaltung von Bereichen
{: #spaceadmin}

Beachten Sie bei der Definition der verschiedenen Bereiche für Ihre Cloud-Organisation die folgenden Hinweise:

* Definieren Sie eine Namenskonvention und machen Sie sie verbindlich. Definieren Sie zum Beispiel eine Namenskonvention, bei der der Name des Bereichs Informationen zum Standort der Organisation und zum Typ der Cloud enthält. Sie können den Namen eines Bereichs ändern, nachdem er erstellt wurde. Wenn ein Bereichsname geändert wird, müssen Sie alle Teammitglieder des Bereichs darüber informieren.
* Definieren Sie die Einschränkungen, die für den Bereich gelten. Definieren Sie zum Beispiel den Typ der Apps, die in jedem Bereich entwickelt, verwaltet und bereitgestellt werden können.
* Geben Sie den Manager des Bereichs an. Es kann sinnvoll sein, die Verwaltung eines Bereichs an mehrere Personen zu delegieren.
