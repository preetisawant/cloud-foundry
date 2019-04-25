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

# 除錯無法使用的編譯打包器
{: #unavailable_stager}

本指導教學顯示如何在 {{site.data.keyword.cfee_full}} (CFEE) 上除錯無法使用的編譯打包器。

## 瞭解元件
{: #stager_components}

「{{site.data.keyword.Bluemix_notm}} 公佈欄系統 (BBS)」是以主動或被動模式執行，並且會在 Locket 中維持鎖定，以確保只有一個 BBS 作用中。有時，如果 Locket 失去與後端資料庫的連線，則 BSS 可能會進入無回應狀態。在此情況下，未選取任何作用中的 BBS、無法存取 BBS API，而且 `cf push` 這類作業會失敗，因為「雲端控制器」無法與 BBS API 通訊。在 CFEE 2.0 版及更高版本中，Diego BBS 及 Locket 會在 diego-api-x Pod 中執行，因此使用者需要重新啟動所有 diego-api-x Pod 才能回復環境。

## 影響
{: #stager_impact}

無法存取 Diego BBS API。使用者無法執行 `cf push app`，因此 CF 應用程式編譯打包會失敗，錯誤為 `Stager is unavailable`，如下所示：

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

## 修正方式
{: #stager_howtofix}

錯誤訊息 `Stager is unavailable` 通常表示「雲端控制器」與 Diego BBS API 通訊時發生問題。請遵循下列步驟，來確認報告的問題是否與此情況相同。如果是，請繼續回復環境。

1. 檢查 api-x Pod 狀態，以確定「雲端控制器」可供使用。

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. 例如，輸出指出有 2 個 api-x Pod 在執行中：
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. 移至 api-0 Pod。

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. 在 api-0 Pod 中，如果您收到如下錯誤，則表示「雲端控制器」無法存取 BBS。
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - 例如，輸出指出連線失敗：
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. 結束 api-0，然後刪除所有 diego-api-x Pod，如下所示。Kubernetes 將會自動重建所有項目。

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    在 CFEE 2.0 之前，Diego Locket 位於名為 diego-locket-x 的個別 Pod 中。如果是這種情況，請如同步驟 5 重新啟動所有 diego-locket-x Pod。

6. 等待所有 diego-api-x Pod 都為 `running` 且 `2/2` 已備妥。請確定其中一個 diego-api-x Pod 標示為作用中。

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. 檢查「雲端控制器」是否可以存取 BBS API（如步驟 3 及 步驟 4）。您應該會取得與下面類似的輸出。

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. 環境應該已備妥，可進行 CF 應用程式編譯打包。
