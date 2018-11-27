---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Gestion des domaines
{: #domains}

Il existe deux types de domaines Cloud Foundry :
* Les domaines partagés, disponibles pour n'importe quelle application dans n'importe quel espace au sein d'{{site.data.keyword.cfee_full_notm}}. Pour accéder aux domaines partagés, accédez à la page **Domaines** dans le panneau de navigation de gauche de l'interface utilisateur (sous *Opérations*).
* Les domaines privés, disponibles uniquement pour les applications et espaces au sein d'une organisation spécifique. Pour accéder aux domaines d'une organisation, accédez à la page **Organisations** dans le panneau de navigation de gauche de l'interface utilisateur, ouvrez l'organisation, et accédez à l'onglet **Domaines**. 

## Création et suppression de domaines
{: #create-domains}

Pour créer un domaine partagé, accédez à **Domaines** dans le panneau de navigation de gauche de l'{{site.data.keyword.cfee_full_notm}}.  

Pour créer un domaine privé, accédez à la page **Organisations** dans le panneau de navigation de gauche de l'interface utilisateur, ouvrez l'organisation, et accédez à l'onglet **Domaines**. 

Une fois sur la page _Domaines_ (pour les domaines partagés) ou dans l'onglet _Domaines_ d'une organisation spécifique (pour des domaines privés), cliquez sur **Créer un domaine** pour créer un domaine, et entrez un nom unique. 

**Remarque :** les noms de domaine doivent être uniques pour l'ensemble de la portée de l'{{site.data.keyword.cfee_full_notm}}. Autrement dit, un domaine privé ne peut pas avoir le même nom qu'un domaine partagé ou privé au sein d'un environnement {{site.data.keyword.cfee_full_notm}} donné. 

Vous pouvez également créer un domaine partagé à partir de l'interface de ligne de commande Cloud Foundry en exécutant la commande suivante :
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
Vous pouvez créer un domaine privé à partir de l'interface de ligne de commande Cloud Foundry en exécutant la commande suivante :
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**Remarque :** les domaines créés à partir de l'interface de ligne de commande Cloud Foundry apparaîtront immédiatement dans l'interface utilisateur, mais il vous faudra peut-être attendre jusqu'à 1 heure pour que leur création soit effective. 

Pour supprimer un domaine, accédez au menu situé tout à fait à droite de la ligne correspondant au domaine que vous souhaitez supprimer, puis sélectionnez **Supprimer le domaine**. 
  
Vous pouvez également supprimer un domaine partagé à partir de l'interface de ligne de commande Cloud Foundry en exécutant la commande suivante :
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## Téléchargement de certificats SSL
 {: #upload-certificates}
 
Vous pouvez télécharger un certificat SSL pour un domaine (partagé ou privé). Cliquez sur **Télécharger** dans la ligne du tableau correspondant au domaine auquel le certificat est ajouté, sélectionnez le fichier contenant le certificat et le fichier contenant la clé privée. 
  
