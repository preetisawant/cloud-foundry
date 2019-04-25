---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Fonctionnement dans un réseau isolé
{: #isolated-network}


A compter de la version 2.2.0, les instances {{site.data.keyword.cfee_full}} (CFEE) peuvent fonctionner au sein d'un réseau isolé qui protège et sécurise l'environnement face aux menaces externes. Vous créez un réseau isolé par le biais de réseaux locaux virtuels (VLAN) privés et d'un ensemble de mécanismes de contrôle permettant d'acheminer, de filtrer et de protéger le trafic dans et hors des ressources au sein du périmètre du réseau. Les réseaux isolés sont configurés à l'aide de technologies telles que des dispositifs VRA ([Virtual Router Appliance](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)). 

**Remarque :** les instances CFEE qui fonctionnent dans un réseau isolé nécessitent la mise à jour du cluster Kubernetes CFEE vers la version 1.13. La mise à jour du cluster Kubernetes à la version 1.13 est indépendante de la mise à jour de CFEE.

Une instance CFEE est mise à disposition dans un cluster à partir d'IBM Kubernetes Service. Les cellules Cloud Foundry de CFEE (où sont hébergées les applications) sont mises à disposition dans les noeuds worker du cluster. Cela signifie que l'accès aux cellules et applications CFEE implique d'accéder aux noeuds worker du cluster. 

Les noeuds worker contiennent des équilibreurs de charge d'application qui répartissent la charge de travail des applications entre les noeuds worker. CFEE version 2.2.0 active les équilibreurs de charge d'application Kubernetes dans les réseaux publics comme privés.  De ce fait, CFEE version 2.2.0 est accessible depuis les réseaux publics comme privés.

## Gestion CFEE dans un réseau isolé
{: #control-plan-access}

En version 2.2.0, le plan de gestion CFEE (sous-système utilisé pour la mise à disposition, les mises à jour et autres activités liées au cycle de vie) ne s'appuie pas directement sur les équilibreurs de charge d'application ou les noeuds worker pour gérer une instance CFEE. Le plan de gestion CFEE utilise plutôt la _connexion VPN entre les noeuds worker et maître Kubernetes_ pour accéder à l'instance CFEE et à ses ressources. Ainsi, le plan de gestion peut contrôler l'instance CFEE.

Une fois votre instance CFEE créée, le plan de gestion crée dans votre compte un [ID de service IAM](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) qu'il donne au noeud maître IKS. Le plan de gestion CFEE utilise cet ID de service pour accéder aux noeuds worker hôtes CFEE via le noeud maître et son accès VPN pour les opérations ultérieures de mise à disposition et de gestion, y compris le déploiement du composant Cloud Foundry principal de CFEE.

Le diagramme ci-dessous présente un environnement CFEE installé derrière un périmètre réseau VRA.   
![Réseau isolé](img/CFEE_IsolatedNetwork.png "Diagramme illustrant le fonctionnement d'un environnement CFEE dans un réseau isolé")

## Contrôle de l'accès aux instances CFEE dans un réseau isolé
{: #oppening-access-points}

Les applications Cloud Foundry qui s'exécutent dans une instance CFEE ont fréquemment besoin d'accéder à des éléments externes au réseau pour diverses raisons. Par exemple, une application peut avoir besoin d'accéder à un service RESTful public ou de télécharger des packages depuis des registres publics, tels qu'une image Docker, des packages NPM, des modules Python, etc. Par conséquent, vous devez configurer vos règles de pare-feu de manière à disposer des accès réseau dont vous avez besoin.

Vous pouvez contrôler la connectivité entrante/sortante vers/depuis un réseau isolé en configurant les règles pour des protocoles ou des noeuds finaux source ou cible spécifiques. Pour ce faire, vous pouvez utiliser des mécanismes de contrôle de la technologie ayant servi à configurer le périmètre de réseau (par exemple, VRA). Le moyen le plus simple pour contrôler ces éléments consiste toutefois à créer des [règles réseau Calico](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy) qui définissent des règles de réseau propres au cluster Kubernetes hôte. Voir la rubrique relative à la [création et application de règles réseau Calico](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies) pour des directives pas à pas.

Les types de règle d'accès réseau pouvant être associées à un réseau isolé CFEE sont les suivants :

* **Accès au trafic entrant :** lorsqu'un cluster Kubernetes est installé, il définit et configures automatiquement une [règle Calico par défaut](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy) qui autorise l'accès en gestion aux noeuds worker (qui, dans ce cas, hébergent votre instance CFEE).

<br>
Règles Calico **par défaut** d'accès aux noeuds worker du **cluster Kubernetes** :

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
Si vous utilisez une autre implémentation de périmètre réseau, vous devrez configurer les mêmes règles à l'aide des mécanismes de contrôle correspondants.
  
* **Accès au trafic sortant :** CFEE s'appuie sur un certain nombre de services dans IBM Cloud avec des noeuds finaux publics. Votre réseau isolé doit autoriser votre instance CFEE à accéder à ces noeuds finaux. Ces noeuds finaux sont répertoriés ci-dessous accompagnés de leurs règles Calico respectives.

| Règle   | Description | Noeud final |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | Autorise l'accès sortant au plan de gestion CFEE | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Autorise l'accès sortant aux registres Docker | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | Autorise l'accès sortant au plan de gestion du cluster Kubernetes de CFEE | [En savoir plus](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | Autorise l'accès sortant et le routage vers les adresses IP portables du cluster Kubernetes de CFEE | Pour trouver les adresses portables de votre cluster, utilisez `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | Autorise l'accès sortant à la base de données Compose for PostgreSQL de CFEE | Vous trouverez le noeud final à partir de la page de tableau de bord de l'instance Compose `<cfee-name>-postgress` et dans la page _Accès privé_ de CFEE. |
| cfee-egress-allow-rc | Autorise l'accès sortant à la plateforme IBM Cloud pour activer la syndication des services | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | Autorise l'accès sortant au service IBM Cloud Container Registry | [En savoir plu](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (facultatif) Autorise le trafic réseau sortant depuis les noeuds worker de CFEE vers des services IBM Cloud Monitoring et IBM Cloud Log Analysis | [En savoir plu](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | Autorise le trafic réseau sortant depuis les noeuds worker de CFEE vers le registre d'image helm | Cette règle Calico est destinée aux adresses IP de Helm Tiller, qui requiert un accès aux domaines `mage:gcr.io` et `storage.googleapis.com` pour envoyer l'image Helm Tiller. |

<br>  
La dernière règle de sécurité réseau (la plus **importante**) est celle qui refuse tout accès au trafic réseau qui ne respecte pas les précédentes règles.
<br>
Règle Calico de **refus de tout accès sortant** (`cfee-egress-deny-all`) :

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-egress-deny-all
spec:
  applyOnForward: true
  egress:
  - action: Deny
    destination: {}
    source: {}
  order: 3000
  selector: ibm.role in { 'worker_public' }
  types:
- Egress
```
{: codeblock}

<br>
Règle Calico de **refus de tout accès entrant** (`cfee-ingress-deny-all') :

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-ingress-deny-all
spec:
  applyOnForward: true
  ingress:
  - action: Deny
    destination: {}
    source: {}
  order: 4000
  selector: ibm.role=='worker_public'
  types:
- Ingress
```
{: codeblock}
<br>  
La complexité avec les accès sortants depuis des réseaux isolés tient au fait que certains noeuds finaux cible se trouvent derrière un réseau _public edge_, tel que Cloudflare ou Akamai. Dans ce cas, vous devrez peut-être accorder l'accès à des centaines d'adresses IP qui changent souvent. Vous pouvez éviter cette situation en **autorisant tous les accès sortants** à l'aide de la règle Calico (`cfee-egress-allow-all`) comme suit :

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
   name: cfee-egress-allow-http
    spec:
   egress:
   - action: Allow
     destination:
       ports:
       - 443
       - 80
     protocol: TCP
     source: {}
   order: 1611
   selector: ibm.role in { 'worker_public' }
   applyOnForward: true
   types:
   - Egress
```
{: codeblock}
  
Dans l'exemple ci-dessus, l'accès sortant (“egress”) vers le réseau public est accordé à tous les appels HTTP et HTTPS (l'intégralité du trafic TCP sur les ports 443 et 80) provenant des noeuds worker du cluster CFEE (“worker_public”).

## Accès privé depuis le plan de contrôle de la gestion
{: #private-access}

La gestion d'une instance CFEE dans un réseau isolé nécessite que le plan de contrôle de la gestion CFEE dispose d'un accès privé à l'instance CFEE. L'accès privé du plan de contrôle de la gestion CFEE à l'instance CFEE est activé par défaut. 

Les utilisateurs ayant un rôle d'_administrateur_ peuvent désactiver l'accès privé du plan de contrôle de la gestion CFEE. Lorsque l'accès privé est désactivé, le plan de contrôle CFEE ne peut pas extraire de données ni gérer l'instance CFEE (que ce soit via l'interface utilisateur, l'interface de ligne de commande ou l'API). Les administrateurs CFEE peuvent désactiver l'accès privé dans la page **Accès privé** (visible uniquement des administrateurs), accessible depuis l'interface utilisateur CFEE. Une fois sur la page, cliquez sur **Désactiver**.  

L'accès au réseau isolé s'effectue via une clé d'API.  Une clé d'API est fournie par défaut. Un administrateur CFEE peut remplacer la clé d'API par défaut par une clé personnalisée. L'activation de l'accès privé une fois qu'il a été désactivé nécessite une clé d'API qui doit être générée dans *_Clés d'API IBM Cloud_* (dans l'en-tête de l'interface utilisateur IBM Cloud, accédez à _Gérer > Accès (IAM) > Clés d'API IBM Cloud_).

