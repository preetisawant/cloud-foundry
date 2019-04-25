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

# 调试不可用的登台程序
{: #unavailable_stager}

本教程说明了如何在 {{site.data.keyword.cfee_full}} (CFEE) 上调试不可用的登台程序。

## 了解组件
{: #stager_components}

{{site.data.keyword.Bluemix_notm}} 公告牌系统 (BBS) 以主动或被动方式运行，并在 Locket 中维护锁定，以确保只有一个 BBS 处于活动状态。有时候，如果 Locket 与后端数据库失去连接，BBS 可能会进入无响应状态。在这种情况下，不会选择任何活动的 BBS，BBS API 不可访问，并且由于 Cloud Controller 无法与 BBS API 进行通信，因此 `cf push` 等操作将会失败。在 CFEE V2.0 及更高版本中，Diego BBS 和 Locket 在 diego-api-x pod 中运行，因此用户需要重新启动所有 diego-api-x pod 才能恢复环境。

## 影响
{: #stager_impact}

Diego BBS API 不可访问。用户无法执行 `cf push app`，并且 CF 应用程序登台失败，错误为`登台程序不可用`，如下所示：

```
    响应代码：503
    CC 代码：       0
    CC 错误代码：
    请求标识：    xxxxxxx-xxxxx-xxx-xxxx-xxxxxxxx
    描述：   {
    "description": "Stager is unavailable: execution expired",
    "error_code": "CF-StagerUnavailable",
    "code": 170010
    }
    服务器错误，状态码：503，错误代码：170010，消息：登台程序不可用：执行已到期
```

## 如何解决
{: #stager_howtofix}

错误消息`登台程序不可用`通常意味着 Cloud Controller 与 Diego BBS API 进行通信时遇到问题。请执行以下步骤来确认报告的问题是否与此案例相同。如果是，请继续恢复环境。

1. 通过检查 api-x pod 状态，确保 Cloud Controller 可用。

    ```
    kubectl get pod -n cf
    ```
    {: pre}

2. 例如，输出指示 2 个 api-x pod 正在运行：
    ```
    名称                            就绪   状态      重新启动   期限
    api-0                           2/2     Running     0          1d
    api-1                           2/2     Running     0          1d
    ```

3. 进入 api-0 pod。

    ```
    kubectl exec -ti api-0 bash -n cf
    ```
    {: pre}

4. 在 api-0 pod 中，如果收到如下错误，那么指示 Cloud Controller 无法访问 BBS。
    ```
    nc -zv diego-api.cf.svc.cluster.local 8889

    ```
    {: pre}

    - 例如，输出指示连接失败：
    ```
    nc: connect to diego-api.cf.svc.cluster.local port 8889 (tcp) 失败：连接超时
    ```

5. 退出 api-0，然后按如下所示删除所有 diego-api-x pod。Kubernetes 将自动重新创建所有项。

    ```
    kubectl delete pod diego-api-0 -n cf
    ```
    {: pre}

    在 CFEE 2.0 之前，Diego Locket 位于名为 diego-locket-x 的不同 pod 中。如果是这种情况，请如步骤 5 所示，重新启动所有 diego-locket-x pod。

6. 等待所有 diego-api-x pod 都处于 `running` 状态并且就绪性为 `2/2`。确保其中一个 diego-api-x pod 标记为活动。

    ```
    kubectl get pod  -n cf -L skiff-role-active
    ```
    {: pre}

7. 检查 Cloud Controller 是否可以访问 BBS API（如步骤 3 和步骤 4 所示）。您应该会获得下面的类似输出。

    ```
    api/0:/$ nc -zv diego-api.cf.svc.cluster.local 8889
    与 diego-api.cf.svc.cluster.local 8889 port [tcp/*] 连接成功！
    ```

8. 环境应该已准备好进行 CF 应用程序登台。
