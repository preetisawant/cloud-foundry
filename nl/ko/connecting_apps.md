---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}

# 연결 관리
{: #connect_app}

서비스 대시보드의 **연결** 탭에서 서비스를 기존의 또는 새 {{site.data.keyword.Bluemix}} 애플리케이션에 연결할 수 있습니다. Cloud Foundry 서비스를 Cloud Foundry 애플리케이션에 연결하면 서로 간에 바인딩이 작성되며, **연결** 탭에서 연결을 언바인딩하거나 연결을 더 추가하거나 연결을 삭제할 수 있습니다.

그러나 {{site.data.keyword.Bluemix_notm}} Identity and Access Management(IAM)에서 관리하는 서비스 인스턴스를 Cloud Foundry 애플리케이션에 연결할 때는 IAM에서 관리하는 서비스의 별명이 지정된 바인딩 정보로 대응되는 Cloud Foundry 영역에서 자동으로 작성됩니다. 이 별명은 IAM-관리 서비스의 Cloud Foundry 서비스 인스턴스로서 표시됩니다.
{:shortdesc}

## 별명의 개념
{: #what_is_alias}

별명은 리소스 그룹 내의 IAM-관리 서비스 및 조직이나 영역 내의 Cloud Foundry 애플리케이션 간의 연결입니다. {{site.data.keyword.Bluemix_notm}} 콘솔에서 연결(별명)은 Cloud Foundry 서비스 인스턴스로서 표시됩니다. 연결을 표시하는 서비스 인스턴스를 수정하여 별명을 관리할 수 있습니다.

별명은 원격 리소스에 대한 참조를 보유하고 플랫폼에서 인스턴스의 재사용 및 상호 운용성을 가능하게 하는 기호 링크와 유사합니다. 예를 들어, 리소스 그룹에서 서비스의 인스턴스를 작성한 후에 해당 지역의 조직이나 영역에서 별명을 작성함으로써 사용 가능한 Cloud Foundry 지역에서 이를 재사용할 수 있습니다.

다음 규칙이 별명에 적용됩니다.

* 별명에 대한 추가 비용은 없습니다. 단, 각각의 별명은 Cloud Foundry 조직에서 사용자 할당량에 대해 계수됩니다.
* {{site.data.keyword.Bluemix_notm}} 콘솔에서 Cloud Foundry 영역당 하나의 별명만 작성이 가능합니다. 그러나 {{site.data.keyword.Bluemix_notm}} CLI를 사용하면 영역당 둘 이상의 별명을 작성할 수 있습니다. 자세한 정보는 [리소스 그룹 및 리소스를 관리하는 명령](/docs/cli/reference/bluemix_cli/bx_cli.html#commands-for-managing-resource-groups-and-resources)을 참조하십시오.
* 권한이 있는 경우에는 동일한 계정의 지역 및 영역, 조직에서 IAM-관리 서비스 및 Cloud Foundry 애플리케이션 간에 다중 연결을 작성할 수 있습니다.
* IAM-관리 서비스 인스턴스에서 서로 다른 Cloud Foundry 앱으로 동일 영역에서 작성된 다중 연결은 동일한 별명을 사용하게 됩니다.
* IAM-관리 서비스 인스턴스를 언바인딩해도 별명을 표시하는 Cloud Foundry 서비스 인스턴스는 삭제되지 *않습니다*.
* IAM-관리 서비스 인스턴스가 연결된 Cloud Foundry 애플리케이션를 삭제해도 별명을 표시하는 Cloud Foundry 인스턴스는 삭제되지 *않습니다*.
* IAM-관리 서비스 인스턴스를 삭제하면 별명을 표시하는 Cloud Foundry 인스턴스가 *삭제됩니다*.

## IAM-관리 서비스 및 Cloud Foundry 앱 간의 연결(별명) 작성
{: #creating_alias}

IAM-관리 서비스 인스턴스를 Cloud Foundry 애플리케이션에 연결하려면 다음을 수행하십시오.

1. 대시보드로 이동하십시오.

2. 앱의 이름을 클릭하여 앱 세부사항 보기를 여십시오.

3. **기존 항목 연결**을 클릭하고 기존 Cloud Foundry 앱에서 선택하십시오. 또는 **연결 작성**을 클릭하여 연결할 Cloud Foundry 앱을 작성하십시오.

4. **연결에 대한 액세스 역할**을 지정하십시오. 이 값은 IAM 서비스 액세스 역할을 설정합니다. 자세한 정보는 [IAM 액세스](/docs/iam/users_roles.html#userroles)를 참조하십시오.

5. 선택사항으로, IAM이 사용자 대신 고유 값을 생성하도록 허용하거나 기존 서비스 ID를 제공함으로써 **연결에 대한 서비스 ID**를 제공할 수 있습니다. 자세한 정보는 [서비스 ID 작성 및 관리](https://console.stage1.bluemix.net/docs/iam/serviceid.html#serviceids)를 참조하십시오.

6. **작성**을 클릭하십시오.

## 별명 보기

IAM-관리 서비스 및 Cloud Foundry 앱 간에 연결이 이루어지면, 연결된 Cloud Foundry 앱의 **연결** 탭에 별명이 표시됩니다. 또한 별명은 실행 중인 Cloud Foundry 서비스 인스턴스로서 대시보드에 표시되며, 이를 열 때만 **연결** 탭이 포함됩니다.

1. 대시보드로 이동하십시오.
2. **Cloud Foundry 서비스** 테이블에서 서비스 인스턴스의 이름을 클릭하여 서비스 세부사항 보기를 여십시오. **연결** 탭만 있는 경우, 이는 별명입니다.

## 별명 삭제

별명을 삭제하는 가장 손쉬운 방법은 IAM-관리 서비스 인스턴스를 삭제하는 것입니다. 그러나 IAM-관리 서비스 인스턴스는 그대로 유지하고 그 대신에 별명을 직접 삭제할 수 있습니다.

1. 대시보드로 이동하십시오.
2. **Cloud Foundry 서비스** 테이블에서 서비스 인스턴스의 이름을 클릭하여 서비스 세부사항 보기를 여십시오. **연결** 탭만 있는 경우, 이는 별명입니다.
3. 인스턴스를 삭제하십시오.

## 여러 Cloud Foundry 서비스 간 연결 작성
{: #cf}

Cloud Foundry 서비스를 다른 Cloud Foundry 서비스에 바인드하는 작업에 대한 세부사항은 [다른 서비스의 서비스 사용](../apps/reqnsi.html#add_service)을 참조하십시오.
