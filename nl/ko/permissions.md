---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2019-01-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 권한
{: #permissions}

사용자가 {{site.data.keyword.cfee_full}}(CFEE) 서비스를 작성하고 관련 작업을 시작하려면, 우선 CFEE 인스턴스가 작성되는 계정의 관리자를 통해 해당 권한을 올바르게 설정해야 합니다. 

## 권한 개요
{: #perm-summary}

다음에는 CFEE 인스턴스에서 다양한 태스크를 수행하는 데 필요한 최소 [IAM](https://cloud.ibm.com/iam#/users) 및 [Cloud Foundry 역할 지정](https://cloud.ibm.com/account/cloud-foundry)이 요약되어 있습니다. 나머지 절에서는 이 권한을 더 자세히 설명합니다.

|  **태스크** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|  **IAM 액세스 역할** &nbsp; &nbsp; &nbsp; |**Cloud Foundry 역할** &nbsp; &nbsp; &nbsp; |
|----------------------------------------|-------------------|-------------------|
|CFEE 작성 |  <ul><li>CFEE를 작성할 리소스 그룹의 뷰어 역할.</li> <li>CFEE 서비스의 편집자 역할.</li> <li>Kubernetes 서비스의 관리자 역할.</li> <li>Cloud Object Storage 서비스의 편집자 역할.</li> </ul> | <ul><li>공용 조직의 사용자 역할.</li> <li>공용 조직의 영역에 있는 개발자 역할. </li></ul>|
|CFEE 버전 업데이트 |  <ul><li>CFEE 리소스 그룹의 뷰어 역할.</li> <li>CFEE 서비스의 편집자 역할.</li></li> <li>Kubernetes 서비스의 운영자 역할.</li> <li>Cloud Object Storage 서비스의 편집자 역할.</li> </ul> | <ul><li>공용 조직의 사용자 역할.</li> <li>공용 조직의 영역에 있는 개발자 역할. </li></ul>|
|CFEE 용량 스케일링(셀 추가/제거)|  <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 관리자 역할.</li> <li>Kubernetes 서비스의 운영자 역할.</li> <li>Cloud Object Storage 서비스의 편집자 역할.</li> </ul> | |
|CFEE 모니터 |  <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 편집자 역할.</li></ul> |  |
|CFEE 리소스 사용량 보기 |  <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 뷰어 역할.</li></ul> |  |
|CFEE 감사 사용| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 편집자 역할.</li></ul> | <ul><li>활동 트래커 서비스 인스턴스가 배치된 공용 Cloud Foundry 영역의 감사자 역할.</li></ul>  |
|CFEE 감사 이벤트 보기| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 편집자 역할.</li></ul> | <ul><li>활동 트래커 서비스 인스턴스가 배치된 공용 Cloud Foundry 영역의 감사자 역할.</li></ul>  |
|CFEE 로그 지속성 사용| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 편집자 역할.</li></ul> |<ul><li>로그 분석 서비스 인스턴스가 배치된 공용 Cloud Foundry 영역의 감사자 역할.</li></ul>  |
|CFEE 지속 로그 보기| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 편집자 역할.</li></ul> | <ul><li>로그 분석 서비스 인스턴스가 배치된 공용 Cloud Foundry 영역의 감사자 역할.</li></ul> |
|CFEE 조직 작성| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 편집자 역할.</li></ul> |  |
|CFEE 영역 작성| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 뷰어 역할.</li></ul> | <ul><li>영역을 작성할 조직의 관리자.</li></ul> |
|공유 도메인 관리|<ul><li>CFEE 인스턴스 리소스 그룹의 뷰어. </li><li>CFEE 인스턴스의 편집자 역할. </li></ul>|  |
|공유 도메인 보기|<ul><li>CFEE 인스턴스 리소스 그룹의 뷰어. </li><li>CFEE 인스턴스의 뷰어 역할. </li></ul>|  |
|사설 도메인 관리|<ul> <li>CFEE 인스턴스 리소스 그룹의 뷰어. </li><li>CFEE 인스턴스의 뷰어 역할. </li></ul>| <ul><li>도메인을 소유하는 조직의 관리자 역할. </li></ul>|
|사설 도메인 보기|<ul> <li>CFEE 인스턴스 리소스 그룹의 뷰어. </li><li>CFEE 인스턴스의 뷰어 역할. </li></ul>|<ul><li>도메인을 소유하는 조직의 뷰어 역할. </li></ul>|
|CFEE 영역에서 IBM Cloud 서비스 인스턴스 작성/삭제| <ul><li>CFEE를 작성할 리소스 그룹의 뷰어 역할.</li> <li>CFEE 인스턴스의 뷰어 역할.</li> <li>서비스 인스턴스를 작성하거나 IAM 관리 서비스를 인스턴스화할 리소스 그룹의 편집자.</li> </ul>| <ul><li>서비스 인스턴스가 작성(및 자동으로 추가/별명 지정)될 CFEE 영역의 개발자 역할.</li></ul> |
|CFEE 영역에/에서 IBM Cloud 서비스 인스턴스 추가/제거(즉, CFEE 영역에서 IBM Cloud 서비스의 별명 작성/삭제)| <ul><li>CFEE 인스턴스 리소스 그룹의 뷰어 역할.</li><li>CFEE 인스턴스의 뷰어 역할. </li><li>추가할 서비스 인스턴스의 운영자 플랫폼 역할 및 독자 서비스 역할. </li></ul>|<ul><li>서비스 인스턴스가 추가(별명 지정)될 CFEE 영역의 개발자 역할.</li></ul> |
|CFEE 영역에서 IBM Cloud 서비스 인스턴스 바인드/바인드 해제|<ul> <li>바인드 또는 바인드 해제할 서비스 인스턴스의 리소스 그룹 편집자.</li><li>CFEE 인스턴스의 뷰어 역할. </li><li>바인드할 서비스 인스턴스의 운영자 플랫폼 역할 및 기록자 서비스 역할.</li></ul> | <ul><li>서비스 인스턴스가 바인드될 CFEE 영역의 개발자 역할.</li></ul> |
|`cf` cli 명령 실행|<ul> <li>CFEE 인스턴스 리소스 그룹의 뷰어 역할. </li><li>CFEE 인스턴스의 뷰어 역할.</li></ul> | <ul><li>명령을 수행하는 데 필요한 조직/영역의 Cloud Foundry 역할.</li></ul> |
{: caption="표 1. CFEE에서 태스크를 수행하는 데 필요한 권한" caption-side="top"}

## 새 환경을 작성하는 데 필요한 권한
{: #perm-creating}

CFEE 서비스의 새 인스턴스를 작성하려면 CFEE 서비스 자체에 대해서는 물론 CFEE 작성 시에 역시 자동으로 작성된 지원 서비스에 대해서도 계정 관리자가 사용자에게 액세스 정책을 부여해야 합니다.

사용자가 {{site.data.keyword.cfee_full_notm}} 인스턴스를 작성하려면 다음의 IAM(Identity & Access Management) 액세스 정책이 필요합니다.

* {{site.data.keyword.Bluemix}} 계정의 **_기본_** **리소스 그룹**에 대한 _뷰어_(또는 그 이상의) 액세스. 리소스 그룹을 사용하면 리소스를 사용자 정의된 그룹으로 구성하여 해당 리소스에 대한 액세스 제어를 용이하게 할 수 있습니다. 새 환경 인스턴스를 작성할 때 리소스 그룹에 대한 프롬프트가 표시됩니다. 항상 Kubernetes 클러스터를 필요로 하는 리소스 그룹이므로, _기본_ 리소스 그룹에 대한 액세스는 반드시 필요합니다.  사용자가 다른 리소스 그룹의 CFEE 인스턴스를 프로비저닝할 수 있지만, 그래도 Kuberetes 클러스터는 여전히 _기본_ 리소스 그룹에 프로비저닝됩니다.  사용자가 다른 사용자 그룹의 CFEE를 프로비저닝하는 경우, 해당 사용자에게는 해당 리소스 그룹의 뷰어 액세스 권한이 필요합니다.

* **{{site.data.keyword.cfee_full_notm}} 서비스** 리소스에 대한 _관리자_ 또는 _편집자_ 역할. 환경이 지정되는 리소스 그룹에서, {{site.data.keyword.cfee_full_notm}} 서비스의 관리자 또는 편집자 역할이 있는 사용자는 환경을 작성하고 삭제할 수 있습니다. 관리자 역할이 있는 사용자만 사용자를 {{site.data.keyword.cfee_full_notm}} 인스턴스에 지정하고 지정된 역할을 해당 인스턴스의 사용자로 변경할 수 있습니다.
   
* **Kubernetes 서비스** 리소스에 대한 _관리자_ 역할.  {{site.data.keyword.cfee_full_notm}}의 인스턴스는 Kubernetes 서비스에서 제공하는 컨테이너 클러스터 인프라에 배치됩니다. {{site.data.keyword.cfee_full_notm}} 서비스의 인스턴스를 작성할 때 해당 서비스는 자동으로 Kubernetes 클러스터를 작성합니다. Kubernetes 서비스에 대한 액세스는 해당 클러스터 인프라의 작성을 위해 필요합니다. Kubernetes 서비스 정책에 대한 액세스 범위를 CFEE 인스턴스를 프로비저닝하고자 하는 특정 지역으로 지정하거나, 액세스 범위를 모든 지역으로 지정할 수 있습니다.

* CFEE 서비스의 필수 종속 항목인 **IBM Cloud Object Storage 서비스**에 대한 _관리자_ 또는 _편집자_ 플랫폼 역할 및 관리자 서비스 액세스 역할.  IBM Cloud Object Storage 서비스의 인스턴스는 ICFEE 애플리케이션 컨테이너(예: 업로드된 애플리케이션 패키지, 빌드팩 및 컴파일된 실행 파일) 작성 중에 생성된 데이터를 저장하는 데 사용됩니다.

* Compose for PostgreSQL 서비스의 인스턴스는 CFEE 서비스의 필수 종속 항목입니다.  Compose for PostgreSQL은 CFEE 인스턴스에 대한 Cloud Foundry 데이터를 저장하는 데 사용됩니다(예: 애플리케이션 배치 감사, 이벤트 시작 및 중지, CFEE 사용자 멤버십, 조직, 영역, 애플리케이션 및 서비스 연결의 레코드 유지).  **Compose for PostgreSQL 서비스**의 해당 인스턴스는 {{site.data.keyword.cfee_full_notm}} 인스턴스 작성 시에 선택한 퍼블릭 Cloud Foundry 조직(CFEE 조직과 무관함) 내의 영역에 배치됩니다.  이는 {{site.data.keyword.cfee_full_notm}} 인스턴스 작성 시에 최소한 CFEE 인스턴스를 프로비저닝하고자 하는 위치의 조직에 대한 _관리자_ 액세스 권한을 보유해야 함을 의미합니다.  해당 조직의 하나 이상의 영역에 대한 _개발자_ 액세스 권한도 필요합니다. 

  CFEE 인스턴스를 작성하고자 하는 위치의 최소한 하나의 퍼블릭 조직의 구성원이 아닌 경우에는 자신을 이에 초대하도록 IBM Cloud 관리자에게 요청하십시오. 계정의 관리자 역할을 보유한 경우에는 다음을 수행하여 계정의 퍼블릭 조직과 영역에 사용자를 추가할 수 있습니다.

     * [**관리 > 계정 > Cloud Foundry 조직**](https://console.bluemix.net/account/organizations)으로 이동하여 **조직 추가**를 클릭하거나 기존 조직을 선택하십시오.
     * 조직 페이지 맨 위에서 **사용자** 탭으로 이동하십시오.
     * CFEE 인스턴스를 작성해야 하는 사용자를 찾으십시오. CFEE 인스턴스 작성이 가능하도록 하려는 사용자가 목록에 없으면 테이블 위에서 **사용자 추가 또는 초대**를 클릭하여 사용자를 조직에 추가하거나 초대하십시오.
     * 조직 페이지 맨 위에서 **영역** 탭으로 이동하십시오.
     * Compose for PostgreSQL 서비스의 인스턴스가 프로비저닝되는 영역을 찾고 **개발자** 역할 선택란을 선택하십시오.

다음 화면은 사용자가 {{site.data.keyword.cfee_full_notm}} 인스턴스를 작성할 수 있는 {{site.data.keyword.Bluemix_notm}}의 ID 및 액세스 페이지에 표시되는 액세스 정책을 보여줍니다.

![액세스 정책](img/AccessPolicies_Creator.png)

{{site.data.keyword.Bluemix}} 명령행을 사용하여 사용자 권한을 부여할 수 있습니다.  또한 정책을 작성하는 명령에 의해 호출되는 JSON 형식 파일에 정책의 매개변수(예: 서비스, 역할, 지역 등)를 지정하여 사용자에 대한 액세스 정책을 정의할 수 있습니다.  자세한 정보는 [명령행을 사용하여 IAM 정책 지정](https://console.bluemix.net/docs/services/cloud-monitoring/security/assign_policy.html#assign_policy_commandline)을 참조하거나 명령행에서 `ibmcloud iam -help`를 실행하십시오. 이를 위해서는 [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use)를 설치해야 합니다.
{:tip}

{{site.data.keyword.cfee_full_notm}} 인스턴스를 작성하는 데 필요한 액세스 정책이 있는지 확인하려면 다음을 수행하십시오.
1. {{site.data.keyword.Bluemix_notm}} 헤더의 [**관리 > 액세스(IAM) > 사용자**](https://console.bluemix.net/iam/#/users) 메뉴로 이동하여 **ID & 액세스** 페이지를 여십시오.
2. 액세스 정책 탭에서 환경을 작성 중인 사용자를 클릭하여 해당 사용자에 대한 액세스 정책을 지정하거나 보십시오.

여러 사용자에게 한 번에 액세스 지정을 용이하게 하기 위해 사용자 및 서비스 ID 세트의 구성 방법을 포함하여 {{site.data.keyword.Bluemix}}에서 사용자 및 액세스 관리에 대한 자세한 정보는 [사용자 및 액세스 관리](https://console.bluemix.net/docs/iam/iamusermanage.html#iamusermanage)를 참조하십시오.

### CLI를 사용하여 환경을 작성하기 위한 권한 설정의 빠른 처리
{: #permcli-creating}

`ibmcloud cfee create-permission-set`을 통해 CFEE 인스턴스의 작성에 대한 권한 설정을 빠르게 진행할 수 있습니다.  이 명령을 통해 CFEE 관리자는 CFEE 인스턴스 및 해당하는 모든 보조 서비스 작성에 대한 필수 액세스 정책을 단일 명령으로 설정할 수 있습니다. 

명령은 IAM _액세스 그룹_에 권한을 설정하고 사용자를 해당 _액세스 그룹_에 추가합니다.  명령을 실행하는 관리자는 명령에 기존 _액세스 그룹_을 포함할 수 있습니다.  _액세스 그룹_이 제공되지 않는 경우 기본 _cfee-provision-access-group_이 자동으로 작성됩니다.

```
ibmcloud cfee create-permission-set USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

명령은 대상 사용자에 대해 다음 액세스 정책을 설정합니다.

*  현재 IBM Cloud 계정의 Cloud Object Storage 및 CFEE 서비스에 대한 편집자 역할.
*  현재 IBM Cloud 계정의 Kubernetes 서비스에 대한 관리자 역할.
*  Compose for PostgreSQL의 프로비저닝을 위한 현재 조직의 현재 영역에 대한 개발자 역할.

명령에 대한 세부사항은 다음을 실행하십시오.

```
cfee create-permission-set -help
```
{: pre}

`ibmcloud cfee create-permission-get`을 사용하여 사용자를 위해 준비된 액세스 정책을 알아보거나 유효성을 검증할 수 있습니다.

```
ibmcloud cfee provision-permission-get USER_NAME [-ag, --access-group GROUP_NAME] [--output TYPE]
```
{: pre}

## 환경에 대해 작업하는 데 필요한 권한
{: #perm-working}

{{site.data.keyword.cfee_full_notm}}의 인스턴스에 대해 작업하려면 사용자가 다음과 같아야 합니다.
1. {{site.data.keyword.cfee_full_notm}} 인스턴스가 작성된 {{site.data.keyword.Bluemix_notm}} 계정의 구성원이어야 합니다.
2. 계정 관리자가 다음 IAM _액세스 정책_을 부여해야 합니다(현재 계정 액세스 정책을 확인하려면 {{site.data.keyword.Bluemix_notm}} 헤더의 [**관리 > 액세스(IAM) > 사용자**](https://console.bluemix.net/iam/#/users) 메뉴 아래에서 _ID 및 액세스_ 페이지 참조).

    CFEE 인스턴스에서 작업하는 모든 사용자는 다음과 관련하여 _뷰어_ 플랫폼 역할 이상이 필요합니다.
  - CFEE ㅇ니스턴스가 작성되는 리소스 그룹.
  - CFEE 인스턴스 자체. 
  
   CFEE 인스턴스에서 사용자가 보유하는 액세스 및 제어 레벨은 액세스 정책에 부여된 역할에 따라 달라집니다.

  - CFEE 인스턴스와 관련하여 _뷰어_ 역할이 지정된 사용자는 기본 {{site.data.keyword.Bluemix_notm}} 대시보드에 나열되어 있는지 확인하고 해당 사용자 인터페이스를 열 수 있습니다. 환경 내의 특정 조직 및 영역에 대한 사용자 액세스 권한은 특정 조직 및 영역의 관리자가 지정하는 해당 조직 및 영역 역할에 따라 조정됩니다. 자세한 정보는 [조직에 사용자 추가](add-users.html)를 참조하십시오.
  
  - CFEE 인스턴스와 관련하여 _관리자_ 또는 _편집자_ 역할이 지정된 사용자는 조직을 작성하고, 조직 및 영역에 관리자를 지정하고, 환경 내의 모든 조직 및 영역에 대한 전체 권한을 보유하며, 클라우드 제어기 API를 통해 운영 조치를 수행할 수 있습니다. 이러한 사용자에게는 Cloud Foundry _사용자 계정 및 인증 범위_의 _cloud_controller.admin 범위_가 자동으로 부여됩니다.

  - **CFEE를 새 버전으로 업데이트**할 수 있으려면 CFEE 인스턴스와 관련하여 _편집자_ 플랫폼 역할 이상이 필요하고, CFEE가 프로비저닝되는 Kubernetes 클러스터에 대한 _운영자_ 역할 이상이 필요합니다.

  - cfee의 **용량을 변경**할 수 있으려면(셀 추가 또는 제거) CFEE 인스턴스와 관련하여 _관리자_ 플랫폼 역할이 필요하고, CFEE가 프로비저닝되는 Kubernetes 클러스터에 대한 _운영자_ 역할 이상이 필요합니다.
 
  - *서비스 인스턴스*를 CFEE 영역에 **추가**할 수 있으려면(즉, CFEE 영역으로 서비스 인스턴스 별명 지정) IBM Cloud 서비스 인스턴스와 관련하여 _운영자_ 플랫폼 역할 이상이 필요합니다.
 
  - CFEE 영역에 배치된 애플리케이션에 서비스 인스턴스를 **바인드**할 수 있으려면 IBM Cloud 서비스 인스턴스와 관련하여 _운영자_ 플랫폼 역할 이상 및 _기록자_ 서비스 역할 이상이 필요합니다.


## 우수 사례: 액세스 그룹
{: #access-groups}

액세스 그룹을 사용하여 CFEE의 액세스 제어를 관리하고 간소화하십시오.  액세스 그룹을 사용하면 액세스 정책을 지정할 수 있는 임의 그룹을 정의할 수 있습니다.  액세스 그룹에 추가된 모든 그룹에 그룹의 액세스 정책이 자동으로 지정됩니다. 

IBM Cloud 사용자 인터페이스 또는 `ibmcloud` cli를 통해 액세스 그룹을 작성하고 관리할 수 있습니다. 

사용자 인터페이스에서 메뉴 표시줄로 이동하여 **관리 > 액세스(IAM)**를 클릭하고 [액세스 그룹](https://cloud.ibm.com/iam#/groups)을 선택하십시오.

또는 `ibmcloud` cli를 사용할 수 있습니다.

1. 액세스 그룹을 작성하십시오.

  ```
  ibmcloud iam access-group-create GROUP_NAME [-d, --description DESCRIPTION]
```
  {: pre}

2. 액세스 그룹의 액세스 정책을 작성하십시오.

  ```
  ibmcloud iam access-group-policy-create GROUP_NAME
  ```
  {: pre}

3. 액세스 그룹에 사용자를 추가하십시오.

  ```
  ibmcloud iam access-group-user-add <user-name> [<user-name2...]
  ```
  {: pre}

<br>
자세한 정보는 [액세스 그룹 설정](https://cloud.ibm.com/docs/iam/groups.html#groups)의 내용을 참조하십시오.
