---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment의 새로운 기능

이 문서는 {{site.data.keyword.cfee_full_notm}} 서비스의 이 날짜까지 릴리스된 각 버전의 새로운 기능에 대해 설명합니다.

## 버전 2.2.0
{: #v220}

_릴리스 날짜:_ 2019-04-01

CFEE v2.2.0에는 다음과 같은 구성 컴포넌트 버전이 포함되어 있습니다.
* Cloud Foundry: v2.7.1.15.5
* Cloud Foundry API: v2.115.0
* CFEE 빌드팩: v0.1.5
* IBM Kubernetes 서비스: 서비스 업데이트가 제공되지 않았습니다. **중요:** CFEE v2.2.0(CFEE 인스턴스가 격리된 네트워크에서 작동할 때 필요)으로 업데이트하기 전에 CFEE Kubernetes 클러스터를 v1.13으로 업데이트하는 것이 좋습니다.

다음 변경사항은 {{site.data.keyword.cfee_full_notm}} 서비스(CFEE)의 버전 2.2.0에서 릴리스되었습니다. CFEE 버전을 업데이트하려면 CFEE 사용자 인터페이스에서 **업데이트 및 스케일링** 페이지로 이동하고 **업데이트**로 클릭하십시오.

* **다중 구역** Kubernetes 클러스터에서 CFEE 인스턴스를 **작성**하는 새 옵션. 다중 구역 클러스터에서 작성한 CFEE 인스턴스는 데이터 센터의 작업자 노드 전체뿐 아니라 데이터 센터 전체에도 애플리케이션 인스턴스를 분배하므로 인프라 가동 중단에 대비하여 애플리케이션의 복원력이 향상됩니다. 또한 셀을 추가하거나 현재 구역에서 기존 셀을 제거하여 다중 구역 CFEE를 **스케일링**할 수 있습니다. CFEE 인스턴스를 작성하고 나면 다중 구역 CFEE에서 구역을 추가하거나 제거할 수 없습니다.
* CFEE v2.2.0 인스턴스는 이제 [**격리된 네트워크**에서 작동](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)할 수 있습니다. CFEE 인스턴스가 격리된 네트워크에서 VLAN에 배치된 경우 CFEE 인스턴스가 작동하려면 일부 엔드포인트(IP 주소)를 [적절하게 식별하고 라우팅해야 합니다](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points). CFEE 인스턴스가 격리된 네트워크에서 작동하려면 Kubernetes 클러스터 v1.13이 있어야 합니다.
* 내부 IBM 네트워크를 통해 애플리케이션(CFEE 영역에 배치)을 서비스 인스턴스에 바인드하는 새로운 기능. 이 기능을 사용하면 공용 인터넷에 액세스하지 않고도 IBM Cloud Service Endpoint를 지원하는 서비스를 이용할 수 있습니다.
* **모니터링** 도구:
    * CFEE를 작성할 때 더 이상 기본적으로 모니터링 도구(Prometheus, Grafana 및 Alertmanager)를 프로비저닝하지 않습니다. CFEE v2.2.0에서는 CFEE 관리자가 명시적으로 사용으로 설정하는 경우에만 모니터링 도구가 프로비저닝됩니다. 또한 사용으로 설정하면 모니터링이 더 이상 CFEE 제어 플레인 작업자 노드에 프로비저닝되지 않습니다. 제어 플레인 외부의 고유 작업자 노드에 프로비저닝됩니다. 모니터링 도구를 사용으로 설정하여 프로비저닝하려면 CFEE _모니터링_ 페이지(왼쪽 탐색창)로 이동하고 **모니터링 사용**을 클릭하십시오. 
    * 기존 CFEE를 버전 2.2.0으로 업데이트할 때 제어 플레인에서 기존 모니터링 도구가 삭제됩니다. 모니터링 도구의 기존 사용자 정의 구성은 유실됩니다. 
    *  경보 처리, 그룹화 및 알림 라우팅을 사용자 정의할 수 있는 사용자 정의 구성으로 기본 [Alertmanager 구성](https://prometheus.io/docs/alerting/configuration/)을 바꾸는 새로운 기능. _모니터링_ 페이지에서 기본 구성 파일을 _다운로드_하고 로컬 파일 시스템에서 구성 파일을 _업로드_할 수 있습니다. 구성 파일의 [예](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml)를 참조하십시오.
* {{site.data.keyword.Bluemix_notm}} [_리소스 목록_](https://cloud.ibm.com/resources)과 CFEE 사용자 인터페이스에서 CFEE 인스턴스에 태그를 지정하는 새로운 기능.
* {{site.data.keyword.Bluemix_notm}} [**Cloud Foundry 대시보드**](https://cloud.ibm.com/dashboard/cloudfoundry/overview)의 일반적인 사용자 경험 향상. _Cloud Foundry 대시보드_에서는 CFEE 영역으로 별명이 지정된 CFEE 인스턴스, 애플리케이션 및 공용 서비스의 글로벌 보기를 보여줍니다. 

**참고:** 새 CFEE 인스턴스를 작성할 때 새로운 **Eirini 기술 미리보기** 플랜을 사용할 수 있습니다. 이 플랜은 위에서 설명한 v2.2.0에 독립적이며 _표준_ 플랜에만 적용됩니다. Eirini 기술 미리보기 플랜을 사용하면 기본 Kubernetes를 컨테이너 스케줄러(Diego 대신)로 사용하여 CFEE를 탐색할 수 있습니다. 자세한 정보는 [Eirini 기술 미리보기 시작하기](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)를 참조하십시오.

이 [간략한 동영상](https://ibm.biz/CFEE-V220){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 CFEE v2.1.0의 새로운 기능 데모를 참조하십시오.  


## 버전 2.1.1
{: #v211}

_릴리스 날짜:_ 2019-03-20

다음 변경사항은 {{site.data.keyword.cfee_full_notm}} 서비스(CFEE)의 버전 2.1.1에서 릴리스되었습니다. CFEE 버전을 업데이트하려면 CFEE 사용자 인터페이스에서 _업데이트 및 스케일링_ 페이지로 이동하십시오.

* 성공적인 프로비저닝을 방지하는 문제점이 해결되었습니다. 


## 버전 2.1.0
{: #v210}

_릴리스 날짜:_ 2019-02-20

**참고:** 버전 **2.0.2**에서 이 버전으로만 업데이트할 수 있습니다. 버전 v2.1.0으로 업데이트하기 전에 버전 2.0.2로 업데이트하십시오.

다음 변경사항은 {{site.data.keyword.cfee_full_notm}} 서비스(CFEE)의 버전 2.1.0에서 릴리스되었습니다. CFEE 버전을 업데이트하려면 CFEE 사용자 인터페이스에서 **업데이트 및 스케일링** 페이지로 이동하고 **업데이트**로 클릭하십시오.

* 사용자 정의 규칙을 기반으로 자동으로 Cloud Foundry 애플리케이션 인스턴스를 스케일링하는 새로운 Autoscaling 기능. Autoscaling은 CLI 및 Stratos 콘솔에서 액세스할 수 있습니다. Stratos 콘솔은 CFEE 사용자 인터페이스의 _개요_ 페이지에서 선택적으로 설치 및 실행할 수 있습니다. Stratos 콘솔의 _애플리케이션_ 페이지에서 애플리케이션을 선택하고 **Auto Scaling** 탭을 검색하십시오. *정책 작성*을 클릭하여 대상 애플리케이션의 스케일링 정책을 정의하는 Autoscaling 편집기를 실행하십시오.
  자세한 정보는 [autoscaling 문서](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps)를 참조하십시오.
* 우선순위 목록에서 빌드팩을 끌어서 놓아 위치 지정하는 기능을 포함하여 CFEE 사용자 인터페이스에서 빌드팩을 관리하는 새로운 기능. 이 기능은 CFEE 사용자 인터페이스(Stratos 콘솔이 아님)의 새로운 **빌드팩** 페이지에서 사용할 수 있습니다. 이 릴리스에서는 크기가 1MB 이하인 빌드팩 zip 파일만 사용자 인터페이스를 통해 추가하거나 업데이트할 수 있습니다. 1MB보다 큰 빌드팩 zip 파일은 `cf create-buildpack` 및 `cf update-buildpack` 명령을 사용하여 업로드할 수 있습니다. 
* 특정 할당량을 사용 중인 조직 시각화를 포함하여 사용자 인터페이스에서 조직 할당량을 관리하는 새 기능. 이 기능은 CFEE 사용자 인터페이스(Stratos 콘솔이 아님)의 새로운 **할당량** 페이지에서 사용할 수 있습니다. 새 할당량을 작성하고 기존 할당량을 편집할 수 있습니다. 할당량 메뉴에서 **기본값에 복사**를 호출하여 기존 할당량 값으로 기본 할당량 값도 업데이트할 수 있습니다.
* 사용자 인터페이스의 새로운 **시작하기** 페이지에서는 환경을 설정하고 사용하는 데 가장 중요한 태스크를 안내합니다.
* **태그**는 IBM Cloud 리소스 목록의 CFEE 인스턴스에 추가할 수 있습니다. 리소스 목록에 추가된 태그는 CFEE 개요 페이지의 헤더에도 표시됩니다.
* **Cloud Foundry** 버전 2.7.21.
* 보안 패치를 포함하는 **Stratos** 콘솔 버전 2.3.0. CFEE 버전을 업데이트한다고 해서 STratos 콘솔 버전이 업데이트되지는 않습니다. Stratos 콘솔(CFEE 개요 페이지에서)을 삭제하고 다시 설치해야 합니다. 그러면 자동으로 최신 Stratos 콘솔 버전을 선택합니다.
* 사용자가 CFEE 개요 페이지의 오버플로우 메뉴에서 CFEE Kubernetes **클러스터** 페이지로 이동할 수 있습니다.

**참고:** v2.0.x 버전에서 CFEE v2.1.0으로 업데이트하는 경우 제어 플레인과 셀을 순서대로 자동 업데이트하는 단일 _업데이트_ 조치로 업데이트가 수행됩니다. v1.x.x 버전에서 업데이트하면 업데이트에 두 개의 개별 _업데이트_ 조치가 필요합니다. 하나는 제어 플레인을 업데이트하고(처음) 다른 하나는 셀을 업데이트합니다. 

이 [간략한 동영상](https://ibm.biz/CFEE-V210){: new_window} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")에서 CFEE v2.1.0의 새로운 기능 데모를 참조하십시오.  


## 버전 2.0.2
{: #v202}

_릴리스 날짜:_ 2019-02-08

다음 변경사항은 {{site.data.keyword.cfee_full_notm}} 서비스(CFEE)의 버전 2.0.2에서 릴리스되었습니다. CFEE 버전을 업데이트하려면 CFEE 사용자 인터페이스에서 _업데이트 및 스케일링_ 페이지로 이동하십시오.

* 성공적인 버전 업데이트를 방지하는 문제점이 해결되었습니다. 이 버전은 **2.1.0** 버전으로 업데이트하기 위한 전제조건입니다.


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
