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

# Tutoriel d'initiation
{: #getting-started}

L'environnement CFEE ({{site.data.keyword.cfee_full}}) est une plateforme cloud pour l'hébergement d'applications et de services dans le cloud. {{site.data.keyword.cfee_full_notm}} facilite la mise à l'échelle des applications à mesure de l'augmentation de la consommation, en simplifiant le contexte d'exécution, le middleware et l'infrastructure de sorte que vous puissiez vous concentrer sur le développement d'applications.
{: shortdesc}

Ce tutoriel d'initiation montre comment créer un environnement {{site.data.keyword.cfee_full_notm}}, ajouter des utilisateurs, créer une organisation et des espaces, déployer des applications et lier ces applications à des services.

**Remarque :** la procédure suivant s'applique aux environnements CFEE créés à partir du plan **Standard**. Si l'environnement CFEE a été créé à partir du plan **Aperçu technique Eirini**, effectuez **uniquement les étapes 1 à 6** et l'étape **11**. Les fonctionnalités décrites dans les étapes 8 à 11 ne sont pas prises en charge dans le plan _Aperçu technique Eirini_. Voir [Initiation à l'aperçu technique Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).
Le plan _Aperçu technique Eirini_ vous permet d'explorer un environnement CFEE en utilisant le système Kubernetes natif comme planificateur de conteneur (au lieu de Diego). Le planificateur Kubernetes est utilisé dans l'environnement CFEE pour déployer et exécuter des applications dans le contexte d'exécution d'application Cloud Foundry, ajouter des utilisateurs, créer une organisation et des espaces, déployer des applications et lier ces applications à des services.  

## Etape 1 : Créez votre instance CFEE
{: #create-environment}

Vous pouvez créer une instance d'environnement CFEE ({{site.data.keyword.cfee_full_notm}}) à partir du catalogue {{site.data.keyword.Bluemix_notm}}. Avant de créer l'instance CFEE, consultez la documentation relative à la [création d'un environnement](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment) pour vous aider à préparer votre compte {{site.data.keyword.Bluemix_notm}} de manière à disposer des droits requis et pour les étapes de création de l'instance CFEE.


## Etape 2 : Créez des organisations et des espaces
{: #create-orgsandspaces}

Une fois l'environnement {{site.data.keyword.cfee_full_notm}} créé, voir [Création d'organisations et d'espaces](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html) pour savoir comment structurer l'environnement en créant des organisations et des espaces. Dans un environnement {{site.data.keyword.cfee_full_notm}}, les applications sont limitées à des espaces spécifiques. Un espace existe lui-même au sein d'une organisation spécifique. Les membres d'une organisation se partagent un plan d'établissement des quotas, des applications, des instances de service et des domaines personnalisés.

Lorsque vous créez une organisation, vous lui affectez un quota. Le quota définit des limites sur les ressources (mémoire, UC, etc.) disponibles pour cette organisation. Vous pouvez modifier le quota ultérieurement. Chaque environnement CFEE dispose d'un ensemble de quotas préconfigurés, mais vous pouvez également créer vos propres quotas personnalisés dans la page **Quotas** de l'interface utilisateur CFEE. Vous pouvez définir un quota personnalisé comme quota _par défaut_ en appelant l'action _Copier vers le quota par défaut_ à partir du menu de quota afin de copier les valeurs du quota personnalisé dans le quota par défaut.

**Remarque :** la page _Organisations Cloud Foundry_ accessible via le menu **_Gérer > Compte > Organisations Cloud Foundry_** de l'en-tête IBM Cloud du haut est conçue exclusivement pour les organisations IBM Cloud publiques, **pas pour les organisations CFEE**. Les organisations CFEE sont gérées dans la page _Organisations_ d'une instance CFEE.  Ouvrez l'interface utilisateur CFEE et cliquez sur la page **_Organisations_** pour créer et gérer des organisations pour cet environnement CFEE.

## Etape 3 : Ajoutez des utilisateurs aux organisations et espaces
{: #add-users}

[Ajoutez des utilisateurs](https://console.bluemix.net/docs/cloud-foundry/add-users.html) à ces organisations et espaces avec des affectations de rôles spécifiques qui contrôlent leur niveau d'accès.  Pour pouvoir devenir membres d'organisations et d'espaces d'un environnement CFEE, les utilisateurs doivent préalablement obtenir un droit d'accès à l'instance CFEE. Voir [Droits](https://console.bluemix.net/docs/cloud-foundry/permissions.html).

## Etape 4 : Déployez et affichez des applications
{: #deploy-apps}

Lorsque vous êtes prêt, vous pouvez [déployer l'application](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html) à l'aide de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.  Affichez dans l'interface utilisateur la liste des applications déployées dans un espace CFEE spécifique ou globalement dans toutes les instances CFEE.  Vous pouvez également démarrer, arrêter ou supprimer des applications dans ces vues.

## Etape 5 : Créez ou ajoutez des instances de service IBM Cloud dans des espaces CFEE
{: #service-instances}

[Créez des services](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace) ou [ajoutez des services existants](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) disponibles dans le compte IBM Cloud.  Une fois qu'une instance de service est disponible dans un espace CFEE, vous pouvez la lier aux applications CFEE qui sont déployées dans cet espace.

## Etape 6 : Liez des applications à des instances de service
{: #bind-apps}

[Liez votre application](https://cloud.ibm.com/docs/cloud-foundry/binding.html) à un alias d'instance de service afin d'utiliser les fonctions du service.

Dans le [tableau de bord Cloud Foundry](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe"), vous pouvez afficher une vue consolidée de l'ensemble des applications et services, *Public* comme *Enterprise*.  Une fois dans le tableau de bord Cloud Foundry, cliquez sur *Public* dans le panneau de navigation de gauche pour voir les applications publiques et les services disponibles dans le compte IBM Cloud.  Cliquez sur *Enterprise* pour voir tous les environnements CFEE, les applications déployées dans des espaces CFEE et les services disponibles pour les espaces CFEE.
{:tip}

## Etape 7 : Activez l'audit et la persistance de journalisation (facultatif)
{: #enable-auditingandlogging}

Activez l'environnement pour les [événements d'audit](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) et la [persistance de journalisation](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging).

## Etape 8 : Activez les outils de surveillance (facultatif)
{: #enable-monitoring}

Les outils de surveillance ne sont pas automatiquement mis à disposition sur les instances CFEE version 2.2.0 ou ultérieure. Les administrateurs CFEE peuvent [activer les outils de surveillance](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring) une fois l'instance CFEE créée. L'ensemble des outils de surveillance inclut Prometheus, Grafana et Alertmanager.

## Etape 9 : Créez et sécurisez les domaines Cloud Foundry (facultatif)
{: #create-domains}

Créez des [domaines](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains) pour toutes les applications du CFEE (domaines partagés) ou pour une organisation spécifique (domaines privés) et sécurisez-les à l'aide de certificats SSL.

## Etape 10 : Configurez l'ordre de priorité des packs de construction Cloud Foundry
{: #create-buildpacks}

Les packs de construction fournissent le support d'exécution pour les applications déployées dans un environnement Cloud Foundry, en configurant automatiquement le contexte d'exécution d'une application et en gérant ses dépendances. Cloud Foundry inclut un ensemble de packs de construction pour les langues et les infrastructures couramment utilisées. [En savoir plus](https://docs.cloudfoundry.org/buildpacks/) sur les packs de construction Cloud Foundry.  

Vous pouvez créer et télécharger des packs de construction personnalisés dans la page **Packs de construction** de l'interface utilisateur CFEE. Les packs de construction ont une position ordinale dans la liste des priorités. En phase de préproduction d'une application, Cloud Foundry vérifie la compatibilité de l'application par rapport à l'ensemble de packs de construction, en commençant à la position 1. Les vérifications de compatibilité s'effectuent en descendant dans la liste des priorités jusqu'à trouver un pack de construction compatible. Assurez-vous que la séquence de priorités de l'ensemble de packs de construction répond aux besoins de vos équipes de développement. Vous pouvez modifier la position d'un pack de construction dans la séquence des priorités en faisant glisser son nom puis en le déposant à un autre emplacement dans la liste. Vous pouvez également gérer les packs de construction via l'[interface de ligne de commande Cloud Foundry](https://docs.cloudfoundry.org/adminguide/buildpacks.html).

## Etape 11 : Installez la console Stratos pour gérer les applications (facultatif)
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
