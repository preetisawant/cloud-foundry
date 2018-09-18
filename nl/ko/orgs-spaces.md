---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 조직 및 영역 작성
{: #create_orgs}

{{site.data.keyword.cfee_full}}의 앱은 특정 범위 내로 범위가 지정됩니다. 결국 영역이 특정 조직 내에 존재합니다. 조직의 구성원이 할당량 플랜, 앱, 서비스 인스턴스 및 사용자 정의 도메인을 공유합니다. 조직 및 영역이 작성된 후 해당 조직 및 영역에 대한 액세스 및 제어 레벨을 판별하는 특정 역할을 사용하여 사용자를 추가할 수 있습니다. 조직을 작성하고 해당 조직에 관리자를 지정하려면 {{site.data.keyword.cfee_full_notm}} 서비스 및 사용자가 추가되는 특정 환경 인스턴스 모두에 대한 관리자 역할이 필요합니다. 이러한 권한은 {{site.data.keyword.Bluemix}} 헤더의 **관리 > 사용자** 메뉴 아래의 _ID 및 액세스_ 페이지에서 설정됩니다.
{: shortdesc}

## 조직 작성
{: #create-org}

{{site.data.keyword.cfee_full_notm}}에서 조직을 작성하려면 다음을 수행하십시오.

1. [{{site.data.keyword.Bluemix_notm}} Cloud Foundry 환경 대시보드](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments){: new_window}로 이동하여 조직을 작성할 {{site.data.keyword.cfee_full_notm}}를 여십시오.
2. {{site.data.keyword.cfee_full_notm}} 사용자 인터페이스에서 탐색 분할창에 있는 **조직** 항목으로 이동하여 _조직_ 페이지를 여십시오.
3. **새로 추가**를 클릭하십시오.
4. 새 조직의 **이름**을 입력하십시오.
5. **관리자** 아래에서 하나 이상의 사용자를 식별하십시오. 관리자 역할이 있는 사용자만 해당 조직에 구성원을 추가할 수 있습니다.
6. **할당량 플랜** 아래에서 사용 가능한 플랜을 선택하십시오. 할당량 플랜은 조직의 앱에 사용 가능한 메모리, 호스팅되는 최대 앱 인스턴스 수 및 최대 라우트 수를 제한합니다.

조직 관리자는 조직 멤버십 관리 이외에 조직 내에서 영역을 작성, 보기, 편집 또는 삭제할 수 있습니다. 조직 관리자는 조직의 사용량 및 할당량을 보고, 사용자를 조직에 초대하고, 조직의 멤버십 및 역할을 관리하고, 조직에 대한 사용자 정의 도메인을 관리할 수 있습니다.

조직 내에 영역을 작성하려면 _조직_ 페이지에서 **영역** 탭으로 이동하여 **새로 추가**를 클릭하십시오. 조직의 구성원은 조직 내에 자체 영역을 작성하고 관리할 수도 있습니다. Cloud Foundry 역할에 대한 자세한 정보는 [Cloud Foundry 액세스](https://console.bluemix.net/docs/iam/cfaccess.html#cfroles){: new_window}를 참조하십시오.

**참고**: {{site.data.keyword.cfee_full_notm}} 내의 조직 및 영역에 액세스하려면 사용자에게 환경 자체에 액세스할 수 있는 권한이 있어야 합니다. {{site.data.keyword.cfee_full_notm}}에 액세스할 수 있는 권한이 없으면 해당 조직 및 영역의 멤버십과 역할에 관계없이 사용자 환경 내의 조직 및 영역에 액세스할 수 없습니다.
