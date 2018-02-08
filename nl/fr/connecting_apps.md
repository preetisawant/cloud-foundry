---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# Gestion des connexions
{: #connect_app}

Vous pouvez connecter un service à une application {{site.data.keyword.Bluemix}} nouvelle ou existants depuis l'onglet **Connexions** du tableau de bord de votre service. La connexion d'un service Cloud Foundry à une application Cloud Foundry crée une liaison entre ces deux éléments et vous pouvez les dissocier, ajouter des connexions supplémentaires ou supprimer des connexions depuis l'onglet **Connexions**.

Toutefois, lorsque vous connectez une instance de service gérée par {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) à une application Cloud Foundry, un alias du service géré par IAM est automatiquement créé dans l'espace Cloud Foundry correspondant avec les informations de liaison que vous avez fournies. Cet alias est représenté comme une instance de service Cloud Foundry de votre service géré par IAM.
{:shortdesc}

## Qu'est-ce qu'un alias ?
{: #what_is_alias}

Un alias est une connexion entre votre service géré par IAM dans un groupe de ressources et une application Cloud Foundry dans une organisation ou un espace. Dans la console {{site.data.keyword.Bluemix_notm}}, la connexion (alias) est représentée comme une instance de service Cloud Foundry. Vous pouvez gérer votre alias en modifiant l'instance de service qui représente votre connexion.

Les alias sont comme des liens symboliques qui contiennent des références à des ressources distantes et qui activent l'interopérabilité et la réutilisation d'une instance sur l'ensemble de la plateforme. Par exemple, vous pouvez créer une instance d'un service dans un groupe de ressources, puis la réutiliser à partir de n'importe quelle région Cloud Foundry disponible en créant un alias dans une organisation ou un espace de ces régions.

Les règles suivantes s'appliquent aux alias :

* Un alias ne génère pas de coût supplémentaire, mais chaque alias est décompté de votre quota dans votre organisation Cloud Foundry.
* Vous ne pouvez créer qu'un seul alias par espace Cloud Foundry dans la console {{site.data.keyword.Bluemix_notm}}. Mais vous pouvez cependant créer plusieurs alias par espace à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [Commandes de gestion des groupes de ressources et des ressources](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources).
* Vous pouvez créer plusieurs connexions entre votre service géré par IAM et toute application Cloud Foundry de n'importe quel espace, organisation et région dans le même compte si vous disposez du droit requis
* Toutes les connexions établies dans le même espace vers différentes applications Cloud Foundry à partir d'une instance de service gérée par IAM utilisent le même alias.
* La suppression de la liaison d'une instance de service gérée par IAM *ne supprime pas* l'instance de service Cloud Foundry qui représente l'alias.
* La suppression de l'application Cloud Foundry à laquelle votre instance de service gérée par IAM est connecté *ne supprime pas* l'instance Cloud Foundry qui représente l'alias.
* La suppression d'une instance de service gérée par IAM *supprime* l'instance de service Cloud Foundry qui représente l'alias.

## Création d'une connexion (alias) entre un service géré par IAM et une application Cloud Foundry
{: #creating_alias}

Pour connecter votre instance de service gérée par IAM à une application Cloud Foundry :

1. Accédez à votre tableau de bord.

2. Cliquez sur le nom de votre application pour ouvrir la vue des détails d'application.

3. Cliquez sur **Connecter un existant**, puis sélectionner votre application Cloud Foundry existante. Ou cliquez sur **Créer une connexion** pour créer une application Cloud Foundry à laquelle se connecter.

4. Spécifiez le **Rôle d'accès pour la connexion**. Cette valeur définit le rôle d'accès du service IAM. Pour plus d'informations, voir [Accès IAM](/docs/iam/users_roles.html#userroles).

5. Facultatif : vous pouvez renseigner la zone **ID de service pour la connexion** soit en autorisant IAM à générer automatiquement une valeur unique, soit en fournissant l'ID d'un service existant. Pour plus d'informations, voir [Création et gestion des ID de service](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids).

6. Cliquez sur **Créer**.

## Affichage d'un alias

Une fois que vous avez créé une connexion entre un service géré par IAM et une application Cloud Foundry, l'alias est affiché dans l'onglet **Connexions** de l'application Cloud Foundry connectée. De plus, l'alias est affiché en tant qu'instance de service Cloud Foundry en cours d'exécution sur votre tableau de bord et ne contient un onglet **Connexions** que lorsque vous l'ouvrez.

1. Accédez à votre tableau de bord.
2. Dans la table **Services Cloud Foundry**, cliquez sur le nom de l'instance de service pour ouvrir la vue des détails du service. Si elle ne contient qu'un onglet **Connexions**, il s'agit d'un alias.

## Suppression d'un alias

La manière la plus simple de supprimer un alias est de supprimer l'instance de service gérée par IAM. Vous pouvez toutefois conserver l'instance de service gérée par IAM et supprimer directement l'alias.

1. Accédez à votre tableau de bord.
2. Dans la table **Services Cloud Foundry**, cliquez sur le nom de l'instance de service pour ouvrir la vue des détails du service. Si elle ne contient qu'un onglet **Connexions**, il s'agit d'un alias.
3. Supprimez l'instance.

## Création d'une connexion entre plusieurs services Cloud Foundry
{: #cf}

Pour plus de détails sur la liaison d'un service Cloud Foundry à un autre service Cloud Foundry, voir [Utilisation des services dans un autre service](../apps/reqnsi.html#add_service).
