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

# Création d'organisations et d'espaces
{: #create_orgs}

Dans un environnement {{site.data.keyword.cfee_full}}, les applications sont limitées à des espaces spécifiques. Un espace existe lui-même au sein d'une organisation spécifique. Les membres d'une organisation se partagent un plan d'établissement des quotas, des applications, des instances de service et des domaines personnalisés. Une fois des organisations et espaces créés, des utilisateurs peuvent y être ajoutés avec des rôles spécifiques qui déterminent leur niveau d'accès et de contrôle dans ces organisations et espaces. Pour créer des organisations et affecter des responsables à ces organisations, vous devez détenir le rôle d'administrateur sur le service {{site.data.keyword.cfee_full_notm}} et sur l'instance d'environnement spécifique auxquels des utilisateurs sont ajoutés. Ces droits sont définis dans la page _Identité et accès_ du menu **Gérer > Utilisateurs** dans l'en-tête {{site.data.keyword.Bluemix}}.
{: shortdesc}

## Création d'organisations
{: #create-org}

Pour créer des organisations dans un environnement {{site.data.keyword.cfee_full_notm}} :

1. Accédez au [tableau de bord des environnements Cloud Foundry d'{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments){: new_window} et ouvrez l'environnement {{site.data.keyword.cfee_full_notm}} dans lequel vous voulez créer des organisations.
2. Dans l'interface utilisateur de l'environnement {{site.data.keyword.cfee_full_notm}}, accédez à l'entrée **Organisations** dans le panneau de navigation pour ouvrir la page _Organisations_.
3. Cliquez sur **Ajouter**.
4. Entrez un **Nom** pour la nouvelle organisation.
5. Sous **Responsables**, identifiez au moins un utilisateur. Seuls les utilisateurs ayant un rôle de responsable peuvent ajouter des membres à cette organisation.
6. Sous **Plan d'établissement des quotas**, sélectionnez un plan disponible. Un plan d'établissement des quotas limite la mémoire disponible pour les applications de l'organisation, le nombre maximum d'instances d'application hébergées et le nombre maximum de routes.

Outre la gestion de l'appartenance à une organisation, les responsables de l'organisation peuvent créer, afficher, éditer ou supprimer des espaces au sein de l'organisation. Les responsables de l'organisation peuvent également afficher le quota et l'utilisation de l'organisation, inviter des utilisateurs dans l'organisation, gérer les appartenances et les rôles dans l'organisation et gérer des domaines personnalisés pour l'organisation.

Pour créer des espaces au sein d'une organisation, dans la page _Organisations_, accédez à l'onglet **Espaces**, puis cliquez sur **Ajouter**. Les membres d'une organisation peuvent également créer et gérer leurs propres espaces au sein d'une organisation. Pour plus d'informations sur les rôles Cloud Foundry, voir [Accès Cloud Foundry](https://cloud.ibm.com/docs/iam/cfaccess.html#cfroles){: new_window}.

**Remarque** : pour accéder à des organisations et des espaces au sein d'un environnement {{site.data.keyword.cfee_full_notm}}, les utilisateurs doit détenir le droit d'accès à l'environnement lui-même. Sans droit d'accès à l'environnement {{site.data.keyword.cfee_full_notm}}, les utilisateurs ne peuvent pas accéder aux organisations et aux espaces de cet environnement, quels que soient leur appartenance et rôle dans ces organisations et espaces.
