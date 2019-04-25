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

# 환경 작성
{: #create-environment}

## 전제조건
* 환경을 작성하려는 {{site.data.keyword.Bluemix_notm}} 계정에 있는지 확인하십시오.
* {{site.data.keyword.cfee_full_notm}}의 인스턴스를 작성하기 전에 올바른 [권한](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html)이 있는지 확인하십시오. 
* CFEE 인스턴스에 필요한 인프라 리소스를 작성할 수 있도록(CFEE 인스턴스는 Kubernetes 서비스에서 Kubernetes 작업자 노드에 배치됨) [IBM Cloud 계정을 준비](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)하십시오.  

## CFEE 인스턴스 작성
1.  {{site.data.keyword.Bluemix_notm}} [카탈로그](https://cloud.ibm.com/catalog)를 여십시오.

2.  카탈로그에서 {{site.data.keyword.cfee_full_notm}} 서비스를 찾아 클릭하여 서비스에 대한 개요 페이지를 여십시오.  첫 번째 페이지에는 서비스의 기본 기능에 관한 개요가 제공됩니다. **계속**을 클릭하십시오.

3.  작성할 CFEE 인스턴스를 구성하십시오.
    * 플랜을 선택하십시오. 플랜의 제한사항에 관한 설명을 보려면 [Eirini 기술 미리보기](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini) 섹션을 참조하십시오.
    * CFFE 인스턴스의 **이름**을 입력하십시오.
    * 환경이 그룹화되는 **리소스 그룹**을 선택하십시오. 현재 IBM Cloud 계정에서 액세스할 수 있는 리소스 그룹만 _리소스 그룹_ 드롭 다운에 나열되며, 이는 계정에 하나 이상의 리소스 그룹에 액세스할 수 있는 권한이 있어야 CFEE를 작성할 수 있음을 의미합니다.
    * 서비스 인스턴스가 프로비저닝될 **지역**과 **위치**를 선택하십시오. CFEE 및 지원 서비스에 대해 지역별로 [사용 가능한 프로비저닝 위치 및 데이터 센터](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")의 목록을 보십시오. 

4. CFEE 인스턴스는 Kubernetes 클러스터에 프로비저닝됩니다. Cloud Foundry 셀은 Kubernetes 클러스터의 작업자 영역에서 프로비저닝됩니다. 클러스터의 위치, 하드웨어 및 암호화를 구성할 수 있습니다.
    * Kubernetes 클러스터의 하드웨어 격리를 선택하십시오.   
      * _Virtual-shared_: 하이퍼바이저 및 실제 하드웨어와 같은 클러스터의 인프라 리소스는 사용자와 기타 IBM 고객 간에 분배되지만 각 작업자 노드는 단일 테넌트에 있습니다.
      * _Virtual-dedicated_: 클러스터의 작업자 노드가 계정 전용인 인프라에서 호스팅됩니다.
    * 클러스터의 데이터는 기본적으로 암호화됩니다. _로컬 디스크 암호화_를 끄는 옵션이 있습니다.
    * Kubernetes 클러스터가 프로비저닝될 **지리** 및 **지역**을 선택하십시오.
    * Kubernetes 작업자 노드가 배치될 **구역**을 선택하십시오. 동일한 구역(**단일 구역**) 또는 다중 구역(**다중 구역**)에 작업자 노드를 프로비저닝하는 옵션이 있습니다. 다중 구역 CFEE를 작성하려면 {{site.data.keyword.Bluemix_notm}} 계정에 [VRF가 사용](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud)된 경우에도 지원되는 [VLAN Spanning](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning)이 필요하다는 점을 **참고**하십시오.
    
    선택한 구역에서 사용 가능한 VLAN을 자동으로 검색합니다. 사용 가능한 VLAN이 없으면 자동으로 작성됩니다.
    
    **참고: 격리된 네트워크에서 프로비저닝:** 격리된 네트워크의 VLAN을 대상으로 지정할 수 있습니다. 격리된 네트워크에 CFEE 인스턴스를 작성할 때 CFEE가 제대로 프로비저닝되려면 격리된 네트워크의 정책(예: Calico 정책 또는 VRA 규칙)에서는 CFEE 인스턴스에서 모든 아웃바운드 액세스가 가능하도록 허용해야 합니다. CFEE가 작성되고 나면 아웃바운드 액세스 제한사항을 복구할 수 있습니다. 단, IBM Cloud의 특정 서비스와 마이크로 서비스에 대한 아웃바운드 액세스는 제외입니다. 자세한 정보는 [격리된 네트워크에서 작동](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network) 문서를 참조하십시오.
    
    CFEE가 작서오디면 환경이 프로비저닝될 Kubernetes 클러스터가 {{site.data.keyword.Bluemix_notm}} [대시보드](https://https://cloud.ibm.com/catalog/dashboard/apps/)에 표시됩니다(IBM Cloud 계정의 다른 리소스와 마찬가지). 자세한 정보는 [Kubernetes 서비스 문서](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov)를 참조하십시오.

5.  다음과 같이 CFEE의 용량을 구성하십시오.
    * CFEE의 **셀 수**를 선택하십시오. CFEE에 배치된 애플리케이션을 호스팅할 애플리케이션 셀입니다.  
    * Cloud Foundry 셀(CPU 및 메모리)의 용량을 판별하는 **노드 크기**를 선택하십시오.
    
    위에서 지정한 애플리케이션 셀 외에도 추가 _제어 플레인 셀_이 작성되어 CFEE의 Cloud Foundry 플랫폼의 오퍼레이션 및 제어용으로 예약됩니다. 

    **참고:** Kubernetes 클러스터의 작업자 노드가 서로 다른 서브넷에서 프로비저닝되는 경우에는 VLAN Spanning을 사용하도록 권장합니다.  VLAN Spanning을 사용하지 않으면 서로 다른 서브넷의 작업자 노드가 이들 간의 연결을 차단할 수 있습니다.  자세한 정보는 [VLAN Spanning](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning) 문서를 참조하십시오.

6.  **Compose for PostgreSQL** 필드에서 퍼블릭 조직 중 하나를 선택한 후에 해당 조직에서 사용 가능한 영역 중 하나를 선택하십시오. Compose for PostgreSQL 인스턴스의 인스턴스가 선택된 영역에서 프로비저닝됩니다. Compose for PostgreSQL 서비스는 CFEE 서비스의 필수 종속 항목입니다.

    **참고:** _Compose for PostgreSQL_에서는 액세스 권한을 보유 중이며 CFEE 인스턴스를 프로비저닝(위의 4단계)하고자 하는 위치의 조직만 선택할 수 있습니다.  특정 조직 내에서 _개발자_ 액세스 권한이 있는 영역만 선택할 수 있습니다. 

7.  페이지 오른쪽의 **주문 요약**은 월별 추정 총계와 함께 CFEE 인스턴스 및 보조 서비스의 비용을 반영합니다.

8.  **작성**을 클릭하면 환경 대시보드가 열리고 작성 진행상태 및 상태가 표시됩니다.

**참고:** 작성 프로세스가 시작되면 CFEE의 테이블 행이 {{site.data.keyword.Bluemix_notm}} 대시보드, _리소스 목록_ 및 [Cloud Foundry 환경 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments)에 표시됩니다.  테이블 행의 상태는 작성이 완료된 시기를 나타냅니다.

환경을 작성하는 자동화된 프로세스가 Kubernetes 클러스터에 인프라를 배치하여 사용할 준비가 되도록 구성합니다. 이 프로세스에는 90 - 120분이 걸립니다.

CFEE가 작성되면 해당되는 주문의 상태를 알려주는 이메일은 물론 CFEE의 프로비저닝을 확인하고 서비스를 지원하는 다수의 이메일을 받습니다.

CFEE 인스턴스를 작성하면 동일한 IBM Cloud 계정에 작성된 추가 지원 서비스 인스턴스가 3개 있습니다. 이 지원 서비스 인스턴스는 CFEE 인스턴스 이름을 따서 명명합니다. 따라서 CFEE를 작성하면 IBM Cloud 계정에 작성된 서비스 인스턴스가 총 4개가 됩니다.
* CFEE 인스턴스("_cfeename_").
* Kubernetes 클러스터("_cfeename_-cluster"). 클러스터에서는 CFEE 인스턴스가 프로비저닝될 인프라를 제공합니다.
* Cloud Object Storage 인스턴스("_cfeename_-cos"). 이 인스턴스는 CFEE 애플리케이션 컨테이너(예: 업로드된 애플리케이션 패키지, 빌드팩 및 컴파일된 실행 파일) 작성 중에 생성된 데이터를 저장하는 데 사용됩니다.
* Compose for PosgreSQL 인스턴스("_cfeename_-postgres"). 이 인스턴스는 CFEE 인스턴스의 Cloud Foundry 데이터를 저장하는 데 사용됩니다(예: 애플리케이션 배치 감사, 이벤트 시작 및 중지, CFEE 사용자 멤버십, 조직, 영역, 애플리케이션 및 서비스 연결의 레코드 유지). 

## Eirini 기술 미리보기 플랜
{: #eirini}

 Eirini 기술 미리보기 플랜을 사용하면 기본 Kubernetes를 컨테이너 스케줄러(Diego 대신)로 사용하여 CFEE를 탐색할 수 있습니다. Kubernetes 스케줄러는 Cloud Foundry 애플리케이션 런타임에서 앱을 배치하고 실행하며 사용자를 추가하고 조직과 영역을 작성하고 앱을 배치하며 해당 앱을 서비스에 바인드하가 위해 CFEE에서 사용합니다. Cloud Foundry Foundation의 Eirini 인큐베이터 프로젝트에 관한 자세한 정보는 [Eirini 프로젝트](https://www.cloudfoundry.org/project-eirini/) 문서를 참조하십시오.
 다음 제한사항은 Eirini 기술 미리보기 플랜에서 작성된 CFEE 인스턴스에 적용됩니다.
 
* `containerd`가 있는 Kubernetes는 지원되지 않습니다. `containerd`가 아니라 Docker를 사용하는 Kubernetes 버전만 지원됩니다. Docker를 지원하는 IKS(IBM Container Service)의 최신 버전은 v1.10입니다.
* Cloud Foundry SSH는 지원되지 않습니다.
* Docker 이미지의 `cf push`는 지원되지 않습니다.
* Kubernetes 기본 Eirini 스테이징은 지원되지 않습니다. Eirini 기술 미리보기 플랜에서 작성된 CFEE 인스턴스에서는 앱을 스테이징하는 것이 아니라 앱을 실행하는 데 Eirini를 사용합니다. Diego 셀은 앱을 스테이징하는 데 여전히 사용합니다.
* 특정 앱 인스턴스(`cf restart-app-instance`) 다시 시작은 지원되지 않습니다.

 
