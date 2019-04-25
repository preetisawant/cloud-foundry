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

# 使用できないステージャーのデバッグ
{: #unavailable_stager}

このチュートリアルでは、{{site.data.keyword.cfee_full}} (CFEE) 上の使用できないステージャーをデバッグする方法を示します。

## コンポーネントの理解
{: #stager_components}

{{site.data.keyword.Bluemix_notm}} Bulletin Board System (BBS) は、アクティブ・モードまたはパッシブ・モードで稼働し、Locket 内にロックを保持して 1 つの BBS だけがアクティブになるようにします。ときには、Locket がバックエンド・データベースとの接続を失う場合に、BSS が無応答の状態になることがあります。このようなケースでは、アクティブな BBS は選択されず、BBS API はアクセス不可となり、Cloud Controller が BBS API と通信できないために `cf push` などの操作は失敗します。
CFEE v2.0 以上では、Diego BBS と Locket が diego-api-x ポッドで稼働するので、ユーザーはすべての diego-api-x ポッドを再始動して環境を元に戻す必要があります。

## 影響
{: #stager_impact}

Diego BBS API にアクセスできません。ユーザーは `cf push app` を実行できず、CF アプリケーションのステージングは、以下のように `Stager is unavailable` のエラーで失敗します。

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

## 解決策
{: #stager_howtofix}

エラー・メッセージの `Stager is unavailable` は、通常、Cloud Controller に Diego BBS API との通信の問題が発生したことを示しています。
以下の手順に従って、報告された問題がこのケースと同じであるかどうかを確認してください。
同じである場合は、環境の復旧を続行します。

1. api-x ポッドの状況を調べて、Cloud Controller が使用可能であることを確認します。

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. 例えば、出力は以下のように 2 つの api-x ポッドが実行中であることを示しています。
    ```
    NAME                            READY   STATUS      RESTARTS   AGE
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. api-0 ポッドに移動します。

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. api-0 ポッドで以下のようなエラーを受け取る場合、それは Cloud Controller が BBS にアクセスできないことを示しています。
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - 例えば、この出力は接続が失敗したことを示しています。
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) failed: Connection timed out
    ```

5. api-0 を終了してから、以下のようにすべての diego-api-x ポッドを削除します。Kubernetes はそれらすべてを自動的に再作成します。

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    CFEE 2.0 より前は、Diego Lockets が diego-locket-x という名前の別個のポッド内にありました。このような場合では、ステップ 5 と同様にすべての diego-locket-x ポッドを再始動してください。

6. すべての diego-api-x ポッドが `running` で `2/2` 準備完了となるまで待ちます。diego-api-x ポッドの 1 つがアクティブとしてラベル付けされていることを確認します。

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. ステップ 3 とステップ 4 のように、Cloud Controller が BBS API にアクセスできるかどうかを確認します。以下のような出力を得られるはずです。

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    Connection to diego-api.cf.svc.cluster.local 8889 port [tcp/*] succeeded!
    ```

8. CF アプリのステージング用の環境が準備できました。
