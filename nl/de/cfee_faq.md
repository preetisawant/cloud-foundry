---



copyright:

  years: 2018

lastupdated: "2018-11-09"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# Häufig gestellte Fragen
{: #cfeefaq}

## Was ist der Unterschied zwischen IBM Cloud Foundry Enterprise Environment (CFEE) und der öffentlichen Cloud Foundry-Version?
{: #cfee_diff}

Sie können {{site.data.keyword.cloud}} Foundry öffentlich verwenden, um für die Cloud native Anwendungen auszuführen, von denen Cloud Foundry zur einfachen Konfiguration, leistungsfähigen Skalierung und Datenverkehrsverwaltung verwendet wird. Außerdem verfügen Sie über einfachen Zugriff auf alle {{site.data.keyword.cloud}}-Services.

Sie können {{site.data.keyword.cfee_full}} für alles verwenden, was auch mit der öffentlichen Version von Cloud Foundry möglich ist; darüber hinaus können Sie jedoch auch isolierte Umgebungen zum Hosten von Cloud Foundry-Anwendungen exklusiv für Ihr Unternehmen erstellen und verwalten.


## Wie unterscheidet sich das neue Angebot von früheren IBM Cloud Foundry-Angeboten?
{: #cfOfferings_diff}

In Bezug auf öffentliche Multi-Tenant-Lösungen besteht der größte Unterschied sicherlich in den Isolationseigenschaften. In Bezug auf das vorhandene Single-Tenant-Angebot in der IBM Cloud-Infrastruktur sind die beiden Hauptunterschiede der reduzierte Speicherbedarf für die Infrastruktur (und damit niedrigere Kosten) sowie das Serviceintegrationsmodell für eine solche Single-Tenant-Umgebung.

## Wo finde ich den CFEE-Service?
{: #where}

Den {{site.data.keyword.cfee_full}}-Service können Sie im {{site.data.keyword.Bluemix_notm}}-[Katalog](https://console.stage1.bluemix.net/catalog) finden und instanziieren.

## Sind in einem regionalen Rechenzentrum mehrere CFEE-Umgebungen möglich?
{: #multiple-cfees}

Ja, Sie können in [diesen Regionen](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link") bei Bedarf so viele CFEE-Instanzen erstellen, wie Sie benötigen.

## Muss ich mit einer Mindestkapazität beginnen?
{: #minimum-capacity}

Ja. Für die Erstellung einer CFEE-Instanz sind mindestens zwei Cloud Foundry-Zellen erforderlich; in jeder Zelle werden 4 Kerne und 16 GB RAM, eine primäre SSD-Platte mit 25 GB Kapazität, eine sekundäre SSD-Platte mit 100 GB Kapazität und eine Netzgeschwindigkeit von 1000 Mb/s bereitgestellt.

## Was ist die Grundlage der IaaS (Infrastructure as a Service), in der die CFEE-Instanz bereitgestellt wird?
{: #why-kubs}

Der CFEE-Service wird in Kubernetes-Containern ausgeführt, was niedrigere Infrastrukturkosten und effizientere Operationen ermöglicht, da Kubernetes eine sehr intelligente IaaS ist, von der viele Betriebsaktivitäten automatisiert werden. 

## Welche Isolationsoptionen habe ich beim Erstellen einer CFEE-Instanz?
{: #isolation}

Sie verfügen über zwei Hardwareoptionen für den Typ der Kubernetes-Infrastruktur, in der die CFEE-Instanz bereitgestellt wird: _Virtuell gemeinsam genutzte_ oder _virtuell dedizierte_ Hardware. Bei der _virtuell gemeinsam genutzten_ Hardware werden die Workerknoten (in denen der Cloud Foundry-Plattformcontainer bereitgestellt wird) von Ihnen und anderen IBM Kunden gemeinsam verwendet. Bei Verwendung _virtuell dedizierter_ Hardware werden die Workerknoten auf der Hardware gehostet, die exklusiv für Ihr Konto dediziert ist. Beachten Sie, dass in beiden Fällen (_Virtuell gemeinsam genutzt_ und _Virtuell dediziert_) jeder Workerknoten für den Kunden eine Single-Tenant-Lösung ist. Das bedeutet, dass die Cloud Foundry-Zellen, unter deren Verwendung die Anwendungen ausgeführt werden, nicht mit anderen Kunden gemeinsam genutzt werden.

## Kann ich die Kapazität einer CFEE-Instanz skalieren?
{: #scaling}

Ja, Sie können die Kapazität einer CFEE-Instanz durch das Hinzufügen oder Entfernen von Cloud Foundry-Zellen je nach Bedarf nach oben oder unten skalieren.

## Kann ich für meine CFEE-Instanz ein Upgrade auf eine neue Version durchführen? Wie funktioniert das Upgrade?
{: #upgrading}
Ja. Sie werden von der CFEE-Benutzerschnittstelle informiert, wenn eine neue CFEE-Version verfügbar ist. Sie legen fest, wann Sie eine Aktualisierung auf eine neue Version durchführen. Die CFEE-Versionsaktualisierung wird von CFEE-Administratoren in der Benutzerschnittstelle aufgerufen. Mit den Paketen der CFEE-Versionsaktualisierungen können neue Versionen der Komponenten oder unterstützenden Services bereitgestellt werden (zum Beispiel Cloud Foundry, Kubernetes, usw.). Sie aktualisieren zuerst die CFEE-Steuerebene und danach die Cloud Foundry-Zellen. Der Aktualisierungsprozess wurde optimiert, um Störungen zu minimieren.

## Was sind die Voraussetzungen für die Erstellung einer CFEE-Instanz?
{: #create}

Sie können einen CFEE-Service suchen, der im {{site.data.keyword.Bluemix_notm}}-Katalog aufgelistet wird. Sie müssen über ein {{site.data.keyword.Bluemix_notm}}-Konto verfügen, für das ein Upgrade durchgeführt wurde; außerdem müssen Sie über Berechtigungen für den CFEE-Service und die zugehörigen unterstützten Services (Kubernetes, Cloud Object Storage und Compose for PostgreSQL) verfügen. Wenn Sie über diese Berechtigungen verfügen, geben Sie einfach einen Namen für die Umgebung an und klicken auf _Erstellen_. Die Erstellung dauert ca. 90 Minuten.

## Kann ich {{site.data.keyword.Bluemix_notm}}-Services in meiner CFEE-Instanz verwenden?
{: #Services-ibmcloud}

Definitiv! Durch die Integration in {{site.data.keyword.Bluemix_notm}} können Entwickler in einer CFEE-Instanz {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen erstellen (oder vorhandene Instanzen verwenden) und diese an Anwendungen binden, die in CFEE-Bereichen bereitgestellt werden.

## Kann ich eigene Services in meiner CFEE-Instanz verwenden?
{: #Services-ibmcloud}

Ja. Ein Administrator kann einen Service-Broker in der CFEE-Instanz registrieren und den Benutzern in dieser CFEE-Instanz angepasste Servicepläne verfügbar machen. Der lokale CFEE-Marktplatz umfasst die Services aus dem {{site.data.keyword.Bluemix_notm}}-Katalog sowie zusätzlich alle Services von Kunden, die vom lokalen Service-Broker der CFEE-Instanz verwaltet werden.

## Wie kann ich den Benutzerzugriff auf eine CFEE-Instanz steuern?
{: #Services}

Wie bei allen anderen {{site.data.keyword.Bluemix_notm}}-Services wird der Zugriff auf eine CFEE-Instanz über _Identity & Access Management_ (IAM) gesteuert. Durch die Zuordnung von Benutzerzugriffsrichtlinien (entweder einzeln oder über Zugriffsgruppen) mit bestimmten Rollen können Benutzern bestimmte Zugriffsebenen für den Zugriff auf eine CFEE-Instanz zugewiesen werden. Abgesehen vom Zugriff auf den CFEE-Service wird der Zugriff auf Cloud Foundry-Organisationen und CFEE-Bereiche über die Cloud Foundry-Mitgliedschaft und die Rollen gesteuert, die Benutzern in bestimmten Organisationen und Bereichen zugeordnet werden.

