---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Audit et journalisation
{: #auditing-logging}

Les fonctions d'audit et de journalisation d'{{site.data.keyword.cfee_full}} (CFEE) permettent aux administrateurs de réaliser des audits sur des événements qui se produisent dans une instance CFEE et aux développeurs de suivre des événements de journal générés à partir de leurs applications Cloud Foundry.

Les fonctions d'audit et de journalisation de CFEE sont prises en charge via l'intégration des services IBM Cloud Log Analysis et Activity Tracker.

## Audit
{: #auditing}

La fonction d'audit permet aux administrateurs CFEE de suivre les activités Cloud Foundry auditables qui se produisent dans une instance CFEE.  Ces activités sont notamment la connexion, la création d'organisations et d'espaces, les affectations d'appartenance et de rôle utilisateur, les déploiements d'application, les liaisons de service et la configuration de domaine. La fonction d'audit est prise en charge via l'intégration au service Activity Tracker dans IBM Cloud. Une instance du service Activity Tracker sélectionné par l'administrateur CFEE est configurée automatiquement pour recevoir des événements qui représentent des actions réalisées dans Cloud Foundry et sur le plan de contrôle CFEE.  L'utilisateur peut voir et gérer ces événements dans l'interface utilisateur de l'instance de service Activity Tracker.

Pour activer la fonction d'audit pour une instance CFEE :

1. Ouvrez l'interface utilisateur d'un environnement CFEE et accédez à l'entrée **Opérations > Audit** dans le panneau de navigation de gauche pour ouvrir la page de journalisation.
2. Cliquez sur **Activer l'audit** et sélectionnez l'une des **instances Activity Tracker** disponibles dans le compte IBM Cloud.  Si aucune instance n'est disponible, une option est affichée pour l'utilisateur afin de lui permettre de créer une nouvelle instance Activity Tracker dans le catalogue IBM Cloud.
3.  Une fois la fonction d'audit activée, les détails de la configuration s'affichent sur la page. Il s'agit notamment du statut de la configuration et d'un lien vers l'instance de service Activity Tracker proprement dite, à laquelle l'utilisateur peut accéder pour voir et gérer les événements d'audit.

Vous pouvez désactiver la fonction d'audit en cliquant sur **Désactiver l'audit**, ce qui aura pour conséquence de retirer l'instance de service Activity tracker que vous avez préalablement ajoutée et configurée. Cette action ne supprimera pas l'instance de service Activity Tracker.

## Persistance de journalisation
{: #logging}

La fonction de journalisation des événements Cloud Foundry est prise en charge via l'intégration au service Log Analysis dans IBM Cloud. Une instance du service Log Analysis sélectionné par l'administrateur CFEE est configurée automatiquement pour recevoir et conserver des événements de journalisation Cloud Foundry générés à partir de l'instance CFEE.  L'utilisateur peut voir et gérer ces événements de journalisation dans l'interface utilisateur de l'instance de service Log Analysis.

Pour activer la journalisation pour une instance CFEE :

1. Assurez-vous que vous possédez une [règle d'accès IAM](https://cloud.ibm.com/iam/#/users) qui vous affecte le rôle Editeur, Opérateur ou Administrateur sur l'instance de service Log Analysis dans laquelle vous souhaitez conserver les événements de journalisation.
2. Ouvrez l'interface utilisateur d'un environnement CFEE et accédez à l'entrée **Opérations > Journalisation** dans le panneau de navigation de gauche pour ouvrir la page de journalisation.
3. Cliquez sur **Activer la persistance** et sélectionnez l'une des **instances Log Analysis** disponibles dans le compte IBM Cloud.  Si aucune instance n'est disponible, une option est affichée pour l'utilisateur afin de lui permettre de créer une instance dans le catalogue IBM Cloud.
4. Une fois la persistance de journalisation activée, les détails de la configuration s'affichent sur la page. Il s'agit notamment du statut de la configuration et d'un lien vers l'instance de service Log Analysis proprement dite, à laquelle l'utilisateur peut accéder pour voir et gérer les événements de journalisation.

**Avertissement :** l'activation de la persistance de journalisation requiert un redémarrage avec interruption des cellules et du plan de contrôle CFEE.  Lors du redémarrage, toutes les fonctionnalités d'administration seront disponibles, mais certains services et applications exécutés dans cette instance CFEE risquent de ne pas l'être.  Le statut des composants CFEE sera indiqué sur la page Diagnostic d'intégrité lors du redémarrage.  Le redémarrage prend environ 20 minutes.

Vous pouvez désactiver la persistance de journalisation en cliquant sur **Désactiver la persistance de journalisation**, ce qui aura pour conséquence de retirer l'instance de service Activity tracker que vous avez préalablement ajoutée et configurée. Cette action ne supprimera pas l'instance de service Log Analysis.

**Remarque :** lorsque vous désactivez la persistance de journalisation, les événements de journalisation Cloud Foundry sont tout de même générés, simplement, ils ne sont pas conservés en dehors de l'instance CFEE.
