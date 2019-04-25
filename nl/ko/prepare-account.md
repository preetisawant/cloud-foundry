---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 계정 준비
{: #prepare}

CFEE 인스턴스는 IBM Cloud 계정에 청구되는 인프라 리소스(IBM Container 서비스의 Kubernetes 작업자 노드)에 배치됩니다. 즉, CFEE 인스턴스가 작성된 IBM Cloud 계정이 유료 계정(구독 계정 또는 구독 계정)이어야 합니다.  CFEE 인스턴스를 작성하려는 IBM Cloud 계정이 평가판 계정이면 CFEE 인스턴스를 작성하려고 시도할 때 계정을 업그레이드하도록 요청됩니다.  IBM Cloud 계정이 평가판 계정에서 종량과금제 또는 구독 계정으로 업그레이드되면 IBM Cloud 계정이 SoftLayer 계정(이를 통해 인프라 리소스를 작성할 수 있음)에 연결됩니다. 자세한 정보는 [계정 유형](https://cloud.ibm.com/docs/account/index.html#accounts)을 참조하십시오. 해당 인프라 리소스의 비용은 IBM Cloud 송장에 표시됩니다.

## IBM Cloud 계정이 CFEE 인스턴스를 작성할 수 있는지 여부를 확인하는 방법
{: #account-check}

IBM Cloud 배너의 오른쪽 상단 모서리에 있는 계정 정보를 확인하여 IBM Cloud 계정이 평가판 또는 유료 계정인지와 SoftLayer 계정에 연결되었는지 여부를 판별할 수 있습니다.

아래 예에서는 _Mary Smith_ 사용자가 평가판 계정인 IBM Cloud 계정 _MyCompany_에 로그인되어 있습니다.
![계정 확인](img/AccountExample_1.png)

아래 예에서 동일한 IBM Cloud 계정 _MyCompany_가 유료 계정으로 업그레이드되었습니다.  이제 업그레이드의 결과로 계정이 SoftLayer 계정 _1684806_에 연결됩니다.  두 계정 모두 "계정" 필드에 표시됩니다.
![계정 확인](img/AccountExample_2.png)

IBM Cloud 계정이 평가판 계정이면 CFEE 인스턴스를 작성하려고 시도할 때 계정을 업그레이드하라는 프롬프트가 표시됩니다. 아래 표시된 화면을 참조하십시오.

![계정 확인](img/UpgradeAccountPage_1.png)

## IBM Cloud 계정을 업그레이드하는 대신 SoftLayer 계정 사용
{: #account-linkswitching}

IBM Cloud 계정의 관리자 역할이 있는 경우 IBM Cloud 계정을 업그레이드하지 않고 CFEE 인스턴스를 작성하는 데 SoftLayer 계정을 사용할 수 있습니다.


**경고:** 지금 SoftLayer 계정을 사용하고 나중에 IBM Cloud 계정을 업데이트하는 경우(종량과금제 또는 구독 계정으로), 업데이트된 IBM Cloud 계정은 나중에 인프라 리소스를 작성할 때 (지금 설정하는 인증 정보의) Softlayer 계정을 계속 사용할 수 있습니다. 또한 나중에 Cloud Foundry Enterprise Environment를 작성하기 위해 다른 SofLayer 계정을 사용하는 경우 IBM Cloud 계정의 사용자가 지금 인증 정보를 설정한 SoftLayer 계정으로 작성된 인프라 리소스에 액세스하지 못할 수도 있습니다. 대신 IBM Cloud 계정을 업그레이드하십시오.

IBM Cloud 계정을 업그레이드하지 않고 SoftLayer 계정을 사용하려면 다음을 수행하십시오(예시는 아래 화면 참조).
1. IBM Cloud 계정이 업그레이드되지 않은 경우 표시되는 화면에서 **SoftLayer 계정 사용**을 클릭하십시오.
2. SoftLayer 계정의 **사용자 이름** 및 **API 키**를 입력하십시오. SoftLayer의 사용자 이름 및 API 키를 가져오려면 [SoftLayer 콘솔](https://control.softlayer.com)에 액세스하십시오. SoftLayer에 로그인한 후 {{site.data.keyword.Bluemix_notm}} 계정에 연결하려는 계정을 선택하십시오. 계정을 선택하면 해당 계정의 프로파일 페이지가 열립니다. 페이지의 끝까지 아래로 스크롤하여 계정의 사용자 이름 및 API 키를 찾으십시오. API 키가 없는 경우 계정 소유자이면 이를 생성할 수 있습니다. 계정 소유자가 아니면 계정 소유자에게 API 키를 생성하도록 요청하십시오.
3. **인증 정보 설정**을 클릭하십시오.

![계정 확인](img/UpgradeAccountPage_2.png)

**참고:** IBM Container 서비스에서 일반 Kubernetes 클러스터를 작성하려면 SoftLayer 계정에 충분한 권한이 있어야 합니다. 그렇지 않으면 SoftLayer 계정 관리자 또는 SoftLayer 계정에 대한 액세스를 부여한 사용자에게 해당 추가 권한을 부여하도록 요청하십시오.
