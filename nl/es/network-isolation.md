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

# Funcionamiento en una red aislada
{: #isolated-network}


A partir de la versión 2.2.0, las instancias de {{site.data.keyword.cfee_full}} (CFEE) pueden operar dentro de una red aislada que protege el entorno frente a amenazas externas. La red aislada se crea a través de VLAN privadas y de un conjunto de mecanismos de control para direccionar, filtrar y proteger el tráfico de entrada y de salida de los recursos dentro del perímetro de la red. Las redes aisladas se configuran mediante tecnologías como Dispositivos de direccionador virtual ([VRA](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)). 

**Nota:** las instancias de CFEE que operan en una red aislada requieren que el clúster CFEE de kubernetes se actualice a v1.13. La actualización del clúster de Kubernetes v1.13 es independiente de la actualización de CFEE.

Una instancia de CFEE se suministra en un clúster desde el servicio IBM Kubernetes. Las células de Cloud Foundry de CFEE (donde las aplicaciones están alojadas) se suministran en los nodos trabajadores del clúster. Esto significa que el acceso a las células y aplicaciones de CFEE implica acceder a los nodos trabajadores del clúster. 

Los nodos trabajadores contienen equilibradores de cargas de aplicaciones (ALB) que distribuyen la carga de trabajo de las aplicaciones entre los nodos trabajadores. CFEE v2.2.0 habilita los ALB de Kubernetes en las redes tanto privadas como públicas.  Esto significa que se puede acceder a CFEE v2.2.0 desde redes tanto públicas como privadas.

## Gestión de CFEE en una red aislada
{: #control-plan-access}

En v2.2.0, el plano de gestión de CFEE (el subsistema utilizado para suministro, actualización y otras actividades del ciclo de vida) no se basa en los ALB ni en los nodos trabajadores directamente para gestionar una instancia de CFEE. En lugar de ello, el plano de gestión de CFEE utiliza la _conexión VPN entre los nodos maestro y trabajador de Kubernetes_ para acceder a la instancia de CFEE y a sus recursos. Esto permite que el plano de gestión controle la instancia de CFEE.

Después de crear la instancia de CFEE, el plano de gestión crea un [ID de servicio de IAM](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) en la cuenta que proporciona al nodo maestro de IKS. El plano de gestión de CFEE utiliza este ID de servicio para acceder a los nodos trabajadores que alojan CFEE a través del nodo maestro y su acceso VPN para las operaciones de suministro y gestión subsiguientes, incluido el despliegue del componente principal Cloud Foundry de CFEE.

En el diagrama siguiente se muestra un CFEE instalado detrás de un perímetro de red de VRA.   
![Aislamiento de red](img/CFEE_IsolatedNetwork.png "Diagrama en el que se describe el funcionamiento de CFEE en una red aislada.")

## Control del acceso a instancias de CFEE en una red aislada
{: #oppening-access-points}

Las apps CF que se ejecutan en una instancia de CFEE con frecuencia tienen que acceder fuera de la red aislada por varias razones. Por ejemplo, una aplicación puede necesitar acceder a un servicio RESTful público, o descargar paquetes de registros públicos, como una imagen de Docker, paquetes NPM, módulos de Python, etc. Por lo tanto, es necesario configurar reglas de cortafuegos para habilitar las necesidades específicas de acceso de red.

Puede controlar la conectividad de entrada/salida hacia/desde una red aislada mediante la configuración de reglas para determinados protocolos, orígenes o puntos finales de destino. Puede crearlos y configurarlos utilizando mecanismos de control en la tecnología específica utilizada para configurar el perímetro de red (por ejemplo, VRA). Sin embargo, la forma más sencilla de controlar esto es la creación de [políticas de red de Calico](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy) que definen reglas de red específicas para el clúster de Kubernetes de host. Consulte el apartado sobre [Creación y aplicación de políticas de red de Calico](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies) para ver una guía paso a paso.

Las reglas de acceso de red relacionadas con un CFEE aislado de red pueden ser de los tipos siguientes:

* **Acceso de tráfico de entrada:** cuando se instala un clúster de Kubernetes, se establece y se configura automáticamente una [política de Calico predeterminada](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy) que permite el acceso de gestión a los nodos trabajadores (en este caso, los que alojan la instancia de CFEE).

<br>
Reglas de Calico **predeterminadas** para acceder a nodos trabajadores de un **clúster de Kubernetes**:

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'
allow-vrrp                      1600    ibm.role == 'worker_public'
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
Si utiliza una implementación de perímetro de red alternativa, tendrá que configurar las mismas políticas utilizando los mecanismos de control correspondientes.
  
* **Acceso de tráfico de salida:** CFEE se basa en una serie de servicios de IBM Cloud con puntos finales públicos. La red aislada debe permitir que la instancia de CFEE acceda a estos puntos finales. Estos se muestran a continuación junto con sus respectivas políticas de Calico.

| Regla   | Descripción | Punto final |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | Permite el acceso de salida al plano de gestión de CFEE | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Permite el acceso de salida a los registros de Docker | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | Permite el acceso de salida al plano de gestión de clústeres de Kubernetes de CFEE | [Más información](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | Permite el acceso de salida y el direccionamiento a las direcciones IP portátiles del clúster de Kubernetes de CFEE | Para encontrar las direcciones portátiles del clúster, utilice el mandato: `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | Permite el acceso de salida a la base de datos Compose for PostgreSQL de CFEE | Encontrará el punto final en la página del panel de control de `<cfee-name>-postgress` de la instancia de Compose y en la página _Acceso privado_ de CFEE |
| cfee-egress-allow-rc | Permite el acceso de salida a la plataforma de IBM Cloud para habilitar la sindicación de servicios | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | Permite el acceso de salida al registro de contenedores de IBM Cloud | [Más información](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (Opcional) Permite el tráfico de red de salida de los nodos trabajadores de CFEE a los servicios IBM Cloud Monitoring e IBM Cloud Log Analysis | [Más información](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | Permite el tráfico de red de salida de los nodos trabajadores de CFEE al registro de imágenes de helm| Esta regla de calico es para las IP del tiller de Helm, que necesita acceso a los dominios `mage:gcr.io` y `storage.googleapis.com` para obtener la imagen de tiller de helm. |

<br>  
La regla de seguridad de red final (la más **importante**) es la que deniega todo el acceso al tráfico de red que no se ajusta a las políticas anteriores.
<br>
Regla de Calico para **denegar todo el acceso de salida** (`cfee-egress-deny-all`):

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
Regla de Calico para **denegar todo el acceso de entrada** (`cfee-ingress-deny-all')
`):

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
Una complejidad que plantea el acceso de salida de redes aisladas es que algunos de los puntos finales de destino están detrás de una red _de extremo pública_, como Cloudflare o Akamai. En este caso, es posible que tenga que permitir el acceso a cientos de direcciones IP que cambian con frecuenta. Puede evitar esta situación **permitiendo todo el acceso de salida** mediante la siguiente regla de Calico (`cfee-egress-allow-all`):

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
  
En el ejemplo anterior, todas las llamadas HTTP y HTTPS (todo el tráfico TCP en los puertos 443 y 80) procedentes de nodos trabajadores del clúster de CFEE ("worker_public") tienen permitido el acceso de salida ("egress") a la red pública.

## Acceso privado desde el plano de control de gestión
{: #private-access}

La gestión de una instancia de CFEE en una red aislada requiere acceso privado a la instancia de CFEE por parte del plano de control de gestión de CFEE. El acceso privado a la instancia CFEE por parte del plano de control de gestión de CFEE está habilitado de forma predeterminada. 

Los usuarios con el rol de _Administrador_ pueden inhabilitar el acceso privado por parte del plano de control de gestión de CFEE. Tenga en cuenta que inhabilitar el acceso privado impedirá que el plano de control de CFEE recupere datos y gestione la instancia de CFEE (ni mediante la interfaz de usuario, ni mediante la CLI y la API). Los administradores de CFEE pueden inhabilitar el acceso privado en la página **Acceso privado** (visible solo para los administradores), que se encuentra en la interfaz de usuario de CFEE. Una vez en la página, pulse **Inhabilitar**.  

El acceso a la red privada se realiza mediante una clave de API.  Se proporciona una clave de API de forma predeterminada. Un administrador de CFEE puede sustituir la clave de API predeterminada por una clave personalizada. Para habilitar el acceso privado después de que se haya inhabilitado, se requiere una clave de API que se debe generar en *_Claves de API de IBM Cloud_* (en la cabecera de la interfaz de usuario de IBM Cloud, vaya a _Gestionar > Acceso (IAM) > Claves de API de IBM Cloud_).

