---

copyright:
  years: 2018
lastupdated: "2018-08-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Utilisation des ressources

Les administrateurs et les développeurs peuvent désormais visualiser comment les applications et les cellules utilisent la capacité de ressources (mémoire et unité centrale) d'un environnement CFEE. Pour surveiller l'utilisation des ressources dans un environnement CFEE :

1. Accédez au [tableau de bord des environnements Cloud Foundry d'{{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments) et ouvrez l'environnement {{site.data.keyword.cfee_full_notm}} dans lequel vous voulez gérer l'utilisation des ressources.
2. Dans l'interface utilisateur de l'environnement {{site.data.keyword.cfee_full_notm}}, accédez à l'entrée **Utilisation des ressources** dans le volet de navigation de gauche pour ouvrir la page _Utilisation des ressources_. Depuis la page _Utilisation des ressources_ vous pouvez accéder aux _Applications_ ou aux sous-entrées _Cellules_ pour ouvrir les pages correspondantes. Les informations affichées dans les pages _Applications_ et _Cellules_ constituent deux aspects différents de l'utilisation des ressources :
   * La page **Applications** analyse l'utilisation des ressources par applications cumulées entre les instances.
   * La page **Cellules** affiche l'utilisation des ressources des instances d'application qui s'exécutent sur des cellules spécifiques. Le schéma d'utilisation des ressources entre les cellules peut fournir un aperçu de la distribution de capacité et de charge. Il peut, par exemple, vous aider à identifier des problèmes au niveau de l'équilibrage de charge des applications (telles de grandes différences d'utilisation des ressources par une application entre les cellules) ou à déceler que l'utilisation des ressources est sur le point d'atteindre la capacité globale (tels de forts pourcentages d'utilisation des ressources dans toutes les cellules).

**Remarque :** les données d'utilisation des ressources correspondent à l'utilisation des ressources au cours du dernier cycle de collecte de 5 minutes. Ces données peuvent être actualisées en cliquant sur **Actualiser les données** en haut de la page.

## Applications
{: #usage_apps}

La page Applications se compose de deux sections :
1. Des graphiques à barres horizontales pour la mémoire et l'unité centrale, qui indiquent :
   * La mémoire *totale disponible* et l'unité centrale disponible dans l'instance CFEE.
   * La mémoire et l'unité centrale qu'utilisent *toutes les applications* dans l'instance CFEE.
   * La mémoire et l'unité centrale qu'utilisent des *applications sélectionnées* dans le tableau du dessous.

   Pour afficher le pourcentage de mémoire et d'unité centrale qu'utilisent toutes les applications ou celles sélectionnées dans le tableau, survolez la portion correspondante du graphique. Lorsque vous survolez la portion *toutes les applications* du graphique, le pourcentage de mémoire et d'unité centrale utilisé par rapport au total disponible s'affiche. Si vous survolez la portion *applications sélectionnées* du graphique, le pourcentage de mémoire et d'unité centrale utilisé par rapport au total de mémoire ou d'unité centrale disponible s'affiche.

2. Un tableau qui répertorie toutes les applications. Chaque ligne du tableau affiche les informations d'utilisation des ressources pour l'application listée. Lorsque vous développez une ligne, les informations d'utilisation des ressources des diverses instances de cette application s'affichent.

  La première colonne du tableau est une case à cocher qui détermine si l'application correspondante doit faire partie de l'ensemble des *applications sélectionnées* à inclure dans le graphique en haut de la page. Cochez la case d'une application pour l'inclure dans l'ensemble sélectionné ou décochez la case pour l'en exclure. Lorsqu'une application est sélectionnée ou désélectionnée pour inclusion dans l'ensemble, ou exclusion, le graphique est actualisé. La légende des _applications sélectionnées_ sur la droite du graphique à barres indique (entre parenthèses) le nombre d'applications actuellement sélectionnées pour inclusion dans le graphique.

  Les informations suivantes sont affichées sous forme de colonnes dans le tableau des applications :
   * **Nom de l'application** : nom de l'application ou de l'instance d'application. Si l'utilisateur n'a pas de droit d'accès à l'application, cette colonne affiche à la place l'identificateur global unique de l'application.
   * **Instances** : pour une application, correspond au nombre d'instances actives. Pour une instance d'application (indiquée sous le nom de l'application lorsque vous développez la ligne de l'application), correspond au nom de la cellule où l'instance d'application s'exécute.
   * **Total Memory-Physical** : nombre de Mo de mémoire physique utilisés par toutes les instances d'une application. La quantité de mémoire physique utilisée par une application est égale à la somme de mémoire physique utilisée par toutes les instances de l'application.
   * **Total Memory-Reserved** : nombre de Mo de mémoire réservés par toutes les instances d'une application. La quantité de mémoire réservée par une application est égale à la somme de mémoire réservée par toutes les instances de l'application.
   * **UC moyenne (% de cellule)** : pour les instances d'application, correspond à l'UC moyenne utilisée par l'instance **au sein de la cellule dans laquelle elle s'exécute**. Pour une application, correspond à l'utilisation moyenne de l'unité centrale de toutes les moyennes de ses instances.
   * **Max CPU (% of cell)** : pour les instances d'application, correspond au maximum d'unité centrale utilisé par l'instance **au sein de la cellule dans laquelle elle s'exécute**.  Pour une application, correspond à l'utilisation maximale la plus élevée de l'unité centrale de ses instances.
   * **Unité centrale (% de système)** : pourcentage du total d'unité centrale disponible dans l'environnement CFEE qu'utilise une application et ses instances. La quantité d'unité centrale utilisée par une application est égale à la somme des pourcentages d'unité centrale utilisés par toutes les instances de l'application.
   * **Moyenne des demandes** : nombre moyen de demandes entrantes vers une application au cours du dernier cycle de collecte de données.
   * **Organisation** : organisation dans laquelle l'application est déployée. Si l'utilisateur n'est pas membre de l'organisation, cette colonne affiche à la place l'identificateur global unique de l'organisation.

Développez une ligne d'application du tableau pour afficher la liste des instances de l'application et leurs mesures correspondantes d'utilisation des ressources.

### Filtrage des applications
Vous pouvez filtrer le contenu du tableau à l'aide des menus déroulants de filtrage des **Applications** et des **Organisations** situés au-dessus le tableau.

En outre, vous pouvez utiliser la zone d'entrée de filtre au-dessus du tableau pour afficher uniquement les applications correspondant à la chaîne que vous entrez dans la zone de filtre. Le filtrage est reflété à la fois dans le tableau et dans le graphique.

**Remarque :** les filtres fonctionnent indépendamment des lignes du tableau sélectionnées (à l'aide des cases à cocher de la première colonne du tableau) pour inclusion dans l'ensemble des _applications sélectionnées_ incluses dans le graphique du dessus. Par exemple,  si l'environnement CFEE contient un total de dix applications et que cinq d'entre elles sont sélectionnées pour inclusion dans le graphique, lorsque vous appliquez un filtre qui ne correspond qu'à une seule instance d'application, seule cette instance d'application s'affiche dans le tableau. De plus, l'ensemble des _applications sélectionnées_ n'inclura désormais que l'application correspondante et le graphique sera actualisé en conséquence. Lorsque vous supprimez le filtre, les dix applications sont de nouveau affichées dans le tableau et l'ensemble des _applications sélectionnées_ est réinitialisé de manière à inclure toutes les applications.


## Cellules
{: #usage_cells}

La page Cellules se compose de deux sections :
1. Des graphiques à barres verticales qui indiquent :
   * La mémoire *totale disponible* et l'unité centrale disponible dans l'instance CFEE.
   * La mémoire et l'unité centrale qu'utilisent *toutes les instances d'application* dans l'instance CFEE.
   * La mémoire et l'unité centrale qu'utilisent les *instances d'application sélectionnées* dans l'instance CFEE.
   * La mémoire et l'unité centrale qu'utilise le *système* dans le tableau du dessous. L'utilisation du système correspond à la ressource utilisée par les composantes du service CFEE plus le cache d'applications.

   Pour afficher le pourcentage de mémoire ou d'unité centrale qu'utilisent toutes les instances d'application ou celles sélectionnées dans le tableau, survolez la portion correspondante du graphique. Lorsque vous survolez le graphique à barres, la quantité absolue de mémoire ou d'unité centrale disponible, la quantité de mémoire ou d'unité centrale utilisée par toutes les applications et la quantité de mémoire ou d'unité centrale utilisée par le système+cache s'affichent. Le pourcentage de mémoire ou d'unité centrale utilisé par toutes les applications et par le système+cache par rapport au total disponible s'affiche également.

2. Un tableau qui répertorie toutes les cellules ainsi que les instances d'application en cours d'exécution dans ces cellules. Chaque ligne du tableau affiche les informations d'utilisation des ressources pour la cellule et l'instance d'application.

  La première colonne du tableau est une case à cocher qui détermine si l'instance d'application correspondante doit faire partie de l'ensemble des *instances d'application sélectionnées* à inclure dans le graphique en haut de la page. Cochez la case d'une instance d'application pour l'inclure dans l'ensemble sélectionné ou décochez la case pour l'en exclure. Lorsqu'une instance d'application est sélectionnée ou désélectionnée pour inclusion dans l'ensemble, ou exclusion, le graphique est actualisé. 

  Les informations suivantes sont affichées sous forme de colonnes dans le tableau :
   * **Nom de cellule** : nom de la cellule.
   * **Nom de l'application** : nom de l'application qui s'exécute dans la cellule. Si l'utilisateur n'a pas de droit d'accès à l'application, cette colonne affiche à la place l'identificateur global unique de l'application.
   * **Instances** : nombre d'instances d'application dans la cellule.
   * **Memory-Physical** : nombre de Mo de mémoire physique utilisés par l'instance d'application qui s'exécute dans la cellule.
   * **Memory-Reserved** : nombre de Mo de mémoire réservés par l'instance d'application qui s'exécute dans la cellule.
   * **Unité centrale (% )** : pourcentage du total d'unité centrale disponible dans l'environnement CFEE qu'utilise l'instance d'application qui s'exécute dans la cellule.

### Filtrage des cellules et des instances d'application
Vous pouvez filtrer le contenu du tableau à l'aide des menus déroulants de filtrage des **Cellules** situés au-dessus du tableau et en sélectionnant les cellules à afficher dans le tableau.

En outre, vous pouvez utiliser la zone d'entrée de filtre au-dessus du tableau pour afficher uniquement les instances d'application correspondant à la chaîne que vous entrez dans la zone de filtre. Le filtrage est reflété à la fois dans le tableau et dans le graphique.

**Remarque :** les filtres fonctionnent indépendamment des lignes du tableau sélectionnées (à l'aide des cases à cocher de la première colonne du tableau) pour inclusion dans l'ensemble des _instances d'application sélectionnées_ incluses dans le graphique du dessus. Par exemple,  si l'environnement CFEE contient un total de dix instances d'application et que cinq d'entre elles sont sélectionnées pour inclusion dans le graphique, lorsque vous appliquez un filtre qui ne correspond qu'à une seule instance d'application, seule cette instance d'application s'affiche dans le tableau. De plus, l'ensemble des _instances d'application sélectionnées_ n'inclura désormais que cette instance d'application et le graphique sera actualisé en conséquence. Lorsque vous supprimez le filtre, les dix instances d'application sont de nouveau affichées dans le tableau et l'ensemble des _instances d'application sélectionnées_ est réinitialisé de manière à inclure toutes les instances d'applications.
