---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# {{site.data.keyword.cfee_full_notm}} 정보
{: #creating}

{{site.data.keyword.cfee_full}}(CFEE)를 사용하면 요청 시 여러 개의 격리된 엔터프라이즈급 Cloud Foundry 플랫폼을 인스턴스화할 수 있습니다. {{site.data.keyword.Bluemix_notm}} Foundry Enterprise 서비스의 인스턴스는 {{site.data.keyword.Bluemix_notm}}의 고유 계정 내에서 실행됩니다. 환경이 격리된 하드웨어(Kubernetes 클러스터)에 배치됩니다. 액세스 제어, 용량 관리, 변경 관리, 모니터링 및 서비스를 포함하여 환경을 완전히 제어할 수 있습니다.
{:shortdesc}

{{site.data.keyword.cfee_full}}는 현재 베타 단계에 있으며 피드백을 찾고 있습니다! 시작하려면 [https://console.bluemix.net/cfadmin/create](https://console.bluemix.net/cfadmin/create)에서 고유한 {{site.data.keyword.cfee_full}} 인스턴스를 작성하고 [IBM CFEE Slack 포럼](https://ibm-cfee.slack.com)에 대한 [액세스 권한을 요청](http://ibm.biz/cfee-forum-signup)하여 피드백을 공유하고 질문하고 제품 팀과 연계하십시오.
{:tip}

프로젝트 성공을 위해 충분한 시간을 들여 필요한 리소스 및 엔터프라이즈 요구사항을 계획하고 디자인하십시오. 시작하는 데 도움을 받으려면 다음 질문을 고려하십시오.

* 개발 중인 앱의 수와 유형은 무엇입니까?
* 앱이 어떤 서비스에 액세스해야 합니까?
* 개발 프로세스에서 누가 협업하고 각각 어떤 역할을 수행합니까?
* 프로젝트의 각 단계에 어느 정도의 격리가 필요합니까?
* 엔터프라이즈에서 인프라 리소스를 제공합니까?
* 회사에서 어떻게 의사소통합니까?
* 조직 및 영역 사용을 명확히 식별하기 위해 구현할 수 있는 이름 지정 표준이 있습니까?

필요한 클라우드 환경의 유형을 결정하는 과정의 일부로 계정, 조직, 영역, 리소스 및 팀 구성원의 구조를 계획하십시오.

대부분의 조직에서는 단일 {{site.data.keyword.Bluemix_notm}} 계정으로 충분합니다. 조직에 둘 이상의 비즈니스 영역이 있는 경우 각 비즈니스 도메인마다 별도의 {{site.data.keyword.Bluemix_notm}} 계정을 작성할 수 있습니다. 예를 들어, 대형 은행은 소매 및 상업 분야에 대한 별도의 계정을 작성할 수 있습니다.

다음 표는 일부 핵심 요소를 요약하여 보여줍니다.

|요소   |설명 |
|-----------|---------------|
|IBM Cloud 계정 |특정 IBM Cloud 계정에 CFEE 인스턴스가 작성되어 해당 사용자에 대해 정의된 역할 및 액세스 정책에 따라 해당 계정의 사용자가 사용할 수 있도록 합니다. |
||CFEE 인스턴스가 작성된 계정은 평가판 계정이 아니라 종량과금제 또는 구독 계정 유형이어야 합니다. |
|CFEE |애플리케이션을 호스팅하기 위한 IBM Cloud Foundry Enterprise Environment 서비스입니다. |
||IBM Cloud 카탈로그에서 사용할 수 있습니다. |
|CFEE 인스턴스 |IBM Cloud 계정의 관리자 또는 편집자 역할이 있는 사용자가 해당 계정으로 작성한 IBM Cloud Foundry Enterprise Environment 서비스의 인스턴스입니다. |
||IBM Cloud 계정에는 여러 CFEE 인스턴스가 있을 수 있습니다. |
||하나 이상의 조직이 있을 수 있습니다. |
|조직 |하나 이상의 영역을 포함합니다. |
||하나 이상의 조직 관리자를 포함합니다. |
||하나 이상의 팀 구성원을 포함합니다. 각 팀 구성원은 하나 이상의 역할을 부여받을 수 있습니다. |
||영역 내 배치된 애플리케이션에서 생성된 사용 요금은 조직 레벨에서 보고됩니다. |
|영역 |하나 이상의 리소스를 포함합니다. |
||하나 이상의 앱을 포함합니다. |
||하나 이상의 영역 관리자를 포함합니다. |
||하나 이상의 팀 구성원을 포함합니다. 각 사용자는 이미 소유 조직의 팀 구성원이어야 합니다. 각 팀 구성원은 하나 이상의 역할을 부여받을 수 있습니다. |
|팀 구성원 |여러 계정에 있는 하나 이상의 조직과 영역에 추가될 수 있습니다. |
||동일한 조직, 영역 또는 둘 다에 있는 둘 이상의 역할에 지정될 수 있습니다. |
|서비스 별명 |IBM Cloud에 있는 서비스 인스턴스의 별명입니다. |
||개발자가 IBM Cloud 계정에서 사용 가능한 기존 서비스 인스턴스를 CFEE 내의 영역에 배치된 애플리케이션에 바인드할 수 있도록 합니다. |
{:caption="표 1. 핵심 요소 설명" caption-side="top"}

