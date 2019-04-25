---

copyright:
  years: 2017, 2018
lastupdated: "2019-04-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 環境の作成
{: #create-environment}

## 前提条件
* 環境を作成する {{site.data.keyword.Bluemix_notm}} アカウントで操作していることを確認してください。
* {{site.data.keyword.cfee_full_notm}} のインスタンスを作成する前に、正しい[許可](https://cloud.ibm.com/catalog/docs/cloud-foundry/permissions.html)を持っていることを確認してください。 
* [IBM Cloud アカウントを準備](https://cloud.ibm.com/docs/cloud-foundry/prepare-account.html)して、CFEE インスタンスに必要なインフラストラクチャー・リソースを作成できるようにします (CFEE インスタンスは、Kubernetes サービスから Kubernetes ワーカー・ノードにデプロイされます)。  

## CFEE インスタンスの作成
1.  {{site.data.keyword.Bluemix_notm}} [ カタログ](https://cloud.ibm.com/catalog)を開きます。

2.  カタログで {{site.data.keyword.cfee_full_notm}} サービスを見つけてクリックし、そのサービスの概要ページを開きます。  その最初のページに、サービスの主な機能の概要が示されます。 **「続行」**をクリックします。

3.  作成する CFEE インスタンスを構成します。
    * プランを選択します。このプランの制限事項について詳しくは、[Eirini テクニカル・プレビュー](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment#eirini)のセクションを参照してください。
    * CFEE インスタンスの**「名前」**を入力します。
    * 環境がグループ化される**「リソース・グループ」**を選択します。 現在の IBM Cloud アカウントでアクセスできるリソース・グループのみが、「_リソース・グループ_」ドロップダウンに表示されます。つまり、CFEE を作成するには、アカウントで少なくとも 1 つのリソース・グループにアクセスするための許可を備えている必要があります。
    * サービス・インスタンスがプロビジョンされる**「ジオグラフィー」**と**「ロケーション」**を選択します。 [プロビジョンに使用可能なロケーションおよびデータ・センター](https://cloud.ibm.com/catalog/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") のリスト (CFEE のジオグラフィーおよびサポートされているサービス別) を参照してください。 

4. CFEE インスタンスが Kubernetes クラスター上でプロビジョンされます。Cloud Foundry セルは、Kuberentes クラスターのワーカー・ゾーン内でプロビジョンされます。以下のようにして、クラスターのロケーション、ハードウェア、暗号化を構成できます。
    * Kubernetes クラスターのハードウェアの分離を選択します。   
      * _仮想 - 共有_: ハイパーバイザーや物理ハードウェアなどのクラスター内のインフラストラクチャー・リソースはご自身と他の IBM のお客様との間で分配されますが、各ワーカー・ノードは自分用のシングル・テナントです。
      * _仮想 - 専用_: クラスター内のワーカー・ノードはお客様のアカウント専用のインフラストラクチャーでホストされます。
    * クラスター内のデータは、デフォルトで暗号化されます。_「ローカル・ディスクの暗号化」_をオフにすることもできます。
    * Kubernetes クラスターをプロビジョンする**「地域」**と**「地域」**を選択します。
    * Kubernetes ワーカー・ノードのデプロイ先の**「ゾーン」**を選択します。ワーカー・ノードは、同じゾーン (**単一ゾーン**) または複数のゾーン (**マルチゾーン**) にプロビジョンすることができます。**注意点として**、マルチゾーンの CFEE を作成する場合は [VLAN スパンニング](https://cloud.ibm.com/docs/containers?topic=containers-subnets#vlan-spanning)が必要です。VLAN スパンニングは、{{site.data.keyword.Bluemix_notm}} アカウントが [VRF 対応](https://cloud.ibm.com/docs/infrastructure/direct-link/vrf-on-ibm-cloud.html#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud)である場合もサポートされます。
    
    選択されたゾーンで使用可能な VLAN が自動的に取得されます。使用可能な VLAN がない場合は、自動的に作成されます。
    
    **注: 分離ネットワークでのプロビジョニング:** 分離ネットワーク内の VLAN をターゲットにすることができます。分離ネットワーク内で CFEE インスタンスが作成された場合、CFEE を正常にプロビジョンするには、分離ネットワーク内のポリシー (calico ポリシーや VRA ルールなど) で、CFEE インスタンスからの ALL アウトバウンド・アクセスを許可する必要があります。CFEE が作成されると、IBM Cloud 内の特定のサービスとマイクロサービスへのアウトバウンド・アクセス以外は、アウトバウンド・アクセス制限が復元される可能性があります。詳しくは、[分離ネットワークでの操作](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)の資料を参照してください。
    
    CFEE が作成されると、環境のプロビジョン対象となる Kubernetes クラスターが、IBM Cloud アカウントのその他のリソースの場合と同様に、{{site.data.keyword.Bluemix_notm}} [ダッシュボード](https://https://cloud.ibm.com/catalog/dashboard/apps/)に表示されます。詳しくは、[Kubernetes サービスの資料](https://https://cloud.ibm.com/catalog/docs/containers/cs_why.html#cs_ov)を参照してください。

5.  CFEE の容量を構成します。
    * CFEE の**「セルの数」**を選択します。これらは、CFEE にデプロイされるアプリケーションをホストするアプリケーション・セルです。  
    * **「ノード・サイズ」**を選択します。これにより、Cloud Foundry セルの容量 (CPU とメモリー) が決まります。
    
    上記で指定したアプリケーション・セルに加えて、CFEE 内の Cloud Foundry プラットフォームの操作と制御のために、追加の_コントロール・プレーン・セル_ が作成されて予約されます。 

    **注:** Kubernetes クラスター内の複数のワーカー・ノードが異なるサブネットにプロビジョンされている場合、VLAN スパンニングを有効にすることをお勧めします。  VLAN スパンニングが無効になっている場合、ワーカー・ノードが異なるサブネットにあると、それらのノード間での接続が妨げられることがあります。  詳しくは、[VLAN スパンニング](https://cloud.ibm.com/catalog/docs/containers/cs_subnets.html#vlan-spanning)の資料を参照してください。

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

## Eirini テクニカル・プレビュー・プラン
{: #eirini}

 Eirini テクニカル・プレビュー・プランにより、Diego の代わりにネイティブ Kubernetes をコンテナー・スケジューラーとして使用して CFEE を探索することができます。Kubernetes スケジューラーを CFEE で使用すると、Cloud Foundry アプリケーション・ランタイムでのアプリのデプロイと実行、ユーザーの追加、組織とスペースの作成、アプリのデプロイ、サービスへのそれらのアプリのバインドを行うことができます。Cloud Foundry Foundation の Eirini インキュベーター・プロジェクトについて詳しくは、[Eirini プロジェクト](https://www.cloudfoundry.org/project-eirini/)の資料を参照してください。
 Eirini テクニカル・プレビュー・プランから作成された CFEE インスタンスには、以下の制約が適用されます。
 
* `containerd` を使用する Kubernetes はサポートされません。`containerd` ではなく Docker を使用する Kuberetes バージョンのみサポートされます。Docker をサポートする最新の IBM Container Service (IKS) のバージョンは v1.10 です。
* Cloud Foundry SSH はサポートされません。
* Docker イメージの `cf push` はサポートされません。
* Kubernetes ネイティブ Eirini ステージングはサポートされません。Eirini テクニカル・プレビュー・プランから作成された CFEE インスタンスは、Eirini をアプリの実行に使用しますが、アプリのステージングには使用しません。Diego セルが引き続きアプリのステージングに使用されます。
* 特定のアプリ・インスタンス (`cf restart-app-instance`) の再始動はサポートされません。

 
