---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# 규제 준수 및 규정
{: #compliance}

{{site.data.keyword.cfee_full}}(CFEE)는 PaaS(Platform as a Service)입니다. 이와 같이 클라이언트는 지원할 수 있는 모든 항목에 대해 서비스 인스턴스를 자유롭게 사용할 수 있습니다. CFEE 및 종속 서비스는 가능한 최소한의 개인 데이터에 액세스할 수 있습니다.

명확해야 하지만, CFEE 제어 플레인(UI/API/CLI를 통해)에서 민감한 데이터(예: HIPAA 데이터)를 처리하지 않더라도, {{site.data.keyword.Bluemix_notm}} 계정의 고객이 모든 종속 항목을 관리하고 소유하므로 클라이언트는 CFEE를 책임있게 사용하는지 확인해야 합니다. 

다음 우수 사례를 권장합니다.
*  CFEE(Kubernetes, Cloud Object Storage 및 Compose for PostgreSQL)를 사용하여 작성된 종속 서비스를 수정하지 마십시오.
*  Kubernetes 서비스보다 CFEE 서비스 자체(사용자 인터페이스 또는 명령행 인터페이스)를 통해 CFEE 업데이트 및 관리.

Cloud Foundry 셀이 Kubernetes 노드 상단에 배치되므로 대부분의 CFEE 인프라 및 CFEE에서 실행 중인 애플리케이션을 보유하기 위해 Kubernetes 클러스터가 사용됩니다. 이 클러스터는 고객의 SoftLayer 계정에서 소유하고 관리합니다.

조직, 영역, 사용자 및 역할에 대한 메타데이터를 보유하기 위해 CFEE에 의해 Compose for PostgreSQL 데이터베이스가 사용됩니다. CFEE 인스턴스가 추천한 대로 사용되는 경우 민감한 데이터는 노출되지 않습니다. 그러나 클라이언트가 해당 조직 및 영역을 고객에 대한 개인 또는 민감한 정보를 사용하여 이름을 지정하도록 결정하는 경우에는 PostgreSQL 데이터베이스에 민감한 정보의 다른 유형 또는 HIPAA를 포함할 수 있습니다.

배치, 중지, 시작할 수 있도록 애플리케이션의 드롭릿(droplet)을 유지하기 위해 CFEE에서 Cloud Object Storage 인스턴스를 사용합니다. 이는 Cloud Object Storage 인스턴스가 애플리케이션을 실행하지 않고 단지 해당 이미지만 보유함을 의미합니다. 따라서 Cloud Object Storage 인스턴스가 다음 우수 사례에 사용되는 경우 HIPAA 민감한 정보를 보유하지 않습니다. 고객은 개인 데이터가 해당 애플리케이션(테스트 데이터 등)으로 하드 코딩되지 않도록 확인해야 합니다.
