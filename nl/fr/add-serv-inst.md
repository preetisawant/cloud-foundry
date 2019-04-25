---

copyright:
  years: 2018
lastupdated: "2019-04-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Utilisation des services
{: #workingwith-services}

Les applications déployées dans un environnement {{site.data.keyword.cfee_full_notm}} peuvent être liées à deux types d'instances de service :

1. Les instances de service public créées à partir du catalogue {{site.data.keyword.Bluemix}} et disponibles dans le compte {{site.data.keyword.Bluemix}}.  
Les instances de service public disponibles dans le compte {{site.data.keyword.Bluemix}} ne sont pas en tant que telles être disponibles pour les environnements CFEE. Pour qu'une instance de service public (disponible dans le compte {{site.data.keyword.Bluemix}}) devienne disponible pour les espaces d'un environnement CFEE, elle doit être spécifiquement ajoutée à l'espace CFEE cible. Lorsque vous _ajoutez_ une instance de service public à un environnement CFEE via l'interface utilisateur de l'environnement CFEE, in alias de l'instance de service public est placé dans l'environnement CFEE. Une fois l'instance de service {{site.data.keyword.Bluemix}} ajoutée (associée à un alias) à l'espace CFEE, elle peut être liée à des applications dans cet espace CFEE. Cela permet aux développeurs d'optimiser le vaste catalogue des services {{site.data.keyword.Bluemix}} dans leurs applications déployées dans des environnements CFEE tout en autorisant le contrôle d'accès à ces services {{site.data.keyword.Bluemix}}.

   Outre l'ajout d'instances de service {{site.data.keyword.Bluemix}} existantes à un espace CFEE, vous pouvez créer une nouvelle instance de service {{site.data.keyword.Bluemix}} à partir d'un espace CFEE, ce qui entraîne son ajout automatique dans cet espace CFEE.
  
2. Les instances de service gérées par un courtier de services Cloud Foundry local (local pour l'environnement CFEE). Ces instances peuvent elles-mêmes être de deux types :
   *  2a. Instance d'une offre de service créée depuis la place du marché Cloud Foundry de l'instance {{site.data.keyword.cfee_full_notm}} en cours. Ce type d'instance de service nécessite qu'un courtier de services enregistré soit disponible dans l'environnement. Un courtier de services affiche un catalogue des plans et offres de services, et permet de créer, supprimer, lier et délier des instances depuis ces offres de services. Pour plus d'informations, voir [Gestion des courtiers de services](https://docs.cloudfoundry.org/services/managing-service-brokers.html) dans la documentation Cloud Foundry.
   * 2b. Instance de service fournie par l'utilisateur. La création de ce type est prise en charge par le biais de l'interface de ligne de commande, et non via l'interface utilisateur. Les instances de service fournies par l'utilisateur sont néanmoins répertoriées dans l'interface utilisateur.
   
Vous pouvez également créer une instance de service à partir d'un espace CFEE, depuis l'interface utilisateur CFEE ou à l'aide de l'interface de ligne de commande (voir les sections ci-dessous).  La création d'une instance de service à partir d'un espace CFEE à l'aide de cette commande a un double effet :
* Crée une instance de service dans l'{{site.data.keyword.Bluemix}} public.
* Crée un alias de cette service public publique dans l'espace CFEE à partir duquel l'instance de service a été créée.
    
Les sections suivantes décrivent comment ajouter, créer, contrôler l'accès et lier des instances de service dans l'interface utilisateur et avec l'interface de ligne de commande Cloud Foundry.
   

## Affichage des instances de service {{site.data.keyword.Bluemix_notm}} dans tous les environnements CFEE
{: #viewing-services_across}

Accédez au [tableau de bord des services Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/services) pour visualiser une vue consolidée de toutes les instances de service {{site.data.keyword.Bluemix_notm}} (auxquelles vous avez accès) dans le compte {{site.data.keyword.Bluemix_notm}} et déterminer quelles instances de service ont été ajoutées à quels espaces CFEE.

Cette vue montre toutes les instances de service {{site.data.keyword.Bluemix_notm}} disponibles dans le compte et indique quelles sont celles qui ont été ajoutées (associées à un alias) à quels espaces CFEE. Développez une instance de service pour afficher les espaces CFEE auxquels elle a été ajoutée.  Vous pouvez développer davantage ces espaces pour identifier les applications dans ces espaces CFEE auxquelles ces instances de service ont été liées.  

A partir de cette vue, vous pouvez également lier des applications déployées dans les espaces CFEE auxquels ces instances de service ont été ajoutées. Accédez au menu situé tout à fait à droite de la ligne de l'instance de service correspondante dans le tableau (disponible pour un espace CFEE spécifique) et sélectionnez **Lier à une application**.

## Ajout d'instances de service {{site.data.keyword.Bluemix_notm}} existantes à un espace CFEE
{: #adding-services-inspace}

Vous pouvez lier des instances de service {{site.data.keyword.Bluemix_notm}} à des applications déployées dans un espace CFEE.  Avant de pouvoir être liée à une application déployée dans CFEE, une instance de service IBM Cloud doit être ajoutée à l'espace CFEE dans lequel l'application est déployée. Les prérequis s'appliquent avant l'ajout d'une instance de service {{site.data.keyword.Bluemix_notm}} à un espace CFEE :
* Le service dont l'instance doit être ajoutée ne peut pas être un service Cloud Foundry.  Seuls les services {{site.data.keyword.Bluemix_notm}} qui prennent en charge des groupes de ressources et IAM peuvent être ajoutés (associés à un alias) dans un CFEE. Les services instanciés dans des organisations, espaces et rôles Cloud Foundry publics ne peuvent pas être ajoutés (associés à des alias) dans un environnement CFEE.  Les services {{site.data.keyword.Bluemix_notm}} sont progressivement déplacés pour tirer parti des groupes de ressources.  Une fois qu'un services a été déplacé pour utiliser des groupes de ressources au lieu d'organisation et d'espaces Coud Foundry, vous pouvez migrer toutes vos instances existantes de ce service vers un groupe de ressources et le service peut alors être ajouté à un environnement CFEE.  Voir [Migration d'instances de service Cloud Foundry vers un groupe de ressources](https://cloud.ibm.com/docs/resources/instance_migration.html#migrate).
* Le service {{site.data.keyword.Bluemix_notm}} doit être disponible dans le même compte {{site.data.keyword.Bluemix_notm}} que celui dans lequel l'instance CFEE réside.
* Vous devez disposer du rôle de plateforme _Opérateur_ (ou supérieur) sur l'instance de service {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir la page Identité & Accès du menu **Gérer > Utilisateurs** dans l'en-tête {{site.data.keyword.Bluemix_notm}} pour vérifier vos règles d'accès au compte en cours.

Pour ajouter une instance de service {{site.data.keyword.Bluemix_notm}} existante à un espace CFEE :
1. Accédez au [tableau de bord des services Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/services).  
2. Localisez l'instance de service {{site.data.keyword.Bluemix_notm}} dans la liste et appelez le menu situé tout à fait à droite de la ligne de l'instance de service correspondante dans le tableau.
3. Sélectionnez **Ajouter un service**.
4. Dans la boîte de dialogue _Ajouter un service_, sélectionnez l'environnement CFEE, l'organisation et l'espace dans lesquels vous souhaitez ajouter le service, puis cliquez sur **Ajouter**.
5. Développez le service {{site.data.keyword.Bluemix_notm}} cible pour trouver le nouvel environnement CFEE auquel le service a été ajouté.


Vous avez aussi la possibilité d'ajouter une instance de service {{site.data.keyword.Bluemix_notm}} à partir de l'espace CFEE où vous voulez l'ajouter :
1. Dans votre [tableau de bord](https://cloud.ibm.com/dashboard) {{site.data.keyword.Bluemix_notm}} ou le [tableau de bord des services Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/services), recherchez l'environnement Cloud Foundry Enterprise qui héberge votre application.
2. Accédez à **Organisations** dans le panneau de navigation et ouvrez l'organisation et l'espace où se trouve l'application.
3. Accédez à l'onglet **Espaces** et recherchez l'espace qui contient l'application.
4. Sur la page de l'espace cible, accédez à l'onglet **Services**, puis cliquez sur **Ajouter un service**.  La boîte de dialogue __Ajouter un service__ s'ouvre.  Cette page répertorie les instances de service disponibles dans le compte {{site.data.keyword.Bluemix_notm}}.
5. Recherchez et sélectionnez une instance de service disponible que vous voulez ajouter à l'espace CFEE. 
6. L'instance de service sera ajoutée à la liste de services disponibles dans l'espace CFEE.

   **Remarque :** lorsque vous ajoutez un service {{site.data.keyword.Bluemix_notm}} à un espace CFEE, un alias de cette instance de service est créé dans cet espace. Lorsque vous **retirez** l'instance de service d'un espace CFEE (à partir du menu situé tout à fait à droite de la ligne de l'instance de service correspondante dans le tableau), le service n'est pas supprimé du compte public.  Il est simplement retiré du compte CFEE spécifique et il n'est plus disponible pour être lié aux applications présentes dans cet espace CFEE.  En outre, lorsque vous supprimez l'instance de service proprement dite du compte {{site.data.keyword.Bluemix_notm}}, le service n'est plus disponible pour les espaces CFEE. 

## Création d'instances de service {{site.data.keyword.Bluemix_notm}} à partir d'une interface utilisateur d'espace CFEE
{: #creating-services-inspace}

Vous pouvez créer des instances de service {{site.data.keyword.Bluemix_notm}} à partir d'un espace CFEE.  La création d'une instance de service {{site.data.keyword.Bluemix_notm}} provoque ce qui suit :
* L'instance de service {{site.data.keyword.Bluemix_notm}} est créée dans IBM Cloud.  Cela revient à créer l'instance de service à partir du [catalogue](https://cloud.ibm.com/catalog) {{site.data.keyword.Bluemix_notm}}.
* Un alias est ajouté pour l'instance de service {{site.data.keyword.Bluemix_notm}} dans l'espace CFEE à partir duquel l'action de création a été déclenchée. Une instance de service d'alias (dans un espace CFEE) est une référence vers l'instance de service réelle (dans le compte IBM Cloud). L'alias d'instance de service permet aux développeurs d'interagir avec l'instance de service (c'est-à-dire d'établir des liaisons avec des applications) en gérant toutes les données d'identification automatiquement pour l'interaction avec l'instance de service. .

Pour créer une instance de service à partir d'un espace CFEE :
1. Sur la page de l'espace cible, accédez à l'onglet **Services**, puis cliquez sur **Créer un service**.  La vue **Place de marché** s'ouvre pour le service {{site.data.keyword.cfee_full_notm}}.  La vue recense les offres de service à partir de deux sources (voir la colonne __Source__) :
   * Offres du catalogue {{site.data.keyword.Bluemix_notm}}.
   * Offres de la place du marché {{site.data.keyword.cfee_full_notm}} local.
5. Recherchez et sélectionnez une offre de services disponible que vous voulez instancier. 
6. Selon la source de l'offre de services (catalogue IBM Cloud ou place du marché CFEE local) procédez de l'une des manières suivantes :
   * Si l'offre de service sélectionnée est une offre de catalogue {{site.data.keyword.Bluemix_notm}}, un bouton **Continuer** est présent pour vous permettre de passer à la page de création d'offre de service IBM Cloud.  Il s'agit de la même page que celle qui est disponible à partir du catalogue {{site.data.keyword.Bluemix_notm}}.  Sur cette page, vous indiquez le nom de la nouvelle instance de service, la région, le plan et d'autres propriétés requises pour créer le service dans IBM Cloud.  Lorsque vous cliquez sur Créer, l'instance de service est créée dans IBM Cloud et elle est automatiquement ajoutée à l'espace CFEE en cours.
   * Si l'offre de service sélectionnée provient du catalogue CFEE local, un bouton **Créer** est présent pour vous permettre de créer l'instance de service. Vous êtes invité à spécifier une organisation et un espace dans l'environnement CFEE en cours où l'instance de service sera créée.

## Création d'instances de service {{site.data.keyword.Bluemix_notm}} à partir d'un espace CFEE à l'aide de l'interface de ligne de commande Cloud Foundry
{: #creating-services_cli}

Vous pouvez créer une instance de service à l'aide de l'interface de ligne de commande à partir d'un espace CFEE.  Créer un service à l'aide de l'interface de ligne de commande dans un espace CFEE revient à le créer à l'aide de l'interface utilisateur dans cet espace. Autrement dit, la création d'un service permet d'obtenir les deux résultats suivants :
* L'instance de service {{site.data.keyword.Bluemix_notm}} est créée dans IBM Cloud.  Cela revient à créer l'instance de service à partir du [catalogue](https://cloud.ibm.com/catalog) {{site.data.keyword.Bluemix_notm}}.
* L'instance de service {{site.data.keyword.Bluemix_notm}} est ajoutée (associée à un alias) dans l'espace CFEE à partir duquel l'action de création a été déclenchée.

La différence entre la création d'une instance de service à partir d'un espace CFEE et la création d'une instance de service à partir de l'interface de ligne de commande concerne le cycle de vie de l'instance de service créée.  Lorsque vous créez l'instance de service dans l'interface utilisateur de l'espace CFEE, le cycle de vie de l'instance de service créée est contrôlé à partir de l'instance de service proprement dite dans le compte {{site.data.keyword.Bluemix_notm}}.  Cela signifie que les mises à jour apportées au plan de service sont contrôlées à partir de l'instance dans le compte {{site.data.keyword.Bluemix_notm}} et non à partir de l'espace CFEE.  Sinon, si l'instance de service est créée à partir de l'interface de ligne de commande, le cycle de vie du service est contrôlé à partir de l'espace CFEE (le service est mis à jour à partir de l'espace CFEE).

Les instances de service créées à partir de l'interface de ligne de commande sont également affichées dans l'interface utilisateur et sont signalées par un astérisque (`*`) placé en regard de leur nom.

Pour créer des instances de service à l'aide de l'interface de ligne de commande, procédez comme suit :

1. Téléchargez et installez l'interface de ligne de commande {{site.data.keyword.Bluemix}}, le cas échéant. [Téléchargement de l'interface de ligne de commande Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![Icône de ligne externe](../icons/launch-glyph.svg "Icône de ligne externe").

2. Accédez à la page de présentation d'{{site.data.keyword.cfee_full}} et localisez le noeud final d'API de l'environnement.

3. Dans l'interface de ligne de commande, définissez le noeud final d'API sur le noeud final de votre environnement CFEE :

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. Connectez-vous à l'environnement CFEE :

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Si vous utilisez un ID fédéré, utilisez l'option `-sso` :

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. Créez le service :
vous pouvez émettre une commande `cf create-service` pour créer une instance de service dans l'espace CFEE à partir duquel la commande est émise. La création d'une instance de service à partir d'un espace CFEE à l'aide de cette commande a un double effet :
    * Crée une instance de service dans l'{{site.data.keyword.Bluemix}} public avec un nom fourni par le paramètre `instance_name`. Si le paramètre `instance_name` de la commande ne contient pas de valeur, le nom est attribué par le contrôleur de ressource {{site.data.keyword.Bluemix}}.  
    * Crée un alias de cette instance de service publique dans l'espace CFEE à partir duquel la commande a été émise, avec le nom indiqué par `SERVICE_INSTANCE`. Le nom de l'instance de service publique n'est pas automatiquement le même que celui de l'instance de service dans l'espace CFEE. Par conséquent, si vous voulez que les noms de l'instance de service publique et de l'instance de service (alias de l'instance publique) soient identiques dans l'espace CFEE, vous devez spécifier la même valeur pour `instance_name` et `SERVICE_INSTANCE` dans la commande suivante :

  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"instance_name":"value", "resource_group":"value", "target":"value"}'
  ```
  {: pre}
  
L'exemple suivant crée une instance du service Cloudant (plan standard) nommée "myCloudant" (avec le même nom pour l'instance publique et l'alias CFEE), dans la région "bluemix-us-south" et la place dans un groupe de ressources spécifique :

  ```
  cf create-service cloudant standard myCloudant -c '{"instance_name":"myCloudant", "resource_group":"b0daaf6c3ccd4392a266da916cce2e8c", "target":"bluemix-us-south"}'
  ```
  {: pre}

 La commande `create-service` peut être émise avec des paramètres facultatifs afin de gérer des cas d'utilisation spécifiques :
 
   * Nom d'instance (`instance_name`) : permet d'indiquer un nom personnalisé pour l'instance de service créée dans l'{{site.data.keyword.Bluemix}} public. Si aucune valeur n'est indiquée dans le paramètre `instance_name`, le nom par défaut de l'instance de service publique dans l'espace public sera différent de la valeur de `SERVICE_INSTANCE` (nom de l'instance dans l'espace CFEE). Il est recommandé d'utiliser ce paramètre afin de contrôler le nom de l'instance de service publique ou pour lui attribuer le même nom que l'instance de service dans l'espace CFEE (alias de l'instance publique).
   * Groupe de ressources (`resource_group`) : permet d'indiquer un groupe de ressources dans lequel placer la nouvelle instance. La valeur de ce paramètre doit être l'ID du groupe de ressources (_resource group ID_) et non le nom du groupe de ressources (_resource group name_).  Pour connaître l'ID d'un groupe de ressources spécifique (_resource group ID_), exécutez la commande `ibmcloud resource groups`.
   * Région de déploiement cible (`target`) : région où l'instance de service doit être mise à disposition. Certains services ne nécessitent pas d'indiquer une cible. Toutefois, la commande échoue si aucune cible n'est indiquée lorsque le service créé en exige une.

Vous pouvez éventuellement fournir un fichier JSON contenant ces paramètres. Par exemple :
  ```
  {
    "NewCloudant": 
        {  
        "instance_name":"myCloudant",
        "resource_group": "b0daaf6c3ccd4392a266da916cce2e8c",
        "target": "bluemix-us-south"
        }
   }
  ```
  {: pre}
  
Le fichier JSON peut être appelé dans le cadre de la commande `cf create-service`. Le chemin d'accès au fichier JSON peut être un chemin d'accès relatif ou absolu :
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
Pour obtenir plus de détails, exécutez la commande suivante :
  ```
  cf create-service -help
  ```
<br>
Pour plus d'informations, voir [Gestion d'instances de service à l'aide de l'interface de ligne de commande cf](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") dans la documentation Cloud Foundry.
  
## Liaison de services à des applications à partir de l'interface utilisateur CFEE
{: #bind-services-ui}

Les utilisateurs dotés du rôle de plateforme _Opérateur_ (ou supérieur) et du rôle de service _Auteur_ (ou supérieur) sur une instance de service {{site.data.keyword.Bluemix_notm}} peuvent lier cette instance à une application déployée dans un espace CFEE, soit depuis le [tableau de bord des services Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/services) ou depuis l'onglet Services de l'interface utilisateur d'un espace CFEE.   

Pour lier une instance de service à une application à partir du [tableau de bord des services Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/services) :
1. Accédez au [tableau de bord des services Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/services) pour visualiser une vue consolidée de toutes les instances de service {{site.data.keyword.Bluemix_notm}} qui sont à votre disposition dans le compte {{site.data.keyword.Bluemix_notm}}.  La vue permet également de déterminer quelles instances de service {{site.data.keyword.Bluemix_notm}} sont disponibles (associées à un alias) dans quels espaces CFEE. Vous pouvez développer une instance de service pour afficher les espaces CFEE auxquels elle a été ajoutée.  Vous pouvez développer davantage ces espaces pour identifier les applications dans ces espaces CFEE auxquelles ces instances de service ont été liées. 
2. Localisez l'instance de service {{site.data.keyword.Bluemix_notm}} que vous souhaitez lier.
3. Développez la vue correspondante pour visualiser tous les espaces CFEE où cette instance de service a été ajoutée. Si cette instance de service n'a pas été ajoutée à l'espace CFEE où l'application est déployée, sélectionnez **Ajouter** dans le menu situé tout à fait à droite de la ligne pour rendre l'instance de service disponible dans l'espace CFEE cible.
4. Accédez au menu situé tout à fait à droite de la ligne correspondant à l'environnement CFEE/l'espace où l'instance de service est disponible et sélectionnez **Lier une application**.
5. Dans la boîte de dialogue __Lier une application__, sélectionnez l'application que vous souhaitez lier. 

   **Remarque :** si le service à lier prend en charge à la fois des noeuds finaux publics (externes) et privés (internes), voir [Noeuds finaux de service IBM Cloud](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about), et/ou prend en charge plusieurs [rôles d'accès au service](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am) (qui indiquent les actions autorisées sur l'instance de service qui peuvent être effectuées via la liaison), une boîte de dialogue en plusieurs étapes vous invite à sélectionner un type de noeud final (public ou privé) et/ou un rôle de service spécifique.
6. L'application est désormais liée à l'instance de service.  Vous pouvez développer une instance de service dans la table pour voir les applications qui lui sont liées (dans un espace CFEE spécifique).


Pour lier une application à une instance de service à partir de la page __Services__ d'un espace CFEE :

1. Ouvrez l'interface utilisateur CFEE où l'application est déployée.
2. Accédez à **Organisations** dans le panneau de navigation de gauche et ouvrez l'organisation et l'espace où l'application est déployée.
3. Accédez à l'onglet **Espaces** et recherchez l'espace qui contient l'application.
4. Dans l'espace cible, accédez à l'onglet **Services**.
5. Dans le tableau **Instances de service**, accédez au menu __Actions__ situé tout à fait à droite de la ligne correspondant à l'instance de service que vous souhaitez lier, puis sélectionnez **Lier**.
6. Sélectionnez l'application que vous voulez lier à l'instance de service.

Pour annuler la liaison d'une application à une instance de service :

1. Dans l'onglet **Services** de l'espace, développez l'instance de service cible pour afficher les applications qui lui sont liées.
2. Accédez au menu Actions dans la ligne d'une application et sélectionnez **Annuler la liaison du service**.

## Liaison de services à des applications à l'aide de l'interface de ligne de commande Cloud Foundry
{: #bind-services-cli}

Vous pouvez utiliser la commande `cf bind-service` pour lier une instance de service à une application dans un environnement CFEE :

 ```
  cf bind-service APP_NAME SERVICE_INSTANCE -c '{"parameter": "value"}' 
  ```
  {: pre}

Dans les cas suivants, la commande nécessite des paramètres spéciaux :

* Lorsque vous utilisez la commande `cf bind-service` pour lier une application à une instance de service qui prend en charge des [Noeuds finaux de service IBM Cloud](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about) qui se connectent à des services IBM Cloud via le réseau privé IBM Cloud. Pour lier une application (déployée dans un environnement CFEE) à un service qui prend en charge à la fois les noeuds finaux publics (externes) et privés (internes), vous devez indiquer lesquels utiliser pour les liaisons. Dans l'exemple suivant, la commande lie le service en utilisant le noeud final interne ("internal") :

  ```
  cf bind-service myApplication myServiceInstance -c '{"service-endpoints":"internal"}' 
  ```
  {: pre}

* Lorsque le service a plusieurs [rôles d'accès au service](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am). Les rôles d'accès au service indiquent les actions autorisées sur l'instance de service qui peuvent être effectuées via la liaison. Vous pouvez indiquer un rôle spécifique d'accès au service à l'aide du paramètre `role`. Dans l'exemple suivant, la liaison spécifie le rôle d'accès au service Auteur (writer) :

  ```
  cf bind-service myApplication myServiceInstance -c '{"role": "writer"}' 
  ```
  {: pre}
<br>
Voir [Bind a Service Instance](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") dans la documentation Cloud Foundry pour plus d'informations sur la liaison d'applications à l'aide de la commande d'interface de ligne de commande `cf bind-service`.

## Visibilité des services
{: #service_visibility}

Les clients peuvent décider qui peut créer de nouveaux services IBM Cloud à partir d'un environnement CFEE.  Ils peuvent également décider qui peut ajouter des services IBM Cloud existants à un espace CFEE.  Ce contrôle s'exerce en vérifiant la visibilité des offres de service (et/ou des instances de ces offres de service) pour les utilisateurs.

### Contrôle de la création d'instances de service
{: #control_servicecreation}

Le contrôle de la création de services peut être réalisé en vérifiant la visibilité des offres de service dans le catalogue IBM Cloud pour tous les utilisateurs du compte IBM Cloud ou pour les utilisateurs d'organisations Cloud Foundry spécifiques.

#### Contrôle de la visibilité dans le catalogue IBM Cloud pour les utilisateurs d'un compte IBM Cloud
{: #creation_accountvisibility}

Les administrateurs de compte IBM Cloud (utilisateurs dotés du rôle _Administrateur_ sur tous les services activés par IAM) peuvent empêcher l'affichage d'un service ou d'un plan de service dans le catalogue pour tous les utilisateurs d'un **compte IBM Cloud** spécifique.  Les administrateurs de compte peuvent empêcher tous les utilisateurs de compte d'utiliser un service en plaçant sur liste noire un service ou un plan de service pour tous les utilisateurs d'un compte. Le placement d'un service sur liste noire empêchera les utilisateurs de ce compte de voir ce service (ou plan de service) dans le catalogue IBM Cloud.  Pour ce faire, utilisez la commande `ibmcloud catalog blacklist` avec la syntaxe suivante :

  ```
  ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]
  ```

Vous pouvez utiliser la forme la plus simple de la commande `catalog backlist` pour rendre une offre de service (ou tous ses plans) invisible pour tous les utilisateurs du compte en cours :

  ```
  Ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]

  ```
  {: pre}

Vous avez la possibilité d'empêcher la visibilité non pas de l'ensemble de l'offre de service, mais d'un plan spécifique dans une région donnée.  Pour ce faire, vous devez utiliser l'ID de l'entrée correspondante dans le catalogue globale et non le nom.   Si vous souhaitez empêcher les utilisateurs de voir un plan spécifique dans une région donnée, vous pouvez exécuter la commande suivante :

  ```
  Ibmcloud catalog blacklist -add <catalogEntryID>
  ```
  {: pre}
  
 Pour retirer des services de la liste noire :
 ```
  Ibmcloud catalog blacklist -remove <catalogEntryID>
  ```
  {: pre}
 
La commande ci-après vous permet de trouver l'ID d'une entrée de catalogue donnée (par exemple, le plan d'un service et sa région de déploiement). Cette commande renvoie tous les plans et leurs régions de déploiement pour un service donné :

  ```
  ibmcloud catalog service <thisService>
  ```
  {: pre}

La commande suivante vous permet de visualiser d'autres détails pour la commande `ibmcloud catalog blacklist` :

  ```
  Ibmcloud catalog blacklist -help
  ```
  {: pre}


#### Contrôle de la visibilité pour les utilisateurs d'une organisation Cloud Foundry
{: #creation_orgvisibility}

Vous pouvez utiliser les commandes `cf enable-service-access` et `cf disable-service-access` afin de contrôler l'accès aux services pour des **organisations Cloud Foundry** spécifiques.  Dans ce cas, le point de contrôle pour l'accès est Cloud Foundry (et non le compte IBM Cloud).  Notez qu'il s'agit d'une commande `cf` native (et non d'une commande `ibmcloud`). 

Tenez compte des points suivants lorsque vous définissez la visibilité des services via l'interface de ligne de commande `cf` :

*  Les commandes `cf` activent et/ou désactivent les offres de service (éventuellement, les plans d'offre de service spécifiques) pour tous les utilisateurs d'organisations Cloud Foundry spécifiques.
* L'activation repose sur la création d'une "liste blanche" d'organisations. En d'autres termes, il s'agit d'une liste d'inclusion d'organisations Cloud Foundry qui ont accès à un service (par opposition à l'approche avec une "liste noire" dans la commande `ibmcloud` décrite précédemment qui repose sur la définition d'une liste de services exclus de la visibilité pour les utilisateurs d'un compte). Cela signifie que le contrôle d'accès à un service de catalogue à l'aide de cette approche repose non pas sur la définition des organisations qui ne peuvent pas voir un service (placement sur liste noire) mais sur la définition des organisations qui peuvent le voir (placement sur liste blanche).
*  Lorsque vous accordez à une organisation l'accès à un service (ou à un plan de service) en ajoutant cette organisation à une liste blanche, vous empêchez de fait toutes les autres organisations d'accéder à ce service.  Autrement dit, dès lors que vous placez une organisation sur liste blanche, vous empêchez toutes les autres organisations d'accéder à ce service (ou à ce plan de service).
*  Avant d'ajouter des organisations à la liste blanche, vous devez désactiver la visibilité pour toutes les organisations.  Vous ne pouvez pas désactiver l'accès à un plan de service si celui-ci est disponible pour toutes les organisations.

En raison du comportement général décrit précédemment, il est recommandé de contrôler l'accès des organisations à des services en exécutant les commandes suivantes :

  * **Désactiver** l'accès à un plan de service pour toutes les organisations :
  ```
  cf disable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}
  
  L'exemple suivant désactive l'accès au plan standard du service Cloudant pour tous les membres de MyOrg :
  ```
  cf disable-service-access cloudant -p standard -o MyOrg
  ```
  {: pre}

  
  * **Activer** l'accès au plan de service pour des organisations CFEE spécifiques.  Le plan de service sera désactivé pour toutes les autres organisations qui ne sont pas spécifiquement activées dans la commande. 
  ```
  cf enable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}

<br>  
**Remarque :** il est recommandé d'exécuter les commandes d'activation et de désactivation de service Cloud Foundry pour l'ensemble d'un service et non pour certains plans.


### Contrôle de l'accès à des instances de service existantes
{: #control_serviceaddition}

Les développeurs dans un espace CFEE peuvent utiliser des instances de service disponibles dans le compte IBM Cloud.  Dans un espace d'un environnement CFEE, les utilisateurs peuvent **ajouter** une instance de service à cet espace (voir la rubrique [Ajout d'instances de service existantes](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) précédente). Lorsqu'une instance de service est ajoutée à un espace CFEE, un alias (une référence) est créé vers cette instance de service, ce qui permet à un développeur de lier l'instance de service à une application déployée dans cette espace CFEE comme s'il s'agissait de l'instance de service réelle.

Les administrateurs de compte peuvent contrôler l'utilisation d'instances de service via des [règles d'accès IAM](https://cloud.ibm.com/docs/iam/iamusermanage.html#iamusermanage).  Depuis l'interface utilisateur ou l'interface de ligne de commande ibmcloud, ils peuvent affecter des rôles aux instances de service proprement dites ou aux groupes de ressources dans lesquels ces instances résident.  Un développeur a besoin du rôle _Afficheur_ ou d'un rôle supérieur sur une instance de service (ou son groupe de ressources) avant de pouvoir ajouter cette instance à un espace.

Vous trouverez des vidéos contenant des discussions et des démonstrations relatives aux services CFEE dans la [liste de lecture des vidéos CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
{:tip}
