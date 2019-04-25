---

copyright:
  years: 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Mise à l'échelle automatique des applications
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} dispose d'un support de mise à l'échelle automatique intégré pour les applications Cloud Foundry afin d'ajuster automatiquement le nombre d'instances d'application via :  
  * une mise à l'échelle dynamique basée sur les métriques de performance des application ; 
  * une mise à l'échelle planifiée basée sur le temps.

Cette fonctionnalité est offerte en parallèle du projet open source Cloud Foundry [App-Autoscaler][autoscaler_project]. Pour démarrer, voir le [guide d'utilisation][autoscaler_user_guide]. 

## Gestion de la mise à l'échelle automatique via l'interface de ligne de commande

Vous pouvez utiliser le plug-in de l'interface de ligne de commande de mise à l'échelle automatique (interface de ligne de commande aka AutoScaler) pour gérer la règle, les paramètres de requête et l'historique des mises à l'échelle. 

### Installation de l'interface de ligne de commande de mise à l'échelle automatique
Utilisez la commande suivante pour installer l'`interface de ligne de commande de mise à l'échelle automatique` qui est un plug-in de l'interface de ligne de commande Cloud Foundry.  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

La même commande permet de mettre à jour le plug-in d'`interface de ligne de commande de mise à l'échelle automatique` vers la version la plus récente si vous disposez d'une installation antérieure. 

### Utilisation de l'interface de ligne de commande de mise à l'échelle automatique

Si vous êtes déjà connecté à un environnement Cloud Foundry sur {{site.data.keyword.Bluemix}} et que des applications s'exécutent dans votre espace comme indiqué dans le [guide de déploiement d'applications][deploy_app], suivez la procédure ci-dessous afin de créer une règle de mise à l'échelle pour votre application, ainsi que les paramètres de requête et l'historique des mises à l'échelle. 

 *  (Facultatif) Vérifiez que le noeud final de l'API App-Autoscaler est correctement défini par défaut.  

    le noeud final de l'API Cloud Foundry se présente sous la forme `api.<DOMAIN>`, le noeud final de l'API App-Autoscaler doit être `autoscaler.<DOMAIN>`.  
    Utilisez la commande suivante pour vérifier le paramétrage du noeud final de l'API App-Autoscaler.

    ```
    cf asa
    ```
    {:codeblock} 

    Si le noeud final de l'API App-Autoscaler est incorrect, vous devez le redéfinir avec la commande :

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  Créez un fichier de règle JSON sur votre machine locale. 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    La règle ci-dessus est utilisée pour déclencher la mise à l'échelle en fonction de l'utilisation de la mémoire lorsque le seuil défini est dépassé d'au moins `120 secondes`. Pour savoir comment créer votre propre règle de mise à l'échelle automatique, voir le [guide d'utilisation de Cloud Foundry App-Autoscaler][autoscaler_user_guide].

*  Associez la règle à votre application

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (Facultatif) Vous pouvez en outre demander les dernières mesures globales de votre application. App-Autoscaler prend en charge plusieurs [types de mesure][metric_type], mais seules les mesures définies dans votre règle peuvent être extraites, par exemple, `memoryutil` (utilisation de la mémoire) dans l'exemple ci-dessus.  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (Facultatif) Demandez l'historique des mises à l'échelle avec la commande suivante :

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    Pour plus d'options d'utilisation de la ligne de commande, voir le [guide du plug-in de l'interface de ligne de commande Cloud Foundry App Autoscaler][autoscaler_cli]. 


## Gestion de la mise à l'échelle automatique via la console Stratos 

Outre l'interface de ligne de commande, vous pouvez également gérer la mise à l'échelle automatique via la console Stratos. 

Si vous avez installé [stratos][stratos] dans votre environnement {{site.data.keyword.cfee_full}} (CFEE), accédez à l'onglet **"Mise à l'échelle automatique**" du tableau de bord des applications pour afficher une présentation de la règle de mise à l'échelle automatique ainsi que les événements de mise à l'échelle les plus récents.
Cliquez sur l'une des icône de l'une des vignettes pour démarrer l'éditeur de règles et modifier la règle.

Si aucune règle de mise à l'échelle automatique n'est définie, la page de présentation ne contient aucune information. Cliquez sur **Créer une politique** pour démarrer l'éditeur de règles et créer une politique.

Il est recommandé de consulter le [guide d'utilisation de Cloud Foundry App-Autoscaler][autoscaler_user_guide] pour comprendre les concepts de base de définition correcte des règles de mise à l'échelle automatique. 

### Statistiques des métriques

Une fois que vous avez défini une politique basée sur un ou plusieurs types de métrique sélectionnés, vous pouvez afficher les valeurs de métrique les plus récentes ainsi que l'historique des métriques au cours des 30 dernières minutes. 

**Remarque :** les métriques représentent les moyennes des données de toutes les instances d'application, et non les données brutes de chaque instance d'application.
    
### Historique des mises à l'échelle

L'onglet **Historique** de l'éditeur de règles affiche les actions de mise à l'échelle effectuées sur votre application qui ont été déclenchées par la règle de mise à l'échelle automatique. Il affiche également les éventuels messages d'erreur liés à des échecs de mise à l'échelle. Vous pouvez demander l'historique des mises à l'échelle des 30 derniers jours. 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]:https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]:https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
