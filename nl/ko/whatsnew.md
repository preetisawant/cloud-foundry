---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment의 새로운 기능

이 문서는 {{site.data.keyword.cfee_full_notm}} 서비스의 이 날짜까지 릴리스된 각 버전의 새로운 기능에 대해 설명합니다.


## 버전 2.0.1
{: #v201}

_릴리스 날짜:_ 2019년 01월 10일

다음 변경사항은 {{site.data.keyword.cfee_full_notm}} 서비스(CFEE)의 버전 2.0.1에서 릴리스되었습니다. CFEE 버전을 업데이트하려면 CFEE 사용자 인터페이스에서 _업데이트 및 스케일링_ 페이지로 이동하십시오.

* 사용자 정의 도메인이 제대로 작동하지 못하게 하는 문제점이 해결되었습니다.
* 새 메트릭을 검색하는 동안 조직 메트릭을 사용할 수 없게 만드는 문제점이 해결되었습니다.


## 버전 2.0.0
{: #v200}

_릴리스 날짜:_ 2018년 12월 13일

다음 변경사항은 {{site.data.keyword.cfee_full_notm}} 서비스(CFEE)의 버전 2.0.0에서 릴리스되었습니다. CFEE 버전을 업데이트하려면 CFEE 사용자 인터페이스에서 _업데이트 및 스케일링_ 페이지로 이동하십시오.

* CFEE 버전 업데이트 복원성 향상.
* CFEE 인스턴스의 작동 가용성 및 복원성 개선사항.
* 서버에서 인증된 클라이언트에만 애플리케이션 액세스 권한을 부여할 수 있도록 하여 애플리케이션에 더 안전하게 액세스하는 데 사용하는 클라이언트 측 인증서.
* CFEE 인스턴스가 작성되면 지원되는 Kubernetes 클러스터와 Cloud Object Storage 서비스 인스턴스가 이제 CFEE 서비스 인스턴스와 동일한 리소스 그룹에 작성됩니다("기본값" 리소스 그룹에 작성되지 않음).
* 보안 패치.
* `ibmcloud cfee` CLI의 개선사항:
    * CFEE 페이지에서 IBM Cloud 서비스 인스턴스를 작성하여 해당 CFEE 공간에 추가하는 새 명령(`ibmcloud cfee service-create`, `ibmcloud cfee service-alias-create`).
    * CFEE의 용량을 스케일링하는 새 명령(`ibmcloud cfee scale-up`, `ibmcloud cfee scale-down`).
    * CFEE 인스턴스를 관리하는 명령의 개선사항(`ibmcloud cfee environments`).
    
      ibmcloud CLI(`ibmcloud update`)를 업데이트하여 해당 명령 개선사항에 액세스하고 `ibmcloud cfee -help`를 실행하여 자세한 정보를 확인하십시오.
      
**참고**: CFEE 인스턴스를 버전 2.0.0으로 업데이트하려면 제어 플레인과 셀을 모두 업데이트하는 단일 _업데이트_ 조치만 수행하면 됩니다. CFEE 제어 플레인과 셀을 개별적으로 업데이트할 필요가 없습니다.


## 버전 1.1.2
{: #v112}

_릴리스 날짜:_ 2018년 12월 07일

다음 변경사항이 {{site.data.keyword.cfee_full_notm}} 서비스의 버전 1.1.2에 릴리스되었습니다.
* 첸나이(che01)와 밀라노(mil01)의 새로운 데이터 센터는 이제 CFEE 인스턴스를 프로비저닝하는 데 사용할 수 있습니다.
* 보안 패치.

## 버전 1.1.1
{: #v111}

_릴리스 날짜:_ 2018년 11월 28일

다음 변경사항이 {{site.data.keyword.cfee_full_notm}} 서비스의 버전 1.1.1에 릴리스되었습니다.
* 보안 패치.
   
## 버전 1.1.0
{: #v110}

_릴리스 날짜:_ 2018년 11월 16일

다음 변경사항이 {{site.data.keyword.cfee_full_notm}} 서비스의 버전 1.1.0에 릴리스되었습니다.

* 새 기능:
   * CFEE 인스턴스는 IBM Cloud 계정에서 전용으로 사용하는 인프라에서 호스팅하는 [가상-전용](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) Kubernetes 작업자 노드에서 프로비저닝할 수 있습니다.
   * 도쿄(tok05)의 새 데이터 센터는 CFEE 인스턴스를 프로비저닝하는 데 사용할 수 있습니다.
   * CFEE 인스턴스를 새 버전으로 [업데이트](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update).
   * Cloud Foundry 셀을 추가하거나 삭제하여 CFEE 인스턴스의 용량 [스케일링](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale).
   * 자동으로 구성된 IBM Cloud 활동 트래커 서비스 인스턴스와의 통합을 통해 Cloud Foundry 활동 [감사](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing).
   * 자동으로 구성된 IBM Cloud 로그 분석 서비스 인스턴스를 통해 Cloud Foundry [로그 이벤트](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging) 지속.
   * CFEE 컴포넌트의 운영 상태를 표시하는 상태 확인 보기.
   * 명령행 인터페이스(CLI)에서 CFEE 관련 조치를 수행하는 새 명령:
     * 명령행 인터페이스에서 CFEE 인스턴스를 작성하고, CFEE를 프로비저닝할 수 있는 사용 가능 데이터 센터 목록을 가져오고, 작성 중인 CFEE의 프로비저닝 상태를 확인하는 `ibmcloud cfee create`, `ibmcloud cfee create-locations` 및 `ibmcloud cfee create-status` 명령.
     * CFEE 인스턴스를 작성하는 데 필요한 권한을 검색하고 설정하는 `ibmcloud cfee create-permission-get` 및 `ibmcloud cfee create-permission-set`  [명령](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating). 이 명령은 CFEE 서비스 및 필수 지원 서비스에 대한 권한 설정을 집계하고 간소화합니다.
     * IBM Cloud 계정의 사용자를 위한 IBM Cloud 서비스의 [가시성 제어](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)를 간소화하는 `ibmcloud catalog blacklist` 명령.

* 해결된 문제점:
   *  해결된 문제점: 셀 메트릭에 액세스하는 중에 간헐적 오류 발생
<br/>   
이 [간략한 동영상](https://ibm.biz/CFEE-V110){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 CFEE v1.1.0의 새로운 기능 데모를 참조하십시오.  다양한 CFEE 주제에 대한 다른 동영상은 [CFEE 동영상 재생 목록](https://ibm.biz/CFEE-Playlist){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 참조할 수 있습니다.
