---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 프로덕션에서 앱을 실행하기 위한 우수 사례
{: #production}

Cloud Foundry는 프로덕션에서 클라우드 준비 애플리케이션을 실행하기 위한 뛰어난 플랫폼입니다. 이러한 우수 사례는 {{site.data.keyword.Bluemix_notm}}으로 프로덕션 Cloud Foundry 앱을 실행하는 데 도움이 됩니다.
{:shortdesc}

## 다중 인스턴스
{: #multiple_instances}

클라우드 준비 앱은 수평으로 확장 가능해서 애플리케이션 인스턴스를 동적으로 추가하거나 제거할 수 있습니다. 격리된 인시던트 또는 플랫폼 유지보수 시 갑작스런 작동 중단을 방지하기 위해 각 애플리케이션당 최소 세 개의 인스턴스를 실행하십시오.

## 모니터링 옵션
{: #monitoring}

{{site.data.keyword.Bluemix_notm}}를 통해 [모니터링 및 분석](/docs/services/monana/index.html), [New Relic ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window}과 같은 서비스를 사용하여 애플리케이션을 좀 더 쉽게 모니터링할 수 있습니다. 자세한 정보는 [통합 로깅 기능](../monitor_log/logging.html#logging_for_bluemix_apps)을 확인하십시오.

## 지원 옵션
{: #support}

{{site.data.keyword.Bluemix_notm}} 유료 가격 책정 플랜은 *선택적* 유료 지원으로 다수의 여러 계정 유형을 제공합니다.  계정 유형에 관계없이 {{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 프로덕션으로 가져올 계획인 경우 이 옵션 등록을 고려하십시오.

유료 지원 여부와 관계없이 [필요한 지원은 어떻게 받습니까?](../get-support/howtogetsupport.html)에 설명된 대로 지원을 받을 수 있으나 유료 지원의 경우에는 지원 티켓에 적절한 수준의 주의가 제공되는지 확인하는 데 도움이 됩니다.
