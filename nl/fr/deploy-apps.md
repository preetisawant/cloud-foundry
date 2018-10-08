---

copyright:
  years: 2018
lastupdated: "2018-09-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Déploiement et affichage d'applications
{: #deploy_apps}

Vous pouvez déployer des applications dans {{site.data.keyword.Bluemix}} avec l'interface de ligne de commande ou les environnements de développement intégré (IDE). Vous pouvez également déployer des applications à l'aide de manifestes d'application. L'utilisation d'un manifeste d'application vous permet de réduire le nombre d'informations de déploiement à spécifier chaque fois que vous déployez une application dans {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Déploiement d'applications avec la commande Cloud Foundry
{: #dep_apps}

[Téléchargement et installation de l'interface de ligne de commande Cloud Foundry](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

Une fois l'interface de ligne de commande installée, procédez comme suit :

1. Accédez au répertoire qui contient votre code. `cd <your_directory>`
2. Accédez à la page de présentation d'{{site.data.keyword.cfee_full}} et localisez le noeud final d'API de l'environnement.
3. Dans l'interface de ligne de commande, définissez le noeud final d'API sur le noeud final de votre environnement :

  ```
  cf api <api_endpoint>
  ```
  {: pre}

4. Connectez-vous à l'environnement

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  Si vous vous servez d'un ID fédéré, utilisez l'option `-sso`.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **Remarque **: vous devez ajouter des apostrophes ou des guillemets autour de `username`, `org_name` et `space_name`, si cette valeur contient un espace. Par exemple, `-o "mon organisation"`.

5.  A partir de `<your_new_directory>`, redéployez votre application dans {{site.data.keyword.Bluemix_notm}} à l'aide de la commande `bluemix app push`. Pour plus d'informations sur la commande `cf app push`, voir [Téléchargement de votre application](/docs/starters/upload_app.html).

  ```
  cf push <nom_app>
  ```
  {: pre}

6.  Accédez à votre application via `https://<app_url>.<AppDomainName>`.

## Affichage des applications déployées dans l'interface utilisateur
{: #view_apps}

Vous pouvez afficher les applications CFEE déployées dans le contexte d'un espace spécifique ou globalement dans toutes les instances CFEE.

### Affichage des applications déployées dans un espace CFEE spécifique
{: #view_specific}

Pour afficher les applications déployées dans un espace spécifique d'une instance de CFEE spécifique :
1. Accédez au [tableau de bord {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/apps/) et ouvrez l'environnement {{site.data.keyword.cfee_full_notm}} dans lequel vous voulez créer des organisations.
2. Dans l'interface utilisateur de l'environnement {{site.data.keyword.cfee_full_notm}}, accédez à l'entrée **Organisations** dans le volet de navigation pour ouvrir la page _Organisations_.
3. Accédez à l'onglet **Espaces** en haut de la page.
4. Dans l'onglet __Espaces__, cliquez sur l'espace dans le tableau pour ouvrir la page de l'espace.
5. Dans la page __Espace__, accédez à l'onglet **Applications**.
6. L'onglet __Applications_)_ affiche toutes les applications déployées dans cet espace.
Eventuellement, vous pouvez démarrer, redémarrer, arrêter ou supprimer une application via le menu situé tout à fait à droite de la ligne correspondant à l'application.

Vous pouvez également développer la ligne d'une application pour afficher les instances de service auxquelles l'application est liée.

### Affichage des applications déployées dans toutes les instances CFEE
{: #view_global}

Pour afficher les applications déployées dans toutes les instances CFEE :
1. Cliquez sur l'icône de menu ![Vérification du compte](img/HamburgerMenu.png "Capture d'écran de l'icône de menu") > **Cloud Foundry** pour ouvrir le tableau de bord Cloud Foundry.
2. Cliquez sur **Enterprise > Applications** dans le volet de navigation de gauche.
Le tableau de la vue affiche les informations suivantes :

| Elément   | Description |
|-----------|---------------|
| Nom | Nom de l'application. |
| Instances | Nombre d'instances de l'application. |
| Environnement | Environnement {{site.data.keyword.cfee_full}} dans lequel l'application est déployée. |
| Organisation | Organisation dans laquelle l'application est déployée. |
| Espace | Organisation de l'instance CFEE où réside l'alias. |
| Mémoire | Quantité de mémoire utilisée par l'application. |
| Statut | Statut de l'application. |
{:caption="Tableau 1. Colonnes du tableau des applications du tableau de bord Cloud Foundry" caption-side="top"}

Eventuellement, vous pouvez démarrer, redémarrer, arrêter ou supprimer une application via le menu situé tout à fait à droite de la ligne correspondant à l'application.
Vous pouvez cliquer sur des applications, des environnements, des organisations ou des espaces pour accéder à la page correspondante dans l'interface utilisateur CFEE.

Dans cette vue, vous avez la possibilité de regrouper des applications par organisation, espace, et/ou nom d'application.  Cette option vous permet de fusionner en une seule entité plusieurs applications ayant des noms différents et/ou devant être déployées dans différents espaces ou organisation CFEE, mais qui correspondent à la même entité d'applications logique.  Par exemple, vous pouvez avoir différentes applications qui représentent des composants d'un projet plus vaste ou qui sont déployées à différents stades de distribution (par exemple, développement, test, production) mais que vous voulez visualiser comme un ensemble d'une même entité logique.

Pour regrouper des applications, accédez au menu déroulant **Groupe** en haut de la page à droite.
Lorsque vous regroupez des applications, chaque groupe obtenu est représenté par une seule entrée dans le tableau. Vous pouvez développer la ligne d'une entrée pour afficher les applications que contient le groupe.

Dans cette vue, vous pouvez effectuer les actions suivantes :
* Trier les éléments du tableau d'après n'importe laquelle des propriétés affichées sous forme de colonnes de tableau.
* Lier des applications à un alias spécifique en accédant au menu déroulant dynamique des alias situé tout à fait à droite de la ligne.
* Développer un alias (ligne) afin de visualiser toutes les applications liées à cet alias.
* Démarrer et arrêter des applications en accédant au menu déroulant dynamique des applications de l'alias situé tout à fait à droite de la ligne.
* Accéder à un environnement, une organisation ou un espace CFEE en cliquant sur le lien à l'environnement, l'organisation oul'space CFEE correspondant.

## Manifeste d'application
{: #appmanifest}

Les manifestes d'application contiennent des options qui sont appliquées à la commande `cf push`. Vous pouvez utiliser un manifeste d'application afin de réduire le nombre d'informations de déploiement que vous devez spécifier chaque fois que vous envoyez par commande push une application sur {{site.data.keyword.Bluemix_notm}}.

Dans les manifestes d'application, vous pouvez spécifier des options, telles que le nombre d'instances d'application à créer, la quantité de mémoire et le quota de disque à allouer ainsi que d'autres variables d'environnement. Vous pouvez aussi utiliser des manifestes d'application pour automatiser le déploiement d'applications. Le nom par défaut d'un fichier manifeste est `manifest.yml`.

### Options prises en charge dans le fichier manifeste

Le tableau suivant décrit les options prises en charge que vous pouvez utiliser dans un fichier manifeste d'application. Si vous décidez d'utiliser un nom de fichier différent de `manifest.yml`, vous devez utiliser l'option **-f** avec la commande `cf push`. Dans l'exemple suivant, le nom du fichier est `appManifest.yml` :

```
cf push -f appManifest.yml
```

| Options | Description | Utilisation ou exemple |
|:----------|:--------------|:---------------|
| **buildpack** | Adresse URL ou nom du pack de construction personnalisé. | `buildpack:` *URL_pack_construction* |
| **disk_quota** | Quota de disque alloué à une application. La valeur par défaut est 1 G. | `disk_quota: 500M` |
| **domain** | Nom de domaine de l'application dans {{site.data.keyword.Bluemix_notm}}. | `domain:` ng.bluemix.net |
| **host** | Nom d'hôte de l'application dans {{site.data.keyword.Bluemix_notm}}. Cette valeur doit être unique dans l'environnement {{site.data.keyword.Bluemix_notm}}. | `host:` *nom_hôte* |
| **name** | Nom de l'application dans {{site.data.keyword.Bluemix_notm}}. Cette valeur doit être unique dans l'environnement {{site.data.keyword.Bluemix_notm}}. | `name:` *nom_app* |
| **path** | Emplacement de votre application. Cette valeur peut être un chemin relatif ou absolu. | `path:` *chemin_application* |
| **command** | Commande de démarrage personnalisée pour votre application ou commande d'exécution de fichiers script. | `command:` *commande_personnalisée* `command:` *bash ./run.sh* |
| **memory** | Quantité de mémoire à allouer à l'application. La valeur par défaut est 1G. | `memory: 512M` |
| **instances** | Nombre d'instances à créer pour votre application. | `instances: 2` |
| **timeout** | Délai de démarrage maximal de l'application, en secondes. La valeur par défaut est 60 secondes. | `timeout: 80` |
| **no-route** | Valeur booléenne permettant d'empêcher d'affecter une route à l'application si l'application s'exécute seulement en arrière-plan. La valeur par défaut est **false**. | `no-route: true` |
| **random-route** | Valeur booléenne permettant d'affecter une route aléatoire à l'application. La valeur par défaut est **false**. | `random-route: true` |
| **services** | Services à lier à l'application. | `services: - mysql_maptest` |
| **env** | Variables d'environnement personnalisées pour l'application. | `env: DEV_ENV: production` |
{: caption="Tableau 2. Options prises en charge dans le fichier manifeste .yml" caption-side="top"}

### Exemple de fichier manifest.yml
{: #sample}

L'exemple ci-dessous illustre un fichier manifeste pour une application Node.js utilisant le pack de construction de communauté intégré Node.js dans {{site.data.keyword.Bluemix_notm}}.

```
--- - name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
