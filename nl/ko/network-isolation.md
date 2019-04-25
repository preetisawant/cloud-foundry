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

# 격리된 네트워크에서 작동
{: #isolated-network}


버전 2.2.0부터 {{site.data.keyword.cfee_full}}(CFEE) 인스턴스는 외부 위협으로부터 환경을 보호하는 격리된 네트워크에서 작동할 수 있습니다. 사설 VLAN을 통한 격리된 네트워크와 제어 메커니즘 세트를 작성하여 네트워크 프리미어의 리소스에서 수신 및 송신하는 트래픽을 라우팅, 필터링 및 보호할 수 있습니다. 격리된 네트워크는 [VRA](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)(Virtual
Router Appliance)와 같은 기술을 사용하여 설정합니다. 

**참고:** 격리된 네트워크에서 작동 중인 CFEE 인스턴스에서는 CFEE Kubernetes 클러스터가 v1.13으로 업데이트되어야 합니다. Kubernetes 클러스터 v1.13으로 업데이트는 CFEE 업데이트와 무관합니다.

CFEE 인스턴스는 IBM Kubernetes Service에서 클러스터로 프로비저닝됩니다. CFEE의 Cloud Foundry 셀(여기에서 애플리케이션이 호스팅됨)은 클러스터의 작업자 노드에 프로비저닝됩니다. 즉, CFEE 셀과 애플리케이션에 액세스하면 클러스터 작업자 노드에 액세스하는 것입니다. 

작업자 노드에는 작업자 노드 간에 애플리케이션의 워크로드를 분배하는 ALB(Application Load Balancer)가 포함되어 있습니다. CFEE v2.2.0을 사용하면 사설 및 공용 네트워크 둘 다에서 Kubernetes ALB를 사용할 수 있습니다. 즉, 공용 및 사설 네트워크 둘 다에서 CFEE v2.2.0에 액세스할 수 있습니다.

## 격리된 네트워크에서 CFEE 관리
{: #control-plan-access}

v2.2.0에서 CFEE 관리 플레인(프로비저닝, 업데이트 및 기타 라이프사이클 활동에 사용되는 하위 시스템)에서는 직접 ALB 또는 작업 노드를 사용하여 CFEE 인스턴스를 관리하지 않습니다. 대신 CFEE 관리 플레인에서는 _Kubernetes 마스터 및 작업자 노드 사이의 VPN 연결_을 사용하여 CFEE 인스턴스와 해당 리소스에 액세스합니다. 그러면 관리 플레인에서 CFEE 인스턴스를 제어할 수 있습니다.

CFEE 인스턴스를 작성한 다음, 관리 프레인에서 IKS 마스터 노드에 제공하는 [IAM 서비스 ID](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature)를 계정에서 작성합니다. CFEE 관리 플레인에서는 CFEE의 기본 Cloud Foundry 컴포넌트에 배치와 같은 후속 프로비저닝 및 관리 오퍼레이션에 사용하기 위해 마스터 노드와 해당 VPN 액세스를 통해 CFEE 호스트 작업자에 액세스하는 데 이 서비스 ID를 사용합니다.

아래 다이어그램에서는 VRA 네트워크 경계에 설치된 CFEE를 보여줍니다.   
![네트워크 격리](img/CFEE_IsolatedNetwork.png "격리된 네트워크에서 CFEE 작동 방식을 설명하는 다이어그램")

## 격리된 네트워크에서 CFEE 인스턴스에 대한 액세스 제어
{: #oppening-access-points}

CFEE 인스턴스에서 실행되는 CF 애플리케이션은 다양한 이유로 격리된 네트워크 외부에 자주 연결해야 합니다. 예를 들어 애플리케이션에서 공용 RESTful 서비스에 액세스하거나 Docker 이미지, NPM 패키지, Python 모듈 등과 같은 공용 레지스트리에서 패키지를 다운로드해야 할 수도 있습니다. 따라서 특정 네트워크 액세스 요구사항을 사용할 수 있도록 방화벽 규칙을 구성해야 합니다.

특정 프로토콜, 소스 또는 대상 엔드포인트의 규칙을 구성하여 격리된 네트워크로/로부터의 인바운드/아웃바운드 연결을 제어할 수 있습니다. 네트워크 경계(예: VRA)를 설정하는 데 사용하는 특정 기술의 제어 메커니즘을 사용하여 이 규칙을 작성하고 구성할 수 있습니다. 그러나 이 연결을 제어하는 가장 쉬운 방법은 특별히 호스트 Kubernetes 클러스터용으로 네트워크 규칙을 정의하는 [Calico 네트워크 정책](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy)을 작성하는 것입니다. 단계별 지침은 [Calico 네트워크 정책 작성 및 적용](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies)을 참조하십시오.

네트워크 격리된 CFEE와 관련된 네트워크 액세스 규칙의 유형은 다음과 같을 수 있습니다.

* **인바운드 트래픽 액세스:** Kubernetes 클러스터가 설치되면 작업자 노드에 대한 관리 액세스를 허용하는 [기본 Calico 정책](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy)을 자동으로 설정하고 구성합니다(이 경우 CFEE 인스턴스 호스팅).

<br>
**Kubernetes 클러스터** 작업자 노드에 액세스하는 **기본** Calico 규칙:

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
대체 네트워크 경계 구현을 사용하는 경우 해당 제어 메커니즘을 사용하여 동일한 정책을 설정해야 합니다.
  
* **아웃바운드 트래픽 액세스:** CFEE에서는 공용 엔드포인트가 있는 IBM Cloud의 여러 서비스를 사용합니다. 사용자의 격리된 네트워크에서 CFEE 인스턴스가 이 엔드포인트에 연결할 수 있어야 합니다. 해당 엔드포인트는 각 Calico 정책과 함께 아래 나열되어 있습니다.

| 규칙 |설명 | 엔드포인트 |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | CFEE 관리 플레인에 대한 아웃바운드 액세스 허용 | 169.46.2.150/32, 169.47.104.126/32,     161.156.68.46/32, 130.198.90.238/32, 169.46.66.254/32, 169.46.186.113/32, 161.156.66.118/32, 130.198.90.238/32|
| cfee-egress-allow-docker | Docker 레지스트리에 대한 아웃바운드 액세스 허용 | `registry-1.docker.io`, `docker.io`, `production.cloudflare.docker.com`|
| cfee-egress-allow-iks | CFEE Kubernetes 클러스터 관리 플레인에 대한 아웃바운드 액세스 허용 | [자세히 보기](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | CFEE의 Kubernetes 클러스터 휴대용 IP 주소에 대한 아웃바운드 액세스 및 라우팅 허용 | 다음을 사용하여 클러스터 휴대용 주소를 찾을 수 있습니다. `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | CFEE의 Compose for PostgreSQL 데이터베이스에 대한 아웃바운드 액세스 허용 |Compose 인스턴스 `<cfee-name>-postgress`의 대시보드 페이지 및 CFEE의 _Private Access_ 페이지에서 엔드포인트를 찾을 수 있습니다. |
| cfee-egress-allow-rc | 서비스 신디케이션을 사용하도록 IBM Cloud 플랫폼에 대한 아웃바운드 액세스 허용 | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | IBM Cloud Container Registry에 대한 아웃바운드 액세스 허용 | [자세히 보기](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (선택사항) CFEE 작업자 노드에서 IBM Cloud Monitoring 및 IBM Cloud Analysis 서비스로의 아웃바운드 네트워크 트래픽 허용 | [자세히 보기](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | CFEE 작업자 노드에서 helm 이미지 레지스트리로의 아웃바운드 네트워크 트래픽 허용 | 이 calico 규칙은 helm tiller 이미지를 가져오기 위해 `mage:gcr.io` 및 `storage.googleapis.com` 도메인에 액세스해야 하는 Helm tiller의 IP용입니다. |

<br>  
최종 네트워크 보안 규칙(가장 **중요한** 규칙)은 이전 정책과 일치하지 않는 네트워크 트래픽에 대한 모든 액세스를 거부하는 규칙입니다. 
<br>
**모든 아웃바운드 액세스를 거부**(`cfee-egress-deny-all`)하는 Calico 규칙:

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
**모든 인바운드 액세스를 거부**하는 Calico 규칙(`cfee-ingress-deny-all')
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
격리된 네트워크로부터의 아웃바운드 액세스가 있으면 일부 대상 엔드포인트가 _공용 에지_ 네트워크(예: Cloudflare 또는 Akamai) 뒤에 있다는 복잡도가 있습니다. 이 경우 자주 변경되는 수백 개의 IP 주소에 대한 액세스를 잠재적으로 허용해야 합니다. 다음 Calico 규칙(`cfee-egress-allow-all`)을 사용하여 **모든 아웃바운드 액세스를 허용**함으로써 선택적으로 이 상황을 방지할 수 있습니다.

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
  
위의 예에서 CFEE 클러스터 작업자 노드(“worker_public”)에서 오는 모든 HTTP 및 HTTPS 호출(포트 443과 80의 모든 TCP 트래픽)은 공용 네트워크의 허용된 아웃바운드(“출력”) 액세스입니다.

## 관리 제어 플레인에서 사설 액세스
{: #private-access}

격리된 네트워크에서 CFEE 인스턴스를 관리하려면 CFEE 관리 제어 플레인에 CFEE 인스턴스에 대한 사설 액세스 권한이 필요합니다. CFEE 관리 제어 플레인에서 CFEE 인스턴스에 사설 액세스하는 기능은 기본적으로 사용됩니다. 

_관리_ 역할이 있는 사용자가 CFEE 관리 제어 플레인의 사설 액세스 기능을 사용 안함으로 설정할 수 있습니다. 사설 액세스를 사용 안함으로 설정하면 CFEE 제어 플레인이 데이터를 검색하고 CFEE 인스턴스를 관리할 수 없습니다(사용자 인터페이스, CLI 및 API 모두 사용 불가). CFEE 관리자는 CFEE 사용자 인터페이스에 있는 **사설 액세스** 페이지(관리자에게만 표시)에서 사설 액세스를 사용 안함으로 설정할 수 있습니다. 이 페이지에서 **사용 안함**을 누르십시오.  

격리된 네트워크에 액세스는 API 키를 통해 수행합니다. API 키는 기본적으로 제공됩니다. CFEE 관리자는 기본 API키를 사용자 정의 키로 대체할 수 있습니다. 사설 액세스를 사용 안함으로 설정한 후 사용으로 설정하려면 *_IBM Cloud API 키_*에서 생성되어야 하는 API 키가 필요합니다(IBM Cloud 사용자 인터페이스 헤더에서 _관리 > 액세스(IAM) > IBM Cloud API 키_로 이동).

