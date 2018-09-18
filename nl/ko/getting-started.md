---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 시작하기 튜토리얼
{: #getting-started}

{{site.data.keyword.cfee_full}}는 클라우드에서 앱 및 서비스를 호스팅하기 위한 클라우드 플랫폼입니다. {{site.data.keyword.cfee_full_notm}}를 사용하면 앱을 개발하는 데 집중할 수 있도록 런타임, 미들웨어 및 인프라를 단순화하여 이용이 증가할 때 앱을 쉽게 스케일링할 수 있습니다.
{: shortdesc}

이 시작하기 튜토리얼은 {{site.data.keyword.cfee_full_notm}}를 작성하고, 사용자를 추가하고, 조직 및 영역을 작성하고, 앱을 배치하고, 해당 앱을 서비스에 바인드하는 방법을 보여줍니다.

## 권한 이해
{: #permissions}

{{site.data.keyword.cfee_full_notm}}의 인스턴스에 대해 작업하려면 서비스 사용자에게 올바른 권한이 있어야 합니다. 자세한 정보는 [권한](/docs/cloud-foundry/permissions.html)을 참조하십시오.

## 1단계: {{site.data.keyword.Bluemix_notm}} 계정이 인프라 리소스를 작성할 수 있는지 확인
{: #accountprep-environment}

CFEE 인스턴스는 IBM Container 서비스의 Kubernetes 작업자 노드인 인프라 리소스에 배치됩니다. CFEE 인스턴스에 필요한 인프라 리소스를 작성할 수 있도록 [IBM Cloud 계정](/docs/cloud-foundry/prepare-account.html)을 준비하십시오.

## 2단계: CFEE 인스턴스 작성
{: #creating-environment}

CFEE를 작성하기 전에 환경을 작성할 {{site.data.keyword.Bluemix_notm}} IBM Cloud 계정에 있는지와 필수 액세스 정책(위의 1단계에 따라)이 있는지 확인하십시오.

1. {{site.data.keyword.Bluemix_notm}} [카탈로그](https://console.bluemix.net/catalog)를 여십시오.
2. 카탈로그에서 {{site.data.keyword.cfee_full_notm}} 서비스를 찾아 클릭하여 서비스에 대한 개요 페이지를 여십시오.
3. 작성 페이지의 첫 번째 페이지에는 서비스의 기본 기능에 대한 개요가 제공됩니다. **계속**을 클릭하십시오.
4. 다음을 제공하여 작성될 인스턴스를 구성하십시오.
    * 플랜(베타 중에 플랜 가용성이 제한될 수 있음)을 선택하십시오.
    * 서비스 인스턴스의 **이름**을 입력하십시오.
    * 서비스 인스턴스가 프로비저닝될 **위치**를 선택하십시오.
    * Cloud Foundry 환경에 대한 **셀 수**를 선택하십시오.
    * Cloud Foundry 셀(CPU 및 메모리)의 크기를 판별하는 **머신 유형**을 선택하십시오.
    * 환경이 그룹화되는 **리소스 그룹**을 선택하십시오. 현재 IBM Cloud 계정에서 액세스할 수 있는 리소스 그룹만 _리소스 그룹_ 드롭 다운에 나열되며, 이는 계정에 하나 이상의 리소스 그룹에 액세스할 수 있는 권한이 있어야 CFEE를 작성할 수 있음을 의미합니다.
5. 선택적으로 **인프라** 섹션을 열어 CFEE를 지원하는 Kubernetes 클러스터의 특성을 확인하십시오. **작업자 노드 수**는 셀의 수에 2(프로비저닝된 Kubernetes 작업자 노드 중 2개가 CFEE 제어 플레인을 지원함)를 더한 값과 같습니다.
6. 페이지의 오른쪽에 있는 **주문 요약**은 CFEE 인스턴스의 비용과 예상 총계를 반영합니다.
7. **작성**을 클릭하면 환경 대시보드가 열리고 작성 진행상태 및 상태가 표시됩니다.
8. 프로비저닝이 시작되면 환경이 {{site.data.keyword.Bluemix_notm}} 대시보드와 [Cloud Foundry Environment 대시보드](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments)에 표시됩니다. 프로비저닝이 완료되면 상태가 표시됩니다.

환경을 작성하는 자동화된 프로세스가 Kubernetes 클러스터에 인프라를 배치하여 사용할 준비가 되도록 구성합니다. 이 프로세스에는 90 - 120분이 걸립니다.

**참고:** 환경이 배치된 Kubernetes 클러스터가 {{site.data.keyword.Bluemix_notm}} [대시보드](https://console.bluemix.net/dashboard/apps/)에 표시됩니다. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} Container Service 문서](/docs/containers/cs_why.html#cs_ov)를 참조하십시오.

## 3단계: 조직 및 영역 작성

{{site.data.keyword.cfee_full_notm}}를 작성한 후 조직 및 영역을 작성하여 환경을 구조화하는 방법에 대한 정보는 [조직 및 영역 작성](/docs/cloud-foundry/orgs-spaces.html)을 참조하십시오. {{site.data.keyword.cfee_full_notm}}의 앱은 특정 범위 내로 범위가 지정됩니다. 결국 영역이 특정 조직 내에 존재합니다. 조직의 구성원이 할당량 플랜, 앱, 서비스 인스턴스 및 사용자 정의 도메인을 공유합니다. 

**참고:** 상단 IBM Cloud 헤더에 있는 **_관리 > 계정 > Cloud Foundry 조직_** 메뉴에서 사용 가능한 _Cloud Foundry 조직_ 페이지는 **CFEE 조직이 아니라** 퍼블릭 IBM Cloud 조직에만 사용됩니다. CFEE 조직은 CFEE 인스턴스의 _조직_ 페이지 내에서 관리됩니다. CFEE 사용자 인터페이스를 열고 **_조직_** 페이지를 클릭하여 해당 CFEE에 대한 조직을 작성하고 관리하십시오.

## 4단계: 조직 및 영역에 사용자 추가

액세스 레벨을 제어하는 특정 역할 지정에 따라 해당 조직 및 영역에 [사용자를 추가](/docs/cloud-foundry/add-users.html)하십시오. CFEE에서 사용자를 조직 및 영역의 구성원으로 추가하려면 해당 사용자에게 CFEE 인스턴스에 대한 사전 액세스 권한이 있어야 합니다. [권한](/docs/cloud-foundry/permissions.html)을 참조하십시오.

## 5단계: 애플리케이션 배치 및 보기

준비가 되면 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 사용하여 [앱을 배치](/docs/cloud-foundry/deploy-apps.html)할 수 있습니다. 특정 CFEE 영역의 컨텍스트에서 또는 모든 CFEE 인스턴스에서 글로벌로 사용자 인터페이스에서 배치된 애플리케이션의 목록을 보십시오. 해당 보기에서 애플리케이션을 시작, 중지 또는 삭제할 수도 있습니다.

## 6단계: 서비스 인스턴스 및 별명 작성

CFEE 애플리케이션에서 활용할 수 있도록 IBM Cloud 계정에 사용 가능한 서비스 인스턴스에서 [서비스 별명](/docs/cloud-foundry/add-serv-inst.html)을 작성하십시오.

## 7단계: 서비스 인스턴스에 애플리케이션 바인드

서비스의 기능을 사용하기 위해 서비스 인스턴스 별명에 [앱을 바인드](/docs/cloud-foundry/binding.html)하십시오.

## 8단계: 애플리케이션을 관리하기 위해 Stratos Console 설치(선택사항)

Stratos Console은 Cloud Foundry에 대해 작업하기 위한 오픈 소스 웹 기반 도구입니다. 특정 CFEE 환경에서 해당 조직, 영역 및 애플리케이션을 관리하기 위해 선택적으로 Stratos Console 애플리케이션을 설치하여 사용할 수 있습니다.

CFEE 인스턴스에서 IBM Cloud 관리자 또는 편집자 역할이 있는 사용자가 해당 CFEE 인스턴스에 Stratos Console 애플리케이션을 설치할 수 있습니다.

Stratos Console 애플리케이션을 설치하려면 다음을 수행하십시오.

1. Stratos Console을 설치할 CFEE 인스턴스를 여십시오.
2. 개요 페이지에서 **Stratos Console 설치**를 클릭하십시오. 이 단추는 해당 CFEE 인스턴스에 대한 관리자 또는 편집자 권한이 있는 사용자에게만 표시됩니다.
3. Stratos Console 설치 대화 상자에서 설치 옵션을 선택하십시오. CFEE 제어 플레인 또는 셀 중 하나에 Stratos Console 애플리케이션을 설치할 수 있습니다. Stratos Console의 버전과 설치할 애플리케이션의 인스턴스 수를 선택하십시오. 셀에 Stratos Console 앱을 설치하는 경우 애플리케이션을 배치할 조직 및 영역에 대한 프롬프트가 표시됩니다.
4. **설치**를 클릭하십시오.

애플리케이션을 설치하는 데 약 5분이 걸립니다. 설치가 완료되면 개요 페이지에 _Stratos Console 설치_ 단추 대신에 **Stratos Console** 단추가 표시됩니다. _Stratos Console_ 단추는 콘솔을 실행하며 CFEE 인스턴스에 대한 액세스 권한이 있는 모든 사용자가 사용할 수 있습니다. 조직 및 영역 멤버십 지정은 사용자가 Stratos Console에서 보고 관리할 수 있는 항목을 제한할 수 있습니다.

Stratos Console을 시작하려면 다음을 수행하십시오.

1. Stratos Console이 설치된 CFEE 인스턴스를 여십시오.
2. 개요 페이지에서 **Stratos Console**을 클릭하십시오.
3. Stratos Console이 별도의 브라우저 탭에 열립니다. 처음으로 콘솔을 열면 자체 서명된 인증서로 인해 두 개의 연속 경고를 승인하라는 프롬프트가 표시됩니다.
4. **로그인**을 클릭하여 콘솔을 여십시오. 애플리케이션에서 {{site.data.keyword.Bluemix_notm}} 신임 정보를 사용하므로 신임 정보가 필요하지 않습니다.

보고 관리할 수 있는 항목은 조직 및 영역 멤버십과 역할에 따라 제한됩니다.
