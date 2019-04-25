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

# Betrieb in einem isolierten Netz
{: #isolated-network}


Ab Version 2.2.0 können Instanzen von {{site.data.keyword.cfee_full}} (CFEE) in einem isolierten Netz betrieben werden, das die Umgebung vor externen Bedrohungen schützt und sichert. Sie erstellen ein isoliertes Netz mithilfe privater VLANs und einer Gruppe von Steuermechanismen, um den Datenverkehr in die und aus den Ressourcen innerhalb des Netzperimeters zu leiten sowie den Datenverkehr zu filtern und zu schützen. Isolierte Netze werden unter Verwendung von Technologien wie Virtual Router Appliances ([VRAs](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)) eingerichtet.  

**Hinweis:** Für CFEE-Instanzen, die in einem isolierten Netz betrieben werden, muss der Kubernetes-Cluster von CFEE auf V1.13 aktualisiert werden. Die Aktualisierung des Kubernetes-Clusters auf V1.13 ist von der CFEE-Aktualisierung unabhängig. 

Eine CFEE-Instanz wird durch den IBM Kubernetes Service in einem Cluster bereitgestellt. Die Cloud Foundry-Zellen von CFEE (dort werden Anwendungen gehostet) werden in den Workerknoten des Clusters bereitgestellt. Das heißt, der Zugriff auf die CFEE-Zellen und -Anwendungen impliziert, dass auf die Cluster-Workerknoten zugegriffen wird.  

Die Workerknoten enthalten Application Load Balancer (ALBs), die die Workload der Anwendungen auf die Workerknoten verteilen. Mit CFEE V2.2.0 können die Kubernetes-ALBs in privaten und öffentlichen Netzen eingesetzt werden. Dies bedeutet, dass auf CFEE V2.2.0 sowohl von öffentlichen als auch von privaten Netzen aus zugegriffen werden kann. 

## CFEE-Management in einem isolierten Netz
{: #control-plan-access}

In V2.2.0 verwendet die CFEE-Managementebene (das Subsystem, das für die Bereitstellung, für Updates und für sonstige Lebenszyklusaktivitäten verwendet wird) nicht direkt die ALBs oder die Workerknoten, um eine CFEE-Instanz zu verwalten. Stattdessen verwendet die CFEE-Managementebene die _VPN-Verbindung zwischen den Kubernetes-Master- und -Workerknoten_ für den Zugriff auf die CFEE-Instanz und die zugehörigen Ressourcen. Auf diese Weise kann die Managementebene die CFEE-Instanz steuern. 

Nachdem Sie Ihre CFEE-Instanz erstellt haben, erstellt die Managementebene in Ihrem Konto eine [IAM-Service-ID](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) und übergibt diese an den IKS-Masterknoten. Die CFEE-Managementebene verwendet diese Service-ID, um über den Masterknoten und den zugehörigen VPN-Zugriff für nachfolgende Bereitstellungs- und Managementoperationen auf die CFEE-Host-Worker zuzugreifen. Zu diesen Operationen gehört auch die Bereitstellung der Cloud Foundry-Hauptkomponente von CFEE. 

Das folgende Diagramm zeigt eine CFEE-Instanz, die hinter einem VRA-Netzperimeter installiert ist.    
![Netzisolierung](img/CFEE_IsolatedNetwork.png "Diagramm, das die Funktionsweise einer CFEE-Instanz in einem isolierten Netz beschreibt.")

## Zugriff auf CFEE-Instanzen in einem isolierten Netz steuern
{: #oppening-access-points}

CF-Anwendungen, die in einer CFEE-Instanz ausgeführt werden, müssen aus verschiedenen Gründen häufig auf Positionen außerhalb des isolierten Netzes zugreifen. Beispielsweise muss eine Anwendung möglicherweise auf einen öffentlichen REST-konformen Service zugreifen oder Pakete aus öffentlichen Registrys herunterladen, wie ein Docker-Image, NPM-Pakete, Python-Module usw. Daher müssen Sie Ihre Firewallregeln so konfigurieren, dass sie Ihre individuellen Netzzugriffsanforderungen unterstützen. 

Sie können die Konnektivität für eingehende/ausgehende Verbindungen zu einem isolierten Netz steuern, indem Sie die Regeln für bestimmte Protokolle, Quellen oder Zielendpunkte konfigurieren. Sie können diese erstellen und konfigurieren, indem Sie die Steuermechanismen in der spezifischen Technologie verwenden, die zum Einrichten des Netzperimeters verwendet wird (z. B. VRA). Der einfachste Weg, dies zu steuern, ist die Erstellung von [Calico-Netzrichtlinien](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy), die Netzregeln speziell für den Kubernetes-Cluster des Hosts definieren. Eine schrittweise Anleitung finden Sie unter [Calico-Netzrichtlinien erstellen und anwenden](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies). 

Netzzugriffsregeln, die sich auf eine CFEE-Instanz in einem isolierten Netz beziehen, können die folgenden Typen haben: 

* **Zugriff für eingehenden Datenverkehr:** Bei der Installation eines Kubernetes-Clusters wird automatisch eine [Calico-Standardrichtlinie](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy) festgelegt und konfiguriert, die den Verwaltungszugriff auf die Workerknoten (die in diesem Fall Ihre CFEE-Instanz hosten) ermöglicht. 

<br>
**Standardmäßige** Calico-Regeln für den Zugriff auf die Workerknoten des **Kubernetes-Clusters**: 

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
Wenn Sie eine alternative Netzperimeterimplementierung verwenden, müssen Sie mit den entsprechenden Steuermechanismen dieselben Richtlinien konfigurieren. 
  
* **Zugriff für ausgehenden Datenverkehr:** CFEE verwendet eine Reihe von Services in IBM Cloud mit öffentlichen Endpunkten. Ihr isoliertes Netz muss es Ihrer CFEE-Instanz ermöglichen, diese Endpunkte zu erreichen. Diese sind im Folgenden zusammen mit den jeweiligen Calico-Richtlinien aufgeführt. 

| Regel  | Beschreibung | Endpunkt |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | Ermöglicht ausgehenden Zugriff auf die CFEE-Managementebene | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Ermöglicht ausgehenden Zugriff auf die Docker-Registrys | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | Ermöglicht ausgehenden Zugriff auf die CFEE-Managementebene für Kubernetes-Cluster | [Weitere Informationen](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | Ermöglicht ausgehenden Zugriff auf und Weiterleitung an die portierbaren IP-Adressen des Kubernetes-Clusters von CFEE | Sie finden die portierbaren Adressen Ihres Clusters mithilfe der folgenden Befehle: `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | Ermöglicht ausgehenden Zugriff auf die Compose for PostgreSQL-Datenbank von CFEE | Sie finden den Endpunkt auf der Dashboardseite `<cfee-name>-postgress` der Compose-Instanz und auf der CFEE-Seite für _privaten Zugriff_. |
| cfee-egress-allow-rc | Ermöglicht ausgehenden Zugriff auf die IBM Cloud-Plattform, um die Servicesyndikation zu aktivieren | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | Ermöglicht ausgehenden Zugriff auf die IBM Cloud-Container-Registry | [Weitere Informationen](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (Optional) Ermöglicht ausgehenden Netzdatenverkehr von den CFEE-Workerknoten zu den IBM Cloud Monitoring- und IBM Cloud Log Analysis-Services | [Weitere Informationen](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | Ermöglicht ausgehenden Netzdatenverkehr von den CFEE-Workerknoten zum Helm-Image-Registry | Diese Calico-Regel gilt für IPs von Helm Tiller, die Zugriff auf die Domänen `mage:gcr.io` und `storage.googleapis.com` benötigen, um das Helm Tiller-Image zu extrahieren. |

<br>  
Die letzte Netzsicherheitsregel (die **wichtigste** Regel) ist die, die den gesamten Zugriff für Netzverkehr verweigert, der nicht mit den vorherigen Richtlinien übereinstimmt. 
<br>
Calico-Regel für die **Verweigerung des gesamten ausgehenden Zugriffs** (`cfee-egress-deny-all`): 

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
Calico-Regel für die **Verweigerung des gesamten eingehenden Zugriffs** (`cfee-ingress-deny-all')
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
Eine der Komplexitäten bei dem ausgehenden Zugriff von isolierten Netzen besteht darin, dass einige der Zielendpunkte hinter einem _öffentlichen Edge_-Netz wie Cloudflare oder Akamai liegen. In diesem Fall müssen Sie möglicherweise den Zugriff von Hunderten von IP-Adressen zulassen, die sich oft ändern. Sie können diese Situation optional vermeiden, indem Sie **den gesamten ausgehenden Zugriff zulassen**. Verwenden Sie dazu die folgende Calico-Regel (`cfee-egress-allow-all`): 

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
  
Im obigen Beispiel ist für alle HTTP- und HTTPS-Aufrufe (den gesamten TCP-Datenverkehr an den Ports 443 und 80), die von den Workerknoten des CFEE-Clusters (“worker_public”) stammen, der ausgehende Zugriff (“egress”) auf das öffentliche Netz zugelassen. 

## Privater Zugriff von der Managementsteuerebene aus
{: #private-access}

Die Verwaltung einer CFEE-Instanz in einem isolierten Netz erfordert den privaten Zugriff auf die CFEE-Instanz durch die CFEE-Managementsteuerebene. Der private Zugriff auf die CFEE-Instanz durch die CFEE-Managementsteuerebene ist standardmäßig aktiviert.  

Benutzer mit der Rolle _Administration_ können den privaten Zugriff durch die CFEE-Managementsteuerebene inaktivieren. Beachten Sie, dass die CFEE-Steuerebene nach der Inaktivierung des privaten Zugriffs keine Daten mehr abrufen kann und die CFEE-Instanz nicht mehr verwalten kann (weder über die Benutzerschnittstelle noch über die CLI oder die API). CFEE-Administratoren können den privaten Zugriff auf der Seite**** für privaten Zugriff inaktivieren. Diese Seite ist nur für Administratoren sichtbar und befindet sich in der CFEE-Benutzerschnittstelle. Wählen Sie auf dieser Seite **Inaktivieren** aus.   

Der Zugriff auf das isoliert Netz erfolgt über einen API-Schlüssel. Ein API-Schlüssel wird standardmäßig bereitgestellt. Ein CFEE-Administrator kann den Standard-API-Schlüssel durch einen angepassten Schlüssel ersetzen. Für die Aktivierung des privaten Zugriffs, nachdem er inaktiviert wurde, ist ein API-Schlüssel erforderlich, der unter *_IBM Cloud-API-Schlüssel_* generiert werden muss. (Rufen Sie dazu im Header der IBM Cloud-Benutzerschnittstelle _Verwalten > Zugriff (IAM) > IBM Cloud-API-Schlüssel_ auf.) 

