---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-12-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment の新機能

本書では、現在日付までにリリースされた {{site.data.keyword.cfee_full_notm}} サービスの各バージョンの新機能について説明します。


## バージョン 2.0.1
{: #v201}

_リリース日:_ 2019-01-10

{{site.data.keyword.cfee_full_notm}} サービス (CFEE) のバージョン 2.0.1 では、以下の変更がリリースされました。 ご使用の CFEE のバージョンを更新するには、CFEE のユーザー・インターフェースの_「更新とスケーリング」_ページに移動します。

* カスタム・ドメインが正しく機能しないという問題が解決されました。
* 新規メトリックの取得中に組織のメトリックを使用できないという問題が解決されました。


## バージョン 2.0.0
{: #v200}

_リリース日:_ 2018-12-13

{{site.data.keyword.cfee_full_notm}} サービス (CFEE) のバージョン 2.0.0 では、以下の変更がリリースされました。 ご使用の CFEE のバージョンを更新するには、CFEE のユーザー・インターフェースの_「更新とスケーリング」_ページに移動します。

* CFEE バージョン更新の回復力が向上しました。
* CFEE インスタンスの運用の可用性と回復力が向上しました。
* アプリケーションへのよりセキュアなアクセスのためのクライアント・サイドの証明書を使用することにより、サーバーがアプリケーションに付与できるアクセス権限は、認証されたクライアントに対するアクセスのみになります。
* CFEE インスタンスを作成する際に、サポートする Kubernetes クラスターと Cloud Object Storage サービス・インスタンスが CFEE サービス・インスタンスと同じリソース・グループに作成されるようになりました (「デフォルトの」リソース・グループの下ではありません)。
* セキュリティー・パッチ。
* `ibmcloud cfee` CLI の改良:
    * CFEE スペースから IBM Cloud サービス・インスタンスを作成して、それをその CFEE スペースに追加するための新規コマンド (`ibmcloud cfee service-create`、`ibmcloud cfee service-alias-create`)。
    * CFEE の容量をスケーリングするための新規コマンド (`ibmcloud cfee scale-up`、`ibmcloud cfee scale-down`)。
    * CFEE インスタンスを管理するためのコマンドの改良 (`ibmcloud cfee environments`)。
    
      これらのコマンド機能拡張にアクセスするための ibmcloud CLI (`ibmcloud update`) の更新。詳しくは、`ibmcloud cfee -help` を発行してください。
      
**注**: CFEE インスタンスをバージョン 2.0.0 に更新する場合は、コントロール・プレーンとセルの両方を更新する_更新_ アクションを 1 回実行するだけで済みます。 CFEE コントロール・プレーンとセルを別個に更新する必要はありません。


## バージョン 1.1.2
{: #v112}

_リリース日:_ 2018-12-07

{{site.data.keyword.cfee_full_notm}} サービスのバージョン 1.1.2 では、以下の変更がリリースされました。
* CFEE インスタンスのプロビジョニングのために、チェンナイ (che01) とミラノ (mil01) の新規データ・センターを利用できるようになりました。
* セキュリティー・パッチ。

## バージョン 1.1.1
{: #v111}

_リリース日:_ 2018-11-28

{{site.data.keyword.cfee_full_notm}} サービスのバージョン 1.1.1 では、以下の変更がリリースされました。
* セキュリティー・パッチ。
   
## バージョン 1.1.0
{: #v110}

_リリース日:_ 2018-11-16

{{site.data.keyword.cfee_full_notm}} サービスのバージョン 1.1.0 では、以下の変更がリリースされました。

* 新規機能:
   * CFEE インスタンスは、IBM Cloud アカウントに使用されるインフラストラクチャー上でホストされた [virtual-dedicated](https://console.bluemix.net/docs/containers/cs_clusters.html#clusters#clusters_ui_standard) Kubernetes ワーカー・ノードでプロビジョンできます。
   * CFEE インスタンスのプロビジョニングのために、東京 (tok05) の新規データ・センターを利用できるようになりました。
   * CFEE インスタンスが新規バージョンに[更新](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update)されました。
   * Cloud Foundry セルを追加または削除して、CFEE インスタンスの容量を[スケーリング](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale)できます。
   * 自動構成される IBM Cloud Activity Tracker サービス・インスタンスと統合して、Cloud Foundry のアクティビティーを[監査](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing)できます。
   * 自動構成される IBM Cloud Log Analysis サービス・インスタンスで、Cloud Foundry の[ログ・イベント](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging)を永続化できます。
   * CFEE コンポーネントの運用状況を示す「ヘルス・チェック」ビュー。
   * コマンド・ライン・インターフェース (CLI) で CFEE 関連のアクションを実行する以下の新規コマンド。
     * `ibmcloud cfee create`、`ibmcloud cfee create-locations`、および `ibmcloud cfee create-status` コマンド。コマンド・ライン・インターフェースから CFEE インスタンスを作成し、CFEE のプロビジョンに利用できるデータ・センターのリストを取得して、作成中の CFEE のプロビジョニングの状況を確認します。
     * `ibmcloud cfee create-permission-get` および `ibmcloud cfee create-permission-set` [コマンド](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating)。CFEE インスタンスの作成に必要な許可を取得して設定します。 これらのコマンドにより、CFEE サービスおよび必要な補助サービスに対する許可の設定をまとめて単純化することができます。
     * `ibmcloud catalog blacklist` コマンド。IBM Cloud アカウント内のユーザーに対する IBM Cloud サービスの[可視性の制御](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)を簡単に行えるようにします。

* 解決された問題:
   *  解決された問題: セルのメトリックへのアクセス中に断続的にエラーが発生する
<br/>   
この[短いビデオ](https://ibm.biz/CFEE-V110){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") で、CFEE v1.1.0 の新機能について説明しています。  [CFEE ビデオの再生リスト](https://ibm.biz/CFEE-Playlist){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") には、さまざまな CFEE のトピックに関するその他のビデオもあります。
