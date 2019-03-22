---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Domänen verwalten
{: #domains}

Es gibt zwei Typen an Cloud-Foundry-Domänen:
* Gemeinsam genutzte Domänen, die für jede beliebige Anwendung in einem Bereich in einer {{site.data.keyword.cfee_full_notm}}-Instanz verfügbar sind.  Um auf die gemeinsam genutzten Domänen zuzugreifen, rufen Sie die Seite **Domänen** im linken Navigationsfenster der Benutzerschnittstelle auf (unter *Operationen*).
* Private Domänen, die nur für Anwendungen und Bereiche innerhalb einer bestimmten Organisation verfügbar sind.  Um auf die Domänen innerhalb einer Organisation zuzugreifen, rufen Sie die Seite **Organisationen** im linken Navigationsfenster der Benutzerschnittstelle auf, öffnen die Organisation und wählen die Registerkarte **Domänen** aus.

## Domänen erstellen und löschen
{: #create-domains}

Wenn Sie eine gemeinsam genutzte Domäne erstellen möchten, wechseln Sie zu **Domänen** im linken Navigationsfenster der {{site.data.keyword.cfee_full_notm}}-Instanz.  

Wenn Sie eine private Domäne erstellen möchte, rufen Sie die Seite **Organisationen** im linken Navigationsfenster der Benutzerschnittstelle auf, öffnen die Organisation und wählen die Registerkarte **Domänen** aus.

Wenn die Seite _Domänen_ (bei gemeinsam genutzten Domänen) oder die Registerkarte _Domänen_ für eine bestimmte Organisation angezeigt wird, klicken Sie auf **Domäne erstellen**, um eine Domäne zu erstellen und einen eindeutigen Namen einzugeben.

**Anmerkung:** Domänennamen müssen im gesamten Bereich einer {{site.data.keyword.cfee_full_notm}}-Instanz eindeutig sein.  Dies bedeutet, dass eine private Domäne nicht den Namen einer gemeinsam genutzten oder privaten Domäne innerhalb einer bestimmten {{site.data.keyword.cfee_full_notm}}-Instanz aufweisen darf.

Sie können eine gemeinsam genutzte Domäne auch mithilfe der Cloud Foundry-Befehlszeilenschnittstelle erstellen, indem Sie den folgenden Befehl absetzen:
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
Sie können eine private Domäne mithilfe der Cloud Foundry-Befehlszeilenschnittstelle erstellen, indem Sie den folgenden Befehl absetzen:
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**Anmerkung:** Domänen, die in der Cloud-Foundry-Befehlszeilenschnittstelle erstellt werden, werden in der Benutzerschnittstelle sofort angezeigt, es kann jedoch bis zu einer Stunde dauern, bis sie wirksam werden.

Wenn Sie eine Domäne löschen möchten, wechseln Sie zu dem Menü ganz rechts in der Tabellenzeile für die entsprechende Domäne, die Sie löschen möchten, und wählen **Domäne löschen** aus.
  
Sie können eine gemeinsam genutzte Domäne auch mithilfe der Cloud Foundry-Befehlszeilenschnittstelle löschen, indem Sie den folgenden Befehl absetzen:
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## SSL-Zertifikate hochladen
 {: #upload-certificates}
 
Sie können ein SSL-Zertifikat für eine Domäne (gemeinsam genutzt oder privat) hochladen. Klicken Sie in der Tabellenzeile für die Domäne, zu der das Zertifikat hinzugefügt wird, auf **Hochladen**, und wählen Sie die Datei mit dem Zertifikat und die Datei mit dem privaten Schlüssel aus.
  
