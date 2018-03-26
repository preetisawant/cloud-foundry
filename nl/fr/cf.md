---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Fonctionnement de Cloud Foundry avec {{site.data.keyword.cloud_notm}}
{: #howwork}

Lorsque vous déployez une application dans Cloud Foundry, vous devez configurer {{site.data.keyword.cloud_notm}} avec les informations nécessaires à la prise en charge de celle-ci.

* Dans le cas d'une application mobile, {{site.data.keyword.cloud_notm}} contient un artefact qui représente le système de back end de l'application mobile, comme les services que l'application mobile utilise pour communiquer avec un serveur.
* Dans le cas d'une application Web, vous devez vous assurer que les informations sur l'environnement d'exécution et l'infrastructure sont communiquées à {{site.data.keyword.cloud_notm}}, de sorte que {{site.data.keyword.cloud_notm}} puisse configurer l'environnement d'exécution approprié pour exécuter l'application.

Chaque environnement d'exécution, y compris mobile et web, est distinct de celui des autres applications. Les environnements d'exécution sont isolés, même si les applications sont sur la même machine physique. La figure suivante présente le flux de base suivi par Cloud Foundry pour gérer le déploiement des applications dans {{site.data.keyword.cloud_notm}} :

![Déploiement d'une application](images/deploy.png)

Figure 1. Déploiement d'une application

Lorsque vous créez une application et la déployez dans Cloud Foundry, l'environnement {{site.data.keyword.cloud_notm}} choisit un serveur virtuel approprié auquel envoyer l'application ou les artefacts représentés par l'application. Pour une application mobile, une projection de back end mobile est créée dans {{site.data.keyword.cloud_notm}}. Tout code de l'application mobile exécuté sur le cloud l'est finalement dans l'environnement {{site.data.keyword.cloud_notm}}. Pour une application Web, le code exécuté sur le cloud correspond à l'application elle-même, que le développeur déploie dans {{site.data.keyword.cloud_notm}}. Le choix du serveur virtuel dépend de plusieurs facteurs, dont :

* La charge actuelle de la machine
* Les environnements d'exécution ou les infrastructures pris en charge par le serveur virtuel

Une fois le serveur virtuel choisi, un gestionnaire d'application sur chaque serveur virtuel installe l'infrastructure et l'environnement d'exécution appropriés pour l'application. Celle-ci peut alors être déployée dans cette infrastructure. Ensuite, les artefacts d'application sont démarrés.

La figure suivante présente la structure d'un serveur virtuel, aussi appelé agent DEA (Droplet Execution Agent), sur lequel plusieurs applications sont déployées :

![Conception d'un serveur virtuel](images/container-diego.png)

Figure 2. Conception d'un serveur virtuel

Sur chaque serveur virtuel, un gestionnaire d'application communique avec le reste de l'infrastructure {{site.data.keyword.cloud_notm}} et gère les applications déployées. Chaque serveur virtuel dispose de conteneurs pour séparer et protéger les applications. Dans chaque conteneur, {{site.data.keyword.cloud_notm}} installe l'infrastructure et l'environnement d'exécution requis pour chaque application.

Si l'application déployée dispose d'une interface Web (par exemple, une application Web Java) ou de services REST (par exemple, des services mobiles exposés publiquement à l'application mobile), les utilisateurs de cette application peuvent communiquer avec elle via des demandes HTTP normales.

![Appel d'application {{site.data.keyword.cloud_notm}}](images/execute.png)

Figure 3. Appel d'une application {{site.data.keyword.cloud_notm}}

Chaque application peut être associée à une ou plusieurs adresses URL, mais elles doivent toutes désigner le noeud final {{site.data.keyword.cloud_notm}}. Lorsqu'une demande arrive, {{site.data.keyword.cloud_notm}} l'examine, détermine l'application à laquelle elle est adressée, puis sélectionne l'instance de l'application qui recevra la demande.


## Architecture de Cloud Foundry dans {{site.data.keyword.cloud_notm}}
{: #architecture}

En général, il est inutile de se préoccuper des couches du système d'exploitation et de l'infrastructure lorsque vous exécutez des applications dans {{site.data.keyword.cloud_notm}}, dans Cloud Foundry. Les couches, telles que les systèmes de fichiers racine et les composants de middleware, sont masquées pour que vous puissiez vous concentrer sur le code de votre application. Cependant, vous pouvez obtenir plus de détails sur ces couches si vous avez besoin d'informations spécifiques sur l'emplacement d'exécution de votre application.

Pour plus d'informations, voir [Affichage des couches de l'infrastructure {{site.data.keyword.cloud_notm}}](cf.html#infralayers).

En tant que développeur, vous pouvez interagir avec l'infrastructure {{site.data.keyword.cloud_notm}} via une interface utilisateur basée sur un navigateur. Vous pouvez également utiliser une interface de ligne de commande Cloud Foundry, appelée cf, pour déployer des applications Web.

Les clients, qui peuvent être des applications mobiles, des applications exécutées en externe, des applications construites dans {{site.data.keyword.cloud_notm}} ou des développeurs qui utilisent des navigateurs, interagissent avec les applications hébergées par {{site.data.keyword.cloud_notm}}. Ils utilisent des API REST OU HTTP pour router les demandes via {{site.data.keyword.cloud_notm}} vers l'une des instances d'application ou des services composites.

La figure suivante présente l'architecture générale de Cloud Foundry sur {{site.data.keyword.cloud_notm}}.

Architecture ![{{site.data.keyword.cloud_notm}}](images/arch.png)

Figure 4. Architecture de Cloud Foundry sur {{site.data.keyword.cloud_notm}}

Vous pouvez déployer vos applications dans différentes régions {{site.data.keyword.cloud_notm}}, pour des raisons de sécurité ou pour réduire le temps d'attente. Vous pouvez procéder au déploiement dans une région ou dans plusieurs régions.


![Développement d'applications dans plusieurs régions](images/multi-region.png)

Figure 5. Déploiement d'applications dans plusieurs régions

Couches de l'infrastructure {{site.data.keyword.Bluemix_notm}}
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} fait abstraction des couches du système d'exploitation et de
l'infrastructure et les masque pour que vous n'ayez pas à les gérer. Toutefois, il se peut que vous souhaitiez en savoir plus sur le système d'exploitation et le
middleware utilisés pour votre application.
{:shortdesc}

### Affichage des couches de l'infrastructure {{site.data.keyword.Bluemix_notm}}
{: #viewinfra}

Vous pouvez exécuter la commande **bluemix app stacks** pour afficher les piles, ou systèmes de fichiers racine, disponibles dans lesquelles vos applications seront déployées. Vous pouvez aussi spécifier la pile lorsque vous utilisez la commande **bluemix app push** avec l'option *-s* et l'argument *stack_name*, où stack_name est le système de fichiers racine, par exemple `lucid64` ou `cflinuxfs2` :

```
bluemix app push appName -s stack_name
```

Vous pouvez utiliser la commande `cf buildpacks` pour afficher les composants de middleware, par exemple le profil WebSphere Liberty et SDK for Node.js, qui sont disponibles en tant que contextes d'exécution dans lesquels votre application peut s'exécuter. De plus, vous pouvez spécifier l'environnement d'exécution pour votre application avec la commande
suivante :

```
bluemix app push appName -b buildpackname
```
