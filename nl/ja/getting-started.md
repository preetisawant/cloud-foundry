---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 入門チュートリアル
{: #getting-started}

{{site.data.keyword.cfee_full}} は、クラウドでアプリおよびサービスをホストするためのクラウド・プラットフォームです。 {{site.data.keyword.cfee_full_notm}} を使用すると、使用量の拡大に合わせてアプリを拡張するのが容易になり、ランタイム、ミドルウェア、およびインフラストラクチャーが簡素化するため、アプリの開発に集中することができます。
{: shortdesc}

この概要チュートリアルでは、{{site.data.keyword.cfee_full_notm}} の作成、ユーザーの追加、組織およびスペースの作成、アプリのデプロイ、サービスへのアプリのバインドを行う方法について説明します。

## 許可について
{: #permissions}

{{site.data.keyword.cfee_full_notm}} のインスタンスで作業するには、サービス・ユーザーは適切な許可を備えている必要があります。 詳しくは、『[許可](https://console.bluemix.net/docs/cloud-foundry/permissions.html)』を参照してください。

## ステップ 1: {{site.data.keyword.Bluemix_notm}} アカウントでインフラストラクチャー・リソースを作成できることの確認
{: #accountprep-environment}

CFEE インスタンスは、Kubernetes サービスからの Kubernetes ワーカー・ノードであるインフラストラクチャー・リソースにデプロイされます。  [IBM Cloud アカウントを準備](https://console.bluemix.net/docs/cloud-foundry/prepare-account.html)して、CFEEインスタンスに必要なインフラストラクチャー・リソースを作成できることを確認します。

## ステップ 2: CFEE インスタンスの作成
{: #creating-environment}

CFEE を作成する前に、環境を作成する {{site.data.keyword.Bluemix_notm}} アカウントで作業していて、必要なアクセス・ポリシーを持っていることを、(上記のステップ 1 に従って) 確認してください。

1.  {{site.data.keyword.Bluemix_notm}} [ カタログ](https://console.bluemix.net/catalog)を開きます。

2.  カタログで {{site.data.keyword.cfee_full_notm}} サービスを見つけてクリックし、そのサービスの概要ページを開きます。

3.  作成ページの最初のページに、サービスの主な機能の概要が示されます。 **「続行」**をクリックします。

4.  以下を指定して、作成する CFEE インスタンスを構成します。
    * プランを選択します (プランの可用性は、ベータでは制限されることがあります)。
    * サービス・インスタンスの**「名前」**を入力します。
    * サービス・インスタンスがプロビジョンされる**ロケーション**を選択します。 [プロビジョンに使用可能なロケーションおよびデータ・センター](https://console.bluemix.net/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") のリスト (CFEE のジオグラフィーおよびサポートされているサービス別) を参照してください。 
    * Cloud Foundry 環境の**「セル数 (Number of cells)」**を選択します。
    * **「マシン・タイプ (Machine type)」**を選択します。これにより、Cloud Foundry セルのサイズ (CPU およびメモリー) が決まります。
    * 環境がグループ化される**「リソース・グループ」**を選択します。 現在の IBM Cloud アカウントでアクセスできるリソース・グループのみが、「_リソース・グループ_」ドロップダウンに表示されます。つまり、CFEE を作成するには、アカウントで少なくとも 1 つのリソース・グループにアクセスするための許可を備えている必要があります。

5.  **「Compose for PostgreSQL」**フィールドで、パブリック組織のうちのいずれかを選択し、その組織内で使用可能なスペースの 1 つを選択します。 Compose for PostgreSQL のインスタンスが、選択したスペースにプロビジョンされます。 Compose for PostgreSQL サービスは、CFEE サービスの必須の依存関係です。

**注:** CFEE インスタンスをプロビジョンする予定のロケーション (上記のステップ 4) にあり、かつ、アクセス権限をお持ちの組織のみが選択可能です。  特定の組織内では、_開発者_ アクセス権限をお持ちのスペースのみが選択可能です。 

6.  オプションとして、**「インフラストラクチャー」**セクションを開き、CFEE インスタンスをサポートする Kubernetes クラスターのプロパティーを表示します。 **ワーカー・ノード数**はセル数に 2 を加えた値に等しいことに注意してください (プロビジョンされた Kubernetes ワーカー・ノードのうちの 2 つが CFEE 制御プレーンをサポートします)。
環境がデプロイされた Kubernetes クラスターは、{{site.data.keyword.Bluemix_notm}} [ダッシュボード](https://console.bluemix.net/dashboard/apps/)に表示されます。 詳しくは、[Kubernetes サービスの資料](https://console.bluemix.net/docs/containers/cs_why.html#cs_ov)を参照してください。

**注:** Kubernetes クラスター内の複数のワーカー・ノードが異なるサブネットにプロビジョンされている場合、VLAN スパンニングを有効にすることをお勧めします。  VLAN スパンニングが無効になっている場合、ワーカー・ノードが異なるサブネットにあると、それらのノード間での接続が妨げられることがあります。  詳しくは、[VLAN スパンニング](https://console.bluemix.net/docs/containers/cs_subnets.html#vlan-spanning)の資料を参照してください。

7.  ページの右側にある**「発注要約」**に、CFEE インスタンスおよび付属サービスのコストが、月次合計の見積もりと共に示されます。

8.  **「作成」**をクリックします。これにより、環境ダッシュボードが開き、作成の進行および状況が示されます。

9.  プロビジョニングが開始すると、{{site.data.keyword.Bluemix_notm}} ダッシュボードおよび [Cloud Foundry 環境ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments)に当該環境が表示されます。  プロビジョニングが完了すると、状況でそれが示されます。

環境を作成する自動化プロセスにより、インフラストラクチャーが Kubernetes クラスターにデプロイされ、使用する準備ができた状態になるように構成されます。 このプロセスには、90 から 120 分かかります。

環境が正常に作成されると、CFEE およびサポートされるサービスのプロビジョンを確認する複数の E メールと、対応する注文の状況を知らせる E メールが送られてきます。

## ステップ 3: 組織およびスペースの作成

{{site.data.keyword.cfee_full_notm}} の作成後は、『[組織およびスペースの作成](https://console.bluemix.net/docs/cloud-foundry/orgs-spaces.html)』を参照して、組織およびスペースを作成して環境を構造化する方法に関する情報を確認します。 {{site.data.keyword.cfee_full_notm}} のアプリは、特定のスペース内にスコープ設定されます。 そして、スペースは、特定の組織内に存在します。 組織のメンバーは、割り当て量プラン、アプリ、サービス・インスタンス、およびカスタム・ドメインを共有します。

**注:** 上部の IBM Cloud ヘッダーにある**_「管理」>「アカウント」>「Cloud Foundry の組織」_**メニューで表示される「_Cloud Foundry の組織 (Cloud Foundry organizations)_」ページは、パブリック IBM Cloud 組織専用であり、**CFEE 組織用ではありません**。 CFEE 組織は、CFEE インスタンスの「_組織_」ページで管理します。  CFEE ユーザー・インターフェースを開き、**「_Organizations_」**ページをクリックして、その CFEE の組織を作成および管理します。

## ステップ 4: 組織およびスペースへのユーザーの追加

アクセス・レベルを制御する特定の役割の割り当てが行われる組織およびスペースに[ユーザーを追加](https://console.bluemix.net/docs/cloud-foundry/add-users.html)します。  CFEE で組織およびスペースのメンバーとしてユーザーを追加するには、そのユーザーは CFEE インスタンスに事前にアクセスできるようになっている必要があります。 『[許可](https://console.bluemix.net/docs/cloud-foundry/permissions.html)』を参照してください。

## ステップ 5: アプリケーションのデプロイおよび表示

準備ができたら、{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを使用して [アプリをデプロイ](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)できます。  ユーザー・インターフェースでデプロイ済みアプリケーションのリストを表示します。これは、特定の CFEE スペースのコンテキストで、あるいはすべての CFEE インスタンスでグローバルに表示できます。  該当するビューからアプリケーションを開始、停止、または削除することもできます。

## ステップ 6: サービスの処理

IBM Cloud アカウント内で[サービスの作成](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#creating-services_inspace)や[既存サービスの追加](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#adding-services_inspace)を実行できます。  CFEE スペース内でサービス・インスタンスが使用可能になると、そのサービス・インスタンスをそのスペース内にデプロイされた CFEE アプリケーションにバインドすることができます。

## ステップ 7: サービス・インスタンスへのアプリケーションのバインド

サービスの機能を使用するためにサービス・インスタンス別名に[アプリをバインド](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#bind_services)します。

[Cloud Foundry ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/overview)についてご存じですか? そこでは、{{site.data.keyword.Bluemix_notm}} の_パブリック_ と_エンタープライズ_ (CFEE) の両方のすべてのアプリケーションおよびサービスの統合ビューを表示できます。  Cloud Foundry ダッシュボードで、左側のナビゲーション・ペインの_「パブリック」_をクリックすると、IBM Cloud アカウント内の使用可能なパブリック・アプリケーションおよびサービスが表示されます。  _「エンタープライズ」_をクリックすると、すべての CFEE 環境、CFEE スペースにデプロイされたアプリケーション、および CFEE スペースで使用可能なサービスが表示されます。
{:tip}

## ステップ 8: アプリケーションを管理するための Stratos コンソールのインストール (オプション)

Stratos コンソールは、Cloud Foundry で作業するためのオープン・ソースの Web ベース・ツールです。 Stratos コンソール・アプリケーションをオプションで特定の CFEE 環境にインストールして使用することで、組織、スペース、およびアプリケーションを管理できます。

CFEE インスタンスで IBM Cloud の管理者またはエディターの役割を備えているユーザーは、その CFEE インスタンスに Stratos コンソール・アプリケーションをインストールできます。

Stratos コンソール・アプリケーションをインストールするには、以下のようにします。

1. Stratos コンソールをインストールする CFEE インスタンスを開きます。
2. 概要ページで**「Stratos コンソールのインストール (Install Stratos Console)」**をクリックします。 このボタンは、当該 CFEE インスタンスに対する管理者またはエディターの許可を備えているユーザーにのみ表示されます。
3. 「Stratos コンソールのインストール (Install Stratos Console)」ダイアログで、インストール・オプションを選択します。 Stratos コンソール・アプリケーションは、CFEE コントロール・プレーンまたはいずれかのセルにインストールできます。 Stratos コンソールのバージョン、およびインストールするアプリケーションのインスタンス数を選択します。 セルに Stratos コンソール・アプリをインストールする場合、アプリケーションをデプロイする組織およびスペースを指定するように求められます。
4. **「インストール (Install)」**をクリックします。

アプリケーションのインストールに約 5 分かかります。 インストールが完了すると、概要ページに「_Stratos コンソールのインストール (Install Stratos Console)_」ボタンの代わりに**「Stratos コンソール (Stratos Console)」**ボタンが表示されます。 「_Stratos コンソール (Stratos Console)_」ボタンは、当該コンソールを起動するものであり、CFEE インスタンスにアクセスできるすべてのユーザーに使用可能になります。 組織およびスペースのメンバーシップの割り当てにより、Stratos コンソールでユーザーが表示および管理できる内容が制限されることがあります。

Stratos コンソールを開始するには、以下のようにします。

1. Stratos コンソールがインストールされている CFEE インスタンスを開きます。
2. 概要ページの**「Stratos コンソール (Stratos Console)」**をクリックします。
3. 別個のブラウザー・タブに Stratos コンソールが開きます。 コンソールを初めて開いた場合、自己署名証明書が原因で発生する連続する 2 つの警告を受け入れるように求められます。
4. **「ログイン」**をクリックしてコンソールを開きます。 アプリケーションでは {{site.data.keyword.Bluemix_notm}} 資格情報が使用されるため、資格情報は不要です。

CFEE API についての情報は、CFEE [API 資料](https://console.bluemix.net/apidocs/cfaas){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。
{:tip}


## 追加リソース
{: #additional-resources}

`ibmcloud CFEE` CLI コマンドを使用して、CFEE でいくつかの管理タスクを実行できます。これらのコマンドを使用すると、CFEE インスタンスに関する情報の取得、およびその組織とスペースの管理を行うことができます。[IBM Cloud CLI CFEE コマンド・リファレンス](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。

さまざまな CFEE トピックについて詳しく解説し、実演しているビデオが [CFEE ビデオの再生リスト](https://ibm.biz/CFEE-Playlist){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。

CFEE API についての情報は、CFEE [API 資料](https://console.stage1.bluemix.net/apidocs/cfaas){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。
