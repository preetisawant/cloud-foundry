---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Einhaltung von Vorschriften und gesetzlichen Bestimmungen
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) ist eine Platform as a Service-Lösung. Daher steht es dem Kunden frei, die Serviceinstanz für alles zu verwenden, was unterstützt wird. Die CFEE-Instanz und die abhängigen Services verfügen über auf die geringste Menge an persönlichen Daten.

Es sollte jedoch deutlich gemacht werden, dass auch ohne eine Verarbeitung sensibler Daten (zum Beispiel HIPAA-Daten) über die CFEE-Steuerebene der Kunde dafür verantwortlich ist, sicherzustellen, dass die jeweilige CFEE-Instanz verwendet wird, da alle Abhängigkeiten von den Kunden in ihrem {{site.data.keyword.Bluemix_notm}}-Konto verwaltet werden und die Kunden die Eigner dieser Abhängigkeiten sind. 

Die folgenden bewährten Verfahren werden empfohlen:
*  Keine Änderung der abhängigen Services, die mit der CFEE-Instanz erstellt wurden (Kubernetes, Cloud Object Storage und Compose for PostgreSQL).
*  Aktualisierung und Verwaltung der CFEE-Instanz über den CFEE-Service selbst (Benutzerschnittstelle oder Befehlszeilenschnittstelle) und nicht über den Kubernetes-Service.

Der Kubernetes-Cluster wird zum Bereitstellen der Mehrheit der CFEE-Infrastruktur sowie aller Anwendungen verwendet, die auf über die CFEE-Instanz ausgeführt werden, da die Cloud Foundry-Zellen auf den Kubernetes-Knoten bereitgestellt werden. Der Eigner dieses Clusters ist das SoftLayer-Konto des Kunden und der Cluster wird auch von diesem Konto verwaltet.

Die Compose for PostgreSQL-Datenbank wird von der CFEE-Instanz zum Aufbewahren der Metadaten der Organisationen, Bereiche, Benutzer und Rollen verwendet. Wenn die CFEE-Instanz wie empfohlen verwendet wird, werden keine sensiblen Daten verfügbar gemacht. Wenn ein Kunde jedoch seine Organisationen und Bereiche mit persönlichen oder sensiblen Informationen seiner Kunden benennt, kann die PostgreSQL-Datenbank HIPAA-Informationen oder andere Arten von sensiblen Informationen enthalten.

Die Cloud Object Storage-Instanz wird von der CFEE-Instanz zum Speichern der Droplets einer Anwendung verwendet, sodass sie bereitgestellt, gestoppt, gestartet, usw. werden können. Dies bedeutet, dass die Anwendung nicht von der Cloud Object Storage-Instanz ausgeführt wird, sondern nur das zugehörige Image enthält. Wenn die Cloud Object Storage-Instanz nach den bewährten Verfahren verwendet wird, wird sie daher keine HIPAA-sensiblen Informationen enthalten. Der Kunde trägt die Verantwortung dafür, sicherzustellen, dass die persönlichen Daten in keiner Anwendung fest codiert sind (Testdaten, usw.).
