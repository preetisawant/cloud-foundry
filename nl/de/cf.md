---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gemeinsames Funktionieren von Cloud Foundry mit {{site.data.keyword.cloud_notm}}
{: #howwork}

Wenn Sie auf Cloud Foundry eine App bereitstellen, muss {{site.data.keyword.cloud_notm}} mit genügend Informationen konfiguriert sein, um die App unterstützen zu können.

* Für mobile Apps enthält {{site.data.keyword.cloud_notm}} ein Artefakt, das das Back-End für die mobile App darstellt, z. B. die Services, die von der mobilen App verwendet werden, um mit einem Server zu kommunizieren.
* Für Web-Apps muss sichergestellt werden, dass {{site.data.keyword.cloud_notm}} Informationen zur Laufzeit und zum Framework erhält, sodass {{site.data.keyword.cloud_notm}} die richtige Ausführungsumgebung einrichten kann, in der die App ausgeführt wird.

Beide Ausführungsumgebungen, die für die mobile App
wie auch die für die Web-App, sind von den Ausführungsumgebungen anderer Apps isoliert. Die Ausführungsumgebungen werden isoliert, obwohl sich diese Apps auf derselben physischen Maschine befinden. Die folgende Abbildung stellt die grundlegenden Abläufe für die Verwaltung der App-Bereitstellung in {{site.data.keyword.cloud_notm}} durch Cloud Foundry dar:

![App bereitstellen](images/deploy.png)

Abbildung 1. App bereitstellen

Wenn Sie eine App erstellen und auf Cloud Foundry bereitstellen, bestimmt die {{site.data.keyword.cloud_notm}}-Umgebung einen geeigneten virtuellen Server, an den die App bzw. die Artefakte gesendet werden, die die App darstellt. Für mobile Apps wird auf {{site.data.keyword.cloud_notm}} eine mobile Back-End-Projektion erstellt. Jeder Code für die in der Cloud ausgeführte mobile App wird letztendlich in der {{site.data.keyword.cloud_notm}}-Umgebung ausgeführt. Für Web-Apps ist der Code, der in der Cloud ausgeführt wird, die App selbst, die der Entwickler auf {{site.data.keyword.cloud_notm}} bereitstellt. Welcher virtuelle Server dafür ausgesucht wird, basiert auf mehreren Faktoren, wie zum Beispiel:

* Die bestehende Auslastung der Maschine
* Von diesem virtuellen Server unterstützte Laufzeiten oder Frameworks

Nachdem ein virtueller Server ausgewählt wurde, installiert ein Anwendungsmanager auf jedem virtuellen Server das passende Framework und die passende Laufzeit für die App. Anschließend kann die App in diesem Framework bereitgestellt werden. Sobald die Bereitstellung erfolgt ist, werden die Anwendungsartefakte gestartet.

Die folgende Abbildung zeigt die Struktur eines virtuellen Servers, auch als Droplet Execution Agent (DEA) bezeichnet, auf dem mehrere Apps bereitgestellt wurden:

![Struktur eines virtuellen Servers](images/container-diego.png)

Abbildung 2. Struktur eines virtuellen Servers

In jedem virtuellen Server kommuniziert ein Anwendungsmanager mit der übrigen {{site.data.keyword.cloud_notm}}-Infrastruktur und verwaltet die Apps, die auf diesem virtuellen Server bereitgestellt sind. Jeder virtuelle Server verfügt über Container zum Trennen und Schützen der Apps. In jedem dieser Container installiert {{site.data.keyword.cloud_notm}} das geeignete Framework und die geeignete Laufzeit, die für die einzelnen Apps erforderlich sind.

Wenn die
App bereitgestellt wurde und über eine Webschnittstelle (wie für eine Java-Web-App)
oder andere REST-basierte Services (z. B. mobile Services, die für die mobile App öffentlich zugänglich sind)
verfügt, können Benutzer der App durch normale HTTP-Anforderungen mit ihr kommunizieren.

![{{site.data.keyword.cloud_notm}}-App aufrufen](images/execute.png)

Abbildung 3. {{site.data.keyword.cloud_notm}}-App aufrufen

Jeder App kann mindestens eine URL zugeordnet sein, aber jede dieser URLs muss auf den {{site.data.keyword.cloud_notm}}-Endpunkt verweisen. Wenn eine Anforderung eintrifft, prüft {{site.data.keyword.cloud_notm}} diese Anforderung, stellt fest, an welche App sie gerichtet ist, und wählt eine der Instanzen der App für den Empfang der Anforderung aus.


## Cloud Foundry-Architektur in {{site.data.keyword.cloud_notm}}
{: #architecture}

Im Allgemeinen müssen Sie sich bei der Ausführung von Apps auf {{site.data.keyword.cloud_notm}} in Cloud Foundry keine Gedanken über die Betriebssystem- und Infrastrukturebenen machen. Die Ebenen wie Stammdateisysteme und
Middlewarekomponenten sind so abstrahiert, dass Sie sich auf Ihren Anwendungscode
konzentrieren können. Es gibt jedoch noch weitere Informationen zu diesen Ebenen, wenn Sie
spezielle Angaben dazu benötigen, wo Ihre App ausgeführt wird.

Details finden Sie im Abschnitt zum [Anzeigen von {{site.data.keyword.cloud_notm}}-Infrastrukturebenen](cf.html#infralayers).

Als Entwickler haben Sie die Möglichkeit, über eine browserbasierte Benutzerschnittstelle mit der
{{site.data.keyword.cloud_notm}}-Infrastruktur zu interagieren. Zum
Bereitstellen von Web-Apps können Sie außerdem die Cloud
Foundry-Befehlszeilenschnittstelle 'cf' verwenden.

Clients - mobile Apps, extern ausgeführte Apps, auf {{site.data.keyword.cloud_notm}} aufbauende Apps oder auch Entwickler, die gerade einen Browser verwenden - können mit den von {{site.data.keyword.cloud_notm}} gehosteten Apps interagieren. Mithilfe von REST- oder HTTP-APIs leiten Clients Anforderungen über
{{site.data.keyword.cloud_notm}} an eine der
App-Instanzen oder an die zusammengesetzten Services weiter.

In der folgenden Abbildung ist die allgemeine Cloud Foundry-Architektur unter {{site.data.keyword.cloud_notm}} dargestellt.

![{{site.data.keyword.cloud_notm}}-Architektur](images/arch.png)

Abbildung 4. Cloud Foundry-Architektur unter {{site.data.keyword.cloud_notm}}

Sie können Ihre Apps im Hinblick auf Latenz- und Sicherheitsaspekte für unterschiedliche
{{site.data.keyword.cloud_notm}}-Regionen
bereitstellen. Eine Bereitstellung
kann entweder in einer Region oder in mehreren Regionen stattfinden.


![Anwendungsentwicklung in mehreren Regionen](images/multi-region.png)

Abbildung 5. Anwendungsbereitstellung in mehreren Regionen

{{site.data.keyword.Bluemix_notm}}-Infrastrukturebenen
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} abstrahiert und verdeckt Betriebssystem- und Infrastrukturebenen, damit diese von Ihnen nicht verwaltet werden müssen. Manchmal kann es jedoch wünschenswert sein, mehr über das Betriebssystem und die Middleware für Ihre App zu wissen.
{:shortdesc}

### {{site.data.keyword.Bluemix_notm}}-Infrastrukturebenen anzeigen
{: #viewinfra}

Sie können den Befehl **bluemix app stacks** ausführen, um die verfügbaren Stacks bzw. Rootdateisysteme anzuzeigen, auf denen Ihre Apps bereitgestellt werden sollen. Sie können bei der Verwendung des Befehls **bluemix app push** mit der Option *-s* und dem Stacknamen in *stack_name* auch den Stack angeben; dabei ist der 'stack_name' das Stammdateisystem, zum Beispiel `lucid64` oder `cflinuxfs2`:

```
bluemix app push appName -s stack_name
```

Mithilfe des Befehls `cf buildpacks` können Sie die Middlewarekomponenten anzeigen, z. B. WebSphere Liberty Profile und SDK for Node.js; diese sind als Laufzeiten für die Ausführung Ihrer App verfügbar. Des Weiteren können Sie mithilfe des folgenden Befehls
die Laufzeitumgebung für Ihre App angeben:

```
bluemix app push appName -b buildpackname
```
