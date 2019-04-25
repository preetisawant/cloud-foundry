---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Nouveautés dans IBM Cloud Foundry Enterprise Environment

Ce document décrit les nouveautés spécifiques de chaque version publiée à ce jour pour le service {{site.data.keyword.cfee_full_notm}}.

## Version 2.2.0
{: #v220}

_Date d'édition :_ 01/04/2019

CFEE version 2.2.0 inclut les versions suivantes de ses composants constitutifs :
* Cloud Foundry : version 2.7.1.15.5
* API Cloud Foundry : version 2.115.0
* Packs de construction CFEE : version 0.1.5
* IBM Kubernetes Service : pas de mise à jour de version fournie.  **Important :** il est recommandé de procéder à la mise à jour du cluster Kubernetes de CFEE vers la version 1.13 avant la mise à jour de CFEE vers la version 2.2.0 (requis lorsque l'instance CFEE fonctionne dans un réseau isolé).

Les modifications suivantes ont été publiées dans la version 2.2.0 du service {{site.data.keyword.cfee_full_notm}} (CFEE). Pour mettre à jour votre version de CFEE, accédez à la page **Mises à jour et mise à l'échelle** dans l'interface utilisateur de CFEE, puis cliquez sur **Mettre à jour** :

* Nouvelle option pour **créer** une instance CFEE dans un cluster Kubernetes **multizone**. Les instances CFEE créées dans un cluster multizone distribuent des instances d'application, non seulement aux noeuds worker d'un centre de données, mais également aux centres de données, ce qui rend vos applications plus résilientes face aux indisponibilités de l'infrastructure. De plus, les CFEE multizones peuvent être **mis à l'échelle** en ajoutant des cellules supplémentaires ou en en supprimant des zones en cours. Vous ne pouvez ni ajouter ni supprimer des zones d'un environnement CFEE multizone une fois l'instance CFEE créée.
* Les instances CFEE version 2.2.0 peuvent désormais [fonctionner dans un **réseau isolé**](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network). Si l'instance CFEE est déployée dans des réseaux locaux virtuels à partir d'un réseau isolé, certains noeuds finaux (adresses IP) [doivent être identifiés et routés correctement](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points) pour que l'instance CFEE soit opérationnelle. Une instance CFEE nécessite un cluster Kubernetes version 1.13 pour fonctionner dans un réseau isolé.
* Nouvelle fonctionnalité de liaison d'applications (déployées dans un espace CFEE) à des instances de service via le réseau IBM interne. La fonctionnalité permet de consommer les services qui prennent en charge IBM Cloud Service Endpoint sans accéder à l'Internet public.
* Outils de **surveillance** :
    * Les outils de surveillance (Prometheus, Grafana et Alertmanager) ne sont plus mis à disposition par défaut lorsque vous créez un environnement CFEE. Dans CFEE version 2.2.0, les outils de surveillance ne sont mis à disposition que lorsqu'ils sont explicitement activés par des administrateurs CFEE.  De plus, une fois activés, les outils de surveillance ne sont plus mis à disposition dans les noeuds worker du plan de contrôle CFEE. Ils sont mis à disposition dans leurs propres noeuds worker, en dehors du plan de contrôle. Pour activer et mettre à disposition des outils de surveillance, accédez à la page _Surveillance_ de CFEE (dans le panneau de navigation de gauche), puis cliquez sur **Activer la surveillance**. 
    * Lorsque vous mettez à jour un environnement CFEE existant vers la version 2.2.0, les outils de surveillance existants sont supprimés du plan de contrôle. Toute configuration personnalisée existante des outils de surveillance est perdue. 
    *  Nouvelle fonctionnalité de remplacement de la [configuration Alertmanager](https://prometheus.io/docs/alerting/configuration/) par défaut par une configuration personnalisée qui vous autorise à personnaliser le traitement, le regroupement et le réacheminement des notifications d'alertes. Dans la page _Surveillance_ vous pourrez _Télécharger_ le fichier de configuration par défaut et _Transférer_ un fichier de configuration depuis votre système de fichiers local file.  Affichez un [exemple](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml) de fichier de configuration.
* Nouvelle fonctionnalité d'étiquetage des instances CFEE dans la [_Liste de ressources_](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}} et dans l'interface utilisateur CFEE.
* Améliorations générales de l'acquis utilisateur concernant le **tableau de bord Cloud Foundry** [ {{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/dashboard/cloudfoundry/overview). Le _tableau de bord Cloud Foundry_ affiche des vues globales des services publics, des applications et des instances CFEE associés à un alias dans des espaces CFEE. 

**Remarque :** un nouveau plan d'**aperçu technique Eirini** est disponible lors de la création d'une instance CFEE. Le plan est indépendant de la version 2.2.0 décrite précédemment, qui s'applique uniquement au plan _Standard_. Le plan d'aperçu technique Eirini vous permet d'explorer un environnement CFEE en utilisant le système Kubernetes natif comme planificateur de conteneur (au lieu de Diego). Pour plus d'informations, voir [Initiation à l'aperçu technique Eirini](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini).

Regardez une démonstration présentant les nouveautés de CFEE version 2.1.0 dans cette [courte vidéo](https://ibm.biz/CFEE-V220){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").  


## Version 2.1.1
{: #v211}

_Date d'édition :_ 20/03/2019

Les modifications suivantes ont été publiées dans la version 2.1.1 du service {{site.data.keyword.cfee_full_notm}} (CFEE). Pour mettre à jour votre version de CFEE, accédez à la page _Mises à jour et mise à l'échelle_ dans l'interface utilisateur de CFEE :

* Problèmes résolus empêchant la mise à disposition 


## Version 2.1.0
{: #v210}

_Date d'édition :_ 20/02/2019

**Remarque :** vous ne pouvez effectuer une mise à jour vers cette version qu'à partir de la version **2.0.2**. Passez à la version 2.0.2 avant de mettre à jour à la version 2.1.0.

Les modifications suivantes ont été publiées dans la version 2.1.0 du service {{site.data.keyword.cfee_full_notm}} (CFEE). Pour mettre à jour votre version de CFEE, accédez à la page **Mises à jour et mise à l'échelle** dans l'interface utilisateur de CFEE, puis cliquez sur **Mettre à jour** :

* Nouvelle fonctionnalité de mise à l'échelle automatique des instances d'application Cloud Foundry sur la base de règles personnalisées. La mise à l'échelle automatique est accessible à partir de l'interface de ligne de commande et de la console Stratos. La console Stratos peut éventuellement être installée et lancée à partir de la page _Vue d'ensemble_ de l'interface utilisateur CFEE. Dans la page _Applications_ de la console Stratos, sélectionnez une  application et recherchez l'onglet **Mise à l'échelle automatique**. Cliquez sur *Créer une règle* pour lancer l'éditeur de mise à l'échelle automatique afin de définir la règle de mise à l'échelle pour l'application cible.
  Pour plus d'informations, voir la [documentation relative à la mise à l'échelle automatique](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps).
* Nouvelle fonctionnalité de gestion des packs de construction depuis l'interface utilisateur CFEE, y compris le déplacement par glisser-déplacer d'un pack de construction dans la liste des priorités. La fonctionnalité est disponible dans la nouvelle page **Packs de construction** de l'interface utilisateur CFEE (pas dans la console Stratos). Dans cette édition, seuls les fichiers zip de pack de construction de 1 Mo maximum peuvent être ajoutés ou mis à jour via l'interface utilisateur. Vous pouvez télécharger des fichiers zip de pack de construction de plus de 1 Mo à l'aide des commandes `cf create-buildpack` et `cf update-buildpack`. 
* Nouvelle fonctionnalité de gestion des quotas d'organisation à partir de l'interface utilisateur, y compris l'affichage des organisations qui utilisent un quota spécifique. La fonctionnalité est disponible dans la nouvelle page **Quotas** de l'interface utilisateur CFEE (pas dans la console Stratos). Vous pouvez créer de nouveaux quotas et éditer ceux existants. Vous pouvez également mettre à jour les valeurs du quota par défaut avec les valeurs issues d'un quota existant en appelant **Copier vers le quota par défaut** depuis le menu du quota.
* Une nouvelle page **Initiation** dans l'interface utilisateur vous guide dans les tâches les plus importantes de configuration et d'utilisation de l'environnement.
* Vous pouvez ajouter des **étiquettes** à une instance CFEE dans la liste des ressources IBM Cloud. Les étiquettes ajoutées dans la liste des ressources figurent également dans l'en-tête de la page Vue d'ensemble de CFEE.
* **Cloud Foundry** version 2.7.21.
* La console **Stratos** version 2.3.0, qui inclut un correctif de sécurité. La mise à jour de la version de CFEE ne met pas à jour la version de la console Stratos. Vous devez supprimer puis réinstaller la console Stratos (dans la page Vue d'ensemble de CFEE), qui sélectionne automatiquement la version la plus récente de la console Stratos.
* Les utilisateurs peuvent accéder à la page du **cluster** Kubernetes de CFEE depuis le menu déroulant dynamique de la page Vue d'ensemble de CFEE.

**Remarque :** la mise à jour de CFEE vers la version 2.1.0 à partir d'une version 2.0.x s'effectue en une seule opération de _mise à jour_ qui met automatiquement à jour, dans l'ordre, le plan de contrôle et les cellules. Si vous effectuez une mise à jour depuis une version 1.x.x , la mise à jour nécessite deux opérations de _mise à jour_ distinctes, une pour mettre à jour (en premier) le plan ce contrôle et une autre pour mettre à jour les cellules.

Regardez une démonstration présentant les nouveautés de CFEE version 2.1.0 dans cette [courte vidéo](https://ibm.biz/CFEE-V210){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").  


## Version 2.0.2
{: #v202}

_Date d'édition :_ 08/02/2019

Les modifications suivantes ont été publiées dans la version 2.0.2 du service {{site.data.keyword.cfee_full_notm}} (CFEE). Pour mettre à jour votre version de CFEE, accédez à la page _Mises à jour et mise à l'échelle_ dans l'interface utilisateur de CFEE :

* Problèmes résolus empêchant les mises à jour de version. Cette version est un pré-requis pour la mise à jour vers la version **2.1.0**.


## Version 2.0.1
{: #v201}

_Date d'édition :_ 10/01/2019

Les modifications suivantes ont été publiées dans la version 2.0.1 du service {{site.data.keyword.cfee_full_notm}} (CFEE). Pour mettre à jour votre version de CFEE, accédez à la page _Mises à jour et mise à l'échelle_ dans l'interface utilisateur de CFEE :

* Problème résolu qui empêchait le bon fonctionnement des domaines personnalisés.
* Problème résolu relatif à des métriques d'organisation non disponibles lors de l'extraction de nouvelles métriques.


## Version 2.0.0
{: #v200}

_Date d'édition :_ 13/12/2018

Les modifications suivantes ont été publiées dans la version 2.0.0 du service {{site.data.keyword.cfee_full_notm}} (CFEE). Pour mettre à jour votre version de CFEE, accédez à la page _Mises à jour et mise à l'échelle_ dans l'interface utilisateur de CFEE :

* Résilience de la mise à jour de la version CFEE améliorée.
* Améliorations au niveau de la disponibilité opérationnelle et la résilience des instances CFEE.
* Certificats côté client pour un accès plus sécurisé aux applications, ce qui permet au serveur ne n'accorder l'accès aux applications qu'aux clients certifiés.
* Lorsqu'une instance CFEE est créée, le cluster Kubernetes de prise en charge et l'instance de service Cloud Object Storage sont désormais créés dans le même groupe de ressources que l'instance de service CFEE (et non sous le groupe de ressources par défaut).
* Correctif de sécurité.
* Améliorations apportées à l'interface de ligne de commande `ibmcloud cfee` :
    * Nouvelles commandes de création d'une instance de service IBM Cloud à partir d'un espace CFEE et d'ajout de cette instance de service à cet espace CFEE (`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`).
    * Nouvelles commandes de mise à l'échelle de la capacité d'un CFEE (`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`).
    * Améliorations apportées à la commande de gestion des instances CFEE (`ibmcloud cfee environments`).
    
      Mettez à jour l'interface de ligne de commande ibmcloud (`ibmcloud update`) pour accéder à ces améliorations de commande, puis exécutez la commande `ibmcloud cfee -help` pour obtenir plus d'informations.
      
**Remarque** : la mise à jour d'une instance CFEE vers la version 2.0.0 ne nécessite qu'une seule action _update_ qui met à jour à la fois le plan de contrôle et les cellules. Il n'est pas nécessaire d'effectuer des mises à jour séparées pour les cellules et pour le plan de contrôle CFEE.


## Version 1.1.2
{: #v112}

_Date d'édition :_ 07/12/2018

Les modifications suivantes ont été publiées dans la version 1.1.2 du service {{site.data.keyword.cfee_full_notm}} :
* De nouveaux centres de données à Chennai (che01) et Milan (mil01) sont désormais disponibles pour la mise à disposition d'instance CFEE.
* Correctif de sécurité.

## Version 1.1.1
{: #v111}

_Date d'édition : _ 28/11/2018

Les modifications suivantes ont été publiées dans la version 1.1.1 du service {{site.data.keyword.cfee_full_notm}} :
* Correctif de sécurité.
   
## Version 1.1.0
{: #v110}

_Date d'édition : _ 16/11/2018

Les modifications suivantes ont été publiées dans la version 1.1.0 du service {{site.data.keyword.cfee_full_notm}} :

* Nouvelles fonctions :
   * Des instances CFEE peuvent être mises à disposition sur des noeuds worker Kubernetes [virtuels-dédiés](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) hébergés sur une infrastructure réservée à votre compte IBM Cloud.
   * Un nouveau centre de données à Tokyo (tok05) est disponible pour la mise à disposition d'instances CFEE.
   * [Mise à jour](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) d'une instance CFEE vers une nouvelle version.
   * [Mise à l'échelle](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) de la capacité d'une instance CFEE en ajoutant ou en supprimant des cellules Cloud Foundry.
   * [Audit](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) des activités Cloud Foundry via l'intégration à une instance de service IBM Cloud Activity Tracker configurée automatiquement.
   * Persistance des [événements de journal](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) Cloud Foundry via une instance de service IBM Cloud Log Analysis configurée automatiquement.
   * Vue Diagnostic d'intégrité qui indique l'état opérationnel des composants CFEE.
   * Nouvelles commandes permettant d'effectuer des actions liées à CFEE sur l'interface de ligne de commande :
     * Commandes `ibmcloud cfee create`, `ibmcloud cfee create-locations` et `ibmcloud cfee create-status` permettant de créer des instances CFEE à partir de l'interface de ligne de commande, d'obtenir la liste des centres de données disponibles dans lesquels un environnement CFEE peut être mis à disposition et de vérifier le statut de mise à disposition d'un environnement CFEE que vous créez.
     * Commandes `ibmcloud cfee create-permission-get` and `ibmcloud cfee create-permission-set`  [](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) permettant d'extraire et de définir les droits requis pour créer des instances CFEE. Les commandes agrègent et simplifient la définition de droits pour le service CFEE et pour les services de prise en charge requis.
     * Commande `ibmcloud catalog blacklist` qui simplifie le [contrôle de visibilité](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) des services IBM Cloud pour les utilisateurs dans un compte IBM Cloud.

* Problèmes résolus :
   *  Problème résolu : erreur sporadique lors de l'accès aux métriques de cellule
<br/>   
Regardez une démonstration présentant les nouveautés de CFEE v1.1.0 dans cette [courte vidéo](https://ibm.biz/CFEE-V110){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").  Vous trouverez d'autres vidéos sur différents sujets concernant CFEE dans la [liste de lecture des vidéos CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
