---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 권한
{: #permissions}

{{site.data.keyword.cfee_full}} 서비스의 인스턴스를 작성하고 작업하기 전에 관리자 및 나머지 팀 구성원의 권한이 올바르게 설정되어야 합니다.

## 새 환경을 작성하는 데 필요한 권한
{: #perm-creating}

{{site.data.keyword.cfee_full_notm}} 서비스의 새 인스턴스를 작성하려면 인스턴스가 작성될 계정의 관리자가 사용자에게 액세스 정책을 부여해야 합니다.

* {{site.data.keyword.Bluemix}} 계정의 하나 이상의 리소스 그룹에 대한 액세스. 리소스 그룹을 사용하면 리소스를 사용자 정의된 그룹으로 구성하여 해당 리소스에 대한 액세스 제어를 용이하게 할 수 있습니다. 새 환경 인스턴스를 작성할 때 리소스 그룹에 대한 프롬프트가 표시됩니다.

* 환경이 지정되는 리소스 그룹의 {{site.data.keyword.cfee_full_notm}} 서비스에 대한 관리자 또는 편집자 역할. {{site.data.keyword.cfee_full_notm}} 서비스의 관리자 또는 편집자 역할이 있는 사용자는 환경을 작성하고 삭제할 수 있습니다. 관리자 역할이 있는 사용자만 사용자를 {{site.data.keyword.cfee_full_notm}} 인스턴스에 지정하고 지정된 역할을 해당 인스턴스의 사용자로 변경할 수 있습니다.

* CFEE 서비스의 필수 종속 항목인 IBM Cloud Object Storage 서비스에 대한 관리자 또는 편집자 역할. IBM Cloud Object Storage 서비스의 인스턴스는 ICFEE 애플리케이션 컨테이너(예: 업로드된 애플리케이션 패키지, 빌드팩 및 컴파일된 실행 파일) 작성 중에 생성된 데이터를 저장하는 데 사용됩니다.

* Compose for PostgreSQL 서비스의 인스턴스는 CFEE 서비스의 필수 종속 항목입니다. Compose for PostgreSQL은 CFEE 인스턴스에 대한 Cloud Foundry 데이터를 저장하는 데 사용됩니다(예: 애플리케이션 배치 감사, 이벤트 시작 및 중지, CFEE 사용자 멤버십, 조직, 영역, 애플리케이션 및 서비스 연결의 레코드 유지). 해당 Compose for PostgreSQL 서비스 인스턴스는 퍼블릭 Cloud Foundry 조직(CFEE 조직과 관련이 없음)에 배치됩니다. Compose for PostgresSQL 인스턴스가 배치된 퍼블릭 Cloud Foundry 조직은 특정 이름 **_cfee-`<accountId>`_**를 사용합니다. 여기서 "accountId"는 CFEE가 Compose for PostgreSQL 서비스 인스턴스와 함께 프로비저닝될 IBM Cloud 계정의 ID입니다. 계정 소유자가 CFEE 인스턴스를 작동할 때 퍼블릭 Cloud Foundry 조직이 자동으로 작성됩니다. 계정 소유자가 아닌 사용자가 CFEE 인스턴스를 작성하려고 시도하면 조직이 자동으로 작성되지 않고 CFEE 작성 시도가 실패합니다. 따라서 CFEE 인스턴스를 작성하지만 계정 소유자가 아닌 IBM Cloud 계정의 사용자는 **관리자 역할**이 있는 **_cfee-`<accountId>`_** 퍼블릭 Cloud Foundry 조직에 추가되어야 합니다.   

   IBM Cloud 계정의 사용자를 _cfee-`<accountId>`_ 퍼블릭 조직에 추가하려면 다음을 수행하십시오.
    * [**관리 > 계정 > Cloud Foundry 조직**](https://console.bluemix.net/account/organizations)으로 이동하십시오.
    * **_cfee-`<accountId>`_** 조직을 클릭하십시오.
    * 페이지의 맨 위에 있는 **사용자** 탭으로 이동하십시오.
    * CFEE 인스턴스를 작성해야 하는 사용자를 찾고 해당 사용자에 대한 **관리자** 선택란을 클릭하십시오. CFEE 인스턴스를 작성할 수 있도록 하려는 사용자가 목록에 없는 경우 테이블 위에 있는 **사용자 추가 또는 초대**를 클릭하여 사용자를 **_cfee-`<accountId>`_** 조직에 추가하거나 초대하십시오.

   **참고**: IBM Cloud 계정 소유자가 CFEE 인스턴스를 작성할 때 **_cfee-`<accountId>`_** 퍼블릭 조직이 내재적으로 자동 생성되지만 계정 소유자(및 계정 소유자만) CFEE 인스턴스를 작성할 필요 없이 대신 퍼블릭 Cloud Foundry 조직을 수동으로 작성할 수 있습니다. IBM Cloud 계정 소유자가 **관리 > 계정 > Cloud Foundry 조직** 페이지에서 수동으로 _cfee-`<accountId>`_ 조직을 작성할 수 있습니다. 계정 소유자이고 퍼블릭 _cfee-`<accountId>`_ 조직을 작성하는 경우 _cfee-`<accountId>`_와 정확히 동일하게 이름을 지정하는지 확인하십시오. IBM Cloud 계정 ID를 찾으려면 [**관리 > 계정 > Cloud Foundry 조직**](https://console.bluemix.net/account/organizations) 페이지로 이동하여 브라우저에서 사용 가능한 페이지 URL을 확인하십시오. IBM Cloud 계정 ID는 페이지 URL에서 `=` 다음에 오는 영숫자 값 세트입니다. 또는 __관리 > 계정 > 사용자__로 이동하여 페이지의 오른쪽 상단 모서리에 있는 _계정_ 이름 왼쪽의 도구 팁 위로 마우스를 이동할 수 있습니다.
   
* 환경이 지정되는 리소스 그룹의 {{site.data.keyword.Bluemix_notm}} Container 서비스에 대한 관리자 또는 편집자 역할. {{site.data.keyword.cfee_full_notm}}의 인스턴스는 {{site.data.keyword.Bluemix_notm}} Container 서비스에서 제공되는 컨테이너 클러스터 인프라에 배치됩니다. {{site.data.keyword.cfee_full_notm}} 서비스의 인스턴스를 작성할 때 서비스에서 자동으로 {{site.data.keyword.cfee_full_notm}}가 배치되는 Kubernetes 클러스터를 작성합니다. 해당 클러스터 인프라를 작성하려면 IBM Container 서비스(특히, 환경이 지정되는 리소스 그룹의 IBM Container 서비스)에 대한 액세스가 필요합니다.

{{site.data.keyword.cfee_full_notm}} 인스턴스를 작성하는 데 필요한 액세스 정책이 있는지 확인하려면 다음을 수행하십시오.
1. {{site.data.keyword.Bluemix_notm}} 헤더의 [**관리 > 계정 > 사용자**](https://console.bluemix.net/iam/#/users) 메뉴로 이동하여 **ID & 액세스** 페이지를 여십시오.
2. 액세스 정책 탭에서 환경을 작성 중인 사용자를 클릭하십시오.
3. 환경을 작성 중인 사용자에 대한 액세스 정책이 이전에 설명된 정책과 일치하는지 확인하십시오.

다음 화면은 사용자가 {{site.data.keyword.cfee_full_notm}} 인스턴스를 작성할 수 있는 {{site.data.keyword.Bluemix_notm}}의 ID 및 액세스 페이지에 표시되는 액세스 정책을 보여줍니다. 

![액세스 정책](img/AccessPolicies_Creator.png)

## 환경에 대해 작업하는 데 필요한 권한
{: #perm-working}

{{site.data.keyword.cfee_full_notm}}의 인스턴스에 대해 작업하려면 사용자가 다음과 같아야 합니다.
1. {{site.data.keyword.cfee_full_notm}} 인스턴스가 작성된 {{site.data.keyword.Bluemix_notm}} 계정의 구성원이어야 합니다.
2. 계정 관리자가 다음 _액세스 정책_을 부여해야 합니다(현재 계정 액세스 정책을 확인하려면 {{site.data.keyword.Bluemix_notm}} 헤더의 [**관리 > 계정 > 사용자**](https://console.bluemix.net/iam/#/users) 메뉴 아래의 _ID 및 액세스_ 페이지 참조).
  - {{site.data.keyword.Bluemix_notm}} 계정의 하나 이상의 리소스 그룹에 대한 액세스. 리소스 그룹을 사용하면 리소스를 사용자 정의된 그룹으로 구성하여 해당 리소스에 대한 액세스 제어를 용이하게 할 수 있습니다. 새 환경 인스턴스를 작성할 때 리소스 그룹에 대한 프롬프트가 표시됩니다.
  - 사용자에게 환경 인스턴스가 작성된 리소스 그룹의 {{site.data.keyword.cfee_full_notm}} 서비스에 대한 액세스가 지정되어야 합니다. {{site.data.keyword.cfee_full_notm}} 인스턴스의 사용자에 대한 액세스 및 제어 레벨은 액세스 정책에 부여된 역할에 따라 다릅니다.
     - 관리자 또는 편집자 역할에 지정된 사용자는 조직을 작성하고, 조직 및 영역에 관리자를 지정하고, 환경 내의 모든 조직 및 영역에 대한 전체 권한을 보유하고, 클라우드 제어기 API를 사용하여 운영 조치를 수행할 수 있습니다. 이러한 사용자에게는 Cloud Foundry _사용자 계정 및 인증 범위_의 _cloud_controller.admin 범위_가 자동으로 부여됩니다.
     - 뷰어 역할이 지정된 사용자는 기본 {{site.data.keyword.Bluemix_notm}} 대시보드에서 해당 환경을 볼 수 있으며 해당 사용자 인터페이스를 열 수 있습니다. 환경 내의 특정 조직 및 영역에 대한 사용자 액세스 권한은 특정 조직 및 영역의 관리자가 지정하는 해당 조직 및 영역 역할에 따라 조정됩니다. 자세한 정보는 [조직에 사용자 추가](add-users.html)를 참조하십시오.

이 이미지는 {{site.data.keyword.cfee_full_notm}}에 액세스하는 데 필요한 최소 액세스 정책을 보여줍니다({{site.data.keyword.Bluemix_notm}} _ID 및 액세스_ 페이지에 표시되는 대로).

![액세스 정책](img/AccessPolicies_User.png)

