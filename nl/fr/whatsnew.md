---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Nouveautés dans IBM Cloud Foundry Enterprise Environment

Ce document décrit les nouveautés spécifiques de chaque version publiée à ce jour pour le service {{site.data.keyword.cfee_full_notm}}.


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
