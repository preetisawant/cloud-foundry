---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# {{site.data.keyword.cfee_full_notm}} 정보
{: #about}

{{site.data.keyword.cfee_full}} 서비스를 시작합니다.

{{site.data.keyword.cfee_full}}(CFEE)를 사용하면 요청 시 격리된 여러 엔터프라이즈급 Cloud Foundry 플랫폼을 인스턴스화할 수 있습니다. {{site.data.keyword.Bluemix_notm}} Foundry Enterprise 서비스의 인스턴스는 {{site.data.keyword.Bluemix_notm}}의 고유 계정 내에서 실행됩니다. 환경이 격리된 하드웨어(Kubernetes 클러스터)에 배치됩니다. 액세스 제어, 용량, 버전 업데이트, 리소스 사용 및 모니터링을 포함하여 환경을 완전히 제어할 수 있습니다. 뿐만 아니라, {{site.data.keyword.Bluemix_notm}}로의 CFEE 통합을 통해 개발자들은 {{site.data.keyword.Bluemix_notm}} 계정에서 사용 가능한 서비스를 활용할 수 있습니다.  사용자는 이러한 서비스를 CFEE에 추가하고, CFEE 영역으로 배치된 애플리케이션에 서비스를 바인드할 수 있습니다.

CFEE 인스턴스의 작성 및 사용을 [**시작하는**](https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#getting-started) 방법에 대해 알아보십시오.

{:shortdesc}

## CFEE의 핵심 요소
{: #key-elements}

다음 표에서는 {{site.data.keyword.cfee_full}} 서비스의 핵심 요소를 요약하여 보여줍니다.

|요소   |설명 |
|-----------|---------------|
|IBM Cloud 계정 |특정 IBM Cloud 계정에 CFEE 인스턴스가 작성되어 해당 사용자에 대해 정의된 역할 및 액세스 정책에 따라 해당 계정의 사용자가 사용할 수 있도록 합니다. |
||CFEE 인스턴스가 작성된 계정은 평가판 계정이 아니라 종량과금제 또는 구독 계정 유형이어야 합니다.  |
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
||개발자가 IBM Cloud 계정에서 사용 가능한 기존 서비스 인스턴스를 CFEE 내의 영역에 배치된 애플리케이션에 바인드할 수 있도록 합니다.|
{:caption="표 1. 핵심 요소 설명" caption-side="top"}

## CFEE의 대상 프로비저닝 및 서비스 지원
{: #provisioning-targets}

다음은 CFEE 서비스와 종속 서비스(Kubernetes 서비스, Compose for PostgreSQL 및 Cloud Object Storage 서비스)가 프로비저닝에 사용될 수 있는 지역, 위치 및 데이터 센터입니다.

|  **지역** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **CFEE 인스턴스 & Kubernetes 클러스터** | **Cloud Object Storage** | **Compose for PostgreSQL(CF 지역)** |
|----------------------------------------|-------------------|-------------------|-------------------|
|북미 | 몬트리올(mon01) | us-geo | us-east |
|북미 | 토론토(tor01) | us-geo| us-east |
|북미 | 워싱톤 DC(wdc04) | us-geo | us-east |
|북미 | 워싱톤 DC(wdc06) | us-geo | us-east | 
|북미 | 워싱톤 DC(wdc07) | us-geo | us-east |
|북미 | 댈러스(dal10) | us-geo |us-south |
|북미 | 댈러스(dal12) | us-geo |us-south |
|북미 | 댈러스(dal13) | us-geo |us-south |
|북미 | 산호세(sjc03) | us-geo |us-south |
|북미 | 산호세(sjc04) | us-geo |us-south |
|남미 &nbsp; &nbsp;| 상파울로(sao01) | us-geo |us-south |
|유럽 | 런던(lon02) |eu-geo | eu-gb |
|유럽 | 런던(lon04) |eu-geo | eu-gb |
|유럽 | 런던(lon06) |eu-geo | eu-gb | 
|유럽 | 암스테르담(ams03) |eu-geo | eu-de |
|유럽 | 오슬로(osl01) |eu-geo | eu-de | 
|유럽 | 파리(par01) |eu-geo | eu-de |
|유럽 | 프랑크푸르트(fra02) |eu-geo | eu-de |
|유럽 | 프랑크푸르트(fra04) |eu-geo | eu-de | 
|유럽 | 프랑크푸르트(fra05) |eu-geo | eu-de |
|유럽 | 밀라노(mil01) |eu-geo | eu-de |
|아시아 태평양 | 멜버른(mel01) | ap-geo | au-syd |
|아시아 태평양 | 시드니(syd01) | ap-geo | au-syd |
|아시아 태평양 | 시드니(syd04) | ap-geo | au-syd | 
|아시아 태평양 | 홍콩(hkg02) | ap-geo | au-syd |
|아시아 태평양 | 홍콩(seo01) | ap-geo | au-syd |
|아시아 태평양 | 싱가포르(sng01) | ap-geo | au-syd |
|아시아 태평양 | 도쿄(tok02) | ap-geo | au-syd |
|아시아 태평양 | 도쿄(tok04) | ap-geo | au-syd |
|아시아 태평양 | 도쿄(tok05) | ap-geo | au-syd |
|아시아 태평양 | 첸나이(che01) | ap-geo | au-syd |
{: caption="표2. CFEE의 대상 프로비저닝 및 서비스 지원" caption-side="top"}

**예를 들어**, CFEE 서비스는 유럽에서 세 개 데이터 센터에 프로비저닝할 수 있습니다(암스테르담(1개 데이터 센터), 프랑크푸르트(3개 데이터 센터), 런던(3개 데이터 센터), 오슬로(1개 데이터 센터) 및 파리(1개 데이터 센터)). CFEE가 프랑크푸르트에서 프로비저닝되는 경우, Cloud Object Store 서비스 인스턴스는 _eu-geo_ 지역에 배치되며 Compose for PostgreSQL 서비스 인스턴스는 _eu-de_ 퍼블릭 Cloud Foundry 지역에 배치됩니다.

CFEE의 서비스 관련 작업을 위한 자세한 정보 및 데모가 포함된 동영상은 [CFEE 동영상 재생 목록](https://ibm.biz/CFEE_Playlist){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 참조할 수 있습니다.
{:tip}
