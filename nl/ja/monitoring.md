---

copyright:
  years: 2018
lastupdated: "2018-08-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# モニター
{: #monitoring}

{{site.data.keyword.cfee_full}} インスタンスとそのサポートされるインフラストラクチャーのモニターは、Prometheus と Grafana から成るオープン・ソースのツール・セットによってサポートされます。  このソリューションを使用すると、Cloud Foundry 環境でメトリックのアラートの分析、視覚化、および管理を行うことができます。  モニターが行われる 3 つの Web コンソールがあります。Grafana コンソール、Prometheus コンソール、および Prometheus Alert Manager コンソールです。

**注:** {{site.data.keyword.cfee_full}} インスタンスのモニター機能にアクセスするには、CFEE インスタンスをサポートする Kubernetes クラスターで_管理者_ または_エディター_ の役割が必要です。  CFEE インスタンスをサポートする Kubernetes クラスターのデフォルト名は、_`<CFEEname>`-cluster_ です。

## Prometheus
{: #prometheus}

Prometheus はオープン・ソース・システム・モニター/アラート・ツールキットです。 Prometheus は、2012 の登場以降、多くの企業および組織に採用されており、このプロジェクトには非常にアクティブな開発者およびユーザー・コミュニティーが存在します。
これはスタンドアロンのオープン・ソース・プロジェクトであり、どの企業からも独立して保守されています。 これを強調するため、そしてプロジェクトのガバナンス構造を明確化するため、Prometheus は、2016 年に Kubernetes に続く 2 番目のホスト・プロジェクトとして Cloud Native Computing Foundation に参加しました。 詳しくは、[Prometheus の資料](https://prometheus.io/docs/introduction/overview/)を参照してください。

Prometheus エコシステムは、以下の複数のコンポーネントで構成され、その多くはオプションです。

* 時系列データをスクレイピングして保管するメイン Prometheus サーバー。</li>
* アラートを処理する [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/)。</li>
* ノード・エクスポーター、ブラック・ボックス・エクスポーターなど、さまざまな特殊目的のエクスポーター。</li>
* 短期存続ジョブをサポートするためのプッシュ・ゲートウェイ。</li>

Prometheus は、直接、または短期存続ジョブ用の仲介プッシュ・ゲートウェイを介して、インスツルメントされたジョブからメトリックを収集します。 収集されたすべてのサンプルをローカルに保管し、そのデータに対してルールを実行して、既存のデータから新規時系列を集約および記録するか、アラートを生成します。

## Grafana
{: #grafana}

Grafana は、Prometheus によって収集されたすべてのメトリック用のオープン・ソースの分析プラットフォームです。 クラスターにデプロイされた Grafana バージョンは、基盤の Prometheus データベースを使用するように既に構成されています。 また、有用な Grafana ダッシュボードもいくつか含まれています。  詳しくは、[Grafana の資料](http://docs.grafana.org/guides/getting_started/)を参照してください。

## モニターの使用開始
{: #gettingStarted_monitor}

モニター・ソリューションを構成する Prometheus および Grafana コンポーネントは、CFEE インスタンスをサポートする Kubernetes インフラストラクチャーにプリインストールされています。  モニター・ツールにアクセスするには、Prometheus、Prometheus AlertManager、および Grafana の各サーバーのポートを転送する必要があります。これは、Kubernetes CLI を使用して行います。
以下に、必要な CLI をインストールし、サーバーのポートを転送し、コンソールを起動するためのステップを順に示します。

**注:** 以下の説明は、{{site.data.keyword.cfee_full}} ユーザー・インターフェースにもあります。  CFEE インスタンスのユーザー・インターフェースを開き、左ナビゲーション・ペインにある**「モニタリング」**をクリックすると、説明が表示されます。

### 前提条件

1. [アクセス・ポリシー](https://console.bluemix.net/iam/#/users)を調べて、環境をサポートする Kubernetes クラスターに少なくともビューアー役割があることを確認してください。
2. [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use) をインストールします。
3. [Kubernetes CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/) をインストールします。  既存の Kubernetes CLI がある場合は、最新バージョンをインストールすることをお勧めします。
4. 以下のように、コンテナー・サービス・プラグインをインストールします。
```
    ibmcloud plugin install container-service -r Bluemix
```

### Kubernetes クラスターへのアクセス

1. 以下のように、IBM Cloud アカウントにログインします。

  ```
  ibmcloud login -a https://api.ng.bluemix.net
  ```
  {: pre}

  フェデレーテッド ID がある場合は、__ibmcloud login -sso__ を使用して IBM Cloud CLI にログインします。

2. 以下のように、作業する IBM Cloud Container Service 地域 (例えば、us-south) をターゲット化します。

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}

3. 以下のように、CLI でクラスターのコンテキストを設定します。

  a. 以下のように、環境変数を設定し、Kubernetes 構成ファイルをダウンロードするコマンドを取得します。

  ```
  ibmcloud cs cluster-config <CFEE_instance_name>-cluster
  ```
  {: pre}

  b. KUBECONFIG 環境変数を設定します。 前のコマンドからの出力をコピーし、端末に貼り付けます。 コマンド出力は、以下のようなものです。
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### サーバー・ポートの転送
4. Prometheus、AlertManager、および Grafana が実行されているポッド用に Kubernetes クラスターでポート転送をセットアップします。 これにより、ローカル・マシン (localhost) で代わりにモニター・メトリックをホストできるようになります。

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000'
  ```
  {: pre}

### ローカル Web プロキシーでのモニター・コンソールの起動

5. Grafana コンソールを起動して、選択したメトリックでの分析を表示します。  CFEE インスタンスには、デフォルトの Grafana ダッシュボードが含まれています。 このデフォルトのダッシュボードはインタラクティブであり、CFEE インスタンスをホストするために使用されているインフラストラクチャーのビューが示されます。 (Kubernetes クラスター)。 Grafana コンソールを起動したら、Grafana コンソールの上部にある**「Home」**ボタンをクリックして、事前にデプロイされているダッシュボード (下のリストを参照) のいずれかを選択します。これにより、対応するメトリックがグラフ化されます。

   Grafana にはデフォルトの `admin` ユーザーが用意されています。そのデフォルトのパスワードは `admin` に設定されています。 ユーザー/パスワード `admin/admin` を使用してログインし、新規資格情報に変更することをお勧めします。

     [Grafana コンソールの起動](https://localhost:3000)

   CFEE インスタンスでは以下のデフォルトのダッシュボードが用意されており、「_Home_」ドロップダウンから使用できます。

   CFEE 環境をサポートする Kubernetes インフラストラクチャーのダッシュボード:
   - _Kubernetes Capacity Planing_ ダッシュボード
        - kubernetes インフラストラクチャーのキャパシティーを示します。
   - _Kubernetes Cluster Health_ ダッシュボード
        - Kubernetes クラスターの正常性を示します。
   - _Kubernetes Cluster Status_ ダッシュボード
        - Kubernetes クラスターの状況を示します。
   - _Kubernetes Resource Requests_ ダッシュボード
        - Kubernetes クラスターの使用されている CPU、メモリー、およびその他のパラメーターを示します。
   - _Nodes_ ダッシュボード
        - Kubernetes クラスターの各ワーカー・ノードの詳細を示します。
   - _Pods_ ダッシュボード
        - Kubernetes クラスターで実行されている各ポッドの詳細を示します。
   - _Replica Set_ ダッシュボード
        - Kubernetes レプリカ・セットの状況を示します。
   - _Deployment_ ダッシュボード
        - Kubernetes デプロイメントの状況を示します。

   Cloud Foundry ダッシュボード:
   - _CF: Cells Capacity_ ダッシュボード
        - Cloud Foundry アプリケーションがデプロイされている Cloud Foundry セルの一般的な状況を示します。
   - _CF: Router_ ダッシュボード
        - CFEE 環境で実行されている Cloud Foundry ルーターの状況を示します。
   - _CF: Diego_Cell_ ダッシュボード
        - Cloud Foundry セルおよび Diego コンポーネントの状況を示します。

6. オプションとして、以下のように、Prometheus コンソールを起動して Prometheus サーバーによって収集された生データを表示したり、Prometheus Alertmanager を起動して Prometheus サーバーによって送信されたアラートを管理したりすることもできます。

     [Prometheus サーバーの起動 (Launch Prometheus server)](https://localhost:9090)

     [Prometheus Alertmanager サーバーの起動 (Launch Prometheus Alertmanager server)](https://localhost:9093)
