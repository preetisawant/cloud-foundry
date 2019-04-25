---

copyright:
  years: 2019
lastupdated: "2019-02-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 사용 불가능한 Stager 디버깅
{: #unavailable_stager}

이 튜토리얼에서는 {{site.data.keyword.cfee_full}}(CFEE)에서 사용 불가능한 Stager를 디버깅하는 방법을 보여줍니다.

## 컴포넌트 이해
{: #stager_components}

{{site.data.keyword.Bluemix_notm}} BBS(Bulletin Board System)는 활성 또는 수동 모드로 실행되며 하나의 BBS만 활성이 되도록 Locket에서 잠금을 유지보수합니다. 경우에 따라 Locket에서 백엔드 데이터베이스와의 연결이 끊기면 BSS가 응답하지 않음 상태가 될 수 있습니다. 이 경우 Cloud Controller에서 BBS API와 통신할 수 없으므로 활성 BBS가 선택되지 않으며 BBS API에 액세스할 수 없고 `cf push`와 같은 오퍼레이션이 실패합니다. CFEE v2.0 이상에서 Diego BBS와 Locket는 diego-api-x 팟(Pod)에서 실행되므로 사용자가 환경을 다시 실행하려면 모든 diego-api-x 팟을 다시 시작해야 합니다.

## 영향
{: #stager_impact}

Diego BBS API에 액세스할 수 없습니다. 사용자가 `cf push app`을 수행할 수 없으므로 CF 애플리케이션 스테이징에 실패하며 다음과 같이 `Stager is unavailable` 오류가 표시됩니다.

```
    Response code: 503
    CC code:       0
    CC error code:
    Request ID:    xxxxxxx-xxxxx-xxx-xxxx-xxxxxxxx
    Description:   {
    "description": "Stager is unavailable: execution expired",
    "error_code": "CF-StagerUnavailable",
    "code": 170010
    }
    Server error, status code: 503, error code: 170010, message: Stager is unavailable: execution expired
```

## 수정 방법
{: #stager_howtofix}

일반적으로 `Stager is unavailable` 오류 메시지는 Cloud Controller에서 Diego BBS API와 통신하는 데 문제가 있음을 나타냅니다.
다음 단계를 따라 보고된 문제가 이 경우와 동일한지 확인하십시오.
동일하면 계속하여 환경을 복구하십시오.

1. api-x 팟 상태를 확인하여 Cloud Controller를 사용할 수 있는지 확인하십시오.

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. 예를 들어 출력은 2개의 2 api-x 팟이 실행 중임을 나타냅니다.
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. api-0 팟으로 이동하십시오.

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. api-0 팟에서 아래와 같은 오류가 발생하면 Cloud Controller에서 BBS에 액세스할 수 없습니다.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - 예를 들어 출력은 연결에 실패했음을 나타냅니다.
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. api-0을 종료한 다음 아래와 같이 모든 diego-api-x 팟을 삭제하십시오. Kubernetes에서 모든 팟을 자동으로 재작성합니다.

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    CFEE 2.0 이전에는 Diego Lockets가 diego-locket-x라는 개별 팟에 있습니다. 이 경우 5단계와 같이 diego-locket-x 팟을 모두 다시 시작하십시오.

6. 모든 diego-api-x 팟이 `running`이며 `2/2`가 준비될 때까지 기다리십시오. diego-api-x 팟 중 하나가 활성으로 레이블이 지정되었는지 확인하십시오.

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. 3단계와 4단계와 같이 Cloud Controller에서 BBS API에 액세스할 수 있는지 확인하십시오. 다음과 같은 출력이 표시되어야 합니다.

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. CF 앱 스테이징을 위해 환경이 준비되어야 합니다.
