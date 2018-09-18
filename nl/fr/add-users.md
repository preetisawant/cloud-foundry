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

# Ajout d'utilisateurs à des organisations et des espaces
{: #adding_users}

Les membres d'une organisation ayant un rôle de responsable peuvent ajouter des membres à cette organisation. Avant de pouvoir ajouter des utilisateurs à une organisation, ils doivent détenir au moins le rôle d'afficheur sur le service {{site.data.keyword.cfee_full}} et sur le groupe de ressources auquel appartient l'instance {{site.data.keyword.cfee_full_notm}}. Ces droits sont définis dans la page _Identité et accès_ sous **Gérer > Utilisateurs** dans l'en-tête {{site.data.keyword.Bluemix}}.

Pour ajouter des utilisateurs en tant que membres d'une organisation dans une instance {{site.data.keyword.cfee_full_notm}} :

1. Accédez à l'entrée **Organisations** dans le volet de navigation. Localisez l'organisation à laquelle vous voulez ajouter un membre. Accédez au menu _Actions_ dans la ligne du tableau, puis sélectionnez **Ajouter un membre**. Vous pouvez également cliquer sur l'organisation pour ouvrir sa page, accéder à l'onglet **Membres**, puis cliquer sur **Ajouter un membre**.
2. Dans la fenêtre _Ajouter un membre_, recherchez l'utilisateur à ajouter, sélectionnez un **Rôle d'organisation**, puis cliquez sur **Ajouter**.

**Remarque :** si vous prévoyez d'ajouter un utilisateur récemment invité dans votre compte {{site.data.keyword.Bluemix_notm}}, la reconnaissance de cet utilisateur dans la fenêtre d'ajout d'utilisateurs à une organisation ou à un espace peut prendre plusieurs minutes. Si l'utilisateur n'est pas reconnu lorsque vous entrez sont nom d'utilisateur, indiquez son adresse électronique et appuyez sur le signe plus (+) pour ajouter l'utilisateur.

Seuls les responsables d'espace (ou les responsables de l'organisation parent) peuvent ajouter des membres à un espace. Pour ajouter des utilisateurs en tant que membres à un espace d'une organisation dans une instance {{site.data.keyword.cfee_full_notm}} :

1. Accédez à l'entrée **Organisations** dans le volet de navigation, recherchez l'organisation dans laquelle se trouve l'espace cible, pus cliquez dessus pour ouvrir la page de l'organisation.
2. Dans la page de l'organisation, accédez à l'onglet **Espaces**.
3. Recherchez l'espace cible dans le tableau des espaces, accédez au menu _Actions_ dans la ligne du tableau, puis sélectionnez **Ajouter un membre**. Vous pouvez également cliquer sur l'espace cible dans le tableau pour ouvrir sa page, puis cliquer sur **Ajouter un membre**.
4. Dans la fenêtre _Ajouter un membre_, recherchez l'utilisateur à ajouter, sélectionnez un **Rôle d'espace**, puis cliquez sur **Ajouter**.

**Remarque** : les responsables d'organisation peuvent ajouter directement des membres à un espace sans les ajouter d'abord à l'organisation parent. Lorsqu'un responsable d'organisation ajoute des membres à un espace, ces membres intègrent également l'organisation parent.
