---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment の新機能

本書では、現在日付までにリリースされた {{site.data.keyword.cfee_full_notm}} サービスの各バージョンの新機能について説明します。

## バージョン 2.2.0
{: #v220}

_リリース日:_ 2019-04-01

CFEE v2.2.0 には以下のバージョンの構成要素コンポーネントが含まれています。
* Cloud Foundry: v2.7.1.15.5
* Cloud Foundry API: v2.115.0
* CFEE ビルドパック: v0.1.5
* IBM Kubernetes サービス: バージョン更新はありません。**重要:** CFEE Kubernetes クラスターを v1.13 に更新してから CFEE v2.2.0 に更新することをお勧めします (CFEE v2.2.0 は、分離ネットワークで CFEE インスタンスが作動するときに必要です)。

{{site.data.keyword.cfee_full_notm}} サービス (CFEE) のバージョン 2.2.0 では、以下の変更がリリースされました。ご使用の CFEE のバージョンを更新するには、CFEE のユーザー・インターフェースにある**「更新とスケーリング」**ページに移動し、**「更新」**をクリックします。

* **マルチゾーン** Kubernetes クラスターで CFEE インスタンスを**作成**するための新しいオプション。マルチゾーンのクラスターで作成された CFEE インスタンスは、1 つのデータ・センター内のワーカー・ノード間でアプリケーション・インスタンスを分散させるだけでなく、複数のデータ・センター間でもアプリケーション・インスタンスを分散させるので、インフラストラクチャー障害に対するアプリケーションの弾力性が高くなります。また、マルチゾーンの CFEE は、さらにセルを追加したり、既存のセルを現在のゾーンから削除したりすることによって、**スケーリング**することもできます。CFEE インスタンスを作成すると、マルチゾーンの CFEE にゾーンを追加したりそこからゾーンを削除したりすることができなくなることに注意してください。
* CFEE v2.2.0 インスタンスが、[**分離ネットワーク**内で作動](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)できるようになりました。CFEE インスタンスが分離ネットワークから VLAN にデプロイされる場合、CFEE インスタンスを作動させるためには、一部のエンドポイント (IP アドレス) を[適切に特定してルーティングすることが必要になります](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#oppening-access-points)。CFEE インスタンスを分離ネットワークで作動させるためには、Kubernetes クラスター v1.13 が必要です。
* 内部 IBM ネットワーク経由で (CFEE スペースにデプロイされた) アプリケーションをサービス・インスタンスにバインドする新しい機能。この機能を使用すると、IBM Cloud サービス・エンドポイントをサポートするサービスを、パブリック・インターネットにアクセスしないでも利用できます。
* **モニタリング**・ツール:
    * CFEE の作成時に、モニタリング・ツール (Prometheus、Grafana、Alertmanager) は、デフォルトではプロビジョンされなくなりました。CFEE v2.2.0 でモニタリング・ツールがプロビジョンされるのは、CFEE 管理者が明示的に有効にする場合のみです。また、有効にした場合、モニタリング・ツールは CFEE コントロール・プレーンのワーカー・ノードにはプロビジョンされなくなりました。コントロール・プレーン外にある独自のワーカー・ノードにプロビジョンされます。モニタリング・ツールを有効にしてプロビジョンするには、CFEE の_「モニタリング」_ページ (左ナビゲーション・ペイン) に移動し、**「モニタリングの有効化」**をクリックします。 
    * 既存の CFEE をバージョン 2.2.0 に更新すると、既存のモニタリング・ツールがコントロール・プレーンから削除されます。モニタリング・ツールの既存のカスタム構成はすべて失われます。 
    *  デフォルトの [Alertmanager 構成](https://prometheus.io/docs/alerting/configuration/)を、アラートの処理、グループ化、通知ルーティングをカスタマイズできるようにするカスタム構成に置換する新しい機能。_「モニタリング」_ページでは、デフォルトの構成ファイルを_ダウンロード_ したり、ローカル・ファイル・システムから構成ファイルを_アップロード_ したりできます。構成ファイルの[例](https://github.com/prometheus/alertmanager/blob/master/doc/examples/simple.yml)を参照してください。
* {{site.data.keyword.Bluemix_notm}} [_リソース・リスト_](https://cloud.ibm.com/resources) と CFEE ユーザー・インターフェースで CFEE インスタンスをタグ付けする新しい機能。
* {{site.data.keyword.Bluemix_notm}} [**Cloud Foundry ダッシュボード**](https://cloud.ibm.com/dashboard/cloudfoundry/overview)のユーザー・エクスペリエンスに対する全般的な改善。_Cloud Foundry ダッシュボード_ には、CFEE スペースに別名割り当てされた CFEE インスタンス、アプリケーション、パブリック・サービスの全体像が示されます。 

**注:** 新しい **Eirini テクニカル・プレビュー**・プランは、新しい CFEE インスタンスを作成すると利用できます。このプランは前述のように v2.2.0 とは独立しており、_標準_ プランのみに適用されます。Eirini テクニカル・プレビュー・プランにより、Diego の代わりにネイティブ Kubernetes をコンテナー・スケジューラーとして使用して CFEE を探索することができます。詳しくは、[Eirini テクニカル・プレビューの概要](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)を参照してください。

こちらの[短いビデオ](https://ibm.biz/CFEE-V220){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") で CFEE v2.1.0 の新機能のデモンストレーションをご覧ください。


## バージョン 2.1.1
{: #v211}

_リリース日:_ 2019-03-20

{{site.data.keyword.cfee_full_notm}} サービス (CFEE) のバージョン 2.1.1 では、以下の変更がリリースされました。ご使用の CFEE のバージョンを更新するには、CFEE のユーザー・インターフェースの_「更新とスケーリング」_ページに移動します。

* 正常なプロビジョニングを妨げていた問題が解決されました。 


## バージョン 2.1.0
{: #v210}

_リリース日:_ 2019-02-20

**注:** このバージョンへは、バージョン **2.0.2** からのみ更新できます。バージョン 2.1.0 に更新する前に、バージョン 2.0.2 に更新してください。

{{site.data.keyword.cfee_full_notm}} サービス (CFEE) のバージョン 2.1.0 では、以下の変更がリリースされました。ご使用の CFEE のバージョンを更新するには、CFEE のユーザー・インターフェースにある**「更新とスケーリング」**ページに移動し、**「更新」**をクリックします。

* 新しい自動スケーリング機能。カスタム・ルールに基づいて Cloud Foundry アプリケーション・インスタンスを自動的にスケーリングします。自動スケーリングは、CLI および Stratos コンソールから利用できます。Stratos コンソールは、CFEE ユーザー・インターフェースの_「概要」_ページからインストールして起動することができます (オプション)。Stratos コンソールの_「アプリケーション」_ページでアプリケーションを選択し、**「自動スケーリング」**タブを探します。*「ポリシーの作成」*をクリックして、自動スケーリング・エディターを起動し、ターゲット・アプリケーションのスケーリング・ポリシーを定義します。
  詳しくは、[自動スケーリングの資料](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-autoscale_cloud_foundry_apps#autoscale_cloud_foundry_apps)を参照してください。
* CFEE ユーザー・インターフェースからビルドパックを管理する新しい機能。優先順位リストでビルドパックをドラッグ・アンド・ドロップによって位置決めすることもできます。この機能は、CFEE ユーザー・インターフェース (Stratos コンソールではない) の新しい**「ビルドパック」**ページで利用できます。このリリースでは、サイズが 1 MB 以下のビルドパック zip ファイルのみをユーザー・インターフェースで追加または更新できます。1 MB を超えるビルドパック zip ファイルは、`cf create-buildpack` コマンドと `cf update-buildpack` コマンドを使用してアップロードできます。 
* ユーザー・インターフェースから組織の割り当て量を管理する新しい機能。特定の割り当て量を使用している組織を視覚化することもできます。この機能は、CFEE ユーザー・インターフェース (Stratos コンソールではない) の新しい**「割り当て量」**ページで利用できます。新しい割り当て量を作成したり、既存の割り当て量を編集したりできます。割り当て量のメニューから**「デフォルトにコピー (Copy to Default)」**を呼び出して、デフォルトの割り当て量の値を既存の任意の割り当て量の値に更新することも可能です。
* ユーザー・インターフェースの新しい**「開始」**ページを使用すると、ユーザーが環境をセットアップして使用するためのほとんどの重要なタスクが示されます。
* **タグ**を IBM Cloud リソース・リストの CFEE インスタンスに追加できます。リソース・リストで追加されたタグは、CFEE の概要ページのヘッダーにも表示されます。
* **Cloud Foundry** バージョン 2.7.21。
* **Stratos** コンソールのバージョン 2.3.0 (セキュリティー・パッチが含まれます)。CFEE バージョンを単に更新するだけでは Stratos コンソールのバージョンは更新されないことに注意してください。Stratos コンソール (CFEE の概要ページ内) を削除してから再インストールする必要があります。それにより、最新の Stratos コンソール・バージョンが自動的に選出されます。
* ユーザーは、CFEE の概要ページの「オーバーフロー」メニューから、CFEE の「Kubernetes **クラスター**」ページにナビゲートできます。

**注:** CFEE v2.0.x から v2.1.0 にバージョンを更新する場合は、コントロール・プレーンとセルの両方を順に自動的に更新する_更新_ アクションを 1 回実行することによって、更新が行われます。v1.x.x バージョンから更新する場合、更新するには_更新_ アクションを 2 回に分けて行うことが必要で、1 回はコントロール・プレーンの更新用 (最初)、もう 1 回はセルの更新用です。

こちらの[短いビデオ](https://ibm.biz/CFEE-V210){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") で CFEE v2.1.0 の新機能のデモンストレーションをご覧ください。


## バージョン 2.0.2
{: #v202}

_リリース日:_ 2019-02-08

{{site.data.keyword.cfee_full_notm}} サービス (CFEE) のバージョン 2.0.2 では、以下の変更がリリースされました。ご使用の CFEE のバージョンを更新するには、CFEE のユーザー・インターフェースの_「更新とスケーリング」_ページに移動します。

* 正常なバージョン更新を妨げていた問題が解決されました。このバージョンは、バージョン **2.1.0** に更新するための前提条件です。


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
* アプリケーションへのよりセキュアなアクセスのためのクライアント・サイドの証明書により、サーバーはアプリケーションに対するアクセス権限を認証されたクライアントにのみ付与できます。
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
     * `ibmcloud catalog blacklist` コマンド。これは、IBM Cloud アカウント内のユーザーが、IBM Cloud サービスの[可視性の制御](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)を簡単に行えるようにします。

* 解決された問題:
   *  解決された問題: セルのメトリックへのアクセス中に断続的にエラーが発生する
<br/>   
この[短いビデオ](https://ibm.biz/CFEE-V110){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") で、CFEE v1.1.0 の新機能について説明しています。  [CFEE ビデオの再生リスト](https://ibm.biz/CFEE-Playlist){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") には、さまざまな CFEE のトピックに関するその他のビデオもあります。
