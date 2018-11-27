---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Berechtigungen
{: #permissions}

Damit Benutzer Instanzen des {{site.data.keyword.cfee_full}}-Service erstellen und damit arbeiten können, müssen ihre Berechtigungen von einem Administrator des Kontos, in dem die Instanz erstellt werden soll, korrekt festgelegt worden sein. 

## Zum Erstellen einer neuen Umgebung erforderliche Berechtigungen
{: #perm-creating}

Um neue Instanzen des CFEE-Service erstellen zu können, müssen Benutzern Zugriffsrichtlinien von einem Kontoadministrator erteilt werden, nicht nur für den CFEE-Service selbst, sondern auch für die unterstützenden Services, die beim Erstellen des CFEE-Service automatisch erstellt wurden.

Die folgenden Identity & Access Management (IAM)-Zugriffsrichtlinien sind für Benutzer erforderlich, damit sie eine {{site.data.keyword.cfee_full_notm}}-Instanz erstellen können:

* Zugriff als _Anzeigeberechtigter_ (oder höher) auf die **_Standard_**-**Ressourcengruppe** im {{site.data.keyword.Bluemix}}-Konto. Ressourcengruppen ermöglichen das Organisieren von Ressourcen in angepassten Gruppierungen, um die Zugriffssteuerung für diese Ressourcen zu vereinfachen. Wenn Sie eine neue Umgebungsinstanz erstellen, werden Sie zur Eingabe einer Ressourcengruppe aufgefordert. Der Zugriff auf die Ressourcengruppe _Standard_ ist erforderlich, da es sich immer um die Ressourcengruppe handelt, in der der Kubernetes-Cluster erforderlich ist.  Benutzer können die CFEE-Instanz in einer anderen Ressourcengruppe bereitstellen, aber der Kubernetes-Cluster wird weiterhin für die Ressourcengruppe _Standard_ bereitgestellt.  Wenn ein Benutzer die CFEE-Instanz in einer anderen Benutzergruppe bereitstellt, benötigen diese Benutzer die Anzeigeberechtigung für diese Ressourcengruppe.

* Die Rolle _Administrator_ oder _Editor_ für Ressourcen des **{{site.data.keyword.cfee_full_notm}}-Service**. In der Ressourcengruppe, der die Umgebung zugeordnet ist. Benutzer mit einer Administrator- oder Bearbeiterrolle im {{site.data.keyword.cfee_full_notm}}-Service können Umgebungen erstellen und löschen. Aber nur Benutzer mit einer Verwaltungsrolle können Benutzer einer {{site.data.keyword.cfee_full_notm}}-Instanz zuordnen oder die Rollen ändern, die den Benutzern in dieser Instanz zugeordnet sind.
   
* Die Rolle _Administrator_ für Ressourcen des **Kubernetes-Service**. Instanzen von {{site.data.keyword.cfee_full_notm}} werden in einer Container-Clusterinfrastruktur bereitgestellt, die vom Kubernetes-Service bereitgestellt wird. Wenn Sie eine Instanz des {{site.data.keyword.cfee_full_notm}}-Service erstellen, erstellt der Service automatisch einen Kubernetes-Cluster. Der Zugriff auf den Kubernetes-Service ist für die Erstellung dieser Clusterinfrastruktur erforderlich. Sie können den Zugriff auf die Richtlinie des Kubernetes-Service für die Region erweitern, in der Sie die CFEE-Instanz bereitstellen möchten, oder den Zugriff auf alle Regionen ausweiten.

* Die Plattformrolle _Administrator_ oder _Editor_ und die Managerrolle für Servicezugriff auf den **IBM Cloud Object Storage-Service**, der eine erforderliche Abhängigkeit für den CFEE-Service ist. Eine Instanz des IBM Cloud Object Storage-Service wird zum Speichern von Daten verwendet, die während der Erstellung der ICFEE-Anwendungscontainer generiert wurden (zum Beispiel hochgeladene Anwendungspakete, Buildpacks und kompilierte ausführbare Dateien).

* Eine Instanz des Compose for PostgreSQL-Service ist eine erforderliche Abhängigkeit des CFEE-Service.  Compose for PostgreSQL wird zum Speichern von Cloud Foundry-Daten für die CFEE-Instanz verwendet (zum Beispiel die Protokollierung der Anwendungsbereitstellung sowie der Start- und Stoppereignisse oder das Aufbewahren der Datensätze der CFEE-Benutzermitgliedschaft, -Organisationen, -Bereiche, -Anwendungen und -Serviceverbindungen).  Diese Instanz des **Compose for PostgreSQL-Service** ist in einem Bereich innerhalb einer öffentlichen Cloud Foundry-Organisation (ohne Bezug zu CFEE-Organisationen) bereitgestellt, den Sie bei der Erstellung einer {{site.data.keyword.cfee_full_notm}}-Instanz auswählen. Dies bedeutet, dass Sie beim Erstellen einer {{site.data.keyword.cfee_full_notm}}-Instanz über _Manager_-Zugriff auf mindestens eine Organisation an der Position verfügen müssen, an der Sie die CFEE-Instanz bereitstellen möchten. Außerdem benötigen Sie _Entwickler_Zugriff auf mindestens einen Bereich in dieser Organisation. 

  Wenn Sie an der Position, an der Sie eine CFEE-Instanz erstellen möchten, nicht Mitglied mindestens einer öffentlichen Organisation sind, bitten Sie einen IBM Cloud-Administrator, Sie zu einer Instanz einzuladen. Wenn Sie über eine Administratorrolle im Konto verfügen, können Sie Benutzer zu öffentlichen Organisationen und Bereichen in dem Konto hinzufügen, indem Sie Folgendes ausführen:

     * Rufen Sie [**Verwalten > Konto > Cloud Foundry-Organisationen**](https://console.bluemix.net/account/organizations) auf und klicken Sie auf **Organisation hinzufügen** oder wählen Sie eine vorhandene Organisation aus.
     * Wechseln Sie zur Registerkarte **Benutzer** oben auf der Seite der Organisation.
     * Suchen Sie den Benutzer, der CFEE-Instanzen erstellen muss. Wenn der Benutzer, der in der Lage sein soll, CFEE-Instanzen zu erstellen, nicht in der Liste aufgeführt ist, klicken Sie oberhalb der Tabelle auf **Benutzer hinzufügen oder einladen** oder laden Sie Benutzer in die Organisation ein.
     * Wechseln Sie zur Registerkarte **Bereiche** oben auf der Seite der Organisation.
     * Suchen Sie den Bereich, in dem die Instanz des Compose for PostgreSQL-Service bereitgestellt werden soll, und überprüfen Sie das Kontrollkästchen für die Rolle **Entwickler**.

In der folgenden Anzeige werden die Zugriffsrichtlinien wie auf der Seite 'Identität & Zugriff' von {{site.data.keyword.Bluemix_notm}} angezeigt dargestellt; sie ermöglichen einem Benutzer das Erstellen einer {{site.data.keyword.cfee_full_notm}}-Instanz.

![Zugriffsrichtlinien](img/AccessPolicies_Creator.png)

Benutzerberechtigungen können Sie in der {{site.data.keyword.Bluemix}}-Befehlszeile erteilen. Sie können auch eine Zugriffsrichtlinie für einen Benutzer definieren, indem Sie die Parameter der Richtlinie (Services, Rollen, Regionen, usw.) in einer JSON-formatierten Datei angeben, die beim Absetzen des Befehls aufgerufen wird, durch den die Richtlinie erstellt wird. Weitere Informationen hierzu finden Sie unter [IAM-Richtlinie in Befehlszeile zuweisen](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline); alternativ können Sie in der Befehlszeile den Befehl `ibmcloud iam -help` absetzen. Beachten Sie, dass hierfür die Installation der [IBM Cloud-Befehlszeilenschnittstelle](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use) erforderlich ist.
{:tip}

Gehen Sie wie folgt vor, um sicherzustellen, dass Sie über die erforderlichen Zugriffsrichtlinien zum Erstellen einer {{site.data.keyword.cfee_full_notm}}-Instanz verfügen:
1. Wechseln Sie zum Menü [**Verwalten > Konto > Benutzer**](https://console.bluemix.net/iam/#/users) im {{site.data.keyword.Bluemix_notm}}-Header, um die Seite **Identität & Zugriff** zu öffnen.
2. Klicken Sie auf der Registerkarte 'Zugriffsrichtlinien' auf den Benutzer, der die Umgebung erstellt, um die Zugriffsrichtlinien für diesen Benutzer zuzuweisen und anzuzeigen.

Weitere Informationen zum Verwalten der Benutzer und des Zugriffs in {{site.data.keyword.Bluemix}} sowie der Organisation von Benutzergruppen und Service-IDs zur Erleichterung der gleichzeitigen Zuweisung des Zugriffs für mehrere Benutzer finden Sie unter [Benutzer und Zugriff verwalten](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage).

### Festlegen der Berechtigungen zum Erstellen einer Umgebung in der Befehlszeilenschnittstelle beschleunigen
{: #permcli-creating}

Sie können das Einstellen der Berechtigungen zum Erstellen von CFEE-Instanzen mithilfe von `ibmcloud cfee create-permission-set` beschleunigen. Der Befehl ermöglicht es einem CFEE-Administrator, in einem einzigen Befehl die erforderlichen Zugriffsrichtlinien für die Erstellung einer CFEE-Instanz und aller zugehörigen Services zu konfigurieren. 

Mit dem Befehl werden die Berechtigungen für eine IAM-_Zugriffsgruppe_ festgelegt und ein Benutzer zu dieser _Zugriffsgruppe_ hinzugefügt. Der Administrator, der den Befehl absetzt, kann in den Befehl eine vorhandene _Zugriffsgruppe_ einschließen. Wenn keine _Zugriffsgruppe_ angegeben wird, wird automatisch die Standardgruppe _cfee-access-access-group_ erstellt.

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

Mit dem Befehl werden die folgenden Zugriffsrichtlinien für den Zielbenutzer festgelegt:

*  Editorrollen für den Cloud Object Storage-Service und CFEE-Service im aktuellen IBM Cloud-Konto.
*  Administratorrolle für den Kubernetes-Service im aktuellen IBM Cloud-Konto.
*  Entwicklerrolle für den aktuellen Bereich in der aktuellen Organisation für die Bereitstellung vom Compose for PostgreSQL.

Wenn Sie weitere Details zu diesem Befehl wünschen, setzen Sie folgenden Befehl ab:

```
cfee create-permission-set -help
```
{: pre}

Mit dem Befehl `ibmcloud cfee create-permission-get` können Sie die Zugriffsrichtlinien suchen oder überprüfen, die für einen Benutzer verfügbar sind:

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## Für die Arbeit mit einer Umgebung erforderliche Berechtigungen
{: #perm-working}

Damit ein Benutzer mit einer Instanz von {{site.data.keyword.cfee_full_notm}} arbeiten kann, muss er folgende Eigenschaften aufweisen:
1. Er muss Mitglied des {{site.data.keyword.Bluemix_notm}}-Kontos sein, in dem die {{site.data.keyword.cfee_full_notm}}-Instanz erstellt wurde.
2. Die folgenden IAM-_Zugriffsrichtlinien_ wurden vom Kontoadministrator erteilt (auf der Seite _Identity & Access_ unter dem Menü [**Verwalten > Konto > Benutzer**](https://console.bluemix.net/iam/#/users) im {{site.data.keyword.Bluemix_notm}}-Header können Sie Ihre aktuellen Kontozugriffsrichtlinien überprüfen):

    Alle Benutzer benötigen die Berechtigung _Anzeigeberechtigter_ oder eine höhere Berechtigung für die {{site.data.keyword.cfee_full_notm}}-Instanz in der Ressourcengruppe, in der die Umgebungsinstanz erstellt wurde. Die Zugriffsebene und -steuerung eines Benutzers in einer {{site.data.keyword.cfee_full_notm}}-Instanz hängt von der Rolle ab, die ihm in der Zugriffsrichtlinie gewährt wird:
  - Benutzer, denen die Rolle _Administrator_ oder _Editor_ zugeordnet ist, können Organisationen erstellen und Manager zu Organisationen und Bereichen zuordnen; außerdem verfügen Sie über die vollständigen Berechtigungen für alle Organisationen und Bereiche innerhalb der Umgebung und für die Ausführung von operativen Aktionen mithilfe der Cloud-Controller-API. Den Benutzern wird automatisch die Berechtigung für den Bereich _cloud_controller.admin_ im Bereich _Benutzerkonto und Authentifizierung_ von Cloud Foundry erteilt.
  - Benutzer mit der Rolle _Anzeigeberechtigter_ für eine CFEE-Instanz können diese im {{site.data.keyword.Bluemix_notm}}-Hauptdashboard in der Liste anzeigen und die zugehörige Benutzerschnittstelle öffnen. Der Zugriff der Benutzer auf bestimmte Organisationen und Bereiche innerhalb einer Umgebung hängt von den Rollen für die Organisation und Bereiche ab, die ihnen von den Managern dieser Organisationen und Bereiche zugeordnet wurden. Weitere Informationen finden Sie unter [Benutzer zu Organisationen hinzufügen](add-users.html).

     **Anmerkung:** Die Zugriffsberechtigung _Anzeigeberechtigter_ für die Ressourcengruppe, in der sich eine CFEE-Instanz befindet, ist alleine nicht ausreichend, damit die CFEE-Instanz dem Benutzer angezeigt wird. Ein Benutzer benötigt expliziten Zugriff auf die CFEE-Instanz (mit der Rolle eines Anzeigeberechtigtern oder höher), um dieser Instanz anzeigen zu können.

  - Benutzer benötigen die Rolle _Editor_ oder eine höhere Rolle für einen {{site.data.keyword.Bluemix_notm}}-Service, um eine Instanz dieses Service an eine in einem CFEE-Bereich bereitgestellte Anwendung zu **binden**.

  - Benutzer benötigen die Rolle _Editor_ oder eine höhere Rolle für eine CFEE-Instanz und die Rolle _Operator_ oder eine höhere Rolle für den Kubernetes-Cluster, in dem die CFEE-Instanz bereitgestellt wird, um **die CFEE-Instanz auf eine neue Version zu aktualisieren**.

  - Benutzer benötigen die Rolle _Administrator_ für eine CFEE-Instanz und die Rolle _Operator_ oder eine höhere Rolle für den Kubernetes-Cluster, in dem die CFEE-Instanz bereitgestellt wird, um für eine CFEE-Instanz **die Kapazität zu ändern** (Zellen hinzufügen oder entfernen).

