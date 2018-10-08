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

Avant que les utilisateurs puissent commencer à créer et à utiliser des instances du service {{site.data.keyword.cfee_full}}, un administrateur du compte où l'instance doit être créée doit leur accorder des règles d'accès.  

## Droits requis pour créer un nouvel environnement
{: #perm-creating}

Pour que les utilisateurs puissent créer de nouvelles instances du service CFEE, un administrateur de compte doit leur accorder des droits d'accès, non seulement au service CFEE proprement dit, mais aussi aux services de prise en charge qui sont également créés automatiquement lors de la création du service CFEE. 

Les règles d'accès Identity & Access Management (IAM) suivantes sont requises pour que les utilisateurs puissent créer une instance {{site.data.keyword.cfee_full_notm}} : 

* Accès _Afficheur_ (ou ultérieur) au **groupe de ressources** **_par défaut_** dans le compte {{site.data.keyword.Bluemix}}. Les groupes de ressources permettent d'organiser les ressources en regroupements personnalisés afin de faciliter le contrôle d'accès à ces ressources. Vous êtes invité à désigner un groupe de ressources lorsque vous créez une nouvelle instance d'environnement. L'accès au groupe de ressources _par défaut_ est requis car le cluster Kubernetes est toujours requis sur groupe de ressources. Les utilisateurs peuvent mettre à disposition l'instance CFEE dans un autre groupe de ressources, mais le cluster Kubernetes sera tout de même mis à disposition sur le groupe de ressources _par défaut_. Si un utilisateur met à disposition l'instance CFEE dans un autre groupe de ressources, cet utilisateur doit disposer des droits d'accès Afficheur pour ce groupe de ressources. 

* Rôle d'administrateur ou d'éditeur sur les ressources du **service {{site.data.keyword.cfee_full_notm}}** dans le groupe de ressources auquel l'environnement est affecté. Les utilisateurs dotés du rôle d'administrateur ou d'éditeur sur le service {{site.data.keyword.cfee_full_notm}} peuvent créer et supprimer un environnement. Mais seuls les utilisateurs dotés d'un rôle d'administration peuvent affecter des utilisateurs à une instance {{site.data.keyword.cfee_full_notm}} ou modifier les rôles affectés aux utilisateurs dans cette instance.
   
* Rôle d'administrateur sur les ressources du **service Kubernetes**. Les instances du service {{site.data.keyword.cfee_full_notm}} sont déployées sur l'infrastructure de cluster de conteneur, qui est fournie par le service Kubernetes. Lorsque vous créez une instance du service {{site.data.keyword.cfee_full_notm}}, le service crée automatiquement un cluster Kubernetes. Les droits d'accès au service Kubernetes sont requis pour la création de cette infrastructure de cluster. Vous pouvez définir l'étendue des droits d'accès pour les règles du service Kubernetes à la région spécifique où vous prévoyez de mettre à disposition l'instance CFEE ou à toutes les régions. 

* Rôle d'administrateur ou d'éditeur sur le **service IBM Cloud Object Storage**, qui est une dépendance requise du service CFEE. Une instance de service IBM Cloud Object Storage est utilisée pour stocker les données générées lors de la création de vos conteneurs d'applications ICFEE (par exemple, packages d'applications téléchargés, packs de construction et exécutables compilés).

* Une instance de service Compose for PostgreSQL, qui est une dépendance requise du service CFEE.  Compose for PostgreSQL est utilisé pour stocker des données Cloud Foundry sur votre instance CFEE (par exemple, audit de déploiement d'application, événements de démarrage et d'arrêt ; conservation d'enregistrements d'appartenance d'utilisateur CFEE, organisations, espaces, connexions d'applications et de service).  Cette instance du **service Compose for PostgreSQL** est déployée dans un espace au sein d'une organisation Cloud Foundry publique (indépendante des organisations CFEE) que vous sélectionnez lorsque vous créez une instance {{site.data.keyword.cfee_full_notm}}. Cela signifie que lorsque vous créez une instance {{site.data.keyword.cfee_full_notm}}, vous devez disposer de droits d'accès Gestionnaire à au moins une organisation située dans la région où vous prévoyez de mettre à disposition l'instance CFEE. Vous devez également disposer de droits d'accès Développeur à au moins un espace contenu dans cette organisation.  

  Si vous n'êtes pas membre d'au moins une organisation publique dans la région où vous prévoyez de créer une instance CFEE, demandez à un administrateur IBM Cloud de vous inviter dans une organisation publique. Si vous possédez un rôle d'administrateur dans le compte, vous pouvez ajouter des utilisateurs aux organisations publiques et aux espaces de ce compte en procédant comme suit : 

     * Accédez à [**Gérer > Compte > Organisations Cloud Foundry**](https://console.bluemix.net/account/organizations) et cliquez sur **Ajouter une organisation** ou sélectionnez une organisation existante. 
     * Accédez à l'onglet **Utilisateurs** en haut de la page de l'organisation. 
     * Recherchez l'utilisateur qui a besoin de créer des instances CFEE. Si l'utilisateur que vous voulez autoriser à créer des instances CFEE ne figure pas dans la liste, cliquez sur **Ajouter ou inviter un utilisateur** au-dessus du tableau pour ajouter ou inviter des utilisateurs dans l'organisation. 
     * Accédez à l'onglet **Espaces** en haut de la page de l'organisation.
     * Recherchez l'espace dans lequel l'instance de service Compose for PostgreSQL sera mise à disposition et cochez la case du rôle **Développeur**. 

L'écran suivant illustre les règles d'accès, telles qu'elles se présentent sur la page Identity & Access d'{{site.data.keyword.Bluemix_notm}}, qui autorisent un utilisateur à créer une instance {{site.data.keyword.cfee_full_notm}}.

![Règles d'accès](img/AccessPolicies_Creator.png)

Pour confirmer que vous détenez les droits d'accès requis pour créer une instance {{site.data.keyword.cfee_full_notm}} :
1. Accédez au menu [**Gérer > Compte > Utilisateurs**](https://console.bluemix.net/iam/#/users) dans l'en-tête {{site.data.keyword.Bluemix_notm}} pour ouvrir la page **Identité et accès**.
2. Dans l'onglet Règles d'accès, cliquez sur l'utilisateur qui crée l'environnement afin d'affecter et afficher les règles d'accès pour cet utilisateur.

## Droits requis pour exploiter un environnement
{: #perm-working}

Pour utiliser une instance {{site.data.keyword.cfee_full_notm}}, les utilisateurs doivent :
1. Etre membres du compte {{site.data.keyword.Bluemix_notm}} où l'instance {{site.data.keyword.cfee_full_notm}} a été créée.
2. Détenir les _règles d'accès_ IAM suivantes accordées par l'administrateur de compte (voir la page _Identity & Access_ sous le menu [**Gérer > Compte > Utilisateurs**](https://console.bluemix.net/iam/#/users) dans l'en-tête {{site.data.keyword.Bluemix_notm}} pour vérifier vos règles d'accès au compte en vigueur) :

  - Droits d'accès au service {{site.data.keyword.cfee_full_notm}} dans le groupe de ressources sous lequel l'instance d'environnement a été créée. Le niveau d'accès et de contrôle que détiennent les utilisateurs sur une instance {{site.data.keyword.cfee_full_notm}} dépend du rôle qui leur a été accordé dans la règle d'accès :
     - Les utilisateurs dotés du rôle administrateur ou éditeur peuvent créer des organisations, affecter des responsables à des organisations et des espaces, disposer de droits complets sur toutes les organisations et tous les espaces de l'environnement et effectuer des actions opérationnelles à l'aide de l'API du contrôleur de cloud. La _portée cloud_controller.admin_ est automatiquement accordée à ces utilisateurs dans la _portée Compte utilisateur et authentification_ de Cloud Foundry.
     - Les utilisateurs dotés du rôle d'afficheur peut visualiser cet environnement dans le tableau de bord {{site.data.keyword.Bluemix_notm}} principal et ouvrir son interface utilisateur. L'accès utilisateur à des organisations et des espaces spécifiques de l'environnement est régi par les rôles propres aux organisations et espaces affectés par les responsables de ces organisations et espaces. Pour plus d'informations, voir [Ajout d'utilisateurs à des organisations](add-users.html).

Image illustrant les règles d'accès minimales (telles qu'elles se présentent dans la page {{site.data.keyword.Bluemix_notm}} _Identité et accès_) requises pour accéder à l'environnement {{site.data.keyword.cfee_full_notm}}.

![Règles d'accès](img/AccessPolicies_User.png)

