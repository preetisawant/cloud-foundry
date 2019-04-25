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

# 시작하기 튜토리얼
{: #getting-started}

{{site.data.keyword.cfee_full}}(CFEE)는 클라우드에서 앱 및 서비스를 호스팅하기 위한 클라우드 플랫폼입니다. {{site.data.keyword.cfee_full_notm}}를 사용하면 앱을 개발하는 데 집중할 수 있도록 런타임, 미들웨어 및 인프라를 단순화하여 이용이 증가할 때 앱을 쉽게 스케일링할 수 있습니다.
{: shortdesc}

이 시작하기 튜토리얼은 {{site.data.keyword.cfee_full_notm}}를 작성하고, 사용자를 추가하고, 조직 및 영역을 작성하고, 앱을 배치하고, 해당 앱을 서비스에 바인드하는 방법을 보여줍니다.

**참고:** 다음에 오는 단계는 **표준** 플랜에서 작성한 CFEE에 적용할 수 있습니다. 이 CFEE가 **Eirini 기술 미리보기** 플랜에서 작성된 경우 **1단계 - 6단계만** 및 **11**단계를 따르십시오. 8단계 - 11단계에 설명된 기능은 _Eirini 기술 미리보기_ 플랜에서 지원되지 않습니다. [Eirini 기술 미리보기 시작하기](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)를 참조하십시오.
_Eirini 기술 미리보기_ 플랜을 사용하면 기본 Kubernetes를 컨테이너 스케줄러(Diego 대신)로 사용하여 CFEE를 탐색할 수 있습니다. Kubernetes 스케줄러는 Cloud Foundry 애플리케이션 런타임에서 앱을 배치하고 실행하며 사용자를 추가하고 조직과 영역을 작성하고 앱을 배치하며 해당 앱을 서비스에 바인드하가 위해 CFEE에서 사용합니다.  

## 1단계: CFEE 인스턴스 작성
{: #create-environment}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서 {{site.data.keyword.cfee_full_notm}}(CFEE)의 인스턴스를 작성할 수 있습니다. CFEE 인스턴스를 작성하기 전에 {{site.data.keyword.Bluemix_notm}} 계정을 준비하는 지침에 관한 [환경 작성](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment) 문서를 방문하여 CFEE 인스턴스를 작성하는 데 올바른 권한과 단계를 확인하십시오.


## 2단계: 조직 및 영역 작성
{: #create-orgsandspaces}

{{site.data.keyword.cfee_full_notm}}를 작성한 후 조직 및 영역을 작성하여 환경을 구조화하는 방법에 대한 정보는 [조직 및 영역 작성](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)을 참조하십시오. {{site.data.keyword.cfee_full_notm}}의 앱은 특정 범위 내로 범위가 지정됩니다. 결국 영역이 특정 조직 내에 존재합니다. 조직의 구성원이 할당량 플랜, 앱, 서비스 인스턴스 및 사용자 정의 도메인을 공유합니다.

조직을 작성할 때 조직에 할당량을 지정합니다. 할당량은 조직에서 사용 가능한 리소스(메모리, cpu 등)의 한계를 설정합니다. 나중에 다른 할당량을 지정할 수 있습니다. 모든 CFEE에는 사전 구성된 할당량 세트가 있지만, CFEE 사용자 인터페이스의 **할당량** 페이지에서 고유 사용자 정의 할당량도 작성할 수 있습니다. 할댱량 메뉴에서 사용자 정의 할당량 값을 기본 할당량으로 복사하는 _기본값에 복사_ 조치를 호출하여 사용자 정의 할당량을 _기본값_ 할당량으로 만들 수 있습니다.

**참고:** 상단 IBM Cloud 헤더에 있는 **_관리 > 계정 > Cloud Foundry 조직_** 메뉴에서 사용 가능한 _Cloud Foundry 조직_ 페이지는 **CFEE 조직이 아니라** 퍼블릭 IBM Cloud 조직에만 사용됩니다. CFEE 조직은 CFEE 인스턴스의 _조직_ 페이지 내에서 관리됩니다.  CFEE 사용자 인터페이스를 열고 **_조직_** 페이지를 클릭하여 해당 CFEE의 조직을 작성하고 관리할 수 있습니다.

## 3단계: 조직 및 영역에 사용자 추가
{: #add-users}

액세스 레벨을 제어하는 특정 역할 지정에 따라 해당 조직 및 영역에 [사용자를 추가](https://console.bluemix.net/docs/cloud-foundry/add-users.html)하십시오.  CFEE에서 사용자를 조직 및 영역의 구성원으로 추가하려면 해당 사용자에게 CFEE 인스턴스에 대한 사전 액세스 권한이 있어야 합니다. [권한](https://console.bluemix.net/docs/cloud-foundry/permissions.html)을 참조하십시오.

## 4단계: 애플리케이션 배치 및 보기
{: #deploy-apps}

준비가 되면 {{site.data.keyword.Bluemix_notm}} 명령행 인터페이스를 사용하여 [앱을 배치](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html)할 수 있습니다.  특정 CFEE 영역의 컨텍스트에서 또는 모든 CFEE 인스턴스에서 글로벌로 사용자 인터페이스에서 배치된 애플리케이션의 목록을 보십시오.  해당 보기에서 애플리케이션을 시작, 중지 또는 삭제할 수도 있습니다.

## 5단계: IBM Cloud 서비스 인스턴스 작성 또는 CFEE 영역에 추가
{: #service-instances}

[서비스를 작성](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)하거나 IBM Cloud 계정에서 사용 가능한 [기존 서비스를 추가](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)하십시오.  일단 서비스 인스턴스가 CFEE 영역에서 사용 가능하면 이를 해당 영역에 배치된 CFEE 애플리케이션에 바인드할 수 있습니다.

## 6단계: 서비스 인스턴스에 애플리케이션 바인드
{: #bind-apps}

서비스의 기능을 사용하기 위해 서비스 인스턴스 별명에 [앱을 바인드](https://cloud.ibm.com/docs/cloud-foundry/binding.html)하십시오.

[Cloud Foundry 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 모든 애플리케이션과 서비스의 통합 보기(*공용* 및 *엔터프라이즈*)를 볼 수 있습니다.  일단 Cloud Foundry 대시보드의 왼쪽 탐색 분할창에서 *퍼블릭*을 클릭하면 IBM Cloud 계정에서 사용 가능한 퍼블릭 애플리케이션과 서비스를 볼 수 있습니다.  *엔터프라이즈*를 클릭하면 모든 CFEE 환경, CFEE 영역에 배치된 애플리케이션, 그리고 CFEE 영역에 사용 가능한 서비스를 볼 수 있습니다.
{:tip}

## 7단계: 감사 및 로깅 지속성 사용(선택사항)
{: #enable-auditingandlogging}

[이벤트 감사](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing) 및 [지속성 로깅](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging)용 환경을 사용하십시오.

## 8단계: 모니터링 도구 사용(선택사항)
{: #enable-monitoring}

모니터링 도구는 CFEE 인스턴스 v2.2.0 이상에서 자동으로 프로비저닝되지 않습니다. CFEE 인스턴스가 작성되면 CFEE 관리자가 [모니터링 도구를 사용으로 설정](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)할 수 있습니다. 모니터링 도구 세트에는 Prometheus, Grafana 및 Alertmanager가 있습니다.

## 9단계: Cloud Foundry 도메인 작성 및 보안(선택사항)
{: #create-domains}

CFEE(공유 도메인)의 모든 애플리케이션 또는 특정 조직(사설 도메인)의 [도메인](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains)을 작성하고 SSL 인증서로 보안을 설정하십시오.

## 10단계: Cloud Foundry 빌드팩의 우선순위 구성
{: #create-buildpacks}

빌드팩에서는 Cloud Foundry 환경에 배치된 애플리케이션의 런타임 지원을 제공하며 애플리케이션의 런타임을 자동으로 구성하고 해당 종속성을 처리합니다. Cloud Foundry에는 공통 언어와 프레임워크의 빌드팩 세트가 포함되어 있습니다. Cloud Foundry 빌드팩에 관해 [자세히 보십시오](https://docs.cloudfoundry.org/buildpacks/).  

CFEE 사용자 인터페이스의 **빌드팩** 페이지에서 사용자 정의 빌드팩을 작성하고 업로드할 수 있습니다. 빌드팩에는 우선순위 목록에 순서를 나타내는 위치가 있습니다. 애플리케이션 스테이징 중에 Cloud Foundry에서 위치 1부터 빌드팩 세트와 비교하여 애플리케이션의 호환성을 확인합니다. 호환성 검사는 호환 가능한 빌드팩을 찾을 때까지 우선순위 목록에서 아래로 진행합니다. 빌드팩 세트의 우선순위 순서가 개발 팀의 요구사항을 충족하는지 확인하십시오. 빌드팩 이름을 다른 위치로 끌어서 놓아 우선순위 순서에서 빌드팩의 위치를 변경할 수 있습니다. [Cloud Foundry CLI](https://docs.cloudfoundry.org/adminguide/buildpacks.html)를 통해서도 빌드팩을 관리할 수 있습니다.

## 11단계: 애플리케이션을 관리하기 위해 Stratos Console 설치(선택사항)
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
