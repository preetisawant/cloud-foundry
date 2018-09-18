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

# Création et affichage d'instances de service
{: #creating-services}

Les applications déployées dans un environnement {{site.data.keyword.cfee_full_notm}} peuvent être liées à deux types d'instances de service :
1. Les instances de service gérées par un courtier de services Cloud Foundry local (local pour l'environnement CFEE). Ces instances peuvent elles-mêmes être de deux types :
   *  1a. Instance d'une offre de service créée depuis la place du marché Cloud Foundry de l'instance {{site.data.keyword.cfee_full_notm}} en cours. Ce type d'instance de service nécessite qu'un courtier de services enregistré soit disponible dans l'environnement. Un courtier de services affiche un catalogue des plans et offres de services, et permet de créer, supprimer, lier et délier des instances depuis ces offres de services. Pour plus d'informations, voir [Gestion des courtiers de services](https://docs.cloudfoundry.org/services/managing-service-brokers.html) dans la documentation Cloud Foundry.
   * 1b. Instance de service fournie par l'utilisateur. La création de ce type d'instance est prise en charge par le biais de l'interface de ligne de commande, et non via l'interface utilisateur. Les instances de service fournies par l'utilisateur sont néanmoins répertoriées dans l'interface utilisateur.
2. Les instances de service public créées à partir du catalogue {{site.data.keyword.Bluemix}} et disponibles dans le compte {{site.data.keyword.Bluemix}}.
Les instances de service public disponibles dans le compte {{site.data.keyword.Bluemix}} ne peuvent pas en tant que telles être disponibles pour les environnements CFEE. Pour qu'une instance de service public (disponible dans le compte {{site.data.keyword.Bluemix}}) soit disponible pour les espaces d'un environnement CFEE, vous devez créer un alias d'instance de service dans l'espace CFEE cible. L'alias fonctionne comme une référence à l'instance de service public réelle. Une fois l'alias de service créé dans un espace CFEE, il peut être lié à des applications de cet environnement CFEE. La création d'alias de service permet aux développeurs d'optimiser le vaste catalogue des services {{site.data.keyword.Bluemix}} dans leurs applications déployées dans des environnements CFEE.


## Création et affichage d'alias de service dans un espace CFEE
{: #creating-services_inspace}

Un alias d'une instance de service public existante disponible dans votre compte IBM Cloud vous permet de lier cette instance de service à des applications déployées dans un espace CFEE. La création d'un alias pour une instance de service {{site.data.keyword.Bluemix_notm}} existante nécessite de disposer d'un accès utilisateur à l'instance elle-même. Pour plus d'informations, voir la page Identité et accès du menu **Gérer > Utilisateurs** dans l'en-tête {{site.data.keyword.Bluemix_notm}} pour vérifier vos règles d'accès au compte en cours.

Pour créer un alias d'instance de service dans un espace d'un environnement CFEE :

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, recherchez l'environnement CFEE qui héberge votre application.
2. Accédez à **Organisations** dans le volet de navigation et ouvrez l'organisation et l'espace où se trouve l'application.
3. Accédez à l'onglet **Espaces** et recherchez l'espace qui contient l'application.
4. Dans la page de l'espace cible, accédez à l'onglet **Services**, puis cliquez sur **Créer un service**. La page **Catalogue** de l'environnement {{site.data.keyword.cfee_full_notm}} s'ouvre. Cette page répertorie les offres de services de deux sources (voir la colonne _Source_) :
   * Offres du catalogue IBM Cloud.
   * Offres de la place du marché {{site.data.keyword.cfee_full_notm}} local.
5. Recherchez et sélectionnez une offre de services disponible que vous voulez instancier.
6. Selon la source de l'offre de services (IBM Cloud ou environnement CFEE local) procédez de l'une des manières suivantes :
   * **Continuez** jusqu'à la page de création d'offre de services IBM Cloud où vous indiquez le nom de la nouvelle instance de service, la région, le plan et d'autres propriétés requises pour créer le service dans IBM Cloud.  Dès que vous cliquez sur *Créer*, l'instance de service est créée dans IBM Cloud. De plus, un alias de cette instance de service est créé dans l'environnement {{site.data.keyword.cfee_full_notm}}. L'alias sera disponible pour liaison à des applications de l'environnement {{site.data.keyword.cfee_full_notm}}.
   **Remarque :** lors de la création d'un {{site.data.keyword.Bluemix_notm}} de cette manière, outre la création d'une instance de service public disponible pour les utilisateurs dans le compte IBM Cloud, un alias de cette instance de service est créé dans l'environnement {{site.data.keyword.cfee_full_notm}} à partir duquel l'instance a été créée.
   * **Créez** l'instance de service dans la place du marché Cloud Foundry local. Une boîte de dialogue dans laquelle vous indiquez le plan et le nom de la nouvelle instance de service s'ouvre. Lorsque vous cliquez sur *Créer*, l'instance de service est créée dans l'environnement {{site.data.keyword.cfee_full_notm}} et disponible pour liaison à des applications dans l'environnement {{site.data.keyword.cfee_full_notm}}.

Une fois l'instance de service créée, l'instance (si elle a été créée dans la place du marché Cloud Foundry local) ou son alias (si elle a été créée à partir du catalogue IBM Cloud) est répertorié dans l'onglet **Services**.


## Création et affichage des alias de service dans tous les environnements CFEE dans le tableau de bord Cloud Foundry global
{: #creating-services_across}

Vous pouvez afficher une vue d'ensemble de tous les alias d'instance de service (de toutes les instances CFEE) dans le tableau de bord Cloud Foundry global.

1. Cliquez sur l'icône de menu ![Vérification du compte](img/HamburgerMenu.png "Capture d'écran de l'icône de menu") > **Cloud Foundry** pour ouvrir le tableau de bord Cloud Foundry.
2. Cliquez sur **Enterprise > Services** dans le volet de navigation de gauche.
Le tableau de la vue affiche les informations suivantes :

| Elément   | Description |
|-----------|---------------|
| Alias de service | Nom de l'alias de l'instance de service. |
| Instance de service | Instance de service IBM Cloud public à partir de laquelle l'alias est créé. |
| Offre | Offre de service issue du catalogue IBM Cloud où l'instance de service a été créée. |
| CFEE | Environnement {{site.data.keyword.cfee_full}} où réside l'alias. |
| Organisation | Organisation de l'instance CFEE où réside l'alias. |
| Espace | Espace dans l'organisation de l'instance CFEE où réside l'alias. |
{:caption="Tableau 1. Description des éléments clés" caption-side="top"}

Dans cette vue, vous pouvez effectuer les actions suivantes :
* Trier les éléments du tableau selon n'importe laquelle des propriétés affichées sous forme de colonnes de tableau.
* Lier des applications à un alias spécifique en accédant au menu déroulant dynamique des alias situé tout à fait à droite de la ligne.
* Développer un alias (ligne) afin de visualiser toutes les applications liées à cet alias.
* Démarrer et arrêter des applications en accédant au menu déroulant dynamique des applications de l'alias situé tout à fait à droite de la ligne.
* Accéder à un environnement, une organisation ou un espace CFEE en cliquant sur le lien à l'environnement, organisation ou espace CFEE correspondant.

Pour créer un alias de service à partir du tableau de bord Cloud Foundry global :
1. Cliquez sur le bouton **Créer un alias de service** en haut de la page. La boîte de dialogue _Créer un alias de service_ s'ouvre. Elle répertorie toutes les instances de service public disponibles dans le compte IBM Cloud en cours.
2. Sélectionnez l'une des instances de service public.
3. Cliquez sur **Créer**. Une fois créé, le nouvel alias d'instance de service est ajouté à la liste.
L'alias de service s'affiche également dans la liste des services de l'espace CFEE, où il peut être lié à des applications dans cet espace (CFEE > Organisations > Espace > Services).


