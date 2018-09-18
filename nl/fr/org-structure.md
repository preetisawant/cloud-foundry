---

copyright:

  years: 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Détermination de votre architecture d'organisation
{: #orgstructure}

Pour concevoir un environnement qui utilise {{site.data.keyword.Bluemix_notm}} public, {{site.data.keyword.Bluemix_dedicated_notm}}, {{site.data.keyword.Bluemix_local_notm}} ou n'importe quelle combinaison de ces environnements, vous pouvez utiliser les architectures d'organisation suivantes :

* Organisation unique : choisissez ce type d'architecture si vous voulez qu'un même groupe d'utilisateurs accède aux ressources disponibles dans l'organisation.
* Plusieurs organisations : choisissez ce type d'architecture si vous avez besoin d'isoler différents environnements.

## Organisation unique/Plusieurs organisations
{: #singleormulti}

Dans un environnement à organisation unique, les ressources d'infrastructure sont partagées par différents secteurs de la société. En revanche, dans un environnement avec plusieurs organisations, les ressources d'infrastructure ne sont pas partagées.

Chacune de ces architectures d'organisation prend en charge les principes suivants :

* Application de limites pour les applications et/ou les projets.
* Autorisation de gestion des ressources accordée en fonction des rôles utilisateur.

Vous pouvez ensuite définir plusieurs espaces correspondant à différents secteurs d'activité, à des phases de distribution, à des projets spécifiques, à des applications, à des droits utilisateur ou à une combinaison de ces composants.

Pour implémenter une architecture à plusieurs organisations, vous pouvez définir des organisations qui correspondent à différents secteurs d'activité, à des phases de distribution, à des projets spécifiques, à des droits utilisateur ou à une combinaison de ces composants. Vous pouvez ensuite définir plusieurs espaces basés sur les applications ou projets fournis par le même service de la société.

{: tip}

## Remarques relatives à l'organisation
{: #orgconsiderations}

Lorsque vous implémentez une architecture à organisation unique, l'organisation comprend l'ensemble des ressources, services et applications de cloud que vous utilisez pour développer, gérer et déployer des applications de cloud. Dans l'environnement {{site.data.keyword.Bluemix_notm}} public, l'organisation fournit la séparation des comptes et est disponible dans toutes les régions.

 ![Figure illustrant l'architecture à organisation unique](img/singleorg_example.svg "Figure illustrant l'architecture à organisation unique dans {{site.data.keyword.Bluemix_notm}}")

 Figure 1. Exemple d'architecture à organisation unique.
{: #bpfigure1}

Lorsque vous implémentez une architecture avec plusieurs organisations, les organisations fournissent le premier niveau de l'application des limites et l'abstraction que vous pouvez utiliser pour contrôler et définir ce qui peut être effectué et par qui. Concevez chaque organisation autour des différents secteurs d'activité, des phases de distribution, des rôles des utilisateurs, de projets spécifiques ou d'une combinaison de ces composants.  

Le nombre d'organisations dont vous avez besoin dépend de plusieurs facteurs :

* Le niveau de granularité requis au sein de votre organisation pour gérer les quotas et contrôler les coûts.
* Le niveau de sécurité que vous devez appliquer dans vos différents environnements. Par exemple, si vous utilisez des conteneurs, vous souhaiterez peut-être séparer les images de conteneur qui sont utilisées pour le développement des images de conteneur qui sont utilisées pour la production.
* L'emplacement des organisations imposé par les exigences de l'entreprise, du pays et de l'industrie. Par exemple, vous voudrez peut-être exécuter toutes vos applications dans un environnement situé dans une région spécifique de votre unité géographique.

Lorsque vous définissez les différentes organisations de votre structure en cloud, tenez compte des conseils suivants :

* Définissez et appliquez une convention de dénomination. Par exemple, définissez une convention de dénomination dans laquelle le nom de l'organisation inclut des informations sur le secteur d'activité, le type de cloud et la phase du processus (développement, test ou production). Pour les organisations situées dans {{site.data.keyword.Bluemix_notm}} public, vous souhaiterez peut-être ajouter également des informations sur la région.
* Définissez les restrictions qui s'appliquent à l'organisation. Par exemple, définissez le rôle des membres de l'équipe qui va travailler dans l'organisation.
* Identifiez le responsable de l'organisation.
* Identifiez le secteur d'activité attribué à cette organisation.

Les scénarios suivants illustrent les différentes approches que vous pouvez adopter pour définir le nombre d'organisations Cloud Foundry dans un environnement :

### Scénario 1 : Séparation des groupes d'utilisateurs en fonction de la distribution d'applications métier

 Description : Les règles d'entreprise requièrent que les applications de chaque secteur d'activité soient développées, gérées et déployées par des utilisateurs issus de chaque secteur d'activité. Des mesures de sécurité doivent être appliquées de sorte que les utilisateurs puissent accéder uniquement aux applications qui concernent leur secteur d'activité. Ainsi, les utilisateurs travaillent dans différentes domaines d'activité, les applications sur lesquelles ils travaillent accèdent à différentes ressources {{site.data.keyword.Bluemix_notm}} et il n'existe aucun chevauchement d'activité.

  Solution : vous pouvez créer une organisation pour chaque processus de distribution d'application métier. Par exemple, une organisation dédiée au secteur de la banque aux particuliers et une autre dédiée au secteur de la banque d'investissement.

  ![Figure qui illustre la séparation des utilisateurs par distribution d'application métier](img/bank_example.svg "Figure qui illustre la séparation des utilisateurs par distribution d'application métier")

  Figure 2. Exemple d'architecture avec plusieurs organisations alignées sur une distribution par secteur d'activité.
{: #bpfigure2}

### Scénario 2 : Séparation basée sur le type des utilisateurs (utilisateurs internes, utilisateurs externes)

  Description : votre société travaille avec différents partenaires et vous avez besoin de définir des limites claires entre les utilisateurs internes et les utilisateurs externes.

  Solution : vous pouvez créer une organisation pour fournir des applications utilisées en interne. En outre, vous pouvez créer une organisation pour chaque partenaire externe.

### Scénario 3 : Isolement par projet

  Description : votre société conduit des hackathons pour identifier de nouveaux services.  

  Solution : vous pouvez définir une organisation par hackathon et utiliser l'organisation comme bac à sable. Après l'hackathon, vous pouvez promouvoir l'organisation de bac à sable dans une autre organisation de votre compte.

### Scénario 4 : Isolement des utilisateurs par phase de distribution

  Description : une société souhaite que des utilisateurs de développement, de test et de production collaborent à une distribution, mais les droits d'accès de ces utilisateurs sont déterminés par leur rôle utilisateur et leur expérience professionnelle.

  Solution : vous pouvez créer une organisation unique et définir un espace pour chaque phase de distribution. Ensuite, en fonction du rôle utilisateur et de l'expérience professionnelle, accordez les droits d'accès en lecture et en écriture requis pour réaliser le travail et collaborer au sein de l'organisation.

  ![Figure qui illustre l'isolement d'utilisateurs par phase de distribution](img/user_groups_example.svg "Figure qui illustre l'isolement d'utilisateurs par phase de distribution")

   Figure 3. Exemple d'une architecture à organisation unique alignée par phase de distribution.
{: #bpfigure3}

## Dénomination, restrictions et gestion d'une organisation
{: #orgadmin}   

Tenez compte des conseils suivants pour une organisation :

* Définissez et appliquez une convention de dénomination. Par exemple, définissez une convention de dénomination dans laquelle le nom de l'organisation inclut des informations sur le secteur d'activité, le type de cloud et le rôle informatique (développement, test ou production). Pour les organisations situées dans {{site.data.keyword.Bluemix_notm}} public, vous souhaiterez peut-être ajouter également des informations sur la région. Vous pouvez modifier le nom d'une organisation après l'avoir créée. Si le nom d'une organisation est modifié, prévenez tous les membres d'équipe de l'organisation de cette modification.
* Définissez les restrictions qui s'appliquent à l'organisation. Par exemple, définissez le rôle de chacun des membres de l'équipe et les droits requis pour travailler dans l'organisation.
* Identifiez le responsable de l'organisation. Vous souhaiterez peut-être déléguer l'administration de l'organisation à plusieurs personnes.
* Identifiez le secteur d'activité attribué à cette organisation. L'utilisation d'application qui est générée dans chacun des espaces au sein de l'organisation est accumulée et signalée au niveau de l'organisation.
