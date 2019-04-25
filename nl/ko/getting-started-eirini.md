---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Eirini 기술 미리보기 시작하기
{: #getting-started-eirini}

{{site.data.keyword.cfee_full}}(CFEE)는 클라우드에서 앱 및 서비스를 호스팅하기 위한 클라우드 플랫폼입니다. {{site.data.keyword.cfee_full_notm}}를 사용하면 앱을 개발하는 데 집중할 수 있도록 런타임, 미들웨어 및 인프라를 단순화하여 이용이 증가할 때 앱을 쉽게 스케일링할 수 있습니다.
{: shortdesc}

이 시작하기 튜토리얼은 Eirini 기술 미리보기 플랜에서 {{site.data.keyword.cfee_full_notm}}를 작성하고, 사용자를 추가하고, 조직 및 영역을 작성하고, 앱을 배치하고, 해당 앱을 서비스에 바인드하는 방법을 보여줍니다. Cloud Foundry Foundation의 Eirini 인큐베이터 프로젝트에 관한 정보는 [Eirini 프로젝트](https://www.cloudfoundry.org/project-eirini/)를 참조하십시오.
 

## 권한 이해
{: #permissions}

{{site.data.keyword.cfee_full_notm}}의 인스턴스를 작성하기 전에 올바른 액세스 정책이 있어야 합니다. 자세한 정보는 [권한](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)을 참조하십시오.

## 1단계: {{site.data.keyword.Bluemix_notm}} 계정이 인프라 리소스를 작성할 수 있는지 확인
{: #accountprep-environment}

CFEE 인스턴스는 Kubernetes 서비스의 Kubernetes 작업자 노드에 배치됩니다.  CFEE 인스턴스에 필요한 인프라 리소스를 작성할 수 있도록 [IBM Cloud 계정](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)을 준비하십시오.

## 2단계: CFEE 인스턴스 작성
{: #create-environment}

CFEE를 작성하려면 우선 환경을 작성할 {{site.data.keyword.Bluemix_notm}} 계정에 있는지와 필수 액세스 정책이 있는지 확인하십시오(위의 1단계).

1.  {{site.data.keyword.Bluemix_notm}} [카탈로그](https://cloud.ibm.com/catalog)를 여십시오.

2.  카탈로그에서 {{site.data.keyword.cfee_full_notm}} 서비스를 찾아 클릭하여 서비스에 대한 개요 페이지를 여십시오.  첫 번째 페이지에는 서비스의 기본 기능에 관한 개요가 제공됩니다. **계속**을 클릭하십시오.

3.  작성할 CFEE 인스턴스를 구성하십시오.
    * _Eirini 기술 미리보기_ 플랜을 선택하십시오.
    * CFFE 인스턴스의 **이름**을 입력하십시오.
    * 환경이 그룹화되는 **리소스 그룹**을 선택하십시오. 현재 IBM Cloud 계정에서 액세스할 수 있는 리소스 그룹만 _리소스 그룹_ 드롭 다운에 나열되며, 이는 계정에 하나 이상의 리소스 그룹에 액세스할 수 있는 권한이 있어야 CFEE를 작성할 수 있음을 의미합니다.
    * 서비스 인스턴스가 프로비저닝될 **지역**과 **위치**를 선택하십시오. CFEE 및 지원 서비스에 대해 지역별로 [사용 가능한 프로비저닝 위치 및 데이터 센터](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")의 목록을 보십시오. 

4. CFEE 인스턴스는 Kubernetes 클러스터에 프로비저닝됩니다. Cloud Foundry 셀은 Kubernetes 클러스터의 작업자 영역에서 프로비저닝됩니다. 클러스터의 위치, 하드웨어 및 암호화를 구성할 수 있습니다.
    * Kubernetes 클러스터의 하드웨어 격리를 선택하십시오.   
      * _Virtual-shared_: 하이퍼바이저 및 실제 하드웨어와 같은 클러스터의 인프라 리소스는 사용자와 기타 IBM 고객 간에 분배되지만 각 작업자 노드는 단일 테넌트에 있습니다.
      * _Virtual-dedicated_: 클러스터의 작업자 노드가 계정 전용인 인프라에서 호스팅됩니다.
    * 클러스터의 데이터는 기본적으로 암호화됩니다. _로컬 디스크 암호화_를 끄는 옵션이 있습니다.
    * Kubernetes 클러스터가 프로비저닝될 **지리** 및 **지역**을 선택하십시오.
    * Kubernetes 작업자 노드가 배치될 **구역**을 선택하십시오. 선택한 구역에서 사용 가능한 VLAN을 자동으로 검색합니다. 사용 가능한 VLAN이 없으면 자동으로 작성됩니다. CFEE v2.2.0부터 CFEE 인스턴스는 **격리된 네트워크** 뒤에서 작동할 수 있습니다. 격리된 네트워크에서 사설 VLAN을 선택하여 CFEE 인스턴스를 격리된 네트워크로 프로비저닝할 수 있습니다. CFEE가 작동하려면 CFEE를 작성한 다음 네트워크 관리자가 CFEE의 Compose for PostgreSQL 및 Cloudant Object Storage 인스턴스의 IP 주소 외에도 Kubernetes 클러스터의 [ALB](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress)(Application Load Balancer) IP 주소를 격리된 네트워크에서 라우팅해야 합니다.
    
    CFEE가 작성되면 환경이 프로비저닝될 Kubernetes 클러스터가 표시됩니다({{site.data.keyword.Bluemix_notm}} [대시보드](https://cloud.ibm.com/dashboard/apps/)에 표시됩니다(IBM Cloud 계정의 다른 리소스와 마찬가지). 자세한 정보는 [Kubernetes 서비스 문서](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov)를 참조하십시오.

5.  다음과 같이 CFEE의 용량을 구성하십시오.
    * CFEE의 **셀 수**를 선택하십시오. CFEE에 배치된 애플리케이션을 호스팅할 애플리케이션 셀입니다.  
    * Cloud Foundry 셀(CPU 및 메모리)의 용량을 판별하는 **노드 크기**를 선택하십시오.
    
    위에서 지정한 애플리케이션 셀 외에도 추가 _제어 플레인 셀_이 작성되어 CFEE의 Cloud Foundry 플랫폼의 오퍼레이션 및 제어용으로 예약됩니다. 

    **참고:** Kubernetes 클러스터의 작업자 노드가 서로 다른 서브넷에서 프로비저닝되는 경우에는 VLAN Spanning을 사용하도록 권장합니다.  VLAN Spanning을 사용하지 않으면 서로 다른 서브넷의 작업자 노드가 이들 간의 연결을 차단할 수 있습니다.  자세한 정보는 [VLAN Spanning](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning) 문서를 참조하십시오.
    
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

## 3단계: 조직 및 영역 작성
{: #create-orgsandspaces}

{{site.data.keyword.cfee_full_notm}}를 작성한 후 조직 및 영역을 작성하여 환경을 구조화하는 방법에 대한 정보는 [조직 및 영역 작성](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)을 참조하십시오. {{site.data.keyword.cfee_full_notm}}의 앱은 특정 범위 내로 범위가 지정됩니다. 결국 영역이 특정 조직 내에 존재합니다. 조직의 구성원이 할당량 플랜, 앱, 서비스 인스턴스 및 사용자 정의 도메인을 공유합니다.

조직을 작성할 때 조직에 할당량을 지정합니다. 할당량은 조직에서 사용 가능한 리소스(메모리, cpu 등)의 한계를 설정합니다. 나중에 다른 할당량을 지정할 수 있습니다. 모든 CFEE에는 사전 구성된 할당량 세트가 있지만, CFEE 사용자 인터페이스의 **할당량** 페이지에서 고유 사용자 정의 할당량도 작성할 수 있습니다. 할댱량 메뉴에서 사용자 정의 할당량 값을 기본 할당량으로 복사하는 _기본값에 복사_ 조치를 호출하여 사용자 정의 할당량을 _기본값_ 할당량으로 만들 수 있습니다.

**참고:** 상단 IBM Cloud 헤더에 있는 **_관리 > 계정 > Cloud Foundry 조직_** 메뉴에서 사용 가능한 _Cloud Foundry 조직_ 페이지는 **CFEE 조직이 아니라** 퍼블릭 IBM Cloud 조직에만 사용됩니다. CFEE 조직은 CFEE 인스턴스의 _조직_ 페이지 내에서 관리됩니다.  CFEE 사용자 인터페이스를 열고 **_조직_** 페이지를 클릭하여 해당 CFEE의 조직을 작성하고 관리할 수 있습니다.

## 4단계: 조직 및 영역에 사용자 추가
{: #add-users}

액세스 레벨을 제어하는 특정 역할 지정에 따라 해당 조직 및 영역에 [사용자를 추가](https://cloud.ibm.com/docs/cloud-foundry/add-users.html)하십시오.  CFEE에서 사용자를 조직 및 영역의 구성원으로 추가하려면 해당 사용자에게 CFEE 인스턴스에 대한 사전 액세스 권한이 있어야 합니다. [권한](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)을 참조하십시오.

## 5단계: 애플리케이션 배치 및 보기
{: #deploy-apps}

준비가 되면 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 사용하여 [앱을 배치](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)할 수 있습니다.  특정 CFEE 영역의 컨텍스트에서 또는 모든 CFEE 인스턴스에서 글로벌로 사용자 인터페이스에서 배치된 애플리케이션의 목록을 보십시오.  해당 보기에서 애플리케이션을 시작, 중지 또는 삭제할 수도 있습니다.

## 6단계: IBM Cloud 서비스 인스턴스 작성 또는 CFEE 영역에 추가
{: #service-instances}

[서비스를 작성](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)하거나 IBM Cloud 계정에서 사용 가능한 [기존 서비스를 추가](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)하십시오.  일단 서비스 인스턴스가 CFEE 영역에서 사용 가능하면 이를 해당 영역에 배치된 CFEE 애플리케이션에 바인드할 수 있습니다.

## 7단계: 서비스 인스턴스에 애플리케이션 바인드
{: #bind-apps}

서비스의 기능을 사용하기 위해 서비스 인스턴스 별명에 [앱을 바인드](https://console.bluemix.net/docs/cloud-foundry/binding.html)하십시오.

[Cloud Foundry 대시보드](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 모든 애플리케이션과 서비스의 통합 보기(*공용* 및 *엔터프라이즈*)를 볼 수 있습니다.  일단 Cloud Foundry 대시보드의 왼쪽 탐색 분할창에서 *퍼블릭*을 클릭하면 IBM Cloud 계정에서 사용 가능한 퍼블릭 애플리케이션과 서비스를 볼 수 있습니다.  *엔터프라이즈*를 클릭하면 모든 CFEE 환경, CFEE 영역에 배치된 애플리케이션, 그리고 CFEE 영역에 사용 가능한 서비스를 볼 수 있습니다.
{:tip}

## 8단계: 애플리케이션을 관리하기 위해 Stratos Console 설치(선택사항)
{: #install-stratos}

Stratos Console은 Cloud Foundry에 대해 작업하기 위한 오픈 소스 웹 기반 도구입니다. 특정 CFEE 환경에서 해당 조직, 영역 및 애플리케이션을 관리하기 위해 선택적으로 Stratos Console 애플리케이션을 설치하여 사용할 수 있습니다.

CFEE 인스턴스에서 IBM Cloud 관리자 또는 편집자 역할이 있는 사용자가 해당 CFEE 인스턴스에 Stratos Console 애플리케이션을 설치할 수 있습니다.

Stratos Console 애플리케이션을 설치하려면 다음을 수행하십시오.

1. Stratos Console을 설치할 CFEE 인스턴스를 여십시오.
2. 개요 페이지에서 **Stratos Console 설치**를 클릭하십시오. 이 단추는 해당 CFEE 인스턴스에 대한 관리자 또는 편집자 권한이 있는 사용자에게만 표시됩니다.
3. Stratos Console 설치 대화 상자에서 설치 옵션을 선택하십시오. Cloud Foundry 셀 또는 Kubernetes 클러스터에 Stratos 애플리케이션을 설치할 수 있습니다. Stratos Console의 버전과 설치할 애플리케이션의 인스턴스 수를 선택하십시오. Cloud Foundry 셀에 Stratos Console 앱을 설치하는 경우 애플리케이션을 배치할 조직 및 영역의 프롬프트가 표시됩니다.
4. **설치**를 클릭하십시오.

애플리케이션을 설치하는 데 약 5분이 걸립니다. 설치가 완료되면 개요 페이지에 _Stratos Console 설치_ 단추 대신에 **Stratos Console** 단추가 표시됩니다. _Stratos Console_ 단추는 콘솔을 실행하며 CFEE 인스턴스에 대한 액세스 권한이 있는 모든 사용자가 사용할 수 있습니다. 조직 및 영역 멤버십 지정은 사용자가 Stratos Console에서 보고 관리할 수 있는 항목을 제한할 수 있습니다.

Stratos Console을 시작하려면 다음을 수행하십시오.

1. Stratos Console이 설치된 CFEE 인스턴스를 여십시오.
2. 개요 페이지에서 **Stratos Console**을 클릭하십시오.
3. Stratos Console이 별도의 브라우저 탭에 열립니다. 처음으로 콘솔을 열면 자체 서명된 인증서로 인해 두 개의 연속 경고를 승인하라는 프롬프트가 표시됩니다.
4. **로그인**을 클릭하여 콘솔을 여십시오. 애플리케이션에서 {{site.data.keyword.Bluemix_notm}} 인증 정보를 사용하므로 인증 정보가 필요하지 않습니다.


## 추가 리소스
{: #additional-resources}

`ibmcloud CFEE` CLI 명령을 사용하여 CFEE에서 일부 관리 태스크를 수행할 수 있습니다. 이 명령을 통해 해당 조직 및 영역을 관리할 뿐만 아니라 CFEE 인스턴스에 대한 정보를 가져올 수 있습니다. [IBM Cloud CLI CFEE 명령 참조서](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오.

다양한 CFEE 주제에 대한 상세한 토론과 데모가 포함된 동영상은 [CFEE 동영상 재생 목록](https://ibm.biz/CFEE-Playlist){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 참조할 수 있습니다.

CFEE API 관련 정보는 CFEE [API 문서](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 사용 가능합니다.
