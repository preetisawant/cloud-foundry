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

# FAQ
{: #cfeefaq}

## IBM Cloud Foundry Enterprise Environment(CFEE)와 퍼블릭 Cloud Foundry의 차이점은 무엇입니까?
{: #cfee_diff}

{{site.data.keyword.cloud}} Foundry 퍼블릭을 사용하여 단순 설정, 강력한 스케일링 및 트래픽 관리를 위해 Cloud Foundry를 사용하는 클라우드 고유 애플리케이션을 실행할 수 있습니다. 또한 모든 {{site.data.keyword.cloud}} 서비스에 쉽게 액세스할 수 있습니다. 

Cloud Foundry 퍼블릭을 사용하는 것처럼 엔터프라이즈 전용 Cloud Foundry 애플리케이션을 호스팅하기 위한 격리된 환경을 작성하고 관리하는 데뿐만 아니라 전체에 대해 {{site.data.keyword.cfee_full}}를 사용할 수 있습니다. 


## 새 오퍼링은 이전 IBM Cloud Foundry 오퍼링과 어떻게 다릅니까?
{: #cfOfferings_diff}

퍼블릭 멀티 테넌트에 대하여, 가장 주목할 만한 차이점은 격리 특성입니다. IBM Cloud 인프라의 기존 단일 테넌트 오퍼링에 대하여 두 가지 주요 차이점은 인프라 설치 공간(및 비용)의 감소와 단일 테넌트 환경으로의 서비스 통합 모델입니다. 

## CFEE 서비스를 어디에서 찾을 수 있습니까?
{: #where}

{{site.data.keyword.Bluemix_notm}} [카탈로그](https://console.stage1.bluemix.net/catalog)에서 {{site.data.keyword.cfee_full}} 서비스를 찾고 인스턴스화할 수 있습니다. 

## 지역 데이터 센터 내에 두 개 이상의 CFEE 환경을 포함할 수 있습니까?
{: #multiple-cfees}

예, 요청 시 CFEE 인스턴스를 원하는 만큼 [이러한 지역](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에 작성할 수 있습니다.

## 일부 최소 용량에서 시작해야 합니까? 
{: #minimum-capacity}

예. CFEE 인스턴스를 작성하려면 최소 두 개의 Cloud Foundry 셀이 필요하며, 각각 16GB RAM의 4개 코어, 25GB SSD 기본 디스크, 100GB SSD 보조 디스크 및 1000Mbps 네트워크 속도가 필요합니다. 

## CFEE가 배치되는 기본 IaaS는 무엇입니까?
{: #why-kubs}

CFEE 서비스는 Kubernetes 컨테이너에서 실행되며 Kubernetes는 여러 오퍼레이션 활동을 자동화하는 매우 스마트한 IaaS이므로 이를 통해 낮은 인프라 비용과 보다 효율적인 운영이 가능합니다.  

## CFEE를 작성할 때 내 격리 옵션은 무엇입니까?
{: #isolation}

CFEE가 배치되는 Kubernetes 인프라의 유형에 대해 _가상 공유_ 또는 _가상 전용_ 하드웨어라는 두 가지 하드웨어 옵션을 갖습니다. _가상 공유_ 하드웨어를 사용하면, (Cloud Foundry 플랫폼 컨테이너가 배치되는) 작업자 노드가 사용자와 다른 IBM 고객 간에 분배됩니다. _가상 전용_을 사용하면, 사용자 계정 전용인 하드웨어에 작업자 노드가 호스팅됩니다. 두 경우 모두(_가상 공유_ 및 _가상 전용_) 각 작업자 노드는 고객에 대한 단일 테넌트입니다. 이는 애플리케이션이 실행되는 Cloud Foundry 셀은 다른 고객과 공유되지 않음을 의미합니다. 

## CFEE의 용량을 스케일링할 수 있습니까?
{: #scaling}

예, Cloud Foundry 셀을 추가하거나 제거하여 요구사항이 변경되는 대로 CFEE의 용량을 늘리거나 줄일 수 있습니다. 

## 내 CFEE를 새 버전으로 업그레이드할 수 있습니까? 어떻게 작동합니까?
{: #upgrading}
예. CFEE 사용자 인터페이스에서 새 CFEE 버전이 사용 가능한 경우 사용자에게 알림을 전송합니다. 새 버전으로 업데이트할 시기를 조정합니다. CFEE 버전 업데이트는 사용자 인터페이스에서 CFEE 관리자에 의해 호출됩니다. CFEE 버전 업데이트는 해당 컴포넌트 또는 지원 서비스의 새 버전을 패키징할 수 있습니다(예: Cloud Foundry, Kubernetes 등). 먼저 CFEE 제어 플레인을 업데이트한 후 Cloud Foundry 셀을 업데이트합니다. 업데이트 프로세스는 중단을 최소화하도록 최적화됩니다. 

## CFEE 인스턴스를 작성하려면 어떻게 해야 합니까?
{: #create}

{{site.data.keyword.Bluemix_notm}} 카탈로그에 나열된 CFEE 서비스를 찾을 수 있습니다. 업그레이드된 {{site.data.keyword.Bluemix_notm}} 계정이 있어야 하며 CFEE 서비스 및 지원되는 서비스에 대한 권한이 있어야 합니다(Kubernetes, Cloud Object Storage 및 Compose for PostgreSQL). 이러한 권한을 보유하면, 환경의 이름을 제공하고 _작성_을 클릭하십시오. 작성하는 데에는 약 90분이 소요됩니다. 

## 내 CFEE에서 {{site.data.keyword.Bluemix_notm}} 서비스를 사용할 수 있습니까?
{: #Services-ibmcloud}

물론입니다! {{site.data.keyword.Bluemix_notm}}에 통합되면, CFEE의 개발자는 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 작성하고(또는 기존 인스턴스를 사용하고) CFEE 영역에 배치된 애플리케이션에 인스턴스를 바인드할 수 있습니다. 

## 내 CFEE에 내 고유 서비스를 포함할 수 있습니까? 
{: #Services-ibmcloud}

예. 관리자는 서비스 브로커를 CFEE에 등록하여 해당 CFEE의 사용자들이 사용자 정의 서비스 플랜을 사용하도록 할 수 있습니다. 로컬 MCFEE 마켓플레이스에는 {{site.data.keyword.Bluemix_notm}} 카탈로그의 서비스 및 CFEE의 로컬 서비스 브로커가 관리하는 고객 서비스가 포함됩니다. 

## CFEE에 대한 사용자 액세스를 어떻게 제어합니까?
{: #Services}

다른 {{site.data.keyword.Bluemix_notm}} 서비스와 마찬가지로, CFEE에 대한 액세스는 _Identity & Access Management_(IAM)를 통해 제어됩니다. (개별적으로 또는 액세스 그룹을 통해) 특정 역할을 가진 사용자 액세스 정책을 지정하면 CFEE에 대한 특정 레벨의 액세스를 제공합니다. CFEE 서비스에 대한 액세스 외에, CFEE의 Cloud Foundry 조직 및 영역에 대한 액세스는 Cloud Foundry 멤버십 및 특정 조직 및 영역의 사용자에게 지정된 역할을 통해 제어됩니다. 

