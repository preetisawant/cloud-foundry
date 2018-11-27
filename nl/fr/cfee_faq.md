---



copyright:

  years: 2018

lastupdated: "2018-11-09"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# Foire aux questions (FAQ)
{: #cfeefaq}

## Quelle est la différence entre IBM Cloud Foundry Enterprise Environment (CFEE) et Cloud Foundry Public ?
{: #cfee_diff}

Vous pouvez utiliser {{site.data.keyword.cloud}} Foundry Public pour exécuter des applications natives en cloud qui utilisent Cloud Foundry pour une simple configuration, une mise à l'échelle puissante et la gestion de trafic. Vous devez également pouvoir accéder facilement à tous les services {{site.data.keyword.cloud}}. 

Vous pouvez utiliser {{site.data.keyword.cfee_full}} pour tout comme vous le feriez avec Cloud Foundry Public, mais également pour créer et gérer des environnements isolés pour héberger des applications Cloud Foundry exclusivement pour votre entreprise. 


## En quoi la nouvelle offre est-elle différente des précédentes offres IBM Cloud Foundry ?
{: #cfOfferings_diff}

Concernant l'offre à service partagé publique, la différence la plus notable touche incontestablement aux propriétés d'isolement. Concernant l'offre à service exclusif existante sur l'infrastructure IBM Cloud, les deux principales différences sont l'encombrement d'infrastructure réduit (et par conséquent, le coût), ainsi que le modèle d'intégration de service dans ce type d'environnement à service exclusif. 

## Où puis-je trouver le service CFEE ?
{: #where}

Vous pouvez trouver et instancier le service {{site.data.keyword.cfee_full}} dans le [catalogue](https://console.stage1.bluemix.net/catalog) {{site.data.keyword.Bluemix_notm}}. 

## Puis-je avoir plus d'un environnement CFEE dans un centre de données régional ?
{: #multiple-cfees}

Oui, vous pouvez créer des instances CFEE à la demande, autant que vous le souhaitez, dans [ces régions](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

## Ai-je besoin d'une certaine capacité minimale pour commencer ?
{: #minimum-capacity}

Oui. Créer une instance CFEE nécessite au moins deux cellules Cloud Foundry, chacune avec 4 coeurs de 16 Go de mémoire RAM, un disque principal SSD de 25 Go, un disque secondaire SSD de 100 Go et une vitesse réseau de 1000 Mbps. 

## Quelle est l'infrastructure IaaS sous-jacente dans laquelle CFEE est déployé ?
{: #why-kubs}

Le service CFEE s'exécute sur des conteneurs Kubernetes, ce qui permet de réduire les coûts d'infrastructure et d'effectuer des opérations plus efficaces, puisque Kubernetes est une infrastructure IaaS de très petite taille qui automatise un grand nombre d'activités opérationnelles.  

## Quelles sont les options d'isolement dont je dispose lors de la création d'un CFEE ?
{: #isolation}

Vous avez deux options matérielles selon le type d'infrastructure Kubernetes dans laquelle l'instance CFEE est déployée. Il s'agit de l'option de matériel _partagé virtuel_ ou de l'option de matériel _dédié virtuel_. Dans le cadre de l'option de matériel _partagé virtuel_, les noeuds worker (dans lesquels le conteneur de plateforme Cloud Foundry est déployé) sont répartis entre vous et d'autres clients IBM. Avec l'option de matériel _dédié virtuel_, les noeuds worker sont hébergés sur le matériel qui est dédié exclusivement à votre compte. Notez que dans les deux cas (matériel _partagé virtuel_ et matériel _dédié virtuel_, chaque noeud worker est à service exclusif pour le client. Cela signifie que les cellules Cloud Foundry sur lesquelles les applications s'exécutent ne sont pas partagées avec d'autres clients. 

## Puis-je mettre à l'échelle la capacité d'un CFEE ?
{: #scaling}

Oui, vous pouvez augmenter ou réduire la capacité de votre CFEE en fonction de l'évolution de vos besoins en ajoutant ou en retirant des cellules Cloud Foundry. 

## Puis-je mettre à niveau mon CFEE vers une nouvelle version ? Comment cela fonctionne-t-il ?
{: #upgrading}
Oui. L'interface utilisateur CFEE vous prévient qu'une nouvelle version CFEE est disponible. Vous décidez à quel moment effectuer la mise à niveau vers une nouvelle version. La mise à jour de version CFEE est appelée par des administrateurs CFEE dans l'interface utilisateur. Les mises à jour de version CFEE peuvent conditionner de nouvelles versions de leurs composants ou services de prise en charge (par exemple, Cloud Foundry, Kubernetes, etc.). Vous mettez à jour le plan de contrôle CFEE en premier, puis les cellules Cloud Foundry. Le processus de mise à jour est optimisé pour réduire au maximum les interruptions. 

## Que faut-il pour créer une instance CFEE ?
{: #create}

Vous trouverez le service CFEE répertorié dans le catalogue {{site.data.keyword.Bluemix_notm}}. Vous devez disposer d'un compte {{site.data.keyword.Bluemix_notm}} mis à niveau et des droits d'accès nécessaires pour accéder au service CFEE et à ses services pris en charge (Kubernetes, Cloud Object Storage et Compose for PostgreSQL). Une fois que vous possédez ces droits, il vous suffit d'indiquer le nom de l'environnement et de cliquer sur _Créer_. La création dure environ 90 minutes.

## Puis-je utiliser des services {{site.data.keyword.Bluemix_notm}} dans mon environnement CFEE ?
{: #Services-ibmcloud}

Bien sûr ! Etant intégrés dans {{site.data.keyword.Bluemix_notm}}, les développeurs dans une instance CFEE peuvent créer des instances de service {{site.data.keyword.Bluemix_notm}} (ou utiliser des instances existantes) et les lier à des applications déployées dans des espaces CFEE. 

## Puis-je posséder mes propres services dans mon environnement CFEE ?
{: #Services-ibmcloud}

Oui.  Un administrateur peut enregistrer un courtier de services dans l'environnement CFEE et mettre des plans de service personnalisés à la disposition d'utilisateurs dans cet environnement CFEE.  La place du marché MCFEE locale comprend les services du catalogue {{site.data.keyword.Bluemix_notm}} plus les services client gérés par un courtier de services local de l'environnement CFEE. 

## Comment contrôler l'accès utilisateur à un environnement CFEE ?
{: #Services}

Comme n'importe quel autre service {{site.data.keyword.Bluemix_notm}}, l'accès à un environnement CFEE est contrôlé via _Identity & Access Management_ (IAM). Affecter des règles d'accès à des utilisateurs (que ce soit individuellement ou via des groupes d'accès) avec des rôles spécifiques permet de leur octroyer des niveaux d'accès spécifiques à un environnement CFEE. Au-delà de l'accès au service CFEE, l'accès aux organisations et espaces Cloud Foundry dans l'environnement CFEE est contrôlé via l'appartenance à Cloud Foundry et aux rôles affectés aux utilisateurs dans des organisations et des espaces spécifiques. 

