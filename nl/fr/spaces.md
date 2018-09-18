---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Détermination de vos espaces
{: #determinespaces}

Au sein d'une organisation, les espaces fournissent un niveau supplémentaire d'application de limites et d'abstraction.

Un espace est une zone réservée dans l'organisation où les utilisateurs peuvent développer et exécuter des applications et des services. Vous pouvez créer autant d'espaces que nécessaire dans une organisation et définir les utilisateurs pouvant accéder à un espace. Voir [Espaces](/docs/account/orgs_spaces.html#orgsspacesusers) pour plus de détails.

Si vous prévoyez de définir un grand nombre d'espaces, vous souhaiterez peut-être créer une application dédiée à la gestion des espaces. Pour plus de soixante espaces, vous pouvez envisager de définir une autre organisation.

## Espaces pour une organisation unique/pour plusieurs organisations
{: #spaceconsiderations}

Lorsque vous adoptez une architecture à organisation unique, le niveau de séparation et d'abstraction est fourni par les espaces que vous définissez dans l'organisation. Tenez compte des conseils suivants lorsque vous définissez des espaces :

* Définissez un espace qui héberge un service nécessitant une seule mise à disposition et une seule configuration dans l'organisation.
* Définissez des espaces basés sur le cycle de vie de distribution.
  Par exemple, vous pouvez définir un ou plusieurs espaces pour des applications en cours de développement, un ou plusieurs espaces pour des applications en phase de test et un ou plusieurs espaces pour des applications en production.
* Si les limites du cycle de vie de distribution ne sont pas suffisantes, vous pouvez obtenir davantage de séparation en définissant un ou plusieurs espaces par secteur d'activité et par phase de distribution.
* Déterminez si vous devez appliquer des limites pour différents groupes d'utilisateurs.
  Par exemple, vos développeurs ne peuvent pas développer l'application et la tester. Vous avez besoin d'un autre groupe d'utilisateurs pour tester l'application. Dans ce scénario, vous créez deux espaces, un pour les développeurs de l'application et l'autre pour les testeurs de l'application. Ensuite, accordez à chaque groupe d'utilisateurs des droits d'accès à l'espace approprié.

Lorsque vous implémentez une architecture avec plusieurs organisations, vous pouvez séparer chaque organisation par secteur d'activité et/ou cycle de vie de distribution. Vous pouvez ensuite définir plusieurs espaces basés sur le nombre d'applications ou de projets fournis par le même service de la société. Tenez compte des conseils suivants lorsque vous planifiez les espaces d'une organisation :

* Définissez un espace qui héberge un service nécessitant une seule mise à disposition et une seule configuration dans l'organisation.
* Définissez un espace par application, par groupe d'applications connexes ou pour un projet spécifique.
* Si vous devez appliquer des limites pour différents utilisateurs, définissez un espace pour chaque groupe d'utilisateurs. Lorsqu'un utilisateur se voit accorder un rôle de développeur dans un espace, il dispose d'un accès complet aux ressources et aux services {{site.data.keyword.Bluemix_notm}} mis à disposition et qui s'exécutent dans cet espace. Lorsque vous devez appliquer une sécurité renforcée pour empêcher les utilisateurs de contrôler chaque ressource, pensez à définir différents espaces. Au sein de chacun de ces espaces, vous pouvez mettre à disposition des services {{site.data.keyword.Bluemix_notm}} qui sont utilisés par les applications qui s'exécutent dans cet espace.

## Attribution d'un nom à un espace, restrictions et gestion
{: #spaceadmin}

Lorsque vous définissez les différents espaces de votre organisation en cloud, tenez compte des conseils suivants :

* Définissez et appliquez une convention de dénomination. Par exemple, définissez une convention de dénomination dans laquelle le nom de l'espace inclut des informations sur l'emplacement de l'organisation et le type de cloud. Vous pouvez modifier le nom d'un espace après l'avoir créé. Si le nom d'un espace est modifié, prévenez tous les membres d'équipe de l'espace de cette modification.
* Définissez les restrictions qui s'appliquent à l'espace. Par exemple, définissez le type d'application qui peut être développé, géré et déployé dans chaque espace.
* Identifiez le responsable de l'espace. Vous souhaiterez peut-être déléguer l'administration de l'espace à plusieurs personnes.
