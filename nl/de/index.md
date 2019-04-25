---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Informationen zu {{site.data.keyword.cfee_full_notm}}
{: #about}

Willkommen beim {{site.data.keyword.cfee_full}}-Service.

Mit {{site.data.keyword.cfee_full}} (CFEE) können Sie mehrere isolierte und auf Unternehmen abgestimmte Cloud Foundry-Plattformen bedarfsgesteuert instanziieren. Instanzen des {{site.data.keyword.Bluemix_notm}} Foundry Enterprise Environment-Service werden im eigenen Konto in {{site.data.keyword.Bluemix_notm}} ausgeführt. Die Umgebung wird auf isolierter Hardware (Kubernetes-Cluster) bereitgestellt. Sie haben volle Kontrolle über die Umgebung, einschließlich Zugriffssteuerung, Kapazitätsmanagement, Versionsaktualisierungen, Ressourcennutzung und Überwachung. Darüber hinaus ermöglicht die CFEE-Integration in {{site.data.keyword.Bluemix_notm}} den Entwicklern die Nutzung von Services, die in ihrem {{site.data.keyword.Bluemix_notm}}-Konto verfügbar sind.  Benutzer können diese Services zu einer CFEE-Instanz hinzufügen und sie an Anwendungen binden, die in CFEE-Bereichen bereitgestellt werden.

Hier erhalten Sie Informationen für den [**Einstieg**](https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#getting-started) in die Erstellung und Verwaltung einer CFEE-Instanz.

{:shortdesc}

## Wichtigste Elemente einer CFEE
{: #key-elements}

Die folgende Tabelle enthält eine Zusammenfassung der wichtigsten Elemente des {{site.data.keyword.cfee_full}}-Service:

| Element   | Beschreibung |
|-----------|---------------|
| IBM Cloud-Konto | CFEE-Instanzen werden unter einem bestimmten IBM Cloud-Konto erstellt, wodurch es Benutzern in diesem Konto entsprechend den Rollen und Zugriffsrichtlinien zur Verfügung steht, die für diese Benutzer definiert sind. |
|| Das Konto, unter dem die CFEE-Instanzen erstellt werden, muss ein nutzungsabhängiges Konto oder ein Abonnementkonto sein (kein Testkonto).  |
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

## Ziele für CFEE und unterstützende Services bereitstellen
{: #provisioning-targets}

Im Folgenden sind die Geografien, Standorte und Rechenzentren, in denen der CFEE-Service und die abhängigen Services (Kubernetes-Service, Compose for PostgreSQL and Cloud Object Storage-Services) für die Bereitstellung verfügbar sind:

|  **Geography** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **CFEE instance & Kubernetes Cluster** | **Cloud Object Storage** | **Compose for PostgreSQL (CF Region)** |
|----------------------------------------|-------------------|-------------------|-------------------|
|North America | Montreal (mon01) | us-geo | us-east |
|North America | Toronto (tor01) | us-geo| us-east |
|North America | Washington DC (wdc04) | us-geo | us-east |
|North America | Washington DC (wdc06) | us-geo | us-east | 
|North America | Washington DC (wdc07) | us-geo | us-east |
|North America | Dallas (dal10) | us-geo | us-south |
|North America | Dallas (dal12) | us-geo | us-south |
|North America | Dallas (dal13) | us-geo |us-south |
|North America | San Jose (sjc03) | us-geo | us-south |
|North America | San Jose (sjc04) | us-geo | us-south |
|South America &nbsp; &nbsp;| Sao Paolo (sao01) |  us-geo | us-south |
|Europe | London (lon02) | eu-geo | eu-gb |
|Europe | London (lon04) | eu-geo | eu-gb |
|Europe | London (lon06) | eu-geo | eu-gb | 
|Europe | Amsterdam (ams03) | eu-geo | eu-de |
|Europe | Oslo (osl01) |eu-geo | eu-de | 
|Europe | Paris (par01) | eu-geo | eu-de |
|Europe | Frankfurt (fra02) | eu-geo | eu-de |
|Europe | Frankfurt (fra04) | eu-geo | eu-de | 
|Europe | Frankfurt (fra05) |  eu-geo | eu-de |
|Europe | Milan (mil01) |  eu-geo | eu-de |
|Asia Pacific | Melbourne (mel01) | ap-geo | au-syd |
|Asia Pacific | Sydney (syd01) | ap-geo | au-syd |
|Asia Pacific | Sydney (syd04) | ap-geo | au-syd | 
|Asia Pacific | Hong Kong (hkg02) | ap-geo | au-syd |
|Asia Pacific | Hong Kong (seo01) | ap-geo | au-syd |
|Asia Pacific | Singapore (sng01) | ap-geo | au-syd |
|Asia Pacific | Tokyo (tok02) | ap-geo | au-syd |
|Asia Pacific | Tokyo (tok04) | ap-geo | au-syd |
|Asia Pacific | Tokyo (tok05) | ap-geo | au-syd |
|Asia Pacific | Chennai (che01) | ap-geo | au-syd |
{: caption="Tabelle 2. Ziele für CFEE und unterstützende Services bereitstellen" caption-side="top"}

**Beispiel:** Der CFEE-Service kann in Europa in drei Rechenzentren bereitgestellt werden: Amsterdam (1 Rechenzentrum), Frankfurt (3 Rechenzentren), London (3 Rechenzentren), Oslo (1 Rechenzentrum) und Paris (1 Rechenzentrum). Wenn die CFEE in Frankfurt bereitgestellt wird, wird die Cloud Object Store-Serviceinstanz in der Region _eu-geo_ und die Compose for PostgreSQL-Serviceinstanz in der öffentlichen Cloud Foundry-Region _eu-de_ bereitgestellt.

Videos mit umfassenden Informationen und Vorführungen für die Arbeit mit Services in einer CFEE-Instanz finden Sie in der [CFEE-Videowiedergabeliste](https://ibm.biz/CFEE_Playlist){: new_window} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link").
{:tip}
