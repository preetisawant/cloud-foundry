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

# Affectation de rôles
{: #roles}

Vous pouvez accorder plusieurs rôles à des membres d'équipe dans un compte {{site.data.keyword.Bluemix_notm}}. Ces rôles définissent les droits d'accès dont dispose l'utilisateur pour gérer les ressources de l'organisation et du compte : vous pouvez accorder des [rôles utilisateur](/docs/iam/users_roles.html#userroles) à des membres d'une organisation. Ces rôles définissent le niveau d'accès au sein de l'organisation et limitent les personnes habilitées à accéder à un espace et à ses ressources. Par exemple, vous pouvez accorder aux utilisateurs différents droits d'accès sur différents espaces.

## Propriétaire de compte
{: #accountowner}

Lorsque vous concevez une architecture avec plusieurs organisations ou une architecture à organisation unique, le propriétaire de compte est le superutilisateur de l'environnement de cloud.

Les principales tâches du propriétaire de compte sont les suivantes :

* Gérer les ressources du compte global
* Créer des organisations
* Ajouter des membres d'équipe au compte

Le propriétaire du compte peut également ajouter un ou plusieurs utilisateurs en tant que responsables d'une organisation en affectant à ces utilisateurs le rôle **Responsable**. Envisagez d'ajouter deux utilisateurs en tant que responsables de l'organisation. Le premier utilisateur joue le rôle de responsable principal de l'organisation. Le second utilisateur joue le rôle de responsable adjoint et agit si le responsable principal n'est pas disponible.

## Rôles utilisateur
{: #userroles}

Les rôles utilisateur définissent les droits d'accès que vous pouvez affecter à un membre d'équipe dans une organisation et spécifient le niveau d'accès d'un membre d'équipe au sein de l'organisation et de chaque espace.

Dans une architecture avec plusieurs organisations ou dans une architecture à organisation unique, définissez les membres d'équipe et les droits d'accès dont chaque utilisateur a besoin pour pouvoir effectuer pour son travail :

1. Identifiez le groupe d'utilisateurs qui a besoin d'accéder à une organisation.
2. Définissez les droits d'accès pour chaque membre d'équipe dans l'organisation et dans un espace de l'organisation.
3. Sélectionnez le rôle qui accorde à un utilisateur les droits d'accès dont il a besoin.

   * Responsable de l'organisation
   * Auditeur de l'organisation
   * Responsable de la facturation de l'organisation
   * Responsable de l'espace
   * Développeur de l'espace
   * Auditeur de l'espace

### Responsable de l'organisation
{: #bporgmgr}

Le responsable de l'organisation est notamment chargé de créer des espaces, de distribuer le quota entre les espaces, d'inviter les membres d'équipe, et éventuellement de leur accorder des rôles spécifiques, et de définir des domaines personnalisés.

### Auditeur de l'organisation
{: #bporgauditor}

Les membres d'équipe dotés du rôle **Auditeur** de l'organisation peuvent surveiller le quota, l'utilisation des ressources et les membres d'équipe pour tous les espaces de l'organisation.
Les auditeurs peuvent ensuite générer un rapport sur l'efficience de l'organisation et mettre en évidence les problèmes potentiels.

* Lorsque vous adoptez une architecture avec plusieurs organisations, vous avez la possibilité d'accorder le rôle Auditeur aux mêmes membres d'équipe dans chacune des organisations associées au compte.
Cela permet aux membres d'équipe de surveiller le quota dans toutes les organisations de votre environnement de cloud et de disposer d'une vue globale du compte.
* Lorsque vous adoptez une architecture à organisation unique, vous accordez le rôle Auditeur aux membres d'équipe et vous les chargez de surveiller l'utilisation du quota et l'efficience globale de l'organisation.

### Responsable de la facturation de l'organisation
{: #bporgbillingmgr}

Les membres d'équipe dotés du rôle **Responsable de la facturation** de l'organisation peuvent surveiller les coûts de l'organisation.

* Lorsque vous adoptez une architecture avec plusieurs organisations, vous avez la possibilité d'accorder le rôle Responsable de la facturation aux mêmes membres d'équipe dans chacune des organisations associées au compte. Cela permet à ces membres d'équipe de surveiller le coût de chaque organisation et de disposer d'une vue globale du compte.
* Dans une architecture à organisation unique, identifiez les utilisateurs chargés de surveiller le coût.

### Responsable de l'espace
{: #bpspacemgr}

Le **responsable de l'espace** est responsable de l'ensemble du travail effectué dans l'espace dont il assure la gestion et le contrôle. Le responsable d'espace peut également effectuer les tâches suivantes :

* Surveiller le quota alloué à l'espace
* Demander des ressources supplémentaires au responsable de l'organisation
* Prévenir le responsable de l'organisation que des ressources ne sont pas requises
* Ajouter à l'espace des membres d'équipe dotés du rôle **Développeur**
* Le cas échéant, affecter le rôle **Responsable** de l'espace à un membre d'équipe pour permettre à celui-ci d'agir en tant que responsable d'espace adjoint en son absence

### Développeur de l'espace
{: #bpspacedev}

Un développeur de l'espace peut effectuer les tâches suivantes :

* Gérer les applications Cloud Foundry
* Mettre à disposition et configurer les services {{site.data.keyword.Bluemix_notm}}
* Associer des domaines à des applications

### Auditeur de l'espace
{: #bpspaceauditor}

Pour chaque espace, vous avez la possibilité d'accorder le rôle **Auditeur** de l'espace aux membres d'équipe qui disposent du rôle **Auditeur** de l'organisation. Dans votre entreprise, ce rôle devra peut-être être accordé à un groupe d'utilisateurs spécifique.

