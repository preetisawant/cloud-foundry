---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Nouveautés dans IBM Cloud Foundry Enterprise Environment

Ce document décrit les nouveautés spécifiques de chaque version publiée à ce jour pour le service {{site.data.keyword.cfee_full_notm}}. 

## Version 1.1.0
{: #v101}

_Date d'édition : _ 16/11/2018 

Les modifications suivantes ont été publiées dans la version 1.1.0 du service {{site.data.keyword.cfee_full_notm}} :

* Nouvelles fonctions :
   * [Mise à jour](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update) d'une instance CFEE vers une nouvelle version.
   * [Mise à l'échelle](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale) de la capacité d'une instance CFEE en ajoutant ou en supprimant des cellules Cloud Foundry. 
   * [Audit](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) des activités Cloud Foundry via l'intégration à une instance de service IBM Cloud Activity Tracker configurée automatiquement.
   * Persistance des [événements de journal](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) Cloud Foundry via une instance de service IBM Cloud Log Analysis configurée automatiquement. 
   * Nouvelles [commandes](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating) `ibmcloud cfee` permettant d'extraire et de définir des droits pour créer des instances CFEE. Les commandes agrègent et simplifient la définition de droits pour le service CFEE et pour les services de prise en charge requis. 
   * Nouvelle commande `ibmcloud catalog blacklist` permettant de simplifier le [contrôle de la visibilité](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility) des services IBM Cloud pour les utilisateurs dans un compte IBM Cloud. 

* Problèmes résolus :
   *  Problème résolu : erreur sporadique lors de l'accès aux métriques de cellule
   
Regardez une démonstration présentant les nouveautés de CFEE v1.1.0 dans cette [courte vidéo](https://ibm.biz/CFEE-V110){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

Vous trouverez d'autres vidéos sur différents sujets concernant CFEE dans la [liste de lecture des vidéos CFEE](https://ibm.biz/CFEE-Playlist){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
