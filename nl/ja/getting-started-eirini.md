---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Eirini テクニカル・プレビューの概要
{: #getting-started-eirini}

{{site.data.keyword.cfee_full}} (CFEE) は、クラウドでアプリおよびサービスをホストするためのクラウド・プラットフォームです。 {{site.data.keyword.cfee_full_notm}} を使用すると、使用量の拡大に合わせてアプリを拡張するのが容易になり、ランタイム、ミドルウェア、およびインフラストラクチャーが簡素化するため、アプリの開発に集中することができます。
{: shortdesc}

この入門チュートリアルでは、Eirini テクニカル・プレビュー・プランでの {{site.data.keyword.cfee_full_notm}} の作成、ユーザーの追加、組織およびスペースの作成、アプリのデプロイ、サービスへのそれらのアプリのバインドを行う方法について説明します。
Cloud Foundry Foundation の Eirini インキュベーター・プロジェクトについては、[Eirini プロジェクト](https://www.cloudfoundry.org/project-eirini/)を参照してください。

## 許可について
{: #permissions}

{{site.data.keyword.cfee_full_notm}} のインスタンスを作成する前に、正しいアクセス・ポリシーが必要です。 詳しくは、『[許可](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)』を参照してください。

## ステップ 1: {{site.data.keyword.Bluemix_notm}} アカウントでインフラストラクチャー・リソースを作成できることの確認
{: #accountprep-environment}

CFEE インスタンスは、Kubernetes サービスから Kubernetes ワーカー・ノードにデプロイされます。  [IBM Cloud アカウントを準備](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)して、CFEE インスタンスに必要なインフラストラクチャー・リソースを作成できるようにします。

## ステップ 2: CFEE インスタンスの作成
{: #create-environment}

CFEE を作成する前に、環境を作成する {{site.data.keyword.Bluemix_notm}} アカウントで作業していて、必要なアクセス・ポリシーを持っていることを確認してください (上記のステップ 1)。

1.  {{site.data.keyword.Bluemix_notm}} [ カタログ](https://cloud.ibm.com/catalog)を開きます。

2.  カタログで {{site.data.keyword.cfee_full_notm}} サービスを見つけてクリックし、そのサービスの概要ページを開きます。  その最初のページに、サービスの主な機能の概要が示されます。 **「続行」**をクリックします。

3.  作成する CFEE インスタンスを構成します。
    * _Eirini テクニカル・プレビュー_・プランを選択します。
    * CFEE インスタンスの**「名前」**を入力します。
    * 環境がグループ化される**「リソース・グループ」**を選択します。 現在の IBM Cloud アカウントでアクセスできるリソース・グループのみが、「_リソース・グループ_」ドロップダウンに表示されます。つまり、CFEE を作成するには、アカウントで少なくとも 1 つのリソース・グループにアクセスするための許可を備えている必要があります。
    * サービス・インスタンスがプロビジョンされる**「ジオグラフィー」**と**「ロケーション」**を選択します。 [プロビジョンに使用可能なロケーションおよびデータ・センター](https://cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") のリスト (CFEE のジオグラフィーおよびサポートされているサービス別) を参照してください。 

4. CFEE インスタンスが Kubernetes クラスター上でプロビジョンされます。Cloud Foundry セルは、Kuberentes クラスターのワーカー・ゾーン内でプロビジョンされます。以下のようにして、クラスターのロケーション、ハードウェア、暗号化を構成できます。
    * Kubernetes クラスターのハードウェアの分離を選択します。   
      * _仮想 - 共有_: ハイパーバイザーや物理ハードウェアなどのクラスター内のインフラストラクチャー・リソースはご自身と他の IBM のお客様との間で分配されますが、各ワーカー・ノードは自分用のシングル・テナントです。
      * _仮想 - 専用_: クラスター内のワーカー・ノードはお客様のアカウント専用のインフラストラクチャーでホストされます。
    * クラスター内のデータは、デフォルトで暗号化されます。_「ローカル・ディスクの暗号化」_をオフにすることもできます。
    * Kubernetes クラスターをプロビジョンする**「地域」**と**「地域」**を選択します。
    * Kubernetes ワーカー・ノードのデプロイ先の**「ゾーン」**を選択します。選択されたゾーンで使用可能な VLAN が自動的に取得されます。使用可能な VLAN がない場合は、自動的に作成されます。
    CFEE v2.2.0 以降の CFEE インスタンスは、**分離ネットワーク**の背後でも作動可能です。分離ネットワーク内のプライベート VLAN を選択すると、CFEE インスタンスを分離ネットワークにプロビジョンできます。CFEE の作成後、CFEE を作動させるためには、CFEE の Compose for PostgreSQL インスタンス用、Cloudant オブジェクト・ストレージ・インスタンス用、および Kubernetes クラスターのアプリケーション・ロード・バランサー ([ALB](https://cloud.ibm.com/docs/containers/cs_ingress.html#private_ingress)) 用の IP アドレスがネットワーク管理者によって分離ネットワークでルーティングされる必要があります。
    
    CFEE が作成されると、環境のプロビジョン対象となる Kubernetes クラスターが、IBM Cloud アカウントのその他のリソースの場合と同様に、{{site.data.keyword.Bluemix_notm}} [ダッシュボード](https://cloud.ibm.com/dashboard/apps/)に表示されます。詳しくは、[Kubernetes サービスの資料](https://cloud.ibm.com/docs/containers/cs_why.html#cs_ov)を参照してください。

5.  CFEE の容量を構成します。
    * CFEE の**「セルの数」**を選択します。これらは、CFEE にデプロイされるアプリケーションをホストするアプリケーション・セルです。  
    * **「ノード・サイズ」**を選択します。これにより、Cloud Foundry セルの容量 (CPU とメモリー) が決まります。
    
    上記で指定したアプリケーション・セルに加えて、CFEE 内の Cloud Foundry プラットフォームの操作と制御のために、追加の_コントロール・プレーン・セル_ が作成されて予約されます。 

    **注:** Kubernetes クラスター内の複数のワーカー・ノードが異なるサブネットにプロビジョンされている場合、VLAN スパンニングを有効にすることをお勧めします。  VLAN スパンニングが無効になっている場合、ワーカー・ノードが異なるサブネットにあると、それらのノード間での接続が妨げられることがあります。  詳しくは、[VLAN スパンニング](https://cloud.ibm.com/docs/containers/cs_subnets.html#vlan-spanning)の資料を参照してください。
    
6.  **「Compose for PostgreSQL」**フィールドで、パブリック組織のうちのいずれかを選択し、その組織内で使用可能なスペースの 1 つを選択します。 Compose for PostgreSQL のインスタンスが、選択したスペースにプロビジョンされます。 Compose for PostgreSQL サービスは、CFEE サービスの必須の依存関係です。

    **注:** _Compose for PostgreSQL_ では、CFEE インスタンスをプロビジョンする予定のロケーション (上記のステップ 4) にあり、かつ、お客様がアクセス権限を持つ組織のみを選択できます。  特定の組織内では、_開発者_ アクセス権限をお持ちのスペースのみが選択可能です。 

7.  ページの右側にある**「発注要約」**に、CFEE インスタンスおよび付属サービスのコストが、月次合計の見積もりと共に示されます。

8.  **「作成」**をクリックします。これにより、環境ダッシュボードが開き、作成の進行および状況が示されます。

**注:** 作成プロセスが開始すると、CFEE のテーブル行が {{site.data.keyword.Bluemix_notm}} ダッシュボード、_リソース・リスト_、および [Cloud Foundry 環境ダッシュボード](https://cloud.ibm.com/dashboard/cloudfoundry?filter=cf_environments)に表示されます。  作成が完了すると、テーブル行の状況にそれが示されます。

環境を作成する自動化プロセスにより、インフラストラクチャーが Kubernetes クラスターにデプロイされ、使用する準備ができた状態になるように構成されます。 このプロセスには、90 から 120 分かかります。

CFEE が作成されると、CFEE および補助サービスのプロビジョニングを確認する複数の E メールと、対応する注文の状況を通知する E メールが送られてきます。

CFEE インスタンスを作成すると、同じ IBM Cloud アカウントに、さらに 3 つの補助サービス・インスタンスが作成されます。 これらの補助サービス・インスタンスの名前は、CFEE インスタンス名に基づく名前になります。 それで、CFEE を作成すると、以下のように、合計 4 つのサービス・インスタンスが IBM Cloud アカウントに作成されます。
* CFEE インスタンス (「_cfeename_」)。
* Kubernetes クラスター (「_cfeename_-cluster」)。 このクラスターは、CFEE インスタンスがプロビジョンされるインフラストラクチャーを提供します。
* Cloud Object Storage インスタンス (「_cfeename_-cos」)。 このインスタンスは、CFEE アプリケーション・コンテナーの作成中に生成されるデータ (例えば、アップロードされたアプリケーション・パッケージ、ビルドパック、およびコンパイルされた実行可能プログラムなど) を保管するために使用されます。
* Compose for PosgreSQL インスタンス (「_cfeename_-postgres」)。 このインスタンスは、Cloud Foundry データ (例えば、アプリケーションのデプロイメント、開始イベント、停止イベントの監査や、CFEE ユーザーのメンバーシップ、組織、スペース、アプリケーション、およびサービス接続の記録など) を CFEE インスタンスに保管するために使用されます。 

## ステップ 3: 組織およびスペースの作成
{: #create-orgsandspaces}

{{site.data.keyword.cfee_full_notm}} の作成後は、『[組織およびスペースの作成](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)』を参照して、組織およびスペースを作成して環境を構造化する方法に関する情報を確認します。 {{site.data.keyword.cfee_full_notm}} のアプリは、特定のスペース内にスコープ設定されます。 そして、スペースは特定の組織内に存在します。組織のメンバーは、割り当て量プラン、アプリ、サービス・インスタンス、およびカスタム・ドメインを共有します。

組織を作成するときは、それに割り当て量を割り当ててください。割り当て量により、その組織で使用できるリソース (メモリー、CPU など) に制限を設定できます。あとで別の割り当て量を割り当てることができます。各 CFEE で使用可能な一連の事前構成済み割り当て量がありますが、CFEE ユーザー・インターフェースの**「割り当て量」**ページで独自のカスタム割り当て量を作成することもできます。カスタム割り当て量を_デフォルト_ 割り当て量にすることもできます。これを行うには、割り当て量のメニューから_「デフォルトにコピー (Copy to default)」_アクションを呼び出します。これでカスタム割り当て量の値がデフォルト割り当て量にコピーされます。

**注:** 上部の IBM Cloud ヘッダーにある**_「管理」>「アカウント」>「Cloud Foundry の組織」_**メニューで表示される「_Cloud Foundry の組織 (Cloud Foundry organizations)_」ページは、パブリック IBM Cloud 組織専用であり、**CFEE 組織用ではありません**。 CFEE 組織は、CFEE インスタンスの「_組織_」ページで管理します。  CFEE ユーザー・インターフェースを開き、**「_Organizations_」**ページをクリックして、その CFEE の組織を作成および管理します。

## ステップ 4: 組織およびスペースへのユーザーの追加
{: #add-users}

アクセス・レベルを制御する特定の役割の割り当てが行われる組織およびスペースに[ユーザーを追加](https://cloud.ibm.com/docs/cloud-foundry/add-users.html)します。  CFEE で組織およびスペースのメンバーとしてユーザーを追加するには、そのユーザーは CFEE インスタンスに事前にアクセスできるようになっている必要があります。 『[許可](https://cloud.ibm.com/docs/cloud-foundry/permissions.html)』を参照してください。

## ステップ 5: アプリケーションのデプロイおよび表示
{: #deploy-apps}

準備ができたら、{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを使用して [アプリをデプロイ](https://console.bluemix.net/docs/cloud-foundry/deploy-apps.html)できます。  ユーザー・インターフェースでデプロイ済みアプリケーションのリストを表示します。これは、特定の CFEE スペースのコンテキストで、あるいはすべての CFEE インスタンスでグローバルに表示できます。  該当するビューからアプリケーションを開始、停止、または削除することもできます。

## ステップ 6: CFEE スペースへの IBM Cloud サービス・インスタンスの作成または追加
{: #service-instances}

IBM Cloud アカウント内で[サービスの作成](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)や[既存サービスの追加](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)を実行できます。  CFEE スペース内でサービス・インスタンスが使用可能になると、そのサービス・インスタンスをそのスペース内にデプロイされた CFEE アプリケーションにバインドすることができます。

## ステップ 7: サービス・インスタンスへのアプリケーションのバインド
{: #bind-apps}

サービスの機能を使用するためにサービス・インスタンス別名に[アプリをバインド](https://console.bluemix.net/docs/cloud-foundry/binding.html)します。

[Cloud Foundry ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/overview){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") では、*パブリック* と*エンタープライズ* の両方のすべてのアプリケーションとサービスの統合ビューを表示することができます。  Cloud Foundry ダッシュボードで、左側のナビゲーション・ペインの*「パブリック」*をクリックすると、IBM Cloud アカウント内の使用可能なパブリック・アプリケーションおよびサービスが表示されます。  *「エンタープライズ」*をクリックすると、すべての CFEE 環境、CFEE スペースにデプロイされたアプリケーション、および CFEE スペースで使用可能なサービスが表示されます。
{:tip}

## ステップ 8: アプリケーションを管理するための Stratos コンソールのインストール (オプション)
{: #install-stratos}

Stratos コンソールは、Cloud Foundry で作業するためのオープン・ソースの Web ベース・ツールです。 Stratos コンソール・アプリケーションをオプションで特定の CFEE 環境にインストールして使用することで、組織、スペース、およびアプリケーションを管理できます。

CFEE インスタンスで IBM Cloud の管理者またはエディターの役割を備えているユーザーは、その CFEE インスタンスに Stratos コンソール・アプリケーションをインストールできます。

Stratos コンソール・アプリケーションをインストールするには、以下のようにします。

1. Stratos コンソールをインストールする CFEE インスタンスを開きます。
2. 概要ページで**「Stratos コンソールのインストール (Install Stratos Console)」**をクリックします。 このボタンは、当該 CFEE インスタンスに対する管理者またはエディターの許可を備えているユーザーにのみ表示されます。
3. 「Stratos コンソールのインストール (Install Stratos Console)」ダイアログで、インストール・オプションを選択します。 Stratos アプリケーションは、Cloud Foundry セルまたは Kubernetes クラスターにインストールできます。 Stratos コンソールのバージョン、およびインストールするアプリケーションのインスタンス数を選択します。 Cloud Foundry セルに Stratos コンソール・アプリをインストールする場合、アプリケーションをデプロイする組織とスペースを指定するように求められます。
4. **「インストール (Install)」**をクリックします。

アプリケーションのインストールに約 5 分かかります。 インストールが完了すると、概要ページに「_Stratos コンソールのインストール (Install Stratos Console)_」ボタンの代わりに**「Stratos コンソール (Stratos Console)」**ボタンが表示されます。 「_Stratos コンソール (Stratos Console)_」ボタンは、当該コンソールを起動するものであり、CFEE インスタンスにアクセスできるすべてのユーザーに使用可能になります。 組織およびスペースのメンバーシップの割り当てにより、Stratos コンソールでユーザーが表示および管理できる内容が制限されることがあります。

Stratos コンソールを開始するには、以下のようにします。

1. Stratos コンソールがインストールされている CFEE インスタンスを開きます。
2. 概要ページの**「Stratos コンソール (Stratos Console)」**をクリックします。
3. 別個のブラウザー・タブに Stratos コンソールが開きます。 コンソールを初めて開いた場合、自己署名証明書が原因で発生する連続する 2 つの警告を受け入れるように求められます。
4. **「ログイン」**をクリックしてコンソールを開きます。 アプリケーションでは {{site.data.keyword.Bluemix_notm}} 資格情報が使用されるため、資格情報は不要です。


## 追加リソース
{: #additional-resources}

`ibmcloud CFEE` CLI コマンドを使用して、CFEE でいくつかの管理タスクを実行できます。 これらのコマンドを使用すると、CFEE インスタンスに関する情報の取得、およびその組織とスペースの管理を行うことができます。 [IBM Cloud CLI CFEE コマンド・リファレンス](https://console.cloud.ibm.com/docs/cli/reference/ibmcloud/cli_cfee.html#ibmcloud_commands_cfee){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。

さまざまな CFEE トピックについて詳しく解説し、実演しているビデオが [CFEE ビデオの再生リスト](https://ibm.biz/CFEE-Playlist){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。

CFEE API についての情報は、CFEE [API 資料](https://cloud.ibm.com/apidocs/cfaas){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。
