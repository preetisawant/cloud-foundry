---

copyright:
  years: 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 애플리케이션 Autoscaling
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}}에서는 애플리케이션 인스턴스 수를 자동으로 조정하는 Cloud Foundry 애플리케이션용 autoscaling 지원을 기본으로 제공합니다. 
  * 애플리케이션 성능 메트릭을 기반으로 하는 동적 스케일링.
  * 시간에 따라 스케줄되는 스케일링.

이 기능은 Cloud Foundry 오픈 소스 프로젝트 [App-Autoscaler][autoscaler_project]를 기반으로 제공됩니다. 시작하려면 [사용자 안내서][autoscaler_user_guide]를 참조하십시오. 

## CLI를 통한 Autoscaling 관리

App Autoscaler 명령행 인터페이스 플러그인(AutoScaler CLI라고도 함)을 사용하여 정책을 관리하고 메트릭과 스케일링 히스토리를 조회할 수 있습니다. 

### AutoScaler CLI 설치
다음 명령을 사용하여 Cloud Foundry CLI의 플러그인인 `AutoScaler CLI`를 설치하십시오.  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

이전 설치가 있는 경우 동일한 명령을 사용하여 `AutoScaler CLI` 플러그인을 업데이트할 수 있습니다. 

### AutoScaler CLI 사용

이미 {{site.data.keyword.Bluemix}}에서 Cloud Foundry 환경에 로그인했으며 [앱 배치 안내서][deploy_app]에 설명된 대로 영역에서 애플리케이션을 실행 중인 경우 아래 단계를 따라 애플리케이션의 스케일링 정책을 작성하고 메트릭과 스케일링 히스토리를 조회하십시오. 

 *  (선택사항) App-Autoscaler API 엔드포인트가 기본적으로 올바르게 설정되었는지 확인하십시오.  

    Cloud Foundry API 엔드포인트가 `api.<DOMAIN>`로 표시되면 App-Autoscaler API 엔드포인트는 `autoscaler.<DOMAIN>`여야 합니다.  
    아래 명령을 사용하여 App-Autoscaler API 엔드포인트 설정을 확인하십시오.

    ```
    cf asa
    ```
    {:codeblock} 

    App-Autoscaler API 엔드포인트가 올바르지 않으면 다음 명령으로 재설정해야 합니다.

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  로컬 시스템에 정책 JSON 파일을 작성하십시오. 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    위의 정책은 정의된 임계값이 최소 `120    seconds` 동안 위반되면 메모리 활용도를 기반으로 스케일링을 트리거하는 데 사용합니다. 고유 Autoscaling 정책을 작성하는 방법은 [Cloud Foundry App-Autoscaler 사용자 안내서][autoscaler_user_guide]를 참조하십시오.

*  애플리케이션에 정책 첨부

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (선택사항) 가장 최근에 집계한 애플리케이션의 메트릭도 조회할 수 있습니다. App-Autoscaler에서는 여러 [메트릭 유형][metric_type]을 지원하지만 정책에 정의한 메트릭만 검색할 수 있습니다. 예를 들어 위의 예에서 `memoryutil`이 해당됩니다.  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (선택사항) 아래 명령을 사용하여 스케일링 히스토리를 조회하십시오.

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    명령행을 사용하는 추가 옵션은 [Cloud Foundry App Autoscaler CLI 플러그인 안내서][autoscaler_cli]를 참조하십시오. 


## Stratos 콘솔을 통해 Autoscaling 관리 

명령행 인터페이스 외에도 Stratos 콘솔을 통해 autoscaling 설정도 관리할 수 있습니다. 

{{site.data.keyword.cfee_full}}(CFEE)에 [stratos][stratos]를 설치한 경우 애플리케이션 대시보드의 **"Auto scaling**" 탭으로 이동하여 Auto-Scaling 정책 및 최신 스케일링 이벤트의 개요를 확인하십시오.
타일에 있는 아이콘을 클릭하여 정책 편집기를 실행하고 정책을 편집하십시오.

Auto-Scaling 정책이 정의되지 않으면 개요 페이지에 정보가 없습니다. **정책 작성**을 클릭하여 정책 편집기를 실행하고 정책을 작성하십시오.

Auto-Scaling 정책을 제대로 설정하기 위한 기본 개념을 파악하려면 [Cloud Foundry App-Autoscaler 사용자 안내서][autoscaler_user_guide]를 검토하는 것이 좋습니다. 

### 메트릭 통계

선택한 하나 이상의 메트릭 유형을 기반으로 정책을 정의한 경우 최신 메트릭 값과 지난 30분 동안의 메트릭 히스토리를 볼 수 있습니다. 

**참고:** 메트릭은 각 애플리케이션 인스턴스의 원시 데이터가 아니라 모든 애플리케이션 인스턴스에서 평균을 낸 데이터를 나타냅니다.
    
### 스케일링 히스토리

정책 편집기의 **히스토리** 탭에서는 Auto-Scaling 정책을 통해 트리거한 애플리케이션에서 스케일링 조치가 수행되었음을 보여줍니다. 스케일링 실패 때문에 발생한 오류 메시지도 표시합니다. 지난 30일 동안의 스케일링 히스토리를 조회할 수 있습니다. 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]:https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]:https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
