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

# Debugging unavailable stager
{: #unavailable_stager}

This tutorial shows how to debug an unavailable stager on your {{site.data.keyword.cfee_full}} (CFEE).

## Understanding components
{: #stager_components}

The  {{site.data.keyword.Bluemix_notm}} Bulletin Board System (BBS) runs in active or passive mode, and it maintains a lock in Locket to ensure that only one BBS is active. Sometimes, if Locket loses connection with back-end database, BSS may run into an unresponsive state. In this case, no active BBS is elected,  BBS API is not accessible, and operations like `cf push` will fail since the Cloud Controller cannot communicate with BBS API.
In CFEE v2.0 and above, Diego BBS and Locket run in the diego-api-x pod, so users need to restart all diego-api-x pods to bring the environment back.

## Impact
{: #stager_impact}

Diego BBS API is not accessible. Users are not able to do `cf push app` and CF application staging fails with an error `Stager is unavailable` as below:

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

## How to fix it
{: #stager_howtofix}

The error message `Stager is unavailable` usually means that Cloud Controller has troubles to communicate with Diego BBS API.
Please follow these steps to confirm whether the issue reported is the same with this case.
If yes, please continue to recover the environment.

1. Make sure Cloud Controller is available by checking api-x pod status.

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. For example, the output indicates that 2 api-x pods are running:
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. Go into api-0 pod.

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. In api-0 pod, if you get an error like below, it indicates that Cloud Controller cannot access BBS.
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - For example, the output indicates that connection failed:
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. Exit api-0 and then delete all diego-api-x pods as below. Kubernetes will recreate all of them automatically.

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    Before CFEE 2.0, Diego Lockets are located in separate pods named diego-locket-x. If this is the case, please restart all diego-locket-x pods like step 5.

6. Wait until all diego-api-x pods are `running` and `2/2` ready. Make sure one of diego-api-x pods is labeled as active.

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. Check if Cloud Controller can access BBS API like step 3 & step 4. You should get a similar output as below.

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. Environment should be ready for CF app staging.
