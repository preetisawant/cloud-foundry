---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# A propos d'{{site.data.keyword.cfee_full_notm}}
{: #creating}

Avec l'environnement {{site.data.keyword.cfee_full}} (CFEE), vous pouvez instancier plusieurs plateformes Cloud Foundry isolées à la demande au niveau de l'entreprise. Des instances du service {{site.data.keyword.Bluemix_notm}} Foundry Enterprise s'exécutent dans votre propre compte dans l'environnement {{site.data.keyword.Bluemix_notm}}. L'environnement est déployé sur du matériel isolé (clusters Kubernetes). Vous avez un contrôle total sur l'environnement, y compris le contrôle d'accès, la gestion de la capacité, la gestion des changements, la surveillance et les services.
{:shortdesc}

{{site.data.keyword.cfee_full}} est actuellement en phase bêta et vos commentaires sont les bienvenus. Pour commencer, créez votre propre instance {{site.data.keyword.cfee_full}} à [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create) et [demandez un accès](http://ibm.biz/cfee-forum-signup) au [forum IBM CFEE Slack](https://ibm-cfee.slack.com) pour partager vos commentaires, poser des questions et collaborer avec l'équipe du produit.
{:tip}

Pour que votre projet aboutisse, prenez le temps de planifier et concevoir les ressources dont vous avez besoin et les exigences de votre entreprise. Pour vous aider à démarrer, tenez compte des questions suivantes :

* Combien d'applications, et de quel type, allez-vous développer ?
* A quels services ces applications doivent-elles accéder ?
* Qui participe au processus de développement et quel est leur rôle ?
* Quel est le niveau d'isolement requis pour chaque phase du projet ?
* Les ressources d'infrastructure sont-elles fournies par votre entreprise ?
* De quelle manière votre société communique-t-elle ?
* Existe-t-il une norme de dénomination que vous pouvez implémenter pour identifier clairement l'utilisation de l'organisation et de l'espace ?

Lorsque vous déterminez le type d'environnement de cloud dont vous avez besoin, planifiez la structure de votre compte, de vos organisations, de vos espaces, de vos ressources et des membres de votre équipe.

Un seul compte {{site.data.keyword.Bluemix_notm}} suffit pour la plupart des organisations. Si votre organisation a plusieurs secteurs d'activité, vous pouvez créer un compte {{site.data.keyword.Bluemix_notm}} pour chaque secteur, par exemple, une compagnie bancaire de grande taille peut créer des comptes distincts pour le secteur de la vente au détail et le secteur commercial.

Le tableau suivant fournit un récapitulatif de certains des éléments clés.

| Elément   | Description |
|-----------|---------------|
| Compte IBM Cloud | Des instances CFEE sont créées sous un compte IBM Cloud spécifique, et sont disponibles pour les utilisateurs de ce compte en fonction des rôles et droits d'accès définis pour ces utilisateurs. |
|| Le compte sous lequel les instances CFEE sont créées doivent être des comptes Paiement à la carte ou Abonnement (pas des comptes d'essai). |
| CFEE | Service IBM Cloud Foundry Enterprise Environment d'hébergement des applications. |
|| Disponible dans le catalogue IBM Cloud. |
| Instance CFEE | Instance du service IBM Cloud Foundry Enterprise Environment créée sous un compte IBM Cloud par un utilisateur ayant le rôle d'administrateur ou d'éditeur sur ce compte. |
|| Un compte IBM Cloud peut contenir plusieurs instances CFEE. |
|| Peut avoir une ou plusieurs organisations. |
| Organisation | Inclut un ou plusieurs espaces. |
|| Inclut un ou plusieurs responsables d'organisation. |
|| Inclut un ou plusieurs membres d'équipe. Chaque membre d'équipe peut se voir accorder un ou plusieurs rôles. |
|| Les frais d'utilisation, générés par une application déployée dans un espace, sont signalés au niveau de l'organisation. |
| Espace | Inclut une ou plusieurs ressources. |
|| Inclut une ou plusieurs applications. |
|| Inclut un ou plusieurs responsables d'espace. |
|| Inclut un ou plusieurs membres d'équipe. Chaque utilisateur doit déjà être un membre d'équipe dans l'organisation propriétaire. Chaque membre d'équipe peut se voir accorder un ou plusieurs rôles. |
| Membre d'équipe | Peut être ajouté à une ou plusieurs organisations et à un ou plusieurs espaces sur différents comptes. |
|| Peut se voir accorder plusieurs rôles au sein d'une même organisation et/ou d'un même espace. |
| Alias de service | Alias d'une instance de service dans IBM Cloud. |
|| Permet aux développeurs de lier des instances de service existantes disponibles dans leur compte IBM Cloud à leurs applications déployées dans un espace au sein d'un environnement CFEE.|
{:caption="Tableau 1. Description des éléments clés" caption-side="top"}

