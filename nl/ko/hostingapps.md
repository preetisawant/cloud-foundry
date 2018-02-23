---



copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# {{site.data.keyword.Bluemix_notm}}에서 앱 호스팅
{: #hosting_apps}

{{site.data.keyword.Bluemix}}를 사용하면 앱을 작성하고 기존 앱을 호스팅할 수 있습니다. 클라우드 준비 상태이면 {{site.data.keyword.Bluemix_notm}}로 앱을 이동할 수 있습니다. {{site.data.keyword.Bluemix_notm}}는 앱을 실행할 수 있도록 여러 방법을 제공합니다(예: Cloud Foundry, IBM Containers 및 가상 머신).

## 앱 클라우드 준비 상태 만들기
{: #cloud-readyapps}

앱에 다음 원칙이 모두 있는 경우 앱은 클라우드 준비 상태이며 {{site.data.keyword.Bluemix_notm}}에 마이그레이션할 수 있습니다. 앱에서 원칙이 위반되는 경우, 일반적으로 원칙을 고수하도록 [앱 수정](../apps/cloud-ready.html)을 수행할 수 있습니다.

## 앱 마이그레이션
{: #ht_hostapp}

앱을 클라우드 환경으로 완전히 이동하는 대신, 점진적으로 {{site.data.keyword.Bluemix_notm}}에 앱을 마이그레이션할 수 있습니다. 우선 앱의 일부를 마이그레이션한 후에 클라우드 통합 서비스를 사용하여 기존 데이터 또는 SOR(System of Record)에 연결할 수 있습니다.

클라우드 앱에서 백엔드 데이터 또는 서비스에 액세스해야 할 수 있습니다(예: SOR(System of Record)). {{site.data.keyword.Bluemix_notm}}에서는 Secure Gateway 서비스를 사용하여 {{site.data.keyword.Bluemix_notm}} 조직 및 엔터프라이즈 백엔드 네트워크 간의 보안 터널을 설정할 수 있습니다. 서비스를 사용하면 {{site.data.keyword.Bluemix_notm}}의 앱이 백엔드 네트워크의 데이터 및 서비스에 액세스할 수 있습니다. 세부사항은 [Reaching enterprise backend with {{site.data.keyword.Bluemix_notm}} Secure Gateway via console ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}을 참조하십시오.

앱을 Cloud Foundry 앱으로서 {{site.data.keyword.Bluemix_notm}}에 배치하려면 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 런타임을 선택하십시오. 런타임에는 자체 앱으로 바꿀 수 있는 스타터 Hello World 앱이 포함되어 있습니다. 원하는 런타임을 제공하는 스타터를 찾을 수 없는 경우에는 cf push 명령에서 –b 옵션을 사용하여 {{site.data.keyword.Bluemix_notm}}로 사용자 정의, Cloud Foundry 호환 가능 빌드팩을 가져올 수 있습니다. 세부사항은 [커뮤니티 빌드팩 사용](byob.html)을 참조하십시오.

{{site.data.keyword.Bluemix_notm}}에서 제공하는 다음 도구 및 서비스를 사용할 수 있습니다.

| 도구 | 방법 |
|:------|:--------|
| Cloud Foundry 명령행 인터페이스(cf cli) | 로컬 클라이언트에서 코드를 관리하고 Cloud Foundry 명령행 인터페이스를 사용하여 앱을 {{site.data.keyword.Bluemix_notm}}에 수동으로 푸시하십시오. 자세한 정보는 [앱 업로드](../starters/upload_app.html)를 참조하십시오. |
| Eclipse | Eclipse에서 코드를 관리하고 {{site.data.keyword.Bluemix_notm}}용 IBM Eclipse 도구를 사용하여 앱을 푸시하십시오. |
| Git 통합 | GitHub에서 코드를 관리하고 Git를 {{site.data.keyword.Bluemix_notm}}로 통합하십시오. 다른 개발자과 협업할 수 있습니다. 앱은 코드의 변경사항을 커미트할 때 {{site.data.keyword.Bluemix_notm}}에 자동으로 배치됩니다. 앱을 수동으로 푸시할 필요가 없습니다. |
| {{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline | DevOps GitHub 저장소에서 코드를 관리하고 DevOps Delivery Pipeline을 사용하여 앱을 {{site.data.keyword.Bluemix_notm}}에 배치하십시오. |
{: caption="표 1. {{site.data.keyword.Bluemix_notm}} 도구" caption-side="top"}

Cloud Foundry 플랫폼이 앱 요구사항을 충족하지 않는 경우에는 보다 사용자 정의된 옵션으로 런타임이 설정되고 구성되고 유지보수되는 VM 또는 컨테이너를 사용할 수 있습니다.

## Continuous Delivery에서 도구 체인을 사용하여 앱 개발 및 배치
{:ht_cd}

[도구 체인을 앱에](/docs/services/ContinuousDelivery/toolchains_working.html#creating_a_toolchain_from_an_app) 추가한 후에 [Continuous Delivery 도구 체인 UI](/docs/services/ContinuousDelivery/toolchains_using.html#toolchains-using)를 사용하여 앱을 개발하고 배치하십시오.

## cf cli를 사용하여 앱 업로드
{: #ht_cfcli}

로컬 클라이언트에서 코드를 관리하고 Cloud Foundry 명령행 인터페이스를 사용하여 앱을 {{site.data.keyword.Bluemix_notm}}에 수동으로 업로드할 수 있습니다. 코드를 변경하는 경우에는 앱을 {{site.data.keyword.Bluemix_notm}}에 다시 푸시하여 업데이트된 코드를 실행해야 합니다.

다음 단계를 수행하여 앱을 마이그레이션하십시오.

Cloud Foundry 명령행 인터페이스를 설치하십시오.  최신 버전의 cf 명령행 인터페이스를 사용 중인지 확인하십시오.
  1. 운영 체제의 설치 프로그램을 다운로드하십시오.
  2. 도구 마법사에 따라 명령행을 설치하십시오.
  3. 다음 명령을 사용하여 cf 명령행 인터페이스의 버전을 확인하십시오. `cf -v`

선택사항: 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시하기 전에 배치 세부사항을 지정하고 저장하려는 경우 다음 단계를 수행하여 앱 Manifest를 추가할 수 있습니다.

  1. 앱의 작업 디렉토리로 이동하고 이름이 manifest.yml(기본 이름)인 파일을 작성하십시오.</li>
  2. Manifest 파일에서 배치 세부사항을 지정하십시오. 다음 예는 Java™ 앱에 대한 Manifest 파일을 표시합니다.

  ```
  applications:
  - disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M
  ```

이 파일에서 사용할 수 있는 지원 옵션에 대한 자세한 정보는 [앱 Manifest](depapps.html#appmanifest)를 참조하십시오.

### 앱 푸시

`cf push` 명령을 사용하여 앱을 업로드할 수 있습니다.
  1. 다음 명령을 실행하여 {{site.data.keyword.Bluemix_notm}}에 연결하고 로그인하십시오. 프롬프트가 나타나면 조직 및 영역을 선택하십시오.
  ```
cf login -a https://api.ng.bluemix.net
  ```
  조직이 싱글 사인온을 사용하는 경우 `-sso` 플래그를 추가하십시오.

  2. 앱 디렉토리에서 앱 이름과 함께 cf push 명령을 입력하십시오. 앱 이름은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다.

  ```
  cf push appname
  ```

  3. 선택사항: 외부 빌드팩을 사용 중인 경우에는 cf push 명령에서 -b 옵션을 사용해야 합니다. 예를 들어, 다음과 같습니다.

  ```
  cf push appname -b buildpack_URL
  ```

  세부사항은 [커뮤니티 빌드팩 사용](byob.html)을 참조하십시오.

선택사항: 앱을 변경하는 경우 `cf push 명령`을 다시 입력하여 해당 변경사항을 업로드해야 합니다. cf 명령행 인터페이스는 이전 옵션 및 프롬프트에 대한 사용자 응답을 사용하여 새 코드 비트로 앱의 실행 중인 인스턴스를 업데이트합니다.

#### 참고:

* cf push 명령을 사용하는 경우에는 cf 명령행 인터페이스가 현재 디렉토리의 모든 파일 및 디렉토리를 {{site.data.keyword.Bluemix_notm}}에 복사합니다. 앱 디렉토리에 필요한 파일만 있는지 확인하십시오.
* 앱의 모든 인스턴스에 대해 조직에 충분한 메모리가 있는지 확인하십시오. 사용자 조직의 메모리 할당량을 보려면 cf org org_name을 사용하십시오.
* cf push에 대한 자세한 정보는 [cf 명령](../cli/reference/cfcommands/index.html) 명령을 참조하십시오.

## 데이터 마이그레이션 및 서비스 사용
{: #ht_service}

{{site.data.keyword.Bluemix_notm}}에 앱을 업로드한 후 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 앱이 연결된 서비스를 선택하고 서비스 인스턴스를 작성하며 인스턴스를 앱에 바인드한 후에 앱을 다시 시작하십시오.

앱의 VCAP_SERVICES 환경 변수는 {{site.data.keyword.Bluemix_notm}}의 서비스 인스턴스와 상호작용하는 방법에 대한 정보가 포함된 JSON 오브젝트입니다. 이 정보에는 서비스 인스턴스 이름, 신임 정보 및 서비스 인스턴스에 대한 연결 URL이 포함됩니다.

{{site.data.keyword.Bluemix_notm}}에서 코드를 실행하려면, 서비스 연결에 대한 정보를 가져올 수 있도록 VCAP_SERVICES 변수를 구문 분석하기 위한 코드 로직을 추가해야 합니다. 환경 변수를 통해 서비스 인스턴스의 동적 지정된 호스트 및 포트를 가져올 수 있도록 앱을 수정하십시오. 다음 예는 Ruby 앱에서 Postgre SQL 서비스 인스턴스의 신임 정보를 가져오는 방법을 표시합니다.

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```
{:codeblock}

{{site.data.keyword.Bluemix_notm}}용 앱을 수정한 후 앱이 로컬 환경에서 실행될 수 있도록 하려면, 모든 {{site.data.keyword.Bluemix_notm}} Cloud Foundry 앱에 대해 설정된 VCAP_SERVICES 환경 변수가 존재하는지 확인하십시오.


# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [{{site.data.keyword.containershort_notm}}](/docs/containers/container_index.html)
* [가상 머신](/docs/virtualmachines/vm_index.html)
* [Delivery Pipeline 시작하기](/docs/services/DeliveryPipeline/index.html)
* [IBM Eclipse Tools for Bluemix를 사용하여 앱 배치](/docs/manageapps/eclipsetools/eclipsetools.html)
* [The twelve-factor app ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://12factor.net/){: new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console ![외부 링크 아이콘](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){: new_window}
