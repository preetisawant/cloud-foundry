---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Initiation à l'aperçu technique Eirini
{: #getting-started-eirini}

L'environnement CFEE ({{site.data.keyword.cfee_full}}) est une plateforme cloud pour l'hébergement d'applications et de services dans le cloud. {{site.data.keyword.cfee_full_notm}} facilite la mise à l'échelle des applications à mesure de l'augmentation de la consommation, en simplifiant le contexte d'exécution, le middleware et l'infrastructure de sorte que vous puissiez vous concentrer sur le développement d'applications.
{: shortdesc}

Ce tutoriel d'initiation montre comment créer un environnement {{site.data.keyword.cfee_full_notm}} à partir du plan d'aperçu technique Eirini, ajouter des utilisateurs, créer une organisation et des espaces, déployer des applications et lier ces applications à des services.
Voir la documentation relative au [projet Eirini](https://www.cloudfoundry.org/project-eirini/) pour plus d'informations sur le projet d'incubateur Eirini de Cloud Foundry Foundation.

## Comprendre les droits
{: #permissions}

Vous devez disposer des règles d'accès appropriées avant de créer des instances d'{{site.data.keyword.cfee_full_notm}}. Pour plus d'informations, voir [Droits](https://cloud.ibm.com/docs/cloud-foundry/permissions.html).

## Etape 1 : Vérifiez que le compte {{site.data.keyword.Bluemix_notm}} peut créer des ressources d'infrastructure
{: #accountprep-environment}

Les instances CFEE sont déployées dans des noeuds worker Kubernetes à partir du service Kubernetes.  [Préparez votre compte IBM Cloud](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html) afin de vous assurer qu'il peut créer les ressources d'infrastructure nécessaires pour une instance CFEE.

## Etape 2 : Créez votre instance CFEE
{: #create-environment}

Avant de créer votre environnement CFEE, vérifiez que vous vous trouvez dans le compte {{site.data.keyword.Bluemix_notm}} sous lequel vous voulez créer l'environnement et que vous disposez des règles d'accès requises (étape 1 ci-dessus).

1.  Ouvrez le [catalogue](https://cloud.ibm.com/catalog) {{site.data.keyword.Bluemix_notm}}.

2.  Recherchez le service {{site.data.keyword.cfee_full_notm}} dans le catalogue et cliquez dessus pour ouvrir la page de présentation du service.  Cette première page présente les principales fonctions du service. Cliquez sur **Continuer**

3.  Configurez l'instance CFEE à créer :
    * Sélectionnez le plan _Aperçu technique Eirini_.
    * Entrez un **Nom** pour l'instance CFEE.
    * Sélectionnez un **Groupe de ressources** sous lequel l'environnement est regroupé. Seuls les groupes de ressources auxquels vous avez accès dans le compte IBM Cloud en cours sont répertoriés dans le menu déroulant _Groupes de ressources_, ce qui signifie que vous devez détenir le droit d'accès à au moins un groupe de ressources du compte pour pouvoir créer une instance CFEE.
    * Sélectionnez la **zone géographique** et l'**emplacement** où l'instance de service doit être mise à disposition. Consultez la liste des [emplacements et centres de données de mise à disposition disponibles](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") par zone géographique pour CFEE et les services de prise en charge. 

4. Les instances CFEE sont mises à disposition dans un cluster Kubernetes. Les cellules Cloud Foundry sont mises à disposition dans des zones worker du cluster Kuberentes. Vous pouvez configurer l'emplacement, le matériel et le chiffrement du cluster:
    * Sélectionnez l'isolement du matériel du cluster Kubernetes :   
      * _Virtual-shared_ : les ressources d'infrastructure du cluster, telles que l'hyperviseur et le matériel physique, sont réparties entre vous et d'autres clients IBM, mais chaque noeud worker est à votre service exclusif.
      * _Virtual-dedicated_ : les noeuds worker du cluster sont hébergés sur l'infrastructure dédiée à votre compte.
    * Les données du cluster sont chiffrées par défaut. Vous avez la possibilité de désactiver l'option _Chiffrer le disque local_.
    * Sélectionnez la **Zone géographique** et la **Région** où le cluster Kubernetes sera mis à disposition.
    * Sélectionnez les **Zones** où les noeuds worker Kubernetes seront déployés. Les réseaux locaux virtuels (VLAN) disponibles sont automatiquement récupérés pour les zones sélectionnées. Si aucun VLAN n'est disponible, ils sont automatiquement créés. Depuis CFEE version 2.2.0, les instances CFEE peuvent fonctionner derrière un **réseau isolé**. Vous pouvez mettre une instance CFEE à disposition dans un réseau isolé en sélectionnant des réseaux locaux virtuels (VLAN) privés dans le réseau isolé. Une fois l'instance CFEE créée, l'administrateur de réseau doit router les adresses IP des instances Compose for PostgreSQL et Cloudant Object Storage de CFEE, ainsi que des équilibreurs de charge d'application ([ALB, Application Load Balancer](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress)) du cluster Kubernetes dans le réseau isolé pour que l'instance CFEE devienne opérationnelle.
    
    Une fois l'instance CFEE créée, le cluster Kubernetes dans lequel l'instance est mise à disposition s'affiche (comme toutes les autres ressources de votre compte IBM Cloud) dans le [tableau de bord](https://cloud.ibm.com/dashboard/apps/) {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir la [documentation du service Kubernetes](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov).

5.  Configurez la capacité de l'environnement CFEE :
    * Sélectionnez le **Nombre de cellules** pour le CFEE. Ce sont les cellules d'application qui hébergeront les applications déployées dans l'environnement CFEE.  
    * Sélectionnez la **Taille de noeud**, qui détermine la capacité des cellules Cloud Foundry (UC et mémoire) .
    
    Outre les cellules d'application spécifiez ci-dessus, des _cellules de plan de contrôle_ supplémentaires sont créées et réservées à l'exploitation et au contrôle de la plateforme Cloud Foundry dans votre environnement CFEE. 

    **Remarque :** il est recommandé d'activer le spanning VLAN si les noeuds worker du cluster Kubernetes sont mis à disposition sur différents sous-réseaux.  Les noeuds worker présents sur différents sous-réseaux peuvent empêcher la connectivité entre eux si le spanning VLAN est désactivé.  Pour plus d'informations, voir la documentation [spanning VLAN](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning).
    
6.  Dans les zones **Compose for PostgreSQL**, sélectionnez l'une des organisations publiques, puis choisissez l'un des espaces disponibles dans cette organisation. L'instance de l'instance Compose for PostgreSQL sera mise à disposition dans l'espace sélectionné. Le service Compose for PostgreSQL est une dépendance requise du service CFEE.

    **Remarque :** sous _Compose for PostgreSQL_, seules les organisations situées à l'emplacement où vous prévoyez de mettre à disposition l'instance CFEE (voir l'étape 4 ci-dessus) et auxquelles vous avez accès sont disponibles pour sélection.  Au sein d'une organisation spécifique, seuls les espaces pour lesquels vous disposez de droits d'accès _développeur_ sont disponibles pour la sélection. 

7.  Le **Récapitulatif de la commande**, sur la droite de la page, indique le coût de l'instance CFEE et des services auxiliaires, ainsi qu'une estimation mensuelle totale.

8.  Cliquez sur **Créer** pour ouvrir le tableau de bord de l'environnement et afficher le statut et la progression de l'opération de création.

**Remarque :** une fois le processus de création démarré, une ligne de tableau pour le CFEE s'affiche dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, dans la _Liste de ressources_ et dans le [tableau de bord Cloud Foundry Environments](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments).  Le statut dans la ligne de tableau indique lorsque la création est terminée.

Le processus automatisé de création de l'environnement déploie l'infrastructure dans un cluster Kubernetes et la configure de sorte qu'elle soit prête pour utilisation. Ce processus prend entre 90 et 120 minutes.

Une fois l'environnement CFEE créé, vous recevez plusieurs courriers électroniques confirmant que l'instance CFEE et les services de prise en charge ont été mis à disposition, ainsi que des courriers électroniques mentionnant le statut des commandes correspondantes.

Lorsque vous créez une instance CFEE, trois instances de service de prise en charge supplémentaires sont créées dans le même compte IBM Cloud. Ces instances de service de prise en charge sont nommées d'après le nom de l'instance CFEE. Par conséquent, la création d'une instance CFEE entraîne la création de quatre instances de service dans le compte IBM Cloud :
* Une instance CFEE ("_cfeename_").
* Un cluster Kubernetes ("_cfeename_-cluster"). Le cluster fournit l'infrastructure dans laquelle l'instance CFEE est mise à disposition.
* Une instance Cloud Object Storage ("_cfeename_-cos"). Cette instance est utilisée pour stocker les données générées lors de la création des conteneurs d'applications CFEE (par exemple, packages d'applications téléchargés, packs de construction et exécutables compilés).
* Une instance Compose for PosgreSQL ("_cfeename_-postgres"). Cette instance est utilisée pour stocker des données Cloud Foundry sur l'instance CFEE (par exemple, audit de déploiement d'application, événements de démarrage et d'arrêt ; conservation d'enregistrements d'appartenance d'utilisateur CFEE, organisations, espaces, connexions d'applications et de service). 

## Etape 3 : Créez des organisations et des espaces
{: #create-orgsandspaces}

Une fois l'environnement {{site.data.keyword.cfee_full_notm}} créé, voir [Création d'organisations et d'espaces](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) pour savoir comment structurer l'environnement en créant des organisations et des espaces. Dans un environnement {{site.data.keyword.cfee_full_notm}}, les applications sont limitées à des espaces spécifiques. Un espace existe lui-même au sein d'une organisation spécifique. Les membres d'une organisation se partagent un plan d'établissement des quotas, des applications, des instances de service et des domaines personnalisés.

Lorsque vous créez une organisation, vous lui affectez un quota. Le quota définit des limites sur les ressources (mémoire, UC, etc.) disponibles pour cette organisation. Vous pouvez modifier le quota ultérieurement. Chaque environnement CFEE dispose d'un ensemble de quotas préconfigurés, mais vous pouvez également créer vos propres quotas personnalisés dans la page **Quotas** de l'interface utilisateur CFEE. Vous pouvez définir un quota personnalisé comme quota _par défaut_ en appelant l'action _Copier vers le quota par défaut_ à partir du menu de quota afin de copier les valeurs du quota personnalisé dans le quota par défaut.

**Remarque :** la page _Organisations Cloud Foundry_ accessible via le menu **_Gérer > Compte > Organisations Cloud Foundry_** de l'en-tête IBM Cloud du haut est conçue exclusivement pour les organisations IBM Cloud publiques, **pas pour les organisations CFEE**. Les organisations CFEE sont gérées dans la page _Organisations_ d'une instance CFEE.  Ouvrez l'interface utilisateur CFEE et cliquez sur la page **_Organisations_** pour créer et gérer des organisations pour cet environnement CFEE.

## Etape 4 : Ajoutez des utilisateurs aux organisations et espaces
{: #add-users}

[Ajoutez des utilisateurs](https://cloud.ibm.com/docs/cloud-foundry/add-users.html) à ces organisations et espaces avec des affectations de rôles spécifiques qui contrôlent leur niveau d'accès.  Pour pouvoir devenir membres d'organisations et d'espaces d'un environnement CFEE, les utilisateurs doivent préalablement obtenir un droit d'accès à l'instance CFEE. Voir [Droits](https://cloud.ibm.com/docs/cloud-foundry/permissions.html).

## Etape 5 : Déployez et affichez des applications
{: #deploy-apps}

Lorsque vous êtes prêt, vous pouvez [déployer l'application](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html) à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.  Affichez dans l'interface utilisateur la liste des applications déployées dans un espace CFEE spécifique ou globalement dans toutes les instances CFEE.  Vous pouvez également démarrer, arrêter ou supprimer des applications dans ces vues.

## Etape 6 : Créez ou ajoutez des instances de service IBM Cloud dans des espaces CFEE
{: #service-instances}

[Créez des services](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) ou [ajoutez des services existants](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) disponibles dans le compte IBM Cloud.  Une fois qu'une instance de service est disponible dans un espace CFEE, vous pouvez la lier aux applications CFEE qui sont déployées dans cet espace.

## Etape 7 : Liez des applications à des instances de service
{: #bind-apps}

[Liez votre application](https://console.bluemix.net/docs/cloud-foundry/binding.html) à un alias d'instance de service afin d'utiliser les fonctions du service.

Dans le [tableau de bord Cloud Foundry](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe"), vous pouvez afficher une vue consolidée de l'ensemble des applications et services, *Public* comme *Enterprise*.  Une fois dans le tableau de bord Cloud Foundry, cliquez sur *Public* dans le panneau de navigation de gauche pour voir les applications publiques et les services disponibles dans le compte IBM Cloud.  Cliquez sur *Enterprise* pour voir tous les environnements CFEE, les applications déployées dans des espaces CFEE et les services disponibles pour les espaces CFEE.
{:tip}

## Etape 8 : Installez la console Stratos pour gérer les applications (facultatif)
{: #install-stratos}

La console Stratos est un outil Web open source qui fonctionne avec Cloud Foundry. L'application de console Stratos peut éventuellement être installée et utilisée dans un environnement CFEE spécifique afin de gérer ses organisations, ses espaces et ses applications.

Les utilisateurs dotés du rôle d'administrateur ou d'éditeur IBM Cloud dans l'instance CFEE peuvent installer l'application de console Stratos dans cette instance CFEE.

Pour installer l'application de console Stratos :

1. Ouvrez l'instance CFEE dans laquelle vous voulez installer la console Stratos.
2. Cliquez sur **Installer la console Stratos** dans la page de présentation. Le bouton ne s'affiche que pour les utilisateurs ayant des droits d'administrateur ou d'éditeur sur cette instance CFEE.
3. Dans la boîte de dialogue Installer la console Stratos, sélectionnez une option d'installation. Vous pouvez installer l'application Stratos dans une cellule Cloud Foundry ou dans le cluster Kubernetes. Sélectionnez une version de la console Stratos ainsi que le nombre d'instances de l'application à installer. Si vous installez l'application de console Stratos dans une cellule Cloud Foundry, vous êtes invité à indiquer l'organisation et l'espace où déployer l'application.
4. Cliquez sur **Installer**.

L'installation de l'application prend environ 5 minutes. Une fois l'installation terminée, un bouton **Console Stratos** s'affiche dans la page de présentation à la place du bouton _Installer la console Stratos_. Le bouton _Console Stratos_ permet de démarrer la console et il est disponible pour tous les utilisateurs ayant accès à l'instance CFEE. Les affectations d'appartenance à une organisation et à un espace sont susceptibles de limiter les possibilités d'affichage et de gestion d'un utilisateur dans la console Stratos.

Pour démarrer la console Stratos :

1. Ouvrez l'instance CFEE dans laquelle la console Stratos a été installée.
2. Cliquez sur **Console Stratos** dans la page de présentation.
3. La console Stratos s'ouvre dans un onglet de navigateur distinct. A la première ouverture de la console, vous êtes invité à accepter deux avertissements consécutifs en raison de certificats autosignés.
4. Cliquez sur **Connexion** pour ouvrir la console. Aucune donnée d'identification n'est requise puisque l'application utilise vos données d'identification {{site.data.keyword.Bluemix_notm}}.


## Ressources supplémentaires
{: #additional-resources}

Vous pouvez effectuer des tâches d'administration dans une instance CFEE à l'aide de commandes d'interface de ligne de commande `ibmcloud CFEE`. Ces commandes vous permettent d'obtenir des informations sur une instance CFEE et de gérer ses organisations et espaces. Voir le site de [référence de commande CFEE d'interface de ligne de commande IBM Cloud](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

Vous trouverez des vidéos contenant des discussions et des démonstrations relatives à différents sujets concernant CFEE dans la [liste de lecture des vidéos CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

Des informations relatives à l'API CFEE sont disponibles dans la [documentation API CFEE](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
