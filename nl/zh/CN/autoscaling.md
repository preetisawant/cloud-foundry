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

# 自动缩放应用程序
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} 具有针对 Cloud Foundry 应用程序的内置自动缩放支持，用于自动调整应用程序实例数 
  * 根据应用程序性能指标进行动态缩放。
  * 安排基于时间的缩放。

此功能基于 Cloud Foundry 开放式源代码项目 [App-Autosaler][autoscaler_project] 提供。请参阅[用户指南][autoscaler_user_guide]以开始操作。 

## 通过 CLI 管理自动缩放

您可以使用 App Autosscaler 命令行界面插件 (aka AutosScaler CLI) 来管理策略以及查询度量值和缩放历史记录。 

### 安装 AutoScaler CLI
使用以下命令来安装 `AutoScaler CLI`，这是 Cloud Foundry CLI 的插件。  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

如果您有先前的安装，那么可以使用相同的命令将 `AutoScaler CLI` 插件更新到最新版本。 

### 使用 AutoScaler CLI

如果您已登录到 {{site.data.keyword.Bluemix}} 上的 Cloud Foundry 环境，并且如[部署应用程序指南][deploy_app]中所述在空间中运行应用程序，请执行以下步骤为应用程序创建缩放策略，以及查询度量值和缩放历史记录。 

 *  （可选）确认缺省情况下已正确设置 App-Autosaler API 端点。  

    如果 Cloud Foundry API 端点显示为 `api.<DOMAIN>`，那么 App-Autoscaler API 端点应为 `autoscaler.<DOMAIN>`.  
    使用以下命令来检查 App-Autoscaler API 端点设置。

    ```
    cf asa
    ```
    {:codeblock} 

    如果 App-Autoscaler API 端点不正确，那么需要使用以下命令进行重置：

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  在本地计算机上创建策略 JSON 文件。 

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

    上面的策略用于根据内存利用率在超过已定义阈值至少 `120 秒`后触发缩放。有关如何创建您自己的自动缩放策略的信息，请参阅 [Cloud Foundry App-Autosscaler 用户指南][autoscaler_user_guide]。

*  将策略附加到应用程序

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  （可选）此外，您可以查询应用程序的最新聚集度量值。App-Autosscaler 支持多个[度量值类型][metric_type]，但只能检索策略中定义的度量值，即上面示例中的 `memoryutil`。  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  （可选）使用以下命令来查询缩放历史记录：

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    有关使用命令行的更多选项，请参阅 [Cloud Foundry 应用程序 Autoscaler CLI 插件指南][autoscaler_cli]。 


## 通过 Stratos 控制台管理自动缩放 

除了命令行界面外，还可以通过 Stratos 控制台来管理自动缩放设置。 

如果已在 {{site.data.keyword.cfee_full}} (CFEE) 上安装 [stratos][stratos]，请转至应用程序仪表板中的“**自动缩放**”选项卡，以查看自动缩放策略和最新缩放事件的概述。单击任何磁贴中的任何图标以启动策略编辑器并编辑策略。

如果未定义自动缩放策略，那么概述页面将没有任何信息。单击**创建策略**以启动策略编辑器并创建策略。

我们建议浏览 [Cloud Foundry App-Autoscaler 用户指南][autoscaler_user_guide]来了解基本概念，以正确设置自动缩放策略。 

### 度量值统计信息

根据一个或多个所选度量值类型定义策略后，您可以查看最近 30 分钟的最新度量值和度量值历史记录。 

**注：**度量值表示对所有应用程序实例取平均值的数据，而不是来自每个应用程序实例的原始数据。
    
### 缩放历史记录

策略编辑器中的**历史记录**选项卡显示在应用程序上执行了自动缩放策略触发的缩放操作。它还显示因缩放失败而产生的任何错误消息。您可以查询过去 30 天内的缩放历史记录。 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]:https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]:https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
