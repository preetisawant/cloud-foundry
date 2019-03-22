---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# A propos d'{{site.data.keyword.cfee_full_notm}}
{: #about}

Bienvenue dans le service {{site.data.keyword.cfee_full}}.

{{site.data.keyword.cfee_full}} (CFEE) vous permet d'instancier à la demande plusieurs plateformes Cloud Foundry d'entreprise isolées. Des instances du service {{site.data.keyword.Bluemix_notm}} Foundry Enterprise s'exécutent dans votre propre compte dans l'environnement {{site.data.keyword.Bluemix_notm}}. L'environnement est déployé sur du matériel isolé (clusters Kubernetes). Vous avez le contrôle complet de l'environnement, y compris le contrôle d'accès, la capacité, les mises à jour de version, l'utilisation et la surveillance des ressources. De plus, l'intégration CFEE à {{site.data.keyword.Bluemix_notm}} permet aux développeurs de tirer parti des services disponibles dans leur compte {{site.data.keyword.Bluemix_notm}}.  Les utilisateurs peuvent ajouter ces services à une instance CFEE et les lier aux applications déployées dans des espaces CFEE.

Découvrez comment [**commencer**](https://console.bluemix.net/docs/cloud-foundry/getting-started.html#getting-started) à créer et à utiliser une instance CFEE.

{:shortdesc}

## Eléments clés de CFEE
{: #key-elements}

Le tableau suivant récapitule les éléments clés du service {{site.data.keyword.cfee_full}} :

| Elément   | Description |
|-----------|---------------|
| Compte IBM Cloud | Des instances CFEE sont créées sous un compte IBM Cloud spécifique, et sont disponibles pour les utilisateurs de ce compte en fonction des rôles et droits d'accès définis pour ces utilisateurs. |
|| Le compte sous lequel les instances CFEE sont créées doivent être des comptes Paiement à la carte ou Abonnement (pas des comptes d'essai).  |
| CFEE | Service IBM Cloud Foundry Enterprise Environment d'hébergement des applications. |
|| Disponible dans le catalogue IBM Cloud. |
| Instance CFEE | Instance du service IBM Cloud Foundry Enterprise Environment créée sous un compte IBM Cloud par un utilisateur ayant le rôle d'administrateur ou d'éditeur sur ce compte. |
|| Un compte IBM Cloud peut contenir plusieurs instances CFEE. |
|| Peut avoir une ou plusieurs organisations. |
| Organisation | Inclut un ou plusieurs espaces. |
|| Inclut un ou plusieurs responsables d'organisation. |
|| Inclut un ou plusieurs membres d'équipe. Chaque membre d'équipe peut se voir accorder un ou plusieurs rôles. |
|| Les frais d'utilisation, générés par une application déployée dans un espace, sont signalés au niveau de l'organisation. |
| Espace | Inclut une ou plusieurs ressources. |
|| Inclut une ou plusieurs applications. |
|| Inclut un ou plusieurs responsables d'espace. |
|| Inclut un ou plusieurs membres d'équipe. Chaque utilisateur doit déjà être un membre d'équipe dans l'organisation propriétaire. Chaque membre d'équipe peut se voir accorder un ou plusieurs rôles. |
| Membre d'équipe | Peut être ajouté à une ou plusieurs organisations et à un ou plusieurs espaces sur différents comptes. |
|| Peut se voir accorder plusieurs rôles au sein d'une même organisation et/ou d'un même espace. |
| Alias de service | Alias d'une instance de service dans IBM Cloud. |
|| Permet aux développeurs de lier des instances de service existantes disponibles dans leur compte IBM Cloud à leurs applications déployées dans un espace au sein d'un environnement CFEE.|
{:caption="Tableau 1. Description des éléments clés" caption-side="top"}

## Mise à disposition de cibles pour CFEE et les services de prise en charge
{: #provisioning-targets}

Voici les zones géographiques, les emplacements et les centres de données où le service CFEE et les services dépendants (service Kubernetes, services Compose for PostgreSQL et Cloud Object Storage) sont disponibles pour la mise à disposition :

|  **Géographie** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **Instance CFEE & Cluster Kubernetes** | **Stockage d'objets Cloud** | **Compose for PostgreSQL (région CF)** |
|----------------------------------------|-------------------|-------------------|-------------------|
|Amérique du Nord | Montréal (mon01) | us-geo | us-east |
|Amérique du Nord | Toronto (tor01) | us-geo| us-east |
|Amérique du Nord | Washington DC (wdc04) | us-geo | us-east |
|Amérique du Nord | Washington DC (wdc06) | us-geo | us-east | 
|Amérique du Nord | Washington DC (wdc07) | us-geo | us-east |
|Amérique du Nord | Dallas (dal10) | us-geo | us-south |
|Amérique du Nord | Dallas (dal12) | us-geo | us-south |
|Amérique du Nord | Dallas (dal13) | us-geo |us-south |
|Amérique du Nord | San José (sjc03) | us-geo | us-south |
|Amérique du Nord | San José (sjc04) | us-geo | us-south |
|Amérique du Sud &nbsp; &nbsp;| Sao Paolo (sao01) |  us-geo | us-south |
|Europe | Londres (lon02) | eu-geo | eu-gb |
|Europe | Londres (lon04) | eu-geo | eu-gb |
|Europe | Londres (lon06) | eu-geo | eu-gb | 
|Europe | Amsterdam (ams03) | eu-geo | eu-de |
|Europe | Oslo (osl01) |eu-geo | eu-de | 
|Europe | Paris (par01) | eu-geo | eu-de |
|Europe | Francfort (fra02) | eu-geo | eu-de |
|Europe | Francfort (fra04) | eu-geo | eu-de | 
|Europe | Francfort (fra05) |  eu-geo | eu-de |
|Europe | Milan (mil01) |  eu-geo | eu-de |
|Asie-Pacifique | Melbourne (mel01) | ap-geo | au-syd |
|Asie-Pacifique | Sydney (syd01) | ap-geo | au-syd |
|Asie-Pacifique | Sydney (syd04) | ap-geo | au-syd | 
|Asie-Pacifique | Hong Kong (hkg02) | ap-geo | au-syd |
|Asie-Pacifique | Hong Kong (seo01) | ap-geo | au-syd |
|Asie-Pacifique | Singapour (sng01) | ap-geo | au-syd |
|Asie-Pacifique | Tokyo (tok02) | ap-geo | au-syd |
|Asie-Pacifique | Tokyo (tok04) | ap-geo | au-syd |
|Asie-Pacifique | Tokyo (tok05) | ap-geo | au-syd |
|Asie-Pacifique | Chennai (che01) | ap-geo | au-syd |
{: caption="Tableau 2. Mise à disposition de cibles pour CFEE et les services de prise en charge" caption-side="top"}

Par **exemple**, le service CFEE peut être mis à disposition dans trois centres de données en Europe : Amsterdam (1 centre de données), Francfort (3 centres de données), Londres (3 centres de données), Oslo (1 centre de données) et Paris (1 centre de données). Si le service CFEE est mis à disposition à Francfort, l'instance de service Cloud Object Store sera déployée dans la région _eu-geo_, et l'instance de service PostgreSQL service sera déployée dans la région Cloud Foundry _eu-de_ publique.

Vous trouverez des vidéos contenant des informations détaillées et des démonstrations expliquant comment gérer des services dans CFEE dans la [liste de lecture des vidéos CFEE](https://ibm.biz/CFEE_Playlist){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
{:tip}
