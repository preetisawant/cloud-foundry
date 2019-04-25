---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Création d'un environnement
{: #create-environment}

## Prérequis
* Vérifiez que vous vous trouvez dans le compte {{site.data.keyword.Bluemix_notm}} où vous voulez créer l'environnement.
* Vérifiez que vous disposer des [droits](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html) appropriés avant de créer des instances d'{{site.data.keyword.cfee_full_notm}}. 
* [Préparez votre compte IBM Cloud](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html) afin de vous assurer qu'il peut créer les ressources d'infrastructure nécessaires pour une instance CFEE (les instances CFEE sont déployées dans des noeuds worker Kubernetes à partir du service Kubernetes).  

## Création d'une instance CFEE
1.  Ouvrez le [catalogue](https://cloud.ibm.com/catalog) {{site.data.keyword.Bluemix_notm}}.

2.  Recherchez le service {{site.data.keyword.cfee_full_notm}} dans le catalogue et cliquez dessus pour ouvrir la page de présentation du service.  Cette première page présente les principales fonctions du service. Cliquez sur **Continuer**

3.  Configurez l'instance CFEE à créer :
    * Sélectionnez un plan. Voir la section [Aperçu technique Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) pour une description des limitations applicables à ce plan.
    * Entrez un **Nom** pour l'instance CFEE.
    * Sélectionnez un **Groupe de ressources** sous lequel l'environnement est regroupé. Seuls les groupes de ressources auxquels vous avez accès dans le compte IBM Cloud en cours sont répertoriés dans le menu déroulant _Groupes de ressources_, ce qui signifie que vous devez détenir le droit d'accès à au moins un groupe de ressources du compte pour pouvoir créer une instance CFEE.
    * Sélectionnez la **zone géographique** et l'**emplacement** où l'instance de service doit être mise à disposition. Consultez la liste des [emplacements et centres de données de mise à disposition disponibles](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") par zone géographique pour CFEE et les services de prise en charge. 

4. Les instances CFEE sont mises à disposition dans un cluster Kubernetes. Les cellules Cloud Foundry sont mises à disposition dans des zones worker du cluster Kuberentes. Vous pouvez configurer l'emplacement, le matériel et le chiffrement du cluster:
    * Sélectionnez l'isolement du matériel du cluster Kubernetes :   
      * _Virtual-shared_ : les ressources d'infrastructure du cluster, telles que l'hyperviseur et le matériel physique, sont réparties entre vous et d'autres clients IBM, mais chaque noeud worker est à votre service exclusif.
      * _Virtual-dedicated_ : les noeuds worker du cluster sont hébergés sur l'infrastructure dédiée à votre compte.
    * Les données du cluster sont chiffrées par défaut. Vous avez la possibilité de désactiver l'option _Chiffrer le disque local_.
    * Sélectionnez la **Zone géographique** et la **Région** où le cluster Kubernetes sera mis à disposition.
    * Sélectionnez les **Zones** où les noeuds worker Kubernetes seront déployés. Vous avez la possibilité de mettre à disposition les noeuds worker dans la même zone (**Zone unique**) ou dans plusieurs zones (**Multizone**). **Remarque :** la création d'un environnement CFEE à plusieurs zones nécessite un [spanning VLAN](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning), qui est également pris en charge lorsque le compte {{site.data.keyword.Bluemix_notm}} a le [Service VRF activé](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).
    
    Les réseaux locaux virtuels (VLAN) disponibles sont automatiquement récupérés pour les zones sélectionnées. Si aucun VLAN n'est disponible, ils sont automatiquement créés.
    
    **Remarque : mise à disposition sur un réseau isolé** vous pouvez cibler des VLAN dans un réseau isolé. Lorsque l'instance CFEE est créée dans un réseau isolé, les règles du réseau isolé (par exemple, des règles calico ou VRA) doivent autoriser TOUS les accès sortants depuis l'instance CFEE pour que la mise à disposition de l'environnement CFEE aboutisse. Une fois l'environnement CFEE créé, des restrictions d'accès sortant peuvent être rétablies, sauf pour l'accès sortant vers certains services et micro-services dans IBM Cloud. Pour plus d'informations, voir la documentation relative au [fonctionnement dans un réseau isolé](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network).
    
    Une fois l'instance CFEE créée, le cluster Kubernetes dans lequel l'instance est mise à disposition s'affiche (comme toutes les autres ressources de votre compte IBM Cloud) dans le [tableau de bord](https://https://cloud.ibm.com/catalog/dashboard/apps/) {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir la [documentation du service Kubernetes](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov).

5.  Configurez la capacité de l'environnement CFEE :
    * Sélectionnez le **Nombre de cellules** pour le CFEE. Ce sont les cellules d'application qui hébergeront les applications déployées dans l'environnement CFEE.  
    * Sélectionnez la **Taille de noeud**, qui détermine la capacité des cellules Cloud Foundry (UC et mémoire) .
    
    Outre les cellules d'application spécifiez ci-dessus, des _cellules de plan de contrôle_ supplémentaires sont créées et réservées à l'exploitation et au contrôle de la plateforme Cloud Foundry dans votre environnement CFEE. 

    **Remarque :** il est recommandé d'activer le spanning VLAN si les noeuds worker du cluster Kubernetes sont mis à disposition sur différents sous-réseaux.  Les noeuds worker présents sur différents sous-réseaux peuvent empêcher la connectivité entre eux si le spanning VLAN est désactivé.  Pour plus d'informations, voir la documentation [spanning VLAN](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning).

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

## Plan d'aperçu technique Eirini
{: #eirini}

 Le plan d'aperçu technique Eirini vous permet d'explorer un environnement CFEE en utilisant le système Kubernetes natif comme planificateur de conteneur (au lieu de Diego). Le planificateur Kubernetes est utilisé dans l'environnement CFEE pour déployer et exécuter des applications dans le contexte d'exécution d'application Cloud Foundry, ajouter des utilisateurs, créer une organisation et des espaces, déployer des applications et lier ces applications à des services. Voir la documentation relative au [projet Eirini](https://www.cloudfoundry.org/project-eirini/) pour plus d'informations sur le projet d'incubateur Eirini de Cloud Foundry Foundation.
 Les limitations suivantes s'appliquent aux instances CFEE crées à partir du plan d'aperçu technique Eirini :
 
* Kubernetes avec `containerd` n'est pas pris en charge. Seules les versions Kubernetes qui utilisent Docker au lieu de `containerd` sont prises en charge. La dernière version d'IBM Container Service (IKS) qui prend en charge Docker est la version 1.10.
* Cloud Foundry SSH n'est pas pris en charge.
* La transmission d'image Docker via une commande `cf push` n'est pas prise en charge.
* La préproduction Eirini native Kubernetes n'est pas prise en charge. Les instances CFEE créées à partir du plan d'aperçu technique Eirini utilisent Eirini pour exécuter les applications, mais pas pour leur constitution. Des cellules Diego sont encore utilisées pour la constitution des applications.
* Le redémarrage d'instances d'application spécifiques (`cf restart-app-instance`) n'est pas pris en charge.

 
