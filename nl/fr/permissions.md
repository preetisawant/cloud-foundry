---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Droits
{: #permissions}

Avant de commencer à créer et à utiliser des instances de service {{site.data.keyword.cfee_full}}, vous devez définir correctement les droits de l'administrateur et des autres membres de l'équipe.

## Droits requis pour créer un nouvel environnement
{: #perm-creating}

Pour créer de nouvelles instances de service {{site.data.keyword.cfee_full_notm}}, l'administrateur du compte où l'instance doit être créée doit accorder des règles d'accès aux utilisateurs, à savoir :

* Accès à au moins un groupe de ressources du compte {{site.data.keyword.Bluemix}}. Les groupes de ressources permettent d'organiser les ressources en regroupements personnalisés afin de faciliter le contrôle d'accès à ces ressources. Vous êtes invité à désigner un groupe de ressources lorsque vous créez une nouvelle instance d'environnement.

* Rôle d'administrateur ou d'éditeur sur le service {{site.data.keyword.cfee_full_notm}} dans le groupe de ressources auquel l'environnement est affecté. Les utilisateurs dotés du rôle d'administrateur ou d'éditeur sur le service {{site.data.keyword.cfee_full_notm}} peuvent créer et supprimer un environnement. Mais seuls les utilisateurs dotés d'un rôle d'administration peuvent affecter des utilisateurs à une instance {{site.data.keyword.cfee_full_notm}} ou modifier les rôles affectés aux utilisateurs dans cette instance.

* Rôle d'administrateur ou d'éditeur sur le service IBM Cloud Object Storage, qui est une dépendance requise du service CFEE. Une instance de service IBM Cloud Object Storage est utilisée pour stocker les données générées lors de la création de vos conteneurs d'applications ICFEE (par exemple, packages d'applications téléchargés, packs de construction et exécutables compilés).

* Une instance de service Compose for PostgreSQL, qui est une dépendance requise du service CFEE. Compose for PostgreSQL est utilisé pour stocker des données Cloud Foundry sur votre instance CFEE (par exemple, audit de déploiement d'application, événements de démarrage et d'arrêt ; conservation d'enregistrements d'appartenance d'utilisateur CFEE, organisations, espaces, connexions d'applications et de service). Cette instance de service Compose for PostgreSQL est déployée dans une organisation Cloud Foundry publique (indépendante des organisations CFEE). L'organisation Cloud Foundry publique dans laquelle l'instance Compose for PostgresSQL est déployée porte un nom spécifique : **_cfee-`<accountId>`_**, où "accountId" est l'ID du compte IBM Cloud dans lequel CFEE (ainsi que l'instance de service Compose for PostgreSQL) doit être mis à disposition. L'organisation Cloud Foundry publique est créée automatiquement lorsque le propriétaire du compte crée une instance CFEE. L'organisation n'est pas automatiquement créée lorsqu'un utilisateur qui n'est pas propriétaire du compte tente de créer l'instance CFEE (de ce fait, la tentative de création de l'instance CFEE échouera). Par conséquent, tout utilisateur du compte IBM Cloud qui crée des instances CFEE alors qu'il n'est pas propriétaire du compte doit être ajouté à l'organisation Cloud Foundry publique **_cfee-`<accountId>`_** avec le **rôle de responsable**.   

   Pour ajouter un utilisateur à partir du compte IBM Cloud à l'organisation _cfee-`<accountId>`_ publique :
    * Accédez à [**Gérer > Compte > Organisations Cloud Foundry**](https://console.bluemix.net/account/organizations).
    * Cliquez sur l'organisation **_cfee-`<accountId>`_**.
    * Accédez à l'onglet **Utilisateurs** en haut de la page.
    * Recherchez l'utilisateur qui veut créer des instances CFEE eet cochez la case **Responsable** de cet utilisateur. Si l'utilisateur que vous voulez autoriser à créer des instances CFEE ne figure pas dans la liste, cliquez sur **Ajouter ou inviter un utilisateur** au-dessus du tableau pour ajouter ou inviter des utilisateurs dans l'organisation **_cfee-`<accountId>`_**.

   **Remarque** : même si l'organisation publique **_cfee-`<accountId>`_** est implicitement et automatiquement créée lorsque le propriétaire du compte IBM Cloud crée une instance CFEE, ce propriétaire de compte (et uniquement lui) peut créer l'organisation Cloud Foundry publique manuellement, sans créer d'instance CFEE. Le propriétaire du compte IBM Cloud peut créer l'organisation _cfee-`<accountId>`_ publique manuellement dans la page **Gérer > Compte > Organisations Cloud Foundry**. Si vous êtes propriétaire du compte et que vous créez l'organisation _cfee-`<accountId>`_ publique, veillez à la nommer très exactement _cfee-`<accountId>`_. Pour connaître l'ID de compte IBM Cloud, accédez à la page [**Gérer > Compte > Organisations Cloud Foundry**](https://console.bluemix.net/account/organizations) et regardez l'URL de la page affichée dans votre navigateur. L'ID de compte IBM Cloud est la suite de valeurs alphanumériques qui suit le signe `=` dans l'URL de la page. Sinon, vous pouvez accéder à __Gérer > Compte > Utilisateurs__ et survoler l'infobulle à gauche du nom de _compte_ dans l'angle supérieur droit de la page.
   
* Rôle d'administrateur ou d'éditeur sur le service de conteneur {{site.data.keyword.Bluemix_notm}} dans le groupe de ressources auquel l'environnement est affecté. Les instances {{site.data.keyword.cfee_full_notm}} sont déployées dans l'infrastructure de cluster du conteneur fournie par le service de conteneur {{site.data.keyword.Bluemix_notm}}. Lorsque vous créez une instance du service {{site.data.keyword.cfee_full_notm}}, le service crée automatiquement un cluster Kubernetes dans lequel l'environnement {{site.data.keyword.cfee_full_notm}} est déployé. L'accès au service de conteneur IBM, notamment dans le groupe de ressources auquel l'environnement est affecté, est nécessaire pour la création de cette infrastructure de cluster.

Pour confirmer que vous détenez les droits d'accès requis pour créer une instance {{site.data.keyword.cfee_full_notm}} :
1. Accédez au menu [**Gérer > Compte > Utilisateurs**](https://console.bluemix.net/iam/#/users) dans l'en-tête {{site.data.keyword.Bluemix_notm}} pour ouvrir la page **Identité et accès**.
2. Dans l'onglet Règles d'accès, cliquez sur l'utilisateur qui crée l'utilisateur.
3. Confirmez que les règles d'accès de l'utilisateur qui crée l'environnement sont cohérentes avec celles précédemment décrites.

L'écran suivant illustre les règles d'accès, telles qu'elles se présentent dans la page Identité et accès d'{{site.data.keyword.Bluemix_notm}}, qui autorisent un utilisateur à créer une instance {{site.data.keyword.cfee_full_notm}}.

![Règles d'accès](img/AccessPolicies_Creator.png)

## Droits requis pour exploiter un environnement
{: #perm-working}

Pour utiliser une instance {{site.data.keyword.cfee_full_notm}}, les utilisateurs doivent :
1. Etre membres du compte {{site.data.keyword.Bluemix_notm}} où l'instance {{site.data.keyword.cfee_full_notm}} a été créée.
2. Détenir les _règles d'accès_ suivantes accordées par l'administrateur de compte (voir la page _Identité et accès_ dans le menu [**Gérer > Compte > Utilisateurs**](https://console.bluemix.net/iam/#/users) de l'en-tête {{site.data.keyword.Bluemix_notm}} pour vérifier vos règles d'accès au compte en vigueur) :
  - Accès à au moins un groupe de ressources du compte {{site.data.keyword.Bluemix_notm}}. Les groupes de ressources permettent d'organiser les ressources en regroupements personnalisés afin de faciliter le contrôle d'accès à ces ressources. Vous êtes invité à désigner un groupe de ressources lorsque vous créez une nouvelle instance d'environnement.
  - Détenir un droit d'accès au service {{site.data.keyword.cfee_full_notm}} dans le groupe de ressources sous lequel l'instance de l'environnement a été créée. Le niveau d'accès et de contrôle que détiennent les utilisateurs sur une instance {{site.data.keyword.cfee_full_notm}} dépend du rôle qui leur a été accordé dans la règle d'accès :
     - Les utilisateurs dotés du rôle administrateur ou éditeur peuvent créer des organisations, affecter des responsables à des organisations et des espaces, disposer de droits complets sur toutes les organisations et tous les espaces de l'environnement et effectuer des actions opérationnelles à l'aide de l'API du contrôleur de cloud. La _portée cloud_controller.admin_ est automatiquement accordée à ces utilisateurs dans la _portée Compte utilisateur et authentification_ de Cloud Foundry.
     - Les utilisateurs dotés du rôle d'afficheur peut visualiser cet environnement dans le tableau de bord {{site.data.keyword.Bluemix_notm}} principal et ouvrir son interface utilisateur. L'accès utilisateur à des organisations et des espaces spécifiques de l'environnement est régi par les rôles propres aux organisations et espaces affectés par les responsables de ces organisations et espaces. Pour plus d'informations, voir [Ajout d'utilisateurs à des organisations](add-users.html).

Image illustrant les règles d'accès minimales (telles qu'elles se présentent dans la page {{site.data.keyword.Bluemix_notm}} _Identité et accès_) requises pour accéder à l'environnement {{site.data.keyword.cfee_full_notm}}.

![Règles d'accès](img/AccessPolicies_User.png)

