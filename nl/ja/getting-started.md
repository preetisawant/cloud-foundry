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

# 入門チュートリアル
{: #getting-started}

{{site.data.keyword.cfee_full}} (CFEE) は、クラウドでアプリおよびサービスをホストするためのクラウド・プラットフォームです。 {{site.data.keyword.cfee_full_notm}} を使用すると、使用量の拡大に合わせてアプリを拡張するのが容易になり、ランタイム、ミドルウェア、およびインフラストラクチャーが簡素化するため、アプリの開発に集中することができます。
{: shortdesc}

この入門チュートリアルでは、{{site.data.keyword.cfee_full_notm}} の作成、ユーザーの追加、組織およびスペースの作成、アプリのデプロイ、サービスへのアプリのバインドを行う方法について説明します。

**注:** 以下の手順は、**標準**プランから作成された CFEE に適用できます。この CFEE が **Eirini テクニカル・プレビュー**・プランから作成された場合は、**ステップ 1 から 6**、およびステップ **11** のみ行ってください。ステップ 8 から 11 で説明されている機能は、_Eirini テクニカル・プレビュー_・プランではサポートされません。[Eirini テクニカル・プレビューの概要](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-getting-started-eirini#getting-started-eirini)を参照してください。
_Eirini テクニカル・プレビュー_・プランにより、Diego の代わりにネイティブ Kubernetes をコンテナー・スケジューラーとして使用して CFEE を探索することができます。Kubernetes スケジューラーを CFEE で使用すると、Cloud Foundry アプリケーション・ランタイムでのアプリのデプロイと実行、ユーザーの追加、組織とスペースの作成、アプリのデプロイ、サービスへのそれらのアプリのバインドを行うことができます。 

## ステップ 1: CFEE インスタンスの作成
{: #create-environment}

{{site.data.keyword.Bluemix_notm}} カタログから {{site.data.keyword.cfee_full_notm}} (CFEE) のインスタンスを作成できます。CFEE インスタンスを作成する前に、[環境の作成](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-create-environment#create-environment)の資料で {{site.data.keyword.Bluemix_notm}} アカウントの準備に関するガイダンスを探し、適切な許可についてと、CFEE インスタンスを作成する手順について確認してください。


## ステップ 2: 組織およびスペースの作成
{: #create-orgsandspaces}

{{site.data.keyword.cfee_full_notm}} の作成後は、『[組織およびスペースの作成](https://cloud.ibm.com/docs/cloud-foundry/orgs-spaces.html)』を参照して、組織およびスペースを作成して環境を構造化する方法に関する情報を確認します。 {{site.data.keyword.cfee_full_notm}} のアプリは、特定のスペース内にスコープ設定されます。 そして、スペースは、特定の組織内に存在します。 組織のメンバーは、割り当て量プラン、アプリ、サービス・インスタンス、およびカスタム・ドメインを共有します。

組織を作成するときは、それに割り当て量を割り当ててください。割り当て量により、その組織で使用できるリソース (メモリー、CPU など) に制限を設定できます。あとで別の割り当て量を割り当てることができます。各 CFEE で使用可能な一連の事前構成済み割り当て量がありますが、CFEE ユーザー・インターフェースの**「割り当て量」**ページで独自のカスタム割り当て量を作成することもできます。カスタム割り当て量を_デフォルト_ 割り当て量にすることもできます。これを行うには、割り当て量のメニューから_「デフォルトにコピー (Copy to default)」_アクションを呼び出します。これでカスタム割り当て量の値がデフォルト割り当て量にコピーされます。

**注:** 上部の IBM Cloud ヘッダーにある**_「管理」>「アカウント」>「Cloud Foundry の組織」_**メニューで表示される「_Cloud Foundry の組織 (Cloud Foundry organizations)_」ページは、パブリック IBM Cloud 組織専用であり、**CFEE 組織用ではありません**。 CFEE 組織は、CFEE インスタンスの「_組織_」ページで管理します。  CFEE ユーザー・インターフェースを開き、**「_Organizations_」**ページをクリックして、その CFEE の組織を作成および管理します。

## ステップ 3: 組織およびスペースへのユーザーの追加
{: #add-users}

アクセス・レベルを制御する特定の役割の割り当てが行われる組織およびスペースに[ユーザーを追加](https://console.bluemix.net/docs/cloud-foundry/add-users.html)します。  CFEE で組織およびスペースのメンバーとしてユーザーを追加するには、そのユーザーは CFEE インスタンスに事前にアクセスできるようになっている必要があります。 『[許可](https://console.bluemix.net/docs/cloud-foundry/permissions.html)』を参照してください。

## ステップ 4: アプリケーションのデプロイおよび表示
{: #deploy-apps}

準備ができたら、{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを使用して [アプリをデプロイ](https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html)できます。  ユーザー・インターフェースでデプロイ済みアプリケーションのリストを表示します。これは、特定の CFEE スペースのコンテキストで、あるいはすべての CFEE インスタンスでグローバルに表示できます。  該当するビューからアプリケーションを開始、停止、または削除することもできます。

## ステップ 5: CFEE スペースへの IBM Cloud サービス・インスタンスの作成または追加
{: #service-instances}

IBM Cloud アカウント内で[サービスの作成](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#creating-services-inspace)や[既存サービスの追加](https://cloud.ibm.com/docs/cloud-foundry/add-serv-inst.html#workingwith-services#adding-services-inspace)を実行できます。  CFEE スペース内でサービス・インスタンスが使用可能になると、そのサービス・インスタンスをそのスペース内にデプロイされた CFEE アプリケーションにバインドすることができます。

## ステップ 6: サービス・インスタンスへのアプリケーションのバインド
{: #bind-apps}

サービスの機能を使用するためにサービス・インスタンス別名に[アプリをバインド](https://cloud.ibm.com/docs/cloud-foundry/binding.html)します。

[Cloud Foundry ダッシュボード](https://cloud.ibm.com/dashboard/cloudfoundry/overview){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") では、*パブリック* と*エンタープライズ* の両方のすべてのアプリケーションとサービスの統合ビューを表示することができます。  Cloud Foundry ダッシュボードで、左側のナビゲーション・ペインの*「パブリック」*をクリックすると、IBM Cloud アカウント内の使用可能なパブリック・アプリケーションおよびサービスが表示されます。  *「エンタープライズ」*をクリックすると、すべての CFEE 環境、CFEE スペースにデプロイされたアプリケーション、および CFEE スペースで使用可能なサービスが表示されます。
{:tip}

## ステップ 7: 監査およびロギング・パーシスタンスの有効化 (オプション)
{: #enable-auditingandlogging}

[イベントの監査](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing)および[ロギング・パーシスタンス](https://cloud.ibm.com/docs/cloud-foundry/auditing-logging.html#logging)用の環境を有効にします。

## ステップ 8: モニタリング・ツールの有効化 (オプション)
{: #enable-monitoring}

CFEE インスタンス v2.2.0 以降では、モニタリング・ツールは自動的にはプロビジョンされません。CFEE インスタンスが作成されたら、CFEE 管理者が[モニタリング・ツールを有効化](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-monitoring)できます。モニタリング・ツール・セットには、Prometheus、Grafana および Alertmanager が含まれます。

## ステップ 9: Cloud Foundry ドメインの作成および保護 (オプション)
{: #create-domains}

CFEE 内のすべてのアプリケーション用 (共有ドメイン) または特定組織用 (専用ドメイン) の[ドメイン](https://cloud.ibm.com/docs/cloud-foundry/domains.html#domains)を作成し、SSL 証明書を使用してこれらを保護します。

## ステップ 10: Cloud Foundry ビルドパックの優先順位順序の構成
{: #create-buildpacks}

ビルドパックには、Cloud Foundry 環境でデプロイされるアプリケーションのランタイム・サポートが用意されており、自動的にアプリケーションのランタイムが構成され、その依存関係が処理されます。Cloud Foundry には、一般的な言語とフレームワーク用のビルドパック・セットが含まれています。Cloud Foundry ビルドパックについて詳しくは、[こちら](https://docs.cloudfoundry.org/buildpacks/)をご覧ください。  

カスタム・ビルドパックは、CFEE ユーザー・インターフェースの**「ビルドパック」**ページで作成およびアップロードできます。ビルドパックには、優先順位リスト内での順序位置があります。アプリケーションのステージング中、Cloud Foundry は一連のビルドパックに対するアプリケーションの互換性を検査します。この互換性検査は位置 1 から開始し、互換性のあるビルドパックが検出されるまで優先順位リストを下に処理していきます。ビルドパック・セットの優先順位の順序が、開発チームのニーズに合っていることを確認してください。優先順位の順序内でのビルドパックの位置は、ビルドパック名を別の位置にドラッグ・アンド・ドロップすることによって変更できます。ビルドパックは、[Cloud Foundry CLI](https://docs.cloudfoundry.org/adminguide/buildpacks.html) を使用して管理することもできます。

## ステップ 11: アプリケーションを管理するための Stratos コンソールのインストール (オプション)
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
