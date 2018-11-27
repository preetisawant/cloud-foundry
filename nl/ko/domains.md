---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# 도메인 관리
{: #domains}

Cloud Foundry 도메인의 두 가지 유형이 있습니다. 
* {{site.data.keyword.cfee_full_notm}} 내의 영역에서 애플리케이션이 사용할 수 있는 공유 도메인. 공유 도메인에 액세스하려면, UI의 왼쪽 탐색 분할창에 있는 **도메인** 페이지로 이동하십시오(*오퍼레이션* 아래).
* 특정 조직 내의 애플리케이션 및 영역에만 사용 가능한 사설 도메인. 조직 내의 도메인에 액세스하려면, UI의 왼쪽 탐색 분할창에 있는 **조직** 페이지로 이동하여 조직을 열고 **도메인** 탭으로 이동하십시오.

## 도메인 작성 및 삭제
{: #create-domains}

공유 도메인을 작성하려면, {{site.data.keyword.cfee_full_notm}}의 왼쪽 탐색 분할창에 있는 **도메인**으로 이동하십시오.  

사설 도메인을 작성하려면, UI의 왼쪽 탐색 분할창에 있는 **조직** 페이지로 이동하여 조직을 열고 **도메인** 탭으로 이동하십시오.

_도메인_ 페이지(공유 도메인의 경우) 또는 특정 조직의 _도메인_ 탭(사설 도메인의 경우)으로 이동하면, **도메인 작성**을 클릭하여 도메인을 작성하고, 고유 이름을 입력하십시오.

**참고:** 도메인 이름은 {{site.data.keyword.cfee_full_notm}}의 전체 범위에서 고유해야 합니다. 즉, 사설 도메인은 지정된 {{site.data.keyword.cfee_full_notm}} 내의 공유 또는 사설 도메인의 이름을 사용할 수 없습니다.

또한 다음 명령을 실행하여 Cloud Foundry CLI에서 공유 도메인을 작성할 수 있습니다.
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
다음 명령을 실행하여 Cloud Foundry CLI에서 사설 도메인을 작성할 수 있습니다.
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**참고:** Cloud Foundry CLI에서 작성된 도메인은 바로 UI에 반영되지만 효력이 발생하려면 최대 1시간이 걸릴 수 있습니다. 

도메인을 삭제하려면, 삭제하려는 도메인에 해당하는 테이블 행의 맨 오른쪽에 있는 메뉴로 이동하여 **도메인 삭제**를 선택하십시오.
  
또한 다음 명령을 실행하여 Cloud Foundry CLI에서 공유 도메인을 삭제할 수 있습니다.
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## SSL 인증서 업로드
 {: #upload-certificates}
 
도메인(공유 또는 사설)에 대한 SSL 인증서를 업로드할 수 있습니다. 인증서가 추가되는 도메인에 해당하는 테이블 행에서 **업로드**를 클릭하고, 인증서를 포함하는 파일 및 개인 키를 포함하는 파일을 선택하십시오.
  
