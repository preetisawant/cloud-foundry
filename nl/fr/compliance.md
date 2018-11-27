---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Conformité et réglementation
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) est une plateforme sous forme de services. Par conséquent, le client est libre d'utiliser l'instance de service pour tout ce qu'elle a la capacité de prendre en charge. CFEE et les services dépendants ont accès au strict minimum d'informations personnelles. 

Toutefois, il convient de préciser que même si le plan de contrôle CFEE (via une interface utilisateur/API/interface de ligne de commande) ne traitera pas de données sensibles (par exemple, des données HIPAA), il incombe au client de faire en sorte d'utiliser son instance CFEE de manière responsable, car c'est lui qui possède et qui gère toutes les dépendances dans son compte {{site.data.keyword.Bluemix_notm}}.  

Nous recommandons les meilleures pratiques suivantes :
*  Ne modifiez pas les services dépendants créés avec une plateforme CFEE (Kubernetes, Cloud Object Storage et Compose for PostgreSQL).
*  Mettez à jour et gérez la plateforme CFEE via cette plateforme proprement dite (interface utilisateur ou interface de ligne de commande), plutôt que via le service Kubernetes. 

Le cluster Kubernetes sert à contenir la majorité de l'infrastructure CFEE, ainsi que toutes les applications qui s'exécutent sur l'infrastructure CFEE, puisque les cellules Cloud Foundry sont déployées par dessus les noeuds Kubernetes. Le compte SoftLayer du client possède et gère ce cluster. 

La base de données Compose for PostgreSQL est utilisée par CFEE pour contenir des métadonnées sur les organisations, les espaces, les utilisateurs et les rôles. Si l'instance CFEE est utilisée conformément aux recommandations, aucune donnée sensible ne sera exposée. Toutefois, si un client décide de nommer ses organisations et ses espaces en utilisant des informations personnelles sur ses clients, la base de données PostgreSQL peut contenir des données HIPAA ou tout autre type de données sensibles. 

L'instance Cloud Object Storage est utilisée par CFEE pour contenir les gouttelettes d'une application afin qu'elles puissent être déployées, arrêtées, démarrées, etc. Cela signifie que l'instance Cloud Object Storage n'exécute pas l'application, mais qu'elle contient uniquement son image. Par conséquent, si l'instance Cloud Object Storage est utilisée conformément aux meilleures pratiques, elle ne contiendra pas d'informations sensibles HIPAA. Il incombe au client de s'assurer qu'aucune de ses applications ne contient d'informations personnelles codées en dur (données de test, etc.). .
