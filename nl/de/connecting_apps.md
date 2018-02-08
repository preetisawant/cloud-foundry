---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# Verbindungen verwalten
{: #connect_app}

Sie können einen Service über die Registerkarte **Verbindungen** in Ihrem Service-Dashboard mit einer vorhandenen oder neuen {{site.data.keyword.Bluemix}}-Anwendung verbinden. Wenn Sie einen Cloud Foundry-Service mit einer Cloud Foundry-Anwendung verbinden, entsteht eine Bindung zwischen ihnen. Sie können die Bindung aufheben, zusätzliche Verbindungen hinzufügen oder Verbindungen über die Registerkarte **Verbindungen** löschen.

Wenn Sie jedoch eine Serviceinstanz, die von {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) verwaltet wird, mit einer Cloud Foundry-Anwendung verbinden, wird automatisch ein Aliasname des Service, der von IAM verwaltet wird, in dem entsprechenden Cloud Foundry-Bereich mit den von Ihnen angegebenen Bindungsinformationen erstellt. Dieser Aliasname wird als Cloud Foundry-Serviceinstanz Ihres IAM-verwalteten Service dargestellt.
{:shortdesc}

## Was ist ein Aliasname?
{: #what_is_alias}

Ein Aliasname ist eine Verbindung zwischen Ihrem IAM-verwalteten Service in einer Ressourcengruppe und einer Cloud Foundry-Anwendung in einer Organisation oder einem Bereich. In der {{site.data.keyword.Bluemix_notm}}-Konsole wird die Verbindung (Aliasname) als Cloud Foundry-Serviceinstanz dargestellt. Sie können Ihren Aliasnamen verwalten, indem Sie die Serviceinstanz ändern, die Ihre Verbindung darstellt.

Aliasnamen sind wie symbolische Verbindungen (Symlinks), die Verweise auf ferne Ressourcen enthalten und die Interoperabilität und die Wiederverwendung einer Instanz auf der gesamten Plattform ermöglichen. Sie können beispielsweise eine Instanz eines Service in einer Ressourcengruppe erstellen und sie anschließend aus allen verfügbaren Cloud Foundry-Regionen wiederverwenden, indem Sie einen Aliasnamen in einer Organisation oder einem Bereich in diesen Regionen erstellen.

Die folgenden Regeln gelten für Aliasnamen:

* Es wird keine zusätzliche Gebühr für einen Aliasnamen erhoben, aber jeder Aliasname wird auf das Kontingent in Ihrer Cloud Foundry-Organisation angerechnet.
* Sie können pro Cloud Foundry-Bereich in der {{site.data.keyword.Bluemix_notm}}-Konsole nur einen Aliasnamen erstellen. Es kann jedoch mehr als ein Aliasname pro Bereich mit der {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle erstellt werden. Weitere Informationen finden Sie unter [Befehle zum Verwalten von Ressourcengruppen und Ressourcen](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources).
* Sie können mehrere Verbindungen zwischen Ihrem IAM-verwalteten Service und einer beliebigen Cloud Foundry-Anwendung in einem Bereich, einer Organisation und einer Region in demselben Konto erstellen, wenn Sie dazu berechtigt sind.
* Mehrere Verbindungen, die in demselben Bereich zu verschiedenen Cloud Foundry-Anwendungen von einer IAM-verwalteten Serviceinstanz hergestellt wurden, verwenden denselben Aliasnamen.
* Wenn Sie die Bindung einer IAM-verwalteten Serviceinstanz aufheben, wird die Cloud Foundry-Serviceinstanz, die den Aliasnamen darstellt, *nicht* gelöscht.
* Wenn Sie die Cloud Foundry-Anwendung löschen, mit der Ihre IAM-verwaltete Serviceinstanz verbunden ist, wird die Cloud Foundry-Instanz, die den Aliasnamen darstellt, *nicht* gelöscht.
* Wenn Sie eine IAM-verwaltete Serviceinstanz löschen, *wird* die Cloud Foundry-Serviceinstanz gelöscht, die den Aliasnamen darstellt.

## Verbindung (Aliasname) zwischen einem IAM-verwalteten Service und einer Cloud Foundry-App herstellen
{: #creating_alias}

Gehen Sie wie folgt vor, um Ihre IAM-verwaltete Serviceinstanz mit einer Cloud Foundry-Anwendung zu verbinden:

1. Rufen Sie Ihr Dashboard auf.

2. Klicken Sie auf den Namen Ihrer App, um die App-Detailansicht zu öffnen.

3. Klicken Sie auf **Vorhandenen verbinden** und treffen Sie bei Ihrer vorhandenen Cloud Foundry-App eine Auswahl. Oder klicken Sie auf **Verbindung erstellen**, um eine Cloud Foundry-App zu erstellen, zu der eine Verbindung hergestellt werden soll.

4. Geben Sie die **Zugriffsrolle für Verbindung** an. Dieser Wert legt die Zugriffsrolle des IAM-Service fest. Weitere Informationen finden Sie unter [IAM-Zugriff](/docs/iam/users_roles.html#userroles).

5. Optional können Sie eine **Service-ID für Verbindung** bereitstellen, indem Sie IAM einen eindeutigen Wert generieren lassen oder indem Sie eine vorhandene Service-ID bereitstellen. Weitere Informationen finden Sie unter [Service-IDs erstellen und verwalten](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids).

6. Klicken Sie auf **Erstellen**.

## Aliasnamen anzeigen

Nachdem Sie eine Verbindung zwischen einem IAM-verwalteten Service und einer Cloud Foundry-App erstellt haben, wird der Aliasname auf der Registerkarte **Verbindungen** der verbundenen Cloud Foundry-App angezeigt. Darüber hinaus wird der Aliasname als aktive Cloud Foundry-Serviceinstanz in Ihrem Dashboard angezeigt und enthält nur dann eine Registerkarte **Verbindungen**, wenn Sie sie öffnen.

1. Rufen Sie Ihr Dashboard auf.
2. Klicken Sie in der Tabelle **Cloud Foundry-Services** auf den Namen der Serviceinstanz, um die Ansicht mit den Servicedetails zu öffnen. Wenn nur eine Registerkarte **Verbindungen** enthalten ist, handelt es sich um einen Aliasnamen.

## Aliasnamen löschen

Am einfachsten lässt sich der Aliasnamen löschen, indem Sie die IAM-verwaltete Serviceinstanz löschen. Sie können Ihre IAM-verwaltete Serviceinstanz aber auch beibehalten und den Aliasnamen direkt löschen.

1. Rufen Sie Ihr Dashboard auf.
2. Klicken Sie in der Tabelle **Cloud Foundry-Services** auf den Namen der Serviceinstanz, um die Ansicht mit den Servicedetails zu öffnen. Wenn nur eine Registerkarte **Verbindungen** enthalten ist, handelt es sich um einen Aliasnamen.
3. Löschen Sie die Instanz.

## Verbindung zwischen mehreren Cloud Foundry-Services erstellen
{: #cf}

Weitere Informationen zum Binden eines Cloud Foundry-Service an einen anderen Cloud Foundry-Service finden Sie unter [Services in einem anderen Service verwenden](../apps/reqnsi.html#add_service).
