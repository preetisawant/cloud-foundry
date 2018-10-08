---

copyright:
  years: 2018
lastupdated: "2018-09-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 앱 배치 및 보기
{: #deploy_apps}

명령행 인터페이스 또는 IDE(Integrated Development Environment)를 사용하여 {{site.data.keyword.Bluemix}}에 애플리케이션을 배치할 수 있습니다. 애플리케이션 Manifest를 사용하여 애플리케이션을 배치할 수도 있습니다. 애플리케이션 Manifest를 사용하면 {{site.data.keyword.Bluemix_notm}}에 애플리케이션을 배치할 때마다 지정해야 하는 배치 세부사항의 수를 줄일 수 있습니다.
{:shortdesc}

## Cloud Foundry 명령을 사용하여 애플리케이션 배치
{: #dep_apps}

[Cloud Foundry CLI를 다운로드하여 설치 ](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")하십시오. 

명령행 인터페이스를 설치한 후 다음 단계를 따르십시오.

1. 코드가 있는 디렉토리로 변경하십시오. `cd <your_directory>`
2. {{site.data.keyword.cfee_full}} 개요 페이지로 이동하여 환경의 API 엔드포인트를 찾으십시오.
3. 명령행 인터페이스에서 API 엔드포인트를 사용자 환경의 엔드포인트로 설정하십시오.

  ```
  cf api <api_endpoint>
  ```
  {: pre}

4. 환경에 로그인하십시오.

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  연합 ID를 사용 중인 경우 `-sso` 옵션을 사용하십시오.

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}

  **참고**: 값에 간격이 포함되어 있는 경우 `username`, `org_name` 및 `space_name` 앞뒤에 작은따옴표 또는 큰따옴표를 추가해야 합니다(예: `-o "my org"`).

5.  `<your_new_directory>`에서 `bluemix app push` 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}에 앱을 재배치하십시오. `cf app push` 명령에 대한 자세한 정보는 [애플리케이션 업로드](/docs/starters/upload_app.html)를 참조하십시오.

  ```
  cf push <app_name>
  ```
  {: pre}

6.  `https://<app_url>.<AppDomainName>`.

## 사용자 인터페이스에서 배치된 애플리케이션 보기
{: #view_apps}

특정 영역의 컨텍스트에서 또는 모든 CFEE 인스턴스에서 글로벌로 CFEE에 배치된 애플리케이션을 볼 수 있습니다.

### 특정 CFEE 영역에 배치된 애플리케이션 보기
{: #view_specific}

특정 CFEE 인스턴스의 특정 영역에 배치된 애플리케이션을 보려면 다음을 수행하십시오.
1. [{{site.data.keyword.Bluemix_notm}} 대시보드](https://console.bluemix.net/dashboard/apps/)로 이동하여 조직을 작성할 {{site.data.keyword.cfee_full_notm}}를 여십시오.
2. {{site.data.keyword.cfee_full_notm}} 사용자 인터페이스에서 탐색 분할창에 있는 **조직** 항목으로 이동하여 _조직_ 페이지를 여십시오.
3. 페이지의 맨 위에 있는 **영역** 탭으로 이동하십시오.
4. __영역__ 탭에서 테이블의 영역을 클릭하여 영역의 페이지를 여십시오.
5. __영역__ 페이지에서 **애플리케이션** 탭으로 이동하십시오.
6. _애플리케이션_ 탭에는 해당 영역에 배치된 모든 애플리케이션이 표시됩니다.
선택적으로 애플리케이션을 표시하는 행의 맨 오른쪽에 있는 메뉴에 액세스하여 애플리케이션을 시작, 다시 시작, 중지 또는 삭제할 수 있습니다.

애플리케이션에 대한 행을 펼쳐서 애플리케이션이 바인드된 서비스 인스턴스를 볼 수도 있습니다.

### 모든 CFEE 인스턴스에 배치된 애플리케이션 보기
{: #view_global}

모든 CFEE 인스턴스에 배치된 모든 애플리케이션을 보려면 다음을 수행하십시오.
1. 메뉴 아이콘 ![계정 확인](img/HamburgerMenu.png "메뉴 아이콘을 표시하는 화면 캡처") > **Cloud Foundry**를 클릭하여 Cloud Foundry 대시보드를 여십시오.
2. 왼쪽 탐색 분할창에서 **엔터프라이즈 > 애플리케이션**을 클릭하십시오.
이 보기의 표에는 다음 정보가 표시됩니다.

|요소   |설명 |
|-----------|---------------|
|이름 |애플리케이션의 이름입니다. |
|인스턴스 |애플리케이션의 인스턴스 수입니다. |
|환경 |애플리케이션이 배치된 {{site.data.keyword.cfee_full}} 환경입니다. |
|조직 |애플리케이션이 배치된 조직입니다. |
|영역 |별명이 상주하는 CFEE 인스턴스의 조직입니다. |
|메모리 |애플리케이션에서 사용된 메모리의 양입니다. |
|상태 |애플리케이션의 상태입니다. |
{:caption="표 1. Cloud Foundry 대시보드의 애플리케이션 테이블의 열" caption-side="top"}

선택적으로 애플리케이션을 표시하는 행의 맨 오른쪽에 있는 메뉴에 액세스하여 애플리케이션을 시작, 다시 시작, 중지 또는 삭제할 수 있습니다.
애플리케이션, 환경, 조직 또는 영역 중 하나를 클릭하여 CFEE 사용자 인터페이스의 해당 페이지로 이동할 수 있습니다.

이 보기에는 애플리케이션을 조직, 영역 및/또는 애플리케이션 이름으로 그룹화하는 옵션이 있습니다.  이 기능을 사용하면 여러 이름이 있거나 여러 CFEE 조직 또는 영역에 배치될 수 있지만 동일한 논리 애플리케이션 엔티티에 해당하는 단일 엔티티 애플리케이션으로 통합할 수 있습니다.  예를 들어, 광범위한 프로젝트의 컴포넌트를 나타내거나 여러 전달 단계(예: 개발, 테스트, 프로덕션)에서 배치되지만 동일한 논리 엔티티의 일부로 그룹화하여 보려는 여러 애플리케이션이 있을 수 있습니다.

애플리케이션을 그룹화하려면 페이지의 오른쪽 상단에 있는 **그룹** 드롭 다운으로 이동하십시오.
애플리케이션을 그룹화하면 각 결과 그룹이 테이블에 단일 항목으로 표시됩니다. 해당 행을 펼쳐서 해당 그룹 아래에 애플리케이션을 표시할 수 있습니다.

이 보기에서 다음 조치를 수행할 수 있습니다.
* 테이블의 항목을 테이블 열로 표시되는 특성에 따라 정렬합니다.
* 행의 맨 오른쪽에 있는 별명의 별명 오버플로우 메뉴에 액세스하여 애플리케이션을 특정 별명에 바인드합니다.
* 별명(행)을 펼쳐서 해당 별명에 바인드된 애플리케이션을 확인합니다.
* 행의 맨 오른쪽에 있는 별명의 애플리케이션 오버플로우 메뉴에 액세스하여 애플리케이션을 시작하고 중지합니다.
* 해당 CFEE, 조직 또는 영역과의 링크를 클릭하여 CFEE, CFEE 조직 또는 CFEE 영역으로 이동합니다.

## 애플리케이션 Manifest
{: #appmanifest}

애플리케이션 Manifest에는 `cf push` 명령에 적용되는 옵션이 포함되어 있습니다. 애플리케이션 Manifest를 사용하면 {{site.data.keyword.Bluemix_notm}}에 애플리케이션을 푸시할 때마다 지정해야 하는 배치 세부사항의 수를 줄일 수 있습니다.

애플리케이션 Manifest에는 작성할 애플리케이션 인스턴스 수, 할당할 메모리의 양 및 디스크 할당량, 기타 환경 변수와 같은 옵션을 지정할 수 있습니다. 애플리케이션 Manifest를 사용하여 애플리케이션 배치를 자동화할 수도 있습니다. Manifest 파일의 기본 이름은 `manifest.yml`입니다.

### Manifest 파일에서 지원되는 옵션

다음 표는 애플리케이션 Manifest 파일에서 사용할 수 있는 지원되는 옵션을 보여줍니다. `manifest.yml`이 아닌 다른 파일 이름을 사용하도록 선택한 경우 **cf push** 명령과 함께 `-f` 옵션을 사용해야 합니다. 다음 예에서는 `appManifest.yml`이 파일 이름입니다.

```
cf push -f appManifest.yml
```

|옵션 |설명 |사용법 또는 예 |
|:----------|:--------------|:---------------|
|**buildpack** |사용자 정의 빌드팩의 URL 또는 이름입니다. |`buildpack:` *buildpack_URL* |
|**disk_quota** |애플리케이션에 대해 할당된 디스크 할당량입니다. 기본값은 1G입니다. |`disk_quota: 500M` |
|**domain** |{{site.data.keyword.Bluemix_notm}}의 애플리케이션 도메인 이름입니다. |`domain:` ng.bluemix.net |
|**host** |{{site.data.keyword.Bluemix_notm}}의 애플리케이션 호스트 이름입니다. 이 값은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다. |`host:` *host_name* |
|**name** |{{site.data.keyword.Bluemix_notm}}의 애플리케이션 이름입니다. 이 값은 {{site.data.keyword.Bluemix_notm}} 환경에서 고유해야 합니다. |`name:` *appname* |
|**path** |애플리케이션의 위치입니다. 이 값은 상대 경로 또는 절대 경로일 수 있습니다. |`path:` *path_to_application* |
|**command** | 애플리케이션에 대한 사용자 정의 시작 명령 또는 스크립트 파일을 실행하는 명령입니다. |`command:` *custom_command* `command:` *bash ./run.sh* |
|**memory** | 애플리케이션에 대해 할당할 메모리의 양입니다. 기본값은 1G입니다. |`memory: 512M` |
|**instances** | 애플리케이션에 대해 작성될 인스턴스 수입니다. |`instances: 2` |
|**timeout** |애플리케이션을 시작하는 데 사용되는 최대 시간(초)입니다. 기본값은 60초입니다. |`timeout: 80` |
|**no-route** |애플리케이션이 백그라운드에서 실행 중인 경우 라우트가 애플리케이션에 지정되지 않도록 하는 부울 값입니다. 기본값은 **false**입니다. |`no-route: true` |
|**random-route** |애플리케이션에 랜덤 라우트를 지정하는 부울 값입니다. 기본값은 **false**입니다. |`random-route: true` |
|**services** |애플리케이션에 바인딩할 서비스입니다. |`services: - mysql_maptest` |
|**env** |애플리케이션에 대한 사용자 정의 환경 변수입니다. |`env: DEV_ENV: production` |
{: caption="표 2. Manifest YAML 파일에서 지원되는 옵션" caption-side="top"}

### 샘플 manifest.yml 파일
{: #sample}

다음 예는 {{site.data.keyword.Bluemix_notm}}에서 기본 제공 커뮤니티 Node.js 빌드팩을 사용하는 Node.js 애플리케이션에 대한 Manifest 파일을 보여줍니다.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{: codeblock}
