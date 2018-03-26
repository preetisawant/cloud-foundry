---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.cloud_notm}}에서 Cloud Foundry의 작동 방법
{: #howwork}

Cloud Foundry에 앱을 배치할 때는 앱을 지원하는 데 충분한 정보를 사용하여 {{site.data.keyword.cloud_notm}}를 구성해야 합니다.

* 모바일 앱의 경우 {{site.data.keyword.cloud_notm}}에는 모바일 앱의 백엔드(예: 모바일 앱이 서버와 통신하는 데 사용하는 서비스)를 나타내는 아티팩트가 포함됩니다.
* 웹 앱의 경우 런타임 및 프레임워크 관련 정보가 {{site.data.keyword.cloud_notm}}에 전달되는지 확인하여 {{site.data.keyword.cloud_notm}}가 앱을 실행하기 위한 적절한 실행 환경을 설정할 수 있도록 해야 합니다.

모바일 및 웹 모두를 포함하여, 각 실행 환경은 다른 앱의 실행 환경에서 격리됩니다. 이러한 실행 환경은 앱이 동일한 물리적 시스템에 있더라도 격리됩니다. 다음 그림은 {{site.data.keyword.cloud_notm}}에서 Cloud Foundry가 앱의 배치를 관리하는 방법의 기본 플로우를 보여줍니다.

![앱 배치](images/deploy.png)

그림 1. 앱 배치

앱을 작성하고 이를 Cloud Foundry에 배치할 때 {{site.data.keyword.cloud_notm}} 환경은 앱 또는 해당 앱이 나타내는 아티팩트를 전송할 적절한 가상 서버를 결정합니다. 모바일 앱의 경우 모바일 백엔드 투영이 {{site.data.keyword.cloud_notm}}에 작성됩니다. 클라우드에서 실행 중인 모바일 앱의 코드는 {{site.data.keyword.cloud_notm}} 환경에서 실행됩니다. 웹 앱의 경우 클라우드에서 실행 중인 코드는 개발자가 {{site.data.keyword.cloud_notm}}에 배치하는 앱 자체입니다. 가상 서버는 다음을 포함하여 여러 요인을 기반으로 결정됩니다.

* 시스템의 기존 로드
* 해당 가상 서버에서 지원되는 런타임 또는 프레임워크

가상 서버를 선택한 후 각 가상 서버의 애플리케이션 관리자에서 앱에 적절한 프레임워크 및 런타임을 설치합니다. 그런 다음 앱이 해당 프레임워크로 배치될 수 있습니다. 배치가 완료되면 애플리케이션 아티팩트가 시작됩니다.

다음 그림은 여러 앱이 배치되어 있고 DEA(Droplet Execution Agent)라고 알려진 가상 서버의 구조를 보여줍니다.

![가상 서버 디자인](images/container-diego.png)

그림 2. 가상 서버의 디자인

각 가상 서버에서 애플리케이션 관리자는 {{site.data.keyword.cloud_notm}} 인프라의 나머지 부분과 통신하고 이 가상 서버에 배치되는 앱을 관리합니다. 각 가상 서버는 앱을 분리하고 보호하기 위한 컨테이너를 가지고 있습니다. 각 컨테이너에서 {{site.data.keyword.cloud_notm}}는 각 앱에 필요한 적절한 프레임워크 및 런타임을 설치합니다.

앱을 배치할 때 웹 인터페이스(예: Java 웹 앱) 또는 다른 REST 기반 서비스(예: 모바일 앱에 공개적으로 노출된 모바일 서비스)가 있으면 앱의 사용자가 일반적인 HTTP 요청을 사용하여 앱과 통신할 수 있습니다.

![ {{site.data.keyword.cloud_notm}} 앱 호출](images/execute.png)

그림 3. {{site.data.keyword.cloud_notm}} 앱 호출

각 앱은 하나 이상의 URL과 연관될 수 있지만 이 URL은 모두 {{site.data.keyword.cloud_notm}} 엔드포인트를 가리켜야 합니다. 요청이 들어오면 {{site.data.keyword.cloud_notm}}는 요청을 검사하고, 이 요청이 사용되는 앱을 결정한 다음, 요청을 수신할 앱 인스턴스를 선택합니다.


## {{site.data.keyword.cloud_notm}}의 Cloud Foundry 아키텍처
{: #architecture}

일반적으로 Cloud Foundry의 {{site.data.keyword.cloud_notm}}에서 앱을 실행할 때 운영 체제 및 인프라 계층에 대해서는 우려할 필요가 없습니다. 사용자가 자신의 애플리케이션 코드에 집중할 수 있도록 루트 파일 시스템 및 미들웨어 컴포넌트 등의 계층은 추상화됩니다. 단, 앱이 실행되는 특정 계층에 대한 지식이 필요한 경우에는 해당 계층에 대해 자세히 볼 수 있습니다.

세부사항은 [{{site.data.keyword.cloud_notm}} 인프라 계층 보기](cf.html#infralayers)를 참조하십시오.

개발자는 브라우저 기반 사용자 인터페이스를 사용하여 {{site.data.keyword.cloud_notm}} 인프라와 상호 작용할 수 있습니다. 또한 cf라는 Cloud Foundry 명령행 인터페이스를 사용하여 웹 앱을 배치할 수도 있습니다.

모바일 앱, 외부에서 실행되는 앱, {{site.data.keyword.cloud_notm}}에서 빌드된 앱 또는 브라우저를 사용하는 개발자일 수 있는 클라이언트는 {{site.data.keyword.cloud_notm}}에서 호스팅되는 앱과 상호 작용합니다. 클라이언트는 REST 또는 HTTP API를 사용하여 {{site.data.keyword.cloud_notm}}를 통해 앱 인스턴스 또는 복합 서비스 중 하나로 요청을 라우팅합니다.

다음 그림은 {{site.data.keyword.cloud_notm}}에서 상위 레벨 Cloud Foundry 아키텍처를 보여줍니다.

![{{site.data.keyword.cloud_notm}} 아키텍처](images/arch.png)

그림 4. {{site.data.keyword.cloud_notm}}의 Cloud Foundry 아키텍처

대기 시간이나 보안을 고려하여 앱을 다른 {{site.data.keyword.cloud_notm}} 지역에 배치할 수 있습니다. 한 지역에 배치하거나 여러 지역에 걸쳐 배치할지 선택할 수 있습니다.


![다중 지역 애플리케이션 배치](images/multi-region.png)

그림 5. 다중 지역 애플리케이션 배치

{{site.data.keyword.Bluemix_notm}} 인프라 계층
{: #infralayers}


{{site.data.keyword.Bluemix_notm}}는 관리할 필요가 없도록 운영 체제 및 인프라 계층을 추상화하고 숨깁니다. 그러나 때때로 사용자 앱의 운영 체제와 미들웨어에 대한 정보가 필요할 수 있습니다.
{:shortdesc}

### {{site.data.keyword.Bluemix_notm}} 인프라 계층 보기
{: #viewinfra}

**bluemix app stacks** 명령을 실행하여 앱이 배치될 사용 가능한 스택 또는 루트 파일 시스템을 표시할 수 있습니다. **bluemix app push** 명령을 *-s* 옵션 및 *stack_name*과 함께 사용할 때 스택을 지정할 수도 있습니다. 여기서 stack_name은 루트 파일 시스템(예: `lucid64` 또는 `cflinuxfs2`)입니다.

```
bluemix app push appName -s stack_name
```

`cf buildpacks` 명령을 사용하여 앱을 실행할 런타임으로 사용 가능한 미들웨어 컴포넌트(예: WebSphere Liberty 프로파일 및 SDK for Node.js)를 표시할 수 있습니다. 또한 다음 명령을 사용하여 앱의 런타임 환경을 지정할 수 있습니다.

```
bluemix app push appName -b buildpackname
```
