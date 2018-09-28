---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Berechtigungen
{: #permissions}

Bevor Sie damit beginnen, Instanzen eines {{site.data.keyword.cfee_full}}-Service zu erstellen oder mit ihnen zu arbeiten, müssen die Berechtigungen des Administrators und des restlichen Teams ordnungsgemäß festgelegt werden.

## Zum Erstellen einer neuen Umgebung erforderliche Berechtigungen
{: #perm-creating}

Wenn Benutzer neue Instanzen des {{site.data.keyword.cfee_full_notm}}-Service erstellen möchten, müssen ihnen vom Administrator des Kontos, für das die Instanz erstellt werden soll, über Zugriffsrichtlinien die entsprechenden Berechtigungen erteilt werden:

* Zugriff auf mindestens eine Ressourcengruppe im {{site.data.keyword.Bluemix}}-Konto. Ressourcengruppen ermöglichen das Organisieren von Ressourcen in angepassten Gruppierungen, um die Zugriffssteuerung für diese Ressourcen zu vereinfachen. Wenn Sie eine neue Umgebungsinstanz erstellen, werden Sie zur Eingabe einer Ressourcengruppe aufgefordert.

* Rolle eines Administrators oder Bearbeiters für den {{site.data.keyword.cfee_full_notm}}-Service in der Ressourcengruppe, der die Umgebung zugeordnet ist. Benutzer mit einer Administrator- oder Bearbeiterrolle im {{site.data.keyword.cfee_full_notm}}-Service können Umgebungen erstellen und löschen. Aber nur Benutzer mit einer Verwaltungsrolle können Benutzer einer {{site.data.keyword.cfee_full_notm}}-Instanz zuordnen oder die Rollen ändern, die den Benutzern in dieser Instanz zugeordnet sind.

* Rolle eines Administrators oder Bearbeiters für den IBM Cloud Object Storage-Service, eine erforderliche Abhängigkeit des CFEE-Service. Eine Instanz des IBM Cloud Object Storage-Service wird zum Speichern von Daten verwendet, die während der Erstellung der ICFEE-Anwendungscontainer generiert wurden (zum Beispiel hochgeladene Anwendungspakete, Buildpacks und kompilierte ausführbare Dateien).

* Eine Instanz des Compose for PostgreSQL-Service ist eine erforderliche Abhängigkeit des CFEE-Service. Compose for PostgreSQL wird zum Speichern von Cloud Foundry-Daten für die CFEE-Instanz verwendet (zum Beispiel die Protokollierung der Anwendungsbereitstellung sowie der Start- und Stoppereignisse oder das Aufbewahren der Datensätze der CFEE-Benutzermitgliedschaft, -Organisationen, -Bereiche, -Anwendungen und -Serviceverbindungen). Diese Instanz des Compose for PostgreSQL-Service wird in einer öffentlichen Cloud Foundry-Organisation (ohne Bezug zu CFEE-Organisationen) bereitgestellt. Die öffentliche Cloud Foundry-Organisation, in der die Compose for PostgresSQL-Instanz bereitgestellt wird, weist den Namen **_cfee-`<accountId>`_** auf; hierbei steht 'accountId' für die ID des IBM Cloud-Kontos, in dem die CFEE-Umgebung (zusammen mit der Compose for PostgreSQL-Serviceinstanz) bereitgestellt wird. Die öffentliche Cloud Foundry-Organisation wird automatisch erstellt, wenn der Kontoeigner eine CFEE-Instanz erstellt. Die Organisation wird nicht automatisch erstellt, wenn ein Benutzer, der nicht der Kontoeigner ist, versucht, die CFEE-Instanz zu erstellen (der CFEE-Erstellungsversuch schlägt in diesem Fall fehl). Deswegen muss jeder Benutzer des IBM Cloud-Kontos, der CFEE-Instanzen erstellt, aber nicht der Kontoeigner ist, zur öffentlichen Cloud Foundry-Organisation **_cfee-`<accountId>`_** mit einer **Managerrolle** hinzugefügt werden.   

   Gehen Sie wie folgt vor, um einen Benutzer des IBM Cloud-Kontos zur öffentlichen Organisation _cfee-`<accountId>`_ hinzuzufügen:
    * Wechseln Sie zu [**Verwalten> Konto > Cloud Foundry-Organisationen**](https://console.bluemix.net/account/organizations).
    * Klicken Sie auf die Organisation **_cfee-`<accountId>`_**.
    * Wechseln Sie ganz oben auf der Seite zur Registerkarte **Benutzer**.
    * Suchen Sie den Benutzer, der CFEE-Instanzen erstellen muss, und klicken Sie auf das Kontrollkästchen **Manager** für diesen Benutzer. Wenn der Benutzer, der in der Lage sein soll, CFEE-Instanzen zu erstellen, nicht in der Liste aufgeführt ist, klicken Sie oberhalb der Tabelle auf **Benutzer hinzufügen oder einladen**, um den Benutzer zur Organisation **_cfee-`<accountId>`_** hinzuzufügen oder einzuladen.

   **Hinweis:** Die öffentliche Organisation **_cfee-`<accountId>`_** wird implizit und automatisch erstellt, wenn der IBM Cloud-Kontoeigner eine CFEE-Instanz erstellt, der Kontoeigner (und nur der Kontoeigner) kann stattdessen aber auch manuell die öffentliche Cloud Foundry-Organisation erstellen, ohne gleichzeitig eine CFEE-Instanz erstellen zu müssen. Der IBM Cloud-Kontoeigner kann die öffentliche Organisation _cfee-`<accountId>`_ manuell auf der Seite **Verwalten > Konto > Cloud Foundry-Organisationen** erstellen. Falls Sie der Kontoeigner sind und die öffentliche Organisation _cfee-`<accountId>`_ erstellen, stellen Sie sicher, dass Sie für diese genau den Namen _cfee-`<accountId>`_ festlegen. Zum Suchen der IBM Cloud-Account-ID wechseln Sie auf die Seite [**Verwalten > Konto > Cloud Foundry-Organisationen**](https://console.bluemix.net/account/organizations) und zeigen die Seiten-URL an, die im Browser verfügbar ist. Die IBM Cloud-Konto-ID besteht aus alphanumerischen Werten, die auf das Zeichen `=` in der Seiten-URL folgen. Alternativ können Sie zu __Verwalten > Konto > Benutzer__ wechseln und den Mauszeiger über die QuickInfo links neben _Konto_ in der rechten oberen Ecke der Seite bewegen.
   
* Rolle eines Administrators oder Bearbeiters für {{site.data.keyword.Bluemix_notm}} Container-Service in der Ressourcengruppe, der die Umgebung zugeordnet ist. Instanzen der {{site.data.keyword.cfee_full_notm}}-Umgebung werden in der Container-Cluster-Infrastruktur bereitgestellt, die vom {{site.data.keyword.Bluemix_notm}} Container-Service bereitgestellt wird. Wenn Sie eine Instanz des {{site.data.keyword.cfee_full_notm}}-Service erstellen, wird vom Service automatisch ein Kubernetes-Cluster erstellt, in dem die {{site.data.keyword.cfee_full_notm}}-Instanz bereitgestellt wird. Der Zugriff auf den IBM Container-Service, insbesondere in der Ressourcengruppe, der die Umgebung zugeordnet ist, ist für die Erstellung dieser Clusterinfrastruktur erforderlich.

Gehen Sie wie folgt vor, um sicherzustellen, dass Sie über die erforderlichen Zugriffsrichtlinien zum Erstellen einer {{site.data.keyword.cfee_full_notm}}-Instanz verfügen:
1. Wechseln Sie zum Menü [**Verwalten > Konto > Benutzer**](https://console.bluemix.net/iam/#/users) im {{site.data.keyword.Bluemix_notm}}-Header, um die Seite **Identität & Zugriff** zu öffnen.
2. Klicken Sie in der Registerkarte 'Zugriffsrichtlinien' auf den Benutzer, der die Umgebung erstellt.
3. Stellen Sie sicher, dass die Zugriffsrichtlinien für den Benutzer, der die Umgebung erstellt, mit den zuvor beschriebenen Richtlinien konsistent sind.

In der folgenden Anzeige werden die Zugriffsrichtlinien wie auf der Seite 'Identität & Zugriff' von {{site.data.keyword.Bluemix_notm}} angezeigt dargestellt; sie ermöglichen einem Benutzer das Erstellen einer {{site.data.keyword.cfee_full_notm}}-Instanz.

![Zugriffsrichtlinien](img/AccessPolicies_Creator.png)

## Für die Arbeit mit einer Umgebung erforderliche Berechtigungen
{: #perm-working}

Damit ein Benutzer mit einer Instanz von {{site.data.keyword.cfee_full_notm}} arbeiten kann, muss er folgende Eigenschaften aufweisen:
1. Er muss Mitglied des {{site.data.keyword.Bluemix_notm}}-Kontos sein, in dem die {{site.data.keyword.cfee_full_notm}}-Instanz erstellt wurde.
2. Ihm müssen vom Kontoadministrator die folgenden _Zugriffsrichtlinien_ erteilt worden sein (Informationen zum Überprüfen Ihrer derzeitigen Zugriffsrichtlinien finden Sie auf der Seite _Identität & Zugriff_ im Menü [**Verwalten> Konto > Benutzer**](https://console.bluemix.net/iam/#/users) im {{site.data.keyword.Bluemix_notm}}-Header):
  - Zugriff auf mindestens eine Ressourcengruppe im {{site.data.keyword.Bluemix_notm}}-Konto. Ressourcengruppen ermöglichen das Organisieren von Ressourcen in angepassten Gruppierungen, um die Zugriffssteuerung für diese Ressourcen zu vereinfachen. Wenn Sie eine neue Umgebungsinstanz erstellen, werden Sie zur Eingabe einer Ressourcengruppe aufgefordert.
  - Dem Benutzer muss der Zugriff auf den {{site.data.keyword.cfee_full_notm}}-Service in der Ressourcengruppe zugeordnet sein, unter der die Umgebungsinstanz erstellt wurde. Die Zugriffsebene und -steuerung eines Benutzers in einer {{site.data.keyword.cfee_full_notm}}-Instanz hängt von der Rolle ab, die ihm in der Zugriffsrichtlinie gewährt wird:
     - Benutzer, denen eine Administrator- oder Bearbeiterrolle zugeordnet ist, können Organisationen erstellen und Manager zu Organisationen und Bereichen zuordnen; außerdem verfügen Sie über die vollständigen Berechtigungen für alle Organisationen und Bereiche innerhalb der Umgebung und führen mit der Cloud-Controller-API operative Aktionen aus. Den Benutzern wird automatisch die Berechtigung für den Bereich _cloud_controller.admin_ im Bereich _Benutzerkonto und Authentifizierung_ von Cloud Foundry erteilt.
     - Benutzer, denen die Rolle eines Anzeigeberechtigten zugeordnet ist, können diese Umgebung im {{site.data.keyword.Bluemix_notm}}-Hauptdashboard anzeigen und die zugehörige Benutzerschnittstelle öffnen. Der Zugriff der Benutzer auf bestimmte Organisationen und Bereiche innerhalb einer Umgebung hängt von den Rollen für die Organisation und Bereiche ab, die ihnen von den Managern dieser Organisationen und Bereiche zugeordnet wurden. Weitere Informationen finden Sie unter [Benutzer zu Organisationen hinzufügen](add-users.html).

In der Abbildung werden die Mindestzugriffsrichtlinien dargestellt (wie sie auf der {{site.data.keyword.Bluemix_notm}}-Seite _Identität & Zugriff_ anzeigt werden), die für den Zugriff auf eine {{site.data.keyword.cfee_full_notm}}-Umgebung erforderlich sind.

![Zugriffsrichtlinien](img/AccessPolicies_User.png)

