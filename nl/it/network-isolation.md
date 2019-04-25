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

# Utilizzo di una rete isolata 
{: #isolated-network}


A partire dalla versione 2.2.0, le istanze di {{site.data.keyword.cfee_full}} (CFEE) possono operare all'interno di una rete isolata che protegge l'ambiente da minacce esterne. Crea una rete isolata tramite le VLAN private e una serie di meccanismi di controllo per instradare, filtrare e proteggere il traffico in entrata e in uscita delle risorse all'interno del perimetro di rete. Le reti isolate vengono configurate utilizzando tecnologie come Virtual Router Appliance ([VRA](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)). 

**Nota:** le istanze CFEE che operano in una rete isolata richiedono che il cluster Kubernetes CFEE sia aggiornato alla v1.13. L'aggiornamento del cluster Kubernetes alla v1.13 è indipendente rispetto all'aggiornamento del CFEE.

Viene eseguito il provisioning di un'istanza CFEE in un cluster dall'IBM Kubernetes Service. Viene eseguito il provisioning delle celle Cloud Foundry del CFEE (dove le applicazioni sono ospitate) nei nodi di lavoro del cluster. Questo significa che l'accesso alle applicazioni e alle celle CFEE implica l'accesso ai nodi di lavoro del cluster. 

I nodi di lavoro contengono i programmi di bilanciamento del carico dell'applicazione (ALB) che distribuiscono il carico di lavoro delle applicazioni tra i nodi di lavoro. CFEE v2.2.0 abilita gli ALB Kubernetes in entrambe le reti, privata e pubblica.  Questo significa che è possibile accedere a CFEE v2.2.0 sia da reti pubbliche che private.

## Gestione di CFEE in una rete isolata
{: #control-plan-access}

Nella v2.2.0 il piano di gestione di CFEE (il sistema secondario utilizzato per il provisioning, gli aggiornamenti e altre attività del ciclo di vita) non si basa sugli ALB o sui nodi di lavoro direttamente per gestire un'istanza CFEE. Invece, il piano di gestione di CFEE utilizza la _connessione VPN tra il master Kubernetes e i nodi di lavoro_ per accedere all'istanza CFEE e alle relative risorse. Questo consente al piano di gestione di controllare l'istanza CFEE.

Dopo aver creato la tua istanza CFEE, il piano di gestione crea un [ID servizio IAM](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) nel tuo account che fornisce al nodo master IKS. Il piano di gestione CFEE utilizza questo ID servizio per accedere ai nodi di lavoro host CFEE tramite il nodo master e il suo accesso VPN alle successive operazioni di provisioning e gestione, inclusa la distribuzione del componente Cloud Foundry principale di CFEE.

Il seguente diagramma illustra un CFEE installato dietro un perimetro di rete VRA.   
![Rete isolata](img/CFEE_IsolatedNetwork.png "Diagramma che descrive come funziona un CFEE in una rete isolata.")

## Controllo dell'accesso alle istanze CFEE in una rete isolata
{: #oppening-access-points}

Le applicazioni CF in esecuzione in un'istanza CFEE devono frequentemente uscire dalla rete isolata per vari motivi. Ad esempio, un'applicazione potrebbe dover accedere a un servizio RESTful pubblico o scaricare dei pacchetti da registri pubblici, come un'immagine Docker, i pacchetti NPM, i moduli Python, ecc. Pertanto, devi configurare le tue regole del firewall per consentire bisogni di accesso di rete specifici.

Puoi controllare la connettività in entrata/uscita a/da una rete isolata configurando delle regole per endpoint di destinazione, origini o protocolli specifici. Puoi creare e configurare queste regole utilizzando i meccanismi di controllo nella tecnologia specifica utilizzata per configurare il perimetro di rete (ad es. VRA). Tuttavia, il modo più semplice per controllare tutto ciò è di creare delle [politiche di rete Calico](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy) che definiscono le regole di rete in modo specifico per il cluster Kubernetes host. Per delle istruzioni dettagliate, vedi [creazione ed applicazione delle politiche di rete Calico](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies).

Le regole di accesso alla rete correlate a un CFEE isolato di rete possono essere dei seguenti tipi:

* **Accesso traffico in entrata:** quando viene installato un cluster Kubernetes, imposta e configura automaticamente una [politica Calico predefinita](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy) che consente la gestione dell'accesso ai nodi di lavoro (che in questo caso ospitano la tua istanza CFEE).

<br>
Regole Calico **predefinite** per l'accesso ai nodi di lavoro del **cluster Kubernetes**:

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
Se stai utilizzando un'implementazione di perimetro di rete alternativa, dovrai configurare le stesse politiche utilizzando i meccanismi di controllo corrispondenti.
  
* **Accesso traffico in uscita:** CFEE si basa su diversi servizi in IBM Cloud con endpoint pubblici. La tua rete isolata deve consentire alla tua istanza CFEE di raggiungere questi endpoint. Gli endpoint sono elencati qui di seguito insieme alle rispettive politiche Calico.

|Regola| Descrizione | Endpoint |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | Consente l'accesso in uscita al piano di gestione CFEE | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Consente l'accesso in uscita ai registri Docker | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | Consente l'accesso in uscita al piano di gestione del cluster Kubernetes CFEE | [Ulteriori informazioni](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | Consente l'accesso in uscita e l'instradamento agli indirizzi IP portatili del cluster Kubernetes del CFEE |Puoi trovare i tuoi indirizzi portatili del cluster utilizzando: `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | Consente l'accesso in uscita al database Compose for PostgreSQL del CFEE | Puoi trovare l'endpoint dalla pagina del dashboard dell'istanza Compose `<cfee-name>-postgress` e nella pagina _Accesso privato_ del CFEE. |
| cfee-egress-allow-rc | Consente l'accesso in uscita alla piattaforma IBM Cloud per abilitare la diffusione del servizio | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | Consente l'accesso in uscita a IBM Cloud Container Registry | [Ulteriori informazioni](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (facoltativo) Consente il traffico di rete in uscita dai nodi di lavoro CFEE ai servizi IBM Cloud Monitoring e IBM Cloud Log Analysis | [Ulteriori informazioni](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | Consente il traffico di rete in uscita dai nodi di lavoro CFEE al registro di immagini helm | Questa regola calico è per gli IP del tiller Helm, che hanno bisogno dell'accesso ai domini `mage:gcr.io` e `storage.googleapis.com` per eseguire il pull dell'immagine tiller helm. |

<br>  
La regola di sicurezza di rete finale (la più **importante**) è quella che nega tutto l'accesso al traffico di rete che non corrisponde alle precedenti politiche.
<br>
Regola Calico per **negare tutto l'accesso in uscita** (`cfee-egress-deny-all`):

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
Regola Calico per **negare tutto l'accesso in entrata** (`cfee-ingress-deny-all')
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
Una complessità con l'accesso in uscita dalle reti isolate è che alcuni degli endpoint di destinazione sono dietro a una rete _edge pubblica_, come Cloudflare o Akamai. In questo caso potresti dover consentire potenzialmente l'accesso a centinaia di indirizzi IP che cambiano spesso. Puoi facoltativamente evitare questa situazione **consentendo tutto l'accesso in uscita** utilizzando questa regola Calico (`cfee-egress-allow-all`):

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
  
Nel precedente esempio, tutte le chiamate HTTP e HTTPS (tutto il traffico TCP sulle porte 443 e 80) che provengono dai nodi di lavoro del cluster CFEE (“worker_public”) sono accesso in uscita (“egress”) consentito alla rete pubblica.

## Accesso privato dal piano di controllo di gestione
{: #private-access}

La gestione di un'istanza CFEE in una rete isolata richiede l'accesso privato all'istanza CFEE dal piano di controllo di gestione CFEE. L'accesso privato all'istanza CFEE dal piano di controllo di gestione CFEE viene abilitato per impostazione predefinita. 

Gli utenti con un ruolo di _amministrazione_ possono disabilitare l'accesso privato dal piano di controllo di gestione CFEE. Tieni presente che disabilitando l'accesso privato impedirai al piano di controllo CFEE di richiamare i dati e di gestire l'istanza CFEE (né tramite l'interfaccia utente, né con la CLI o l'API). Gli amministratori CFEE possono disabilitare l'accesso privato nella pagina **Accesso privato** (visibile solo agli amministratori), ubicata nell'interfaccia utente di CFEE. Una volta nella pagina premi **Disabilita**.  

L'accesso alla rete isolata avviene tramite una chiave API.  Una chiave API viene fornita per impostazione predefinita. Un amministratore CFEE può sostituire la chiave API predefinita con una chiave personalizzata. L'abilitazione dell'accesso privato dopo che è stato disabilitato richiede una chiave API che deve essere generata nelle *_chiavi API IBM Cloud_* (nell'intestazione dell'interfaccia utente IBM Cloud, vai a _Gestisci > Accesso (IAM) > Chiavi API IBM Cloud_ ).

