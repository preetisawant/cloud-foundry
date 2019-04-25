---

copyright:
  years: 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Surveillance 
{: #monitoring}

La surveillance d'une instance {{site.data.keyword.cfee_full}} et de l'infrastructure prise en charge est assurée par un ensemble d'outils open source composé de Prometheus et Grafana.  La solution permet d'analyser, de visualiser et de gérer les alertes liées aux métriques de l'environnement Cloud Foundry.  Trois consoles Web permettent de mettre en oeuvre la surveillance : la console Grafana, la console Prometheus et la console Prometheus Alert Manager.

A compter de CFEE version 2.2.0, les outils de surveillance ne sont pas activés par défaut lorsqu'un environnement est créé. Les administrateurs peuvent activer la surveillance une fois l'environnement créé. Dans l'interface utilisateur CFEE, accédez à la page _Surveillance_ dans le panneau de navigation de gauche, puis cliquez sur **Activer**. L'activation de la surveillance met automatiquement à disposition des noeuds worker Kubernetes supplémentaires (dans le même compte IBM Cloud) et installe les outils de surveillance dans ces noeuds worker.

**Remarque :** l'accès à la fonction de surveillance dans une instance {{site.data.keyword.cfee_full}} nécessite d'avoir le rôle _Administrateur_ ou _Editeur_ dans l'instance CFEE et le rôle _Opérateur_ dans le cluster Kubernetes qui prend en charge l'instance CFEE (en plus du rôle _Afficheur_ dans le groupe de ressources où l'instance CFEE est regroupée). Le nom par défaut du cluster Kubernetes qui prend en charge l'instance CFEE est _`<CFEEname>`-cluster_. 

## Prometheus
{: #prometheus}

Prometheus est un kit d'outils open source d'alerte et de surveillance des systèmes. Depuis sa création en 2012, de nombreuses entreprises et organisations ont adopté Prometheus et le projet dispose d'une communauté de développeurs et d'utilisateurs très actifs. 
Il s'agit d'un projet open source autonome géré indépendamment de toute société. Pour mettre l'accent sur cette caractéristique et clarifier la structure de gouvernance du projet, Prometheus a rejoint en 2016 la Cloud Native Computing Foundation (fondation pour l'informatique native Cloud) en tant que second projet hébergé, après Kubernetes. Voir la [documentation Prometheus](https://prometheus.io/docs/introduction/overview/) pour plus d'informations.

L'écosystème Prometheus est constitué de nombreux composants, dont beaucoup sont optionnels :

* Le serveur principal Prometheus qui amasse et stocke des données de séries temporelles.</li>
* [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) pour gérer les alertes.</li>
* Divers exportateurs à usages spécifiques tels qu'exportateur de noeud, exportateur de boîte noire, etc.</li>
* Une passerelle de transmission pour la prise en charge des travaux de courte durée.</li>

Prometheus rassemble des métriques à partir de travaux instrumentés, soit directement, soit via une passerelle de transmission intermédiaire pour les travaux de courte durée. Prometheus stocke tous les échantillons rassemblés en local et exécute des règles sur ces données pour les agréger et enregistrer de nouvelles séries temporelles à partir de données existantes ou pour générer des alertes. 

## Grafana
{: #grafana}

Grafana est une plateforme d'analyse open source pour toutes les métriques que Prometheus collecte. La version de Grafana déployée dans votre cluster est déjà configurée pour utiliser la base de données Prometheus sous-jacente. Elle contient également certains tableaux de bord Grafana très utiles.  Voir la [documentation Grafana](http://docs.grafana.org/guides/getting_started/) pour plus d'informations.

## Initiation à la surveillance
{: #gettingStarted_monitor}

Les composants Prometheus et Grafana qui contiennent la solution de surveillance sont préinstallés dans l'infrastructure Kubernetes qui prend en charge l'instance CFEE.  L'accès aux outils de surveillance nécessite de réacheminer les ports des serveurs Prometheus, Prometheus AlertManager et Grafana.  Cette opération s'effectue à l'aide de l'interface de ligne de commande Kubernetes. 
Les sections qui suivent vous guident dans les étapes d'installation de l'interface de ligne de commande requise, de réacheminement des ports des serveurs et de lancement des consoles.

**Remarque :** les instructions suivantes sont également disponibles dans l'interface utilisateur {{site.data.keyword.cfee_full}}.  Ouvrez l'interface utilisateur de l'instance CFEE, cliquez sur **Surveillance** dans le panneau de navigation de gauche et accédez à l'onglet **Accès** pour afficher les instructions.

### Prérequis

1. Vérifiez dans vos [règles d'accès](https://console.bluemix.net/iam/#/users) que vous détenez au minimum le rôle d'afficheur sur le cluster Kubernetes qui prend en charge l'environnement.
2. Vous avez installé l'[interface de ligne de commande d'IBM Cloud](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
3. Installez l'[interface de ligne de commande Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  Si vous disposez déjà d'une interface de ligne de commande Kubernetes, nous vous recommandons d'installer la version la plus récente.
4. Installez le plug-in du service de conteneur :
```
    ibmcloud plugin install container-service -r Bluemix
```
 
### Personnalisation de la configuration d'Alertmanager

Alertmanager dispose d'un fichier de [configuration Alertmanager](https://prometheus.io/docs/alerting/configuration/) par défaut qui définit les règles de gestion, regroupement et routage des notifications des alertes Alertmanager. Vous pouvez télécharger le fichier de configuration par défaut et importer une configuration personnalisée dans l'onglet **Configuration** de la page _Surveillance_.
 
### Accès au cluster Kubernetes

1. Connectez-vous à votre compte IBM Cloud :

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}
  
  Si vous disposez d'un ID fédéré, utilisez la commande __ibmcloud login -sso__ pour vous connecter à l'interface de ligne de commande IBM Cloud.

2. Ciblez la région du service de conteneur IBM Cloud dans laquelle vous voulez travailler (par exemple, sud des Etats-Unis) :

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}
    
3. Définissez le contexte du cluster dans votre interface de ligne de commande : 

  a. Obtenez la commande permettant de définir la variable d'environnement et téléchargez les fichiers de configuration Kubernetes :

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}
    
  b. Définissez la variable d'environnement KUBECONFIG. Copiez la sortie de la commande précédente et collez-la dans votre terminal. La sortie de la commande doit être similaire à l'exemple suivant :
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### Réacheminement des ports de serveur
4. Définissez le réacheminement de port dans le cluster Kubernetes pour les pods qui exécutent Prometheus, AlertManager et Grafana. Cette opération vous permet d'héberger les métriques de surveillance par proxy sur votre machine locale (système hôte local) :

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000 &''
  ```
  {: pre}
  
### Lancement des consoles de surveillance sur votre proxy Web local

5. Lancez la console Grafana pour visualiser l'analyse de métriques sélectionnées.  Des tableaux de bord Grafana par défaut sont inclus dans l'instance CFEE. Ces tableaux de bord par défaut sont interactifs et vous permettent de visualiser l'infrastructure utilisée pour héberger votre instance CFEE. (cluster Kubernetes). Une fois la console Grafana lancée, cliquez sur le bouton **Accueil** en haut de la console Grafana pour sélectionner l'un des tableaux de bord prédéployés (voir la liste ci-dessous), qui présentera sous forme graphique les métriques correspondantes :

   Pour CFEE version 2.1.0 ou antérieure, il existe un utilisateur `admin` par défaut dans Grafana, dont le mot de passe par défaut est `admin`. Nous vous recommandons de vous connecter avec le nom d'utilisateur et le mot de passe `admin/admin`, puis de les remplacer par de nouvelles données d'identification. Pour CFEE version 2.2.0 ou ultérieure, les utilisateurs sont automatiquement authentifiés à l'aide de leur IBMid.

     [Lancement de la console Grafana](https://localhost:3000)

   Les tableaux de bord par défaut suivants sont fournis avec l'instance CFEE et sont disponibles à partir du menu déroulant _Accueil_.

    Tableaux de bord Cloud Foundry :
   - _CF: Cells Capacity_ 
        - Affiche l'état général des cellules Cloud Foundry dans lesquelles les applications Cloud Foundry sont déployées.
   - _CF: Diego Cell_ 
        - Affiche le statut des cellules Cloud Foundry et des composants Diego.
   - _CF: Router_ 
        - Affiche le statut du routeur Cloud Foundry qui s'exécute dans votre environnement CFEE.
  
   Tableaux de bord pour l'infrastructure Kubernetes prenant en charge votre environnement CFEE :
   - _Deployment_ 
        - Affiche le statut de vos déploiements Kubernetes.
   - _Kubernetes Cluster Health_ 
        - Affiche l'état de santé du cluster Kubernetes.
   - _Kubernetes Cluster Status_ 
        - Affiche le statut du cluster Kubernetes.
   - _Kubernetes Resource Requests_ 
        - Affiche l'unité centrale et la mémoire utilisées ainsi que d'autres paramètres du cluster Kubernetes.
   - _Pods_ 
        - Affiche des détails concernant chaque pod du cluster Kubernetes.
   - _Replica Set_ 
        - Affiche le statut des ensembles de répliques Kubernetes.       
   - _Worker Nodes_ 
        - Affiche des détails concernant chaque noeud du cluster Kubernetes.
   - _Worker Nodes Overview_ 
        - Affiche l'utilisation de l'unité centrale et de la mémoire de l'infrastructure Kubernetes, ainsi que son trafic réseau.
        
6. Si vous le souhaitez, vous pouvez également lancer la console Prometheus pour visualiser les données brutes collectées par le serveur Prometheus et Prometheus Alertmanager afin de gérer les alertes envoyées par le serveur Prometheus :

     [Lancement du serveur Prometheus](https://localhost:9090)

     [Lancement du serveur Prometheus Alertmanager](https://localhost:9093)

