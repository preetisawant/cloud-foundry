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

# Organisationen und Bereichen erstellen
{: #create_orgs}

Anwendungen in einer {{site.data.keyword.cfee_full}}-Umgebung können in bestimmten Bereichen verwendet werden. Ein Bereich ist innerhalb einer bestimmten Organisation vorhanden. Mitglieder einer Organisation nutzen einen Kontingentplan, Anwendungen, Serviceinstanzen und angepasste Domänen gemeinsam. Nach der Erstellung der Organisationen und Bereiche können ihnen Benutzer mit bestimmten Rollen hinzugefügt werden; anhand dieser Rollen werden die Zugriffsebene und die Steuerung für diese Organisationen und Bereiche festgelegt. Zum Erstellen der Organisationen und zum Zuordnen der Manager zu diesen Organisationen benötigen Sie eine Administratorrolle für den {{site.data.keyword.cfee_full_notm}}-Service und die konkrete Umgebungsinstanz, zu der die Benutzer hinzugefügt werden. Diese Berechtigungen werden auf der Seite _Identität & Zugriff_ über das Menü **Verwalten > Benutzer** im {{site.data.keyword.Bluemix}}-Header festgelegt.{: shortdesc}

## Organisationen erstellen
{: #create-org}

Gehen Sie wie folgt vor, um Organisationen in einer {{site.data.keyword.cfee_full_notm}}-Umgebung zu erstellen:

1. Wechseln Sie zum [{{site.data.keyword.Bluemix_notm}} Foundry-Umgebungsdashboard](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments){: new_window} und öffnen Sie die {{site.data.keyword.cfee_full_notm}}-Umgebung, in der Sie die Organisationen erstellen möchten.
2. Wechseln Sie in der {{site.data.keyword.cfee_full_notm}}-Benutzerschnittstelle im Navigationsbereich zum Eintrag **Organisationen**, um die Seite _Organisationen_ zu öffnen.
3. Klicken Sie auf **Neues hinzufügen**.
4. Geben Sie einen **Namen** für die neue Organisation ein.
5. Geben Sie unter **Manager** mindestens einen Benutzer an. Nur Benutzer mit der Rolle eines Managers können Mitglieder zu dieser Organisation hinzufügen.
6. Wählen Sie unter **Kontingentplan** einen verfügbaren Plan aus. Anhand eines Kontingentplans werden der für Apps in der Organisation verfügbare Hauptspeicher, die maximale Anzahl der gehosteten Apps und die maximale Anzahl der Routen begrenzt.

Zusätzlich zum Verwalten der Organisationsmitgliedschaft können Organisationsmanager innerhalb der Organisation Bereiche erstellen, anzeigen, bearbeiten oder löschen. Organisationsmanager können auch die Nutzung und das Kontingent der Organisation anzeigen, Benutzer in die Organisation einladen, die Mitgliedschaft und die Rollen in der Organisation verwalten und angepasste Domänen für die Organisation verwalten.

Wenn Sie innerhalb einer Organisation Bereiche erstellen möchten, wechseln Sie auf der Seite _Organisationen_ zur Registerkarte **Bereiche** und klicken auf **Neues hinzufügen**. Mitglieder einer Organisation können auch ihre eigenen Bereiche innerhalb einer Organisation erstellen und verwalten. Weitere Informationen zu Cloud Foundry-Rollen finden Sie unter [Cloud Foundry-Zugriff](https://console.bluemix.net/docs/iam/cfaccess.html#cfroles){: new_window}.

**Hinweis:** Für den Zugriff auf Organisationen und Bereiche innerhalb einer {{site.data.keyword.cfee_full_notm}}-Umgebung müssen diese Benutzer über die Berechtigung auf die Umgebung selbst verfügen. Ohne die Berechtigung für den Zugriff auf die {{site.data.keyword.cfee_full_notm}}-Umgebung können Benutzer unabhängig von ihrer Mitgliedschaft und Rolle in diesen Organisationen und Bereichen nicht auf Organisationen und Bereiche in der Umgebung zugreifen.
