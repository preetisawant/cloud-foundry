---

copyright:
  years: 2018
lastupdated: "2018-08-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 모니터링
{: #monitoring}

{{site.data.keyword.cfee_full}} 인스턴스 및 지원되는 해당 인프라 모니터링은 Prometheus 및 Grafana로 구성된 오픈 소스 도구 세트에서 지원됩니다. 솔루션을 사용하면 Cloud Foundry 환경에서 메트릭에 대한 경보를 분석하고 시각화하고 관리할 수 있습니다. 모니터링이 발생하는 세 가지 웹 콘솔(Grafana 콘솔, Prometheus 콘솔 및 Prometheus Alert Manager 콘솔)이 있습니다.

**참고:** {{site.data.keyword.cfee_full}} 인스턴스의 모니터링 기능에 액세스하려면 CFEE 인스턴스를 지원하는 해당 Kubernetes 클러스터의 _관리자_ 또는 _편집자_ 역할이 필요합니다. CFEE 인스턴스를 지원하는 Kubernetes 클러스터의 기본 이름은 _`<CFEEname>`-cluster_입니다.

## Prometheus
{: #prometheus}

Prometheus는 오픈 소스 시스템 모니터링 및 경보 툴킷입니다. 2012년에 처음 도입된 후 많은 회사와 조직에서 Prometheus를 채택했으며 프로젝트에는 매우 활발하게 활동하는 개발자 및 사용자 커뮤니티가 있습니다. Prometheus는 독립형 오픈 소스 프로젝트이며 모든 회사와 독립적으로 유지됩니다. 이를 강조하고 프로젝트의 통제 구조를 명확히 하기 위해 Prometheus가 2016년에 Kubernetes에 이어 두 번째 호스팅된 프로젝트로 Cloud Native Computing Foundation에 가입했습니다. 자세한 정보는 [Prometheus 문서](https://prometheus.io/docs/introduction/overview/)를 참조하십시오.

Prometheus 에코시스템은 여러 컴포넌트로 구성되며, 다수의 컴포넌트가 선택사항입니다.

* 시계열 데이터를 스크랩하여 저장하는 기본 Prometheus 서버</li>
* 경보를 처리하기 위한 [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/)</li>
* node exporter, blackbox exporter 등과 같은 특수 목적의 다양한 내보내기 프로그램</li>
* 단시간 실행되는 작업을 지원하기 위한 푸시 게이트웨이</li>

Prometheus는 직접 또는 단시간 실행되는 작업의 경우 중개 푸시 게이트웨이를 통해	인스트루먼트된 작업에서 메트릭을 수집합니다. 수집된 모든 샘플을 로컬로 저장하며 이 데이터에 대한 규칙을 실행하여 기존 데이터에서 시계열을 집계하고 기록하거나 경보를 생성합니다.

## Grafana
{: #grafana}

Grafana는 Prometheus에서 수집된 모든 메트릭에 대한 오픈 소스 분석 플랫폼입니다. 클러스터에 배치된 Grafana 버전이 이미 기본 Prometheus 데이터베이스를 사용하도록 구성되어 있습니다. 또한 일부 유용한 Grafana 대시보드를 포함합니다. 자세한 정보는 [Grafana 문서](http://docs.grafana.org/guides/getting_started/)를 참조하십시오.

## 모니터링 시작하기
{: #gettingStarted_monitor}

모니터링 솔루션을 포함하는 Prometheus 및 Grafana 컴포넌트가 CFEE 인스턴스를 지원하는 Kubernetes 인프라에 사전 설치됩니다. 모니터링 도구에 액세스하려면 Prometheus, Prometheus AlertManager 및 Grafana 서버의 포트를 전달해야 합니다. 이는 Kubernetes CLI를 통해 수행됩니다.
다음에서는 필수 CLI 설치, 서버 포트 전달 및 콘솔 실행 단계를 안내합니다.

**참고:** {{site.data.keyword.cfee_full}} 사용자 인터페이스에서도 다음 지시사항을 사용할 수 있습니다. CFEE 인스턴스 사용자 인터페이스를 열고 왼쪽 탐색 분할창에서 **모니터링**을 클릭하여 표시되는 지시사항을 확인하십시오.

### 전제조건

1. [액세스 정책](https://console.bluemix.net/iam/#/users)을 확인하여 환경을 지원하는 Kubernetes 클러스터에 대한 뷰어 이상의 역할이 있는지 확인하십시오.
2. [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use)를 설치하십시오.
3. [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/)를 설치하십시오. 기존 Kubernetes CLI가 있는 경우 최신 버전을 설치하도록 권장합니다.
4. 컨테이너 서비스 플러그인을 설치하십시오.
```
    ibmcloud plugin install container-service -r Bluemix
```

### Kubernetes 클러스터에 액세스

1. IBM Cloud 계정에 로그인하십시오.

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}

  연합 ID가 있는 경우 __ibmcloud login -sso__를 사용하여 IBM Cloud CLI에 로그인하십시오.

2. 작업할 IBM Cloud Container Service 지역을 대상으로 지정하십시오(예: us-south).

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}

3. CLI에서 클러스터의 컨텍스트를 설정하십시오.

  a. 환경 변수를 설정하기 위한 명령을 가져오고 Kubernetes 구성 파일을 다운로드하십시오.

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}

  b. KUBECONFIG 환경 변수를 설정하십시오. 이전 명령의 출력을 복사하여 터미널에 붙여넣으십시오. 명령 출력은 다음과 유사하게 보입니다. __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### 서버 포트 전달
4. Prometheus, AlertManager 및 Grafana를 실행 중인 팟(Pod)에 대한 Kubernetes 클러스터의 포트 전달을 설정하십시오. 이렇게 하면 로컬 시스템(localhost)에서 프록시로 모니터링 메트릭을 호스팅할 수 있습니다.

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000'
  ```
  {: pre}

### 로컬 웹 프록시에서 모니터링 콘솔 실행

5. Grafana 콘솔을 실행하여 선택한 메트릭에 대한 분석을 확인하십시오. CFEE 인스턴스에 포함된 기본 Grafana 대시보드가 있습니다. 이러한 기본 대시보드는 대화식이며 CFEE 인스턴스를 호스팅하는 데 사용되는 인프라의 보기를 제공합니다(Kubernetes 클러스터). Grafana 콘솔을 실행한 후 Grafana 콘솔의 맨 위에 있는 **홈** 버튼을 클릭하여 해당 메트릭을 그래프로 표시하는 사전 배치된 대시보드(아래 목록 참조) 중 하나를 선택하십시오.

   Grafana에는 기본 `admin` 사용자가 있으며 기본 비밀번호가 `admin`으로 설정되어 있습니다. `admin/admin` 사용자 ID/비밀번호로 로그인하여 새 신임 정보로 변경하십시오. 

     [Grafana 서버 실행](https://localhost:3000)

   다음과 같은 기본 대시보드가 CFEE 인스턴스와 함께 제공되며 _홈_ 드롭 다운에서 사용할 수 있습니다.

   CFEE 환경을 지원하는 Kubernetes 인프라에 대한 대시보드:
   - _Kubernetes 용량 계획_ 대시보드
        - Kubernetes 인프라의 용량을 표시합니다. 
   - _Kubernetes 클러스터 상태(health)_ 대시보드
        - Kubernetes 클러스터의 상태(health)를 표시합니다.
   - _Kubernetes 클러스터 상태(status)_ 대시보드
        - Kubernetes 클러스터의 상태(status)를 표시합니다.
   - _Kubernetes 리소스 요청_ 대시보드
        - Kubernetes 클러스터의 사용된 CPU, 메모리 및 기타 매개변수를 표시합니다.
   - _노드_ 대시보드
        - Kubernetes 클러스터의 각 작업자 노드에 대한 세부사항을 표시합니다.
   - _팟(Pod)_ 대시보드
        - Kubernetes 클러스터에서 실행 중인 각 팟(Pod)에 대한 세부사항을 표시합니다.
   - _복제본 세트_ 대시보드
        - Kubernetes 복제본 세트의 상태를 표시합니다.
   - _배치_ 대시보드
        - Kubernetes 배치의 상태를 표시합니다.

   Cloud Foundry 대시보드:
   - _CF: 셀 용량_ 대시보드
        - Cloud Foundry 애플리케이션이 배치된 Cloud Foundry 셀의 일반 상태를 표시합니다.
   - _CF: 라우터_ 대시보드
        - CFEE 환경에서 실행 중인 Cloud Foundry 라우터 상태를 표시합니다.
   - _CF: Diego_Cell_ 대시보드
        - Cloud Foundry 셀 및 Diego 컴포넌트의 상태를 표시합니다.

6. 선택적으로, Prometheus 콘솔을 실행하여 Prometheus 서버에서 수집된 원시 데이터를 확인하고 Prometheus Alertmanager를 실행하여 Prometheus 서버에서 전송된 경보를 관리할 수 있습니다.

     [Prometheus 서버 실행](https://localhost:9090)

     [Prometheus Alertmanager 서버 실행](https://localhost:9093)
