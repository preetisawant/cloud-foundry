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

# アプリケーションの自動スケーリング
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} には、以下の方法でアプリケーション・インスタンス数を自動的に調整する、Cloud Foundry アプリケーション用の自動スケーリングのサポートが標準装備されています。 
  * アプリケーション・パフォーマンス・メトリックに基づく動的スケーリング。
  * 時間に基づくスケジュールされたスケーリング。

この機能は、Cloud Foundry オープン・ソース・プロジェクトの [App-Autoscaler][autoscaler_project] に基づいて提供されます。使用を開始するには、[ユーザー・ガイド][autoscaler_user_guide]を参照してください。 

## CLI による自動スケーリングの管理

App Autoscaler コマンド・ライン・インターフェース・プラグイン (別名 AutoScaler CLI) を使用して、ポリシーの管理、メトリックとスケーリング履歴の照会を行うことができます。 

### AutoScaler CLI のインストール
以下のコマンドを使用して、Cloud Foundry CLI のプラグインである `AutoScaler CLI` をインストールします。  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

以前のインストール済み環境がある場合は、同じコマンドを使用して、`AutoScaler CLI` プラグインを最新のバージョンに更新することもできます。 

### AutoScaler CLI の使用

{{site.data.keyword.Bluemix}} の Cloud Foundry 環境に既にログインしていて、[アプリのデプロイのガイド][deploy_app]に説明されているようにスペース内でアプリケーションが稼働している場合は、以下の手順に従ってアプリケーションのためのスケーリング・ポリシーを作成し、メトリックとスケーリング履歴を照会します。 

 *  (オプション) App-Autoscaler API エンドポイントがデフォルトで正しく設定されていることを確認します。  

    Cloud Foundry API エンドポイントが `api.<DOMAIN>` として示される場合、App-Autoscaler API エンドポイントは `autoscaler.<DOMAIN>` となる必要があります。  
    以下のコマンドを使用して、App-Autoscaler API エンドポイントの設定を確認してください。

    ```
    cf asa
    ```
    {:codeblock} 

    App-Autoscaler API エンドポイントが正しくない場合は、以下のコマンドを使用して再設定する必要があります。

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  ローカル・マシン上にポリシー JSON ファイルを作成します。 

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

    上記のポリシーは、メモリーの使用状況に基づいて、定義されたしきい値を `120 秒`以上超過したときにスケーリングを起動するために使用されます。独自の自動スケーリング・ポリシーを作成する方法について詳しくは、[Cloud Foundry App-Autoscaler ユーザー・ガイド][autoscaler_user_guide]を参照してください。

*  ポリシーをアプリケーションに接続します

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (オプション) さらに、アプリケーションでの最新の集約メトリックを照会することもできます。App-Autoscaler は複数の[メトリック・タイプ][metric_type]をサポートしますが、ポリシー内で定義したメトリックだけを取り出すことができます。上記の例では `memoryutil` です。  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (オプション) 以下のコマンドを使用してスケーリング履歴を照会します。

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    コマンド・ラインを使用するためのその他のオプションについては、[Cloud Foundry App Autoscaler CLI プラグインのガイド][autoscaler_cli]を参照してください。 


## Stratos コンソールによる自動スケーリングの管理 

コマンド・ライン・インターフェースの他に、Stratos コンソールを使用して自動スケーリング設定を管理することもできます。 

[stratos][stratos] を {{site.data.keyword.cfee_full}} (CFEE) にインストールした場合、アプリケーション・ダッシュボードの**「自動スケーリング」**タブに移動して、自動スケーリング・ポリシーの概要および最新のスケーリング・イベントを参照できます。
任意のタイルにある任意のアイコンをクリックしてポリシー・エディターを起動し、ポリシーを編集します。

自動スケーリング・ポリシーが定義されていない場合、概要ページには情報が表示されません。**「ポリシーの作成」**をクリックしてポリシー・エディターを起動し、ポリシーを作成してください。

自動スケーリング・ポリシーを適切に設定するために、[Cloud Foundry App-Autoscaler ユーザー・ガイド][autoscaler_user_guide]を参照して基本概念を理解することをお勧めします。 

### メトリック統計

選択された 1 つ以上のメトリック・タイプに基づいてポリシーを定義した後に、最新のメトリック値と直近 30 分のメトリック履歴を表示できます。 

**注:** メトリックは、各アプリケーション・インスタンスからの生データではなく、すべてのアプリケーション・インスタンスでの平均のデータを表します。
    
### スケーリング履歴

ポリシー・エディターの**「履歴」**タブは、自動スケーリング・ポリシーによってトリガーされたスケーリング・アクションがアプリケーション上で実行されたことを示しています。それには、スケーリングの失敗によるエラー・メッセージも表示されます。過去 30 日間のスケーリング履歴を照会できます。 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]: https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
