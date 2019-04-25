---

copyright:
  years: 2018
lastupdated: "2019-04-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 서비스에 대한 작업
{: #workingwith-services}

{{site.data.keyword.cfee_full_notm}}에 배치된 애플리케이션은 두 가지 유형의 서비스 인스턴스에 바인드될 수 있습니다.

1. {{site.data.keyword.Bluemix}} 카탈로그에서 작성되고 {{site.data.keyword.Bluemix}} 계정에서 사용 가능한 퍼블릭 서비스 인스턴스.  
{{site.data.keyword.Bluemix}} 계정에서 사용 가능한 공용 서비스 인스턴스는 자체적으로 CFEE 환경에 자동으로 사용할 수 없습니다. ({{site.data.keyword.Bluemix}} 계정에서 사용 가능한) 퍼블릭 서비스 인스턴스를 CFEE 환경의 영역에서 사용할 수 있도록 하려면 이를 대상 CFEE 영역에 별도로 추가해야 합니다. CFEE의 사용자 인터페이스를 통해 CFEE에 공용 서비스 인스턴스를 _추가_할 때 공용 서비스 인스턴스의 별명을 CFEE에 둡니다. 일단 {{site.data.keyword.Bluemix}} 서비스 인스턴스가 CFEE 영역에 추가(별명 지정)되면 이를 해당 CFEE 영역의 애플리케이션에 바인드할 수 있습니다. 이에 따라 개발자는 CFEE 환경에 배치된 자체 애플리케이션에서 {{site.data.keyword.Bluemix}} 서비스의 방대한 카탈로그를 활용할 수 있으며, 해당 {{site.data.keyword.Bluemix}} 서비스에 대한 액세스 제어도 허용됩니다.

   기존 {{site.data.keyword.Bluemix}} 서비스 인스턴스를 CFEE 영역에 추가할 수 있음은 물론 사용자가 CFEE 영역 내에서 {{site.data.keyword.Bluemix}} 서비스 인스턴스를 새로 작성할 수도 있으며, 이 역시 해당 CFEE 영역에 자동으로 추가됩니다.
  
2. 로컬 Cloud Foundry 서비스 브로커에서 관리되는 서비스 인스턴스(CFEE에 대해 로컬). 이러한 서비스 인스턴스는 두 가지 유형이 될 수 있습니다.
   *  2a. 현재 {{site.data.keyword.cfee_full_notm}} 인스턴스의 Cloud Foundry 마켓플레이스에서 작성된 서비스 오퍼링의 인스턴스. 이 유형의 서비스 인스턴스에는 환경에서 사용 가능한 등록된 서비스 브로커가 필요합니다. 서비스 브로커는 서비스 오퍼링 및 플랜의 카탈로그를 표시하며 해당 서비스 오퍼링에서 인스턴스 작성, 제거, 바인딩 및 바인딩 해제를 가능하게 합니다. 자세한 정보는 Cloud Foundry 문서에서 [서비스 브로커 관리](https://docs.cloudfoundry.org/services/managing-service-brokers.html)를 참조하십시오.
   * 2b. 사용자 제공 서비스 인스턴스. 이 유형의 작성은 사용자 인터페이스가 아니라 명령행 인터페이스(CLI)를 통해 지원됩니다. 그럼에도 불구하고 사용자 제공 서비스 인스턴스가 사용자 인터페이스에 나열됩니다.
   
CFEE의 사용자 인터페이스 또는 CLI(아래 섹션 참조)를 사용하여 CFEE 영역에서 서비스 인스턴스도 작성할 수 있습니다. 이 명령을 사용하여 CFEE에서 서비스 인스턴스를 작성하면 다음과 같은 이중 결과가 발생합니다.
* 공용 {{site.data.keyword.Bluemix}}에서 서비스 인스턴스를 작성합니다.
* 서비스 인스턴스가 작성된 CFEE 영역에 해당 공용 서비스 인스턴스의 별명을 작성합니다.
    
다음 섹션에서는 사용자 인터페이스 및 Cloud Foundry CLI를 사용하여 서비스 인스턴스를 추가, 작성, 액세스 제어 및 바인드하는 방법을 설명합니다.
   

## 모든 CFEE 환경에서 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 보기
{: #viewing-services_across}

[Cloud Foundry 서비스 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/services)로 이동하여 {{site.data.keyword.Bluemix_notm}} 계정의 모든 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스(사용자에게 액세스 권한이 있는)의 통합 보기를 보고 어떤 서비스 인스턴스가 어떤 CFEE 영역에 추가되었는지를 볼 수 있습니다.

이 보기에는 계정에서 사용 가능한 모든 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스가 표시되고, 어떤 서비스 인스턴스가 어떤 CFEE 영역에 추가(별명 지정)되었는지를 나타냅니다. 서비스 인스턴스를 펼쳐서 서비스 인스턴스가 추가된 CFEE 영역을 표시하십시오.  이를 추가로 펼치면 이 서비스 인스턴스가 바인드된 해당 CFEE 영역의 애플리케이션을 볼 수 있습니다.  

이 보기에서 사용자는 서비스 인스턴스가 추가된 CFEE 영역에 배치된 애플리케이션을 바인드할 수도 있습니다. (특정 CFEE 영역에 사용 가능한) 해당되는 서비스에 대한 테이블 행의 맨 오른쪽에 있는 메뉴로 이동하여 **애플리케이션에 바인드**를 선택하십시오.

## CFEE 영역에 기존 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 추가
{: #adding-services-inspace}

{{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 CFEE 영역에 배치된 애플리케이션에 바인드할 수 있습니다.  IBM Cloud 서비스 인스턴스를 CFEE에 배치된 애플리케이션에 바인드하려면 우선 이를 애플리케이션이 배치된 CFEE 영역에 추가해야 합니다. {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 CFEE 영역에 추가하려면 우선 다음이 필요합니다.
* 인스턴스를 추가할 서비스는 Cloud Foundry 서비스일 수 없습니다.  리소스 그룹과 IAM을 지원하는 {{site.data.keyword.Bluemix_notm}} 서비스만 CFEE에 추가(별명 지정)할 수 있습니다. 퍼블릭 Cloud Foundry 조직, 영역 및 역할로 인스턴스화된 서비스는 CFEE에 추가(별명 지정)할 수 없습니다.  {{site.data.keyword.Bluemix_notm}} 서비스가 리소스 그룹을 이용하기 위해 점진적으로 이동합니다.  Cloud Foundry 조직과 영역이 아니라 리소스 그룹을 사용하여 서비스를 이동하면 해당 서버스의 기존 인스턴스를 리소스 그룹으로 마이그레이션할 수 있습니다. 그러면 CFEE에 추가할 수 있습니다.  [Cloud Foundry 서비스 인스턴스를 리소스 그룹으로 마이그레이션](https://cloud.ibm.com/docs/resources/instance_migration.html#migrate)을 참조하십시오.
* {{site.data.keyword.Bluemix_notm}} 서비스를 CFEE 인스턴스가 상주하는 동일한 {{site.data.keyword.Bluemix_notm}} 계정에서 사용할 수 있어야 합니다.
* {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 자체의 _운영자_ 플랫폼 역할 이상이 있어야 합니다. 자세한 정보를 보려면 {{site.data.keyword.Bluemix_notm}} 헤더의 **관리 > 사용자** 메뉴 아래에서 ID 및 액세스 페이지를 참조하여 현재 계정 액세스 정책을 확인하십시오.

기존 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 CFEE 영역에 추가하려면 다음을 수행하십시오.
1. [Cloud Foundry 서비스 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/services)로 이동하십시오.  
2. 목록에서 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 찾고 해당되는 테이블 행의 맨 오른쪽에 있는 메뉴를 호출하십시오.
3. **서비스 추가**를 선택하십시오.
4. _서비스 추가_ 대화 상자에서 서비스가 추가될 CFEE, 조직 및 영역을 선택하고 **추가**를 클릭하십시오.
5. 대상 {{site.data.keyword.Bluemix_notm}} 서비스를 펼쳐서 서비스가 추가된 새 CFEE를 찾으십시오.


또는 추가를 원하는 CFEE 영역 내에서 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 추가할 수도 있습니다.
1. {{site.data.keyword.Bluemix_notm}} [대시보드](https://cloud.ibm.com/dashboard) 또는 [Cloud Foundry 서비스 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/services)에서 애플리케이션을 호스팅하는 Cloud Foundry Enterprise 환경을 찾으십시오.
2. 탐색 분할창에서 **조직**으로 이동하여 애플리케이션이 있는 조직 및 영역을 여십시오.
3. **영역** 탭으로 이동하여 애플리케이션이 포함된 영역을 찾으십시오.
4. 대상 영역 페이지에서 **서비스** 탭으로 이동하여 **서비스 추가**를 클릭하십시오.  그러면 __서비스 추가__ 대화 상자가 열립니다.  페이지에는 {{site.data.keyword.Bluemix_notm}} 계정에서 사용 가능한 서비스 인스턴스가 나열됩니다.
5. CFEE 영역에 추가할 사용 가능한 서비스 인스턴스를 찾아서 이를 선택하십시오. 
6. 서비스 인스턴스가 CFEE 영역에서 사용 가능한 서비스의 목록에 추가됩니다.

   **참고:** {{site.data.keyword.Bluemix_notm}} 서비스를 CFEE 영역에 추가하면 해당 서비스 인스턴스에 대한 별명이 해당 영역에서 작성됩니다. (테이블의 해당되는 서비스 인스턴스 행의 맨 오른쪽에 있는 메뉴에서) 서비스 인스턴스를 CFEE 영역에서 **제거**하면 서비스가 퍼블릭 계정에서 삭제되지 않습니다.  이 조치를 수행하면 단지 특정 CFEE 계정에서 이를 제거하며, 이는 더 이상 해당 CFEE 영역의 애플리케이션에 바인딩하는 데 사용될 수 없습니다.  또한 {{site.data.keyword.Bluemix_notm}} 계정에서 서비스 인스턴스 자체를 삭제하면 CFEE 영역에서 더 이상 해당 서비스를 사용할 수 없습니다. 

## CFEE 영역의 사용자 인터페이스에서 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 작성
{: #creating-services-inspace}

CFEE 영역 내에서 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 작성할 수 있습니다.  {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스의 작성 결과는 다음과 같습니다.
* {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스가 IBM Cloud에서 작성됩니다.  이는 {{site.data.keyword.Bluemix_notm}} [카탈로그](https://cloud.ibm.com/catalog)에서 서비스 인스턴스를 작성하는 것과 동일합니다.
* {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스에 대한 별명이 작성 조치가 시작되는 CFEE 영역에 추가(별명 지정)됩니다. (CFEE 영역의) 별명 서비스 인스턴스는 (IBM Cloud 계정에 있는) 실제 서비스 인스턴스에 대한 참조입니다. 서비스 인스턴스 별명을 통해 개발자는 서비스 인스턴스와의 상호 작용을 위해 모든 인증 정보를 자동으로 처리하여 서비스 인스턴스와 상호 작용할 수 있습니다(예: 애플리케이션에 바인딩) .

CFEE 영역 내에서 서비스 인스턴스를 작성하려면 다음을 수행하십시오.
1. 대상 영역 페이지에서 **서비스** 탭으로 이동하여 **서비스 작성**을 클릭하십시오.  그러면 {{site.data.keyword.cfee_full_notm}}의 **마켓플레이스** 보기가 열립니다.  이 보기에는 두 가지 소스의 서비스 오퍼링이 나열됩니다(__소스__ 열 참조).
   * {{site.data.keyword.Bluemix_notm}} 카탈로그의 오퍼링
   * 로컬 {{site.data.keyword.cfee_full_notm}} 마켓플레이스의 오퍼링
5. 인스턴스화하려는 사용 가능한 서비스 오퍼링을 찾아서 선택하십시오. 
6. 서비스 오퍼링의 소스(IBM Cloud 카탈로그 또는 로컬 CFEE 마켓플레이스)에 따라 다음 중 하나를 진행하십시오.
   * 선택된 서비스 오퍼링이 {{site.data.keyword.Bluemix_notm}} 카탈로그 오퍼링이면 IBM Cloud 서비스 오퍼링 작성 페이지를 **진행**하는 단추가 나타납니다.  이는 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 사용 가능한 페이지와 동일합니다.  이 페이지에서 사용자는 새 서비스 인스턴스, 지역, 플랜의 이름 및 IBM Cloud에서 서비스 작성에 필요한 기타 특성을 제공합니다.  일단 서비스 인스턴스를 작성하는 경우, 이는 IBM Cloud에서 작성되며 자동으로 현재 CFEE 영역에 추가됩니다.
   * 선택된 서비스 오퍼링을 로컬 CFEE 카탈로그에서 가져오는 경우에는 서비스 인스턴스를 **작성**하는 단추가 나타납니다. 서비스 인스턴스가 작성될 현재 CFEE의 조직 및 영역에 대한 프롬프트가 표시됩니다.

## Cloud Foundry CLI를 사용하여 CFEE 영역에서 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스 작성
{: #creating-services_cli}

CFEE 영역의 CLI에서 서비스 인스턴스를 작성할 수 있습니다.  CFEE 영역의 CLI에서 서비스 작성은 해당 영역의 UI에서 서비스 작성과 동일합니다. 즉, 서비스 작성으로 다음의 두 가지 결과가 나타납니다.
* {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스가 IBM Cloud에서 작성됩니다.  이는 {{site.data.keyword.Bluemix_notm}} [카탈로그](https://cloud.ibm.com/catalog)에서 서비스 인스턴스를 작성하는 것과 동일합니다.
* {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스가 작성 조치가 시작된 CFEE 영역에 추가(별명 지정)됩니다.

CFEE 영역에서 서비스 인스턴스 작성과 CLI에서 서비스 인스턴스 작성 간의 차이는 작성된 서비스 인스턴스의 라이프사이클에 있습니다.  CFEE 영역 UI에서 서비스 인스턴스를 작성하는 경우, 작성된 서비스 인스턴스의 라이프사이클은 {{site.data.keyword.Bluemix_notm}} 계정의 서비스 인스턴스 자체에서 제어됩니다.  이는 서비스 플랜에 대한 업데이트가 CFEE 영역이 아닌 {{site.data.keyword.Bluemix_notm}} 계정의 인스턴스에서 제어됨을 의미합니다.  그 대신에 CLI에서 서비스 인스턴스가 작성되는 경우, 서비스의 라이프사이클은 CFEE 영역에서 제어됩니다(서비스가 CFEE 영역에서 업데이트됨).

CLI에서 작성된 서비스 인스턴스는 UI에도 표시되며, 서비스 인스턴스 이름 옆에는 `*`가 표시됩니다.

CLI를 사용한 서비스 인스턴스 작성 단계는 다음과 같습니다.

1. {{site.data.keyword.Bluemix}} 명령행 인터페이스를 다운로드하여 설치하십시오(아직 수행하지 않은 경우). [Cloud Foundry CLI를 다운로드](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")하십시오.

2. {{site.data.keyword.cfee_full}} 개요 페이지로 이동하여 환경의 API 엔드포인트를 찾으십시오.

3. 명령행 인터페이스에서 API 엔드포인트를 CFEE 환경의 엔드포인트로 설정하십시오.

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. CFEE 환경에 로그인하십시오.

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  연합 ID를 사용 중이면 `-sso` 옵션을 사용하십시오.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. 서비스 작성:
`cf create-service` 명령을 실행하여 명령이 실행되는 CFEE 영역에서 서비스 인스턴스를 작성할 수 있습니다. 이 명령을 사용하여 CFEE에서 서비스 인스턴스를 작성하면 다음과 같은 이중 결과가 발생합니다.
    * `instance_name` 매개변수에서 제공하는 이름을 사용하여 공용 {{site.data.keyword.Bluemix}}에 서비스 인스턴스를 작성합니다. 명령에 `instance_name`이 제공되지 않으면 {{site.data.keyword.Bluemix}} 리소스 제어기에서 이름을 제공합니다.   
    * `SERVICE_INSTANCE`로 지정된 이름을 사용하여 명령을 발행한 CFEE 영역에서 공용 서비스 인스턴스의 별명을 작성하십시오.  공용 서비스 인스턴스의 이름은 자동으로 CFEE의 서비스 인스턴스와 동일한 이름이 되지 않습니다. 따라서 공용 서비스 인스턴스와 CFEE의 서비스 인스턴스(공용 인스턴스의 별명) 둘 다에 동일한 이름을 제공하려는 경우 다음 명령으로 `instance_name`과 `SERVICE_INSTANCE`(동일한 값 사용)를 둘 다 지정해야 합니다.

  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"instance_name":"value", "resource_group":"value", "target":"value"}'
  ```
  {: pre}
  
다음 예에서는 "bluemix-us-south region"에 "myCloudant"라는 Cloudant 서비스(표준 플랜)의 인스턴스를 작성하고(공용 서비스와 CFEE 별명 둘 다에 동일한 이름 사용) 특정 리소스 그룹으로 그룹화합니다.

  ```
  cf create-service cloudant standard myCloudant -c '{"instance_name":"myCloudant", "resource_group":"b0daaf6c3ccd4392a266da916cce2e8c", "target":"bluemix-us-south"}'
  ```
  {: pre}

 `create-service` 명령은 특정 유스 케이스를 처리하도록 선택적 매개변수와 함께 실행할 수 있습니다.
 
   * 인스턴스 이름(`instance_name`): 공용 {{site.data.keyword.Bluemix}}에 작성된 서비스 인스턴스의 사용자 정의 이름을 지정할 수 있습니다. `instance_name` 값이 제공되지 않으면 공용에 있는 공용 서비스 인스턴스의 기본 이름은 `SERVICE_INSTANCE`(CFEE의 인스턴스 이름)와 다릅니다. 이 매개변수를 사용하여 공용 서비스 인스턴스의 이름을 제어하는 것이 좋습니다. 또는 원하는 경우 CFEE의 서비스 인스턴스와 동일한 이름을 제공하십시오(공용 인스턴스로 별명 지정).
   * 리소스 그룹(`resource_group`). 새 인스턴스를 배치할 리소스 그룹을 지정할 수 있습니다. "resource_group"(`resource_group`)입니다. 이 매개변수의 값은 리소스 그룹의 이름(_resource group name_)이 아니라 리소스 그룹의 ID(_리소스 그룹 ID_)여야 합니다. `ibmcloud resource groups` 명령을 사용하여 특정 리소스 그룹의 _리소스 그룹 ID_를 찾을 수 있습니다.
   * 대상 배치 지역(`target`). 서비스 인스턴스가 프로비저닝될 지역입니다. 일부 서비스에는 대상을 지정해야 합니다. 그러나 작성 중인 서비스에 필요하지만 대상이 제공되지 않으면 명령이 실패합니다.

선택적으로 해당 매개변수를 포함하는 JSON 파일을 제공할 수 있습니다다. 예를 들어, 다음과 같습니다.
  ```
  {
    "NewCloudant": 
        {  
        "instance_name":"myCloudant",
        "resource_group": "b0daaf6c3ccd4392a266da916cce2e8c",
        "target": "bluemix-us-south"
        }
   }
  ```
  {: pre}
  
그러면 `cf create-service` 명령의 일부로 JSON 파일을 호출할 수 있습니다. JSON 파일의 경로는 절대 경로이거나 상대 경로일 수 있습니다.
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
다음을 실행하여 세부사항을 얻을 수 있습니다.
  ```
  cf create-service -help
  ```
<br>
자세한 정보는 Cloud Foundry 문서의 [cf CLI를 사용하여 서비스 인스턴스 관리](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오.
  
## CFEE의 사용자 인터페이스에서 애플리케이션에 서비스 바인드
{: #bind-services-ui}

{{site.data.keyword.Bluemix_notm}} 서비스 인스턴스의 _운영자_ 플랫폼 역할 이상 및 _기록자_ 서비스 역할 이상이 있는 사용자는 [Cloud Foundry 서비스 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/services) 또는 CFEE 영역의 사용자 인터페이스에 있는 서비스 탭에서 해당 인스턴스를 CFEE 영역에 배치된 애플리케이션에 바인드할 수 있습니다.   

[Cloud Foundry 서비스 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/services)에서 서비스 인스턴스를 애플리케이션에 바인드하려면 다음을 수행하십시오.
1. [Cloud Foundry 서비스 대시보드](https://cloud.ibm.com/dashboard/cloudfoundry/services)로 이동하여 {{site.data.keyword.Bluemix_notm}} 계정에서 사용 가능한 모든 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스의 통합 보기를 보십시오.  보기에는 어떤 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스가 어떤 CFEE 영역에서 사용 가능한지(별명이 지정되는지) 보여주는 용도도 있습니다. 서비스 인스턴스를 펼쳐서 서비스 인스턴스가 추가된 CFEE 영역을 표시할 수 있습니다.  이를 추가로 펼치면 이 서비스 인스턴스가 바인드된 해당 CFEE 영역의 애플리케이션을 볼 수 있습니다. 
2. 바인드할 {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 찾으십시오.
3. 해당되는 보기를 펼쳐서 서비스 인스턴스가 추가된 모든 CFEE 영역을 보십시오. 애플리케이션이 배치된 CFEE 영역에 서비스 인스턴스가 추가되지 않은 경우에는 행의 맨 오른쪽에 있는 메뉴에서 **추가**를 선택하여 대상 CFEE 영역에서 서비스 인스턴스를 사용할 수 있도록 하십시오.
4. 서비스 인스턴스가 사용 가능한 CFEE/영역에 해당하는 행의 맨 오른쪽에 있는 메뉴로 이동하여 **애플리케이션 바인드**를 선택하십시오.
5. __애플리케이션 바인드__ 대화 상자에서 바인드할 애플리케이션을 선택하십시오. 

   **참고:** 바인드할 서비스에서 공용(외부) 및 사설(내부) 엔드포인트를 둘 다 지원([IBM Cloud Service Endpoints](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about) 참조) 및/또는 여러 [서비스 액세스 역할](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am)(바인딩을 통해 수행할 수 있는 서비스 인스턴스에서 허용되는 조치 지정)을 지원하는 경우 다중 단계 대화 상자에서 엔드포인트 유형(공용 또는 사설) 및/또는 특정 서비스 역할을 선택하도록 프롬프트합니다.
6. 이제 애플리케이션이 서비스 인스턴스에 바인드되었습니다.  테이블에서 서비스 인스턴스를 펼쳐서 (특정 CFEE 영역의) 서비스 인스턴스에 바인드되어 있는 애플리케이션을 볼 수 있습니다.


CFEE 영역의 __서비스__ 페이지에서 애플리케이션을 서비스 인스턴스에 바인드하려면 다음을 수행하십시오.

1. 애플리케이션이 배치된 CFEE 사용자 인터페이스를 여십시오.
2. 왼쪽 탐색 분할창에서 **조직**으로 이동하여 애플리케이션이 배치된 조직과 영역을 여십시오.
3. **영역** 탭으로 이동하여 애플리케이션이 포함된 영역을 찾으십시오.
4. 대상 영역 페이지에서 **서비스** 탭으로 이동하십시오.
5. **서비스 인스턴스**의 테이블에서 바인드할 서비스 인스턴스에 해당하는 행의 맨 오른쪽에 있는 __조치__ 메뉴로 이동하여 **바인드**를 선택하십시오.
6. 서비스 인스턴스에 바인드할 애플리케이션을 선택하십시오.

서비스 인스턴스에서 애플리케이션을 바인드 해제하려면 다음을 수행하십시오.

1. 영역의 **서비스** 탭에서 대상 서비스 인스턴스를 펼쳐서 바인드된 앱을 표시하십시오.
2. 애플리케이션의 행에서 조치 메뉴로 이동하여 **서비스 바인드 해제**를 선택하십시오.

## Cloud Foundry CLI를 사용하여 애플리케이션에 서비스 바인드
{: #bind-services-cli}

`cf bind-service` 명령을 사용하여 CFEE의 애플리케이션에 서비스 인스턴스를 바인드할 수 있습니다.

 ```
  cf bind-service APP_NAME SERVICE_INSTANCE -c '{"parameter": "value"}' 
  ```
  {: pre}

다음과 같은 경우 명령에는 특수 매개변수가 필요합니다.

* IBM Cloud 사설 네트워크를 통해 IBM Cloud 서비스에 연결하는 [IBM Cloud Service Endpoints](https://cloud.ibm.com/docs/services/service-endpoint?topic=service-endpoint-about#about)를 지원하는 서비스 인스턴스에 앱을 바인드하는 데 `cf bind-service` 명령을 사용할 수 있습니다. 공용(외부) 및 사설(내부) 엔드포인트 둘 다를 지원하는 서비스에 애플리케이션(CFEE에 배치됨)을 바인드하려면 바인딩에 사용할 엔드포인트를 지정해야 합니다. 다음 예제에서 명령은 "internal" 엔드포인트를 사용하여 서비스를 바인드합니다.

  ```
  cf bind-service myApplication myServiceInstance -c '{"service-endpoints":"internal"}' 
  ```
  {: pre}

* 서비스에 여러 [서비스 액세스 역할](https://cloud.ibm.com/docs/iam?topic=iam-iamconcepts#am)이 있는 경우입니다. 서비스 액세스 역할을 사용하여 바인딩을 통해 수행할 수 있는 서비스 인스턴스에 대해 허용 가능한 조치를 지정합니다. `role` 매개변수를 통해 특정 서비스 액세스 역할을 지정할 수 있습니다. 다음 예제에서 바인딩은 "writer" 서비스 액세스 역할을 지정합니다.

  ```
  cf bind-service myApplication myServiceInstance -c '{"role": "writer"}' 
  ```
  {: pre}
<br>
`cf bind-service` CLI 명령을 사용하는 바인딩 애플리케이션에 관한 자세한 정보는 Cloud Foundry 문서의 [서비스 인스턴스 바인드](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")를 참조하십시오.

## 서비스 가시성
{: #service_visibility}

고객은 CFEE 환경에서 새 IBM Cloud 서비스를 작성할 수 있는 사용자를 제어할 수 있습니다.  또한 기존 IBM Cloud 서비스를 CFEE 영역에 추가할 수 있는 대상도 제어할 수 있습니다.  이 제어 기능은 사용자에 대한 서비스 오퍼링(및/또는 서비스 오퍼링의 인스턴스)의 가시성을 제어함으로써 수행됩니다.

### 서비스 인스턴스 작성에 대한 제어
{: #control_servicecreation}

서비스 작성을 제어하려면, IBM Cloud 계정의 모든 사용자에 대한 또는 특정 Cloud Foundry 조직의 사용자에 대한 IBM Cloud 카탈로그의 서비스 오퍼링에 대한 가시성을 제어해야 합니다.

#### IBM Cloud 카탈로그에 대한 IBM Cloud 계정의 사용자 가시성 제어
{: #creation_accountvisibility}

IBM Cloud 계정 관리자(모든 IAM 사용 서비스에 대한 _관리자_ 역할이 지정된 사용자)는 서비스 또는 서비스 플랜을 지정된 **IBM Cloud 계정**의 모든 사용자를 위한 카탈로그에 표시되지 않도록 방지할 수 있습니다.  계정 관리자는 계정의 모든 사용자에 대한 서비스 또는 서비스 플랜을 블랙리스트에 올려 모든 계정 사용자가 서비스를 사용하지 못하게 할 수 있습니다. 서비스를 블랙리스트에 올리면 해당 계정의 사용자는 IBM Cloud 카탈로그에서 해당 서비스(또는 서비스 플랜)를 볼 수 없습니다.  다음 구문의 `ibmcloud catalog blacklist` 명령을 통해 수행됩니다.

  ```
  ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]
  ```

가장 간단한 양식으로 `catalog backlist` 명령을 사용하여 현재 계정에 있는 모든 사용자에게 서비스 오퍼링((및 모든 플랜)을 표시되지 않게 할 수 있습니다.

  ```
  Ibmcloud catalog blacklist [--add service NAME or entry ID] [--remove service NAME or entry ID] [--service-list] [--output TYPE]

  ```
  {: pre}

일반적으로 전체 서비스 오퍼링뿐만 아니라 특정 지역의 특정 플랜에 대한 가시성을 블랙리스트에 올릴 수 있습니다.  이를 위해 이름이 아닌, 글로벌 카탈로그의 해당 항목에 대한 ID를 사용해야 합니다.   사용자에게 특정 지역의 특정 플랜이 표시되지 않게 하려는 경우 다음을 실행할 수 있습니다.

  ```
  Ibmcloud catalog blacklist -add <catalogEntryID>
  ```
  {: pre}
  
 블랙리스트에서 서비스를 제거하려면 다음을 실행하십시오.
 ```
  Ibmcloud catalog blacklist -remove <catalogEntryID>
  ```
  {: pre}
 
지정된 카탈로그 항목(예: 서비스 플랜 및 해당 배치 지역)의 ID는 다음 명령을 통해 찾을 수 있습니다. 명령은 지정된 서비스에 대한 배치 지역 및 모든 플랜을 리턴합니다.

  ```
  ibmcloud catalog service <thisService>
  ```
  {: pre}

다음을 실행하여 `ibmcloud catalog blacklist`에 대한 세부사항을 확인할 수 있습니다.

  ```
  Ibmcloud catalog blacklist -help
  ```
  {: pre}


#### Cloud Foundry 조직의 사용자에 대한 가시성 제어
{: #creation_orgvisibility}

`cf enable-service-access` 및 `cf disable-service-access` 명령을 사용하여 특정 **Cloud Foundry 조직**의 서비스에 대한 액세스 권한을 제어할 수 있습니다.  여기 액세스에 대한 제어점은 Cloud Foundry(IBM Cloud 계정이 아닌)입니다.  이는 기본 `cf` 명령(`ibmcloud` 명령이 아님)입니다. 

`cf` CLI를 통해 서비스 가시성을 설정할 때 다음을 고려하십시오.

*  `cf` 명령은 특정 Cloud Foundry 조직의 모든 사용자에 대해 서비스 오퍼링(선택적으로, 특정 서비스 오퍼링 플랜)을 사용 및/또는 사용 안함으로 설정합니다.
* 인에이블먼트는 조직 “화이트리스트”를 빌드함으로써 수행됩니다. 즉, 서비스에 대한 액세스 권한이 있는 Cloud Foundry 조직의 포함 목록입니다(앞서 설명한 `ibmcloud` 명령의 "블랙리스트" 접근 방식과는 대조적이며, 계정 사용자에 대한 가시성에서 제외된 서비스 목록을 정의하여 수행함). 이는 서비스를 볼 수 없는 조직을 정의(블랙리스트 작성)하는 것이 아니라 볼 수 있는 조직을 정의(화이트리스트 작성)하는 이 접근 방식으로 카탈로그 서비스에 대한 액세스 제어를 수행함을 의미합니다.
*  해당 조직을 화이트리스트에 추가하여 서비스(또는 서비스 플랜)에 대한 조직 액세스를 제공하는 경우, 실질적으로 다른 모든 조직을 액세스에서 비활성화(제외)시킵니다.  즉, 조직을 화이트리스트에 올리면 다른 모든 조직은 해당 서비스(또는 서비스 플랜)에 액세스할 수 없게 됩니다.
*  조직을 "볼 수 있는" 목록에 추가하기 전에, 모든 조직에 대한 가시성을 사용 안함으로 설정해야 합니다.  플랜이 현재 모든 조직에서 사용 가능한 경우 서비스 플랜에 대한 액세스를 사용 안함으로 설정할 수 없습니다.

위에 설명된 일반 동작에 따라, 다음 명령을 실행하여 서비스에 대한 조직 액세스를 제어하는 것을 권장합니다.

  * 모든 조직에 대한 서비스 플랜에 대해 액세스를 **사용 안함**으로 설정하십시오.
  ```
  cf disable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}
  
  다음 예에서는 MyOrg에 있는 모든 구성원의 Cloudant 서비스 표준 플랜에 대한 액세스를 사용 안함으로 설정합니다.
  ```
  cf disable-service-access cloudant -p standard -o MyOrg
  ```
  {: pre}

  
  * 특정 CFEE 조직에 대한 서비스 플랜에 대해 액세스를 **사용**으로 설정하십시오.  이 조치는 명령에서 특정하게 사용으로 설정되지 않은 다른 모든 조직에 대해 서비스 플랜을 사용 안함으로 설정합니다. 
  ```
  cf enable-service-access SERVICE [-p PLAN] [-o ORG]
  ```
  {: pre}

<br>  
**참고:** 특정 플랜에 대해서만이 아닌, 전체 서비스에 대해 Cloud Foundry 사용 및 사용 안함 서비스 명령을 실행하도록 권장합니다.


### 기존 서비스 인스턴스에 대한 액세스 제어
{: #control_serviceaddition}

CFEE 영역의 개발자는 IBM Cloud 계정에서 사용 가능한 기존의 서비스 인스턴스를 사용할 수 있습니다.  CFEE의 특정 영역 내에서 사용자는 서비스 인스턴스를 해당 영역에 **추가**할 수 있습니다(위의 [기존 서비스 인스턴스 추가](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace) 참조). 서비스 인스턴스를 CFEE 영역에 추가하면 서비스 인스턴스에 대한 별명(참조)이 작성되며 이를 통해, 개발자는 실제 서비스 인스턴스인 것처럼 해당 CFEE 영역으로 배치된 애플리케이션에 서비스 인스턴스를 바인드할 수 있습니다.

계정 관리자는 [IAM 액세스 정책](https://cloud.ibm.com/docs/iam/iamusermanage.html#iamusermanage)을 통해 서비스 인스턴스의 사용을 제어할 수 있습니다.  UI 또는 ibmcloud CLI에서 서비스 인스턴스 자체에 또는 해당 인스턴스가 있는 리소스 그룹에 역할을 지정할 수 있습니다.  개발자가 해당 인스턴스를 영역에 추가할 수 있으려면 서비스 인스턴스에 대한 _뷰어_ 역할 이상이 필요합니다.

CFEE 서비스에 대한 상세한 토론과 데모가 포함된 동영상은 [CFEE 동영상 재생 목록](https://ibm.biz/CFEE-Playlist){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 참조할 수 있습니다.
{:tip}
