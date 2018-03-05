---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Hébergement d'applications dans {{site.data.keyword.Bluemix_notm}}
{: #hosting_apps}

Avec {{site.data.keyword.Bluemix}}, vous pouvez créer des applications et héberger vos applications existantes. Vous pouvez déplacer votre application dans {{site.data.keyword.Bluemix_notm}} à condition qu'elle soit prête pour le cloud. {{site.data.keyword.Bluemix_notm}} vous offre de nombreuses façons d'exécuter vos applications (Cloud Foundry, IBM Containers et Virtual Machines, par exemple).

## Comment préparer vos applications pour le cloud ?
{: #cloud-readyapps}

Si tous les principes ci-après sont respectés dans votre application, l'application est prête pour le cloud et peut être migrée dans {{site.data.keyword.Bluemix_notm}}. Si un principe n'est pas appliqué dans votre application, vous pouvez généralement [modifier votre application](../apps/cloud-ready.html) pour qu'elle le respecte.

## Migration de vos applications
{: #ht_hostapp}

Vous pouvez migrer vos applications dans {{site.data.keyword.Bluemix_notm}} de façon incrémentielle au lieu de les envoyer intégralement dans l'environnement de cloud. Vous pouvez d'abord migrer une partie de votre application puis vous connecter aux
données ou au système d'enregistrement qui existent en utilisant le service Cloud Integration.

Dans vos applications en cloud, il peut être nécessaire d'accéder aux données ou aux services de back end (un système d'enregistrement, par exemple). Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser le service Secure Gateway afin d'établir un tunnel sécurisé entre une organisation {{site.data.keyword.Bluemix_notm}} et le réseau de back end de l'entreprise. Le service permet aux applications dans {{site.data.keyword.Bluemix_notm}} d'accéder aux données et aux services du réseau de back end. Pour plus de détails, voir [Reaching enterprise backend with {{site.data.keyword.Bluemix_notm}} Secure Gateway via console ![Icône de lien externe](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}.

Pour déployer votre application dans {{site.data.keyword.Bluemix_notm}} en tant qu'application Cloud Foundry, sélectionnez un contexte d'exécution dans le catalogue {{site.data.keyword.Bluemix_notm}}. Le contexte d'exécution contient une application Hello World de démarrage que vous pouvez remplacer par votre propre application. Si vous ne trouvez pas de module de démarrage fournissant le contexte d'exécution que vous recherchez, vous pouvez apporter un pack de construction personnalisé compatible avec Cloud Foundry dans {{site.data.keyword.Bluemix_notm}} en spécifiant l'option -b dans la commande cf push. Pour plus de détails, voir [Utilisation de packs de construction de communauté](byob.html).

Vous pouvez utiliser les outils et les services suivants mis à disposition par {{site.data.keyword.Bluemix_notm}} :

| Outil | Méthode |
|:------|:--------|
| Interface de ligne de commande Cloud Foundry (cf cli) | Gérez votre code sur le client local et utilisez l'interface de ligne de commande Cloud Foundry pour envoyer votre application par commande push dans {{site.data.keyword.Bluemix_notm}} manuellement. Pour plus d'informations, voir [Téléchargement de votre application](../starters/upload_app.html). |
| Eclipse | Gérez votre code dans Eclipse et utilisez IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} pour envoyer votre application par commande push. |
| Intégration Git | Gérez votre code sur GitHub et intégrez Git à {{site.data.keyword.Bluemix_notm}}. Vous pouvez collaborer avec d'autres développeurs. Votre application est déployée automatiquement dans {{site.data.keyword.Bluemix_notm}} quand vous validez des changements dans le code. Vous n'avez pas besoin d'envoyer manuellement l'application par commande push. |
| {{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline | Gérez votre code sur le référentiel DevOps GitHub et déployez votre application dans {{site.data.keyword.Bluemix_notm}} en utilisant DevOps Delivery Pipeline. |
{: caption="Tableau 1. Outils {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Si la plateforme Cloud Foundry ne prend pas en charge les exigences relatives à votre application, vous pouvez utiliser un conteneur ou une machine virtuelle où le contexte d'exécution est défini, configuré et géré avec des options personnalisées supplémentaires.

## Développement et déploiement d'applications à l'aide de chaînes d'outils dans Continuous Delivery
{:ht_cd}

Ajoutez une [chaîne d'outils à votre application](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app), puis utilisez l'[interface utilisateur de la chaîne d'outils Continuous Delivery](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using) pour développer et déployer votre application.

## Téléchargement de votre applications avec cf cli
{: #ht_cfcli}

Vous pouvez gérer votre code sur le client local et utiliser l'interface de ligne de commande Cloud Foundry pour télécharger votre application dans {{site.data.keyword.Bluemix_notm}} manuellement. Si vous changez le code, vous devez à nouveau envoyer votre application par commande push dans {{site.data.keyword.Bluemix_notm}} afin d'exécuter le code mis à jour.

Procédez comme suit pour migrer votre application :

Installez l'interface de ligne de commande Cloud Foundry. Veillez à utiliser la version la plus récente de l'interface de ligne de commande cf.
  1. Téléchargez le programme d'installation pour votre système d'exploitation.
  2. Suivez l'assistant de l'outil pour installer la ligne de commande.
  3. Utilisez la commande suivante pour vérifier la version de l'interface de ligne de commande : `cf -v`

Facultatif : si vous voulez spécifier et sauvegarder les détails du déploiement avant d'envoyer une application par commande push dans {{site.data.keyword.Bluemix_notm}}, vous pouvez ajouter le manifeste d'application en procédant comme suit :

  1. Accédez au répertoire de travail de votre application et créez un fichier dont le nom est manifest.yml par défaut.</li>
  2. Spécifiez les détails du déploiement dans le fichier manifeste. L'exemple ci-dessous est une illustration d'un fichier manifeste pour une application Java™.

  ```
  applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

Pour plus d'informations sur les options prises en charge que vous pouvez utiliser dans ce fichier, voir [Manifeste d'application](depapps.html#appmanifest).

### Envoi de votre application par commande push

Vous pouvez télécharger votre application via la commande `cf push`.
  1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} avec la commande ci-après. Sélectionnez
votre organisation et votre espace lorsque vous y êtes invité.
  ```
  cf login -a https://api.ng.bluemix.net
  ```
  Ajoutez l'indicateur `-sso` si votre organisation utilise la connexion unique.

  2. Depuis le répertoire de votre application, entrez la commande cf push avec le nom de l'application. Le nom de l'application doit être unique dans l'environnement {{site.data.keyword.Bluemix_notm}}.

  ```
  cf push nom_app
  ```

  3. Facultatif : si vous utilisez un pack de construction externe, vous devez utiliser l'option -b avec la commande cf push. Exemple :

  ```
  cf push nom_app -b URL_pack_construction
  ```

  Voir [Utilisation de packs de construction de communauté](byob.html) pour plus de détails.

Facultatif : Si vous modifiez votre application, vous devez télécharger ces changements en entrant à nouveau la commande `cf push`. La ligne de commande cf utilise vos options précédentes et vos réponses aux invites pour mettre à jour les instances en cours d'exécution de votre application avec
les nouvelles parties de code.

#### Remarques :

* Lorsque vous utilisez la commande cf push, l'interface de ligne de commande cf copie tous les fichiers et tous les répertoires du répertoire de travail dans {{site.data.keyword.Bluemix_notm}}. Assurez-vous que votre répertoire d'applications ne contient que les fichiers requis.
* Assurez-vous que votre organisation dispose de suffisamment de mémoire pour toutes les instances de votre application. Afin d'afficher le quota de mémoire de votre organisation, utilisez cf org nom_organisation.
* Pour plus d'informations sur cf push, voir [Commandes cf](../cli/reference/cfcommands/index.html).

## Migration de vos données et utilisation des services
{: #ht_service}

Après avoir téléchargé votre application dans {{site.data.keyword.Bluemix_notm}}, sélectionnez le service auquel votre application est connectée dans le catalogue {{site.data.keyword.Bluemix_notm}}, créez une instance de service, liez l'instance à votre application puis redémarrez cette dernière.

La variable d'environnement VCAP_SERVICES de votre application est un objet JSON qui contient des informations sur la façon d'interagir avec une instance de service dans {{site.data.keyword.Bluemix_notm}}. Les informations incluent le nom de l'instance de service, les données d'identification et l'adresse URL de connexion à l'instance de service.

Pour exécuter votre code dans {{site.data.keyword.Bluemix_notm}}, vous devez ajouter la logique de code pour
l'analyse syntaxique de la variable VCAP_SERVICES afin d'obtenir des informations sur la connexion au service. Modifiez votre application pour obtenir
l'hôte et le port dynamiquement affectés de l'instance de service via les variables d'environnement. L'exemple suivant montre comment obtenir les
données d'identification d'une instance de service Postgre SQL dans une application Ruby :

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

Pour garantir l'exécution de votre application dans un environnement local après sa modification pour {{site.data.keyword.Bluemix_notm}}, vérifiez la présence de la variable d'environnement VCAP_SERVICES, qui est définie pour toutes les applications {{site.data.keyword.Bluemix_notm}} Cloud Foundry.


# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [Virtual Machines](/docs/virtualmachines/vm_index.html)
* [Initiation à Delivery Pipeline](/docs/services/DeliveryPipeline/index.html)
* [Déploiement d'applications avec IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html)
* [The twelve-factor app ![Icône de lien externe](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console ![Icône de lien externe](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
