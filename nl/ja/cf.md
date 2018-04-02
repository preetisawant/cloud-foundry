---


copyright:
  years: 2016, 2018
lastupdated: "2018-01-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cloud Foundry が {{site.data.keyword.cloud_notm}} と連携して機能する仕組み
{: #howwork}

アプリを Cloud Foundry にデプロイする場合は、そのアプリをサポートするのに十分な情報を使用して {{site.data.keyword.cloud_notm}} を構成する必要があります。

* モバイル・アプリの場合、{{site.data.keyword.cloud_notm}} には、モバイル・アプリがサーバーとの通信に使用するサービスなどの、モバイル・アプリケーションのバックエンドを表す成果物が含まれています。
* Web アプリの場合、ランタイムおよびフレームワークに関する情報が {{site.data.keyword.cloud_notm}} に伝達されるようにする必要があります。それにより、{{site.data.keyword.cloud_notm}} がそのアプリを実行するのに適した実行環境をセットアップすることができます。

モバイルおよび Web の両方を含め、各実行環境は他のアプリの実行環境から分離されています。 実行環境は、これらのアプリが同じ物理マシン上にあったとしても互いに分離されます。 以下の図は、{{site.data.keyword.cloud_notm}} でのアプリのデプロイメントを Cloud Foundry が管理する方法についての基本的なフローを示しています。

![アプリのデプロイ](images/deploy.png)

図 1. アプリのデプロイ

アプリを作成し、Cloud Foundry にデプロイすると、{{site.data.keyword.cloud_notm}} 環境は、そのアプリ、またはそのアプリが表す成果物の送信先となる適切な仮想サーバーを決定します。 モバイル・アプリの場合、モバイル・バックエンド・プロジェクションが {{site.data.keyword.cloud_notm}} 上に作成されます。 クラウドで実行されるモバイル・アプリのコードはすべて、結局は {{site.data.keyword.cloud_notm}} 環境で実行されます。 Web アプリの場合、クラウドで実行されるコードは、開発者が {{site.data.keyword.cloud_notm}} にデプロイするアプリ自体です。 仮想サーバーの決定は、以下を含むいくつかの要因に基づいて行われます。

* マシン上に既に存在する負荷
* その仮想サーバーがサポートするランタイムまたはフレームワーク

仮想サーバーが選択された後、各仮想サーバー上のアプリケーション・マネージャーは、そのアプリに適切なフレームワークとランタイムをインストールします。 その後、アプリをそのフレームワークにデプロイすることができます。 デプロイメントが完了すると、アプリケーション成果物が開始されます。

以下の図は、複数のアプリがデプロイされている仮想サーバー (Droplet Execution Agent (DEA) とも呼ばれる) の構造を示しています。

![仮想サーバーの設計](images/container-diego.png)

図 2. 仮想サーバーの設計

各仮想サーバーで、アプリケーション・マネージャーは {{site.data.keyword.cloud_notm}} インフラストラクチャーの残りの部分と通信し、この仮想サーバーにデプロイされたアプリを管理します。 各仮想サーバーには、アプリを分離し保護するためのコンテナーがあります。 それぞれのコンテナーに、{{site.data.keyword.cloud_notm}} は各アプリに必要な、適切なフレームワークとランタイムをインストールします。

アプリがデプロイされた時、そのアプリに Web インターフェース (Java Web アプリ用など)、またはその他の REST ベースのサービス (モバイル・アプリに公開されているモバイル・サービスなど) が含まれている場合、そのアプリのユーザーは、通常の HTTP 要求を使用してそのインターフェースまたはサービスと通信することができます。

![{{site.data.keyword.cloud_notm}} アプリの起動](images/execute.png)

図 3. {{site.data.keyword.cloud_notm}} アプリの起動

各アプリは、そのアプリに関連付けられた 1 つ以上の URL を持つことができますが、それらはすべて {{site.data.keyword.cloud_notm}} エンドポイントを指していなければなりません。 要求が着信すると、{{site.data.keyword.cloud_notm}} はその要求を調べ、対象のアプリを判別し、要求を受け取るアプリのインスタンスを選択します。


## {{site.data.keyword.cloud_notm}} での Cloud Foundry アーキテクチャー
{: #architecture}

一般に、Cloud Foundry で {{site.data.keyword.cloud_notm}} 上のアプリを実行する際にオペレーティング・システムやインフラストラクチャー層について気にする必要はありません。 ルート・ファイル・システムやミドルウェア・コンポーネントなどの層は抽象化されているため、ユーザーはアプリケーション・コードに集中できます。 ただし、アプリケーションがどこで実行されているか詳細を知る必要がある場合は、これらの層について詳しく学ぶことができます。

詳しくは、[{{site.data.keyword.cloud_notm}} インフラストラクチャー・レイヤーの表示](cf.html#infralayers)を参照してください。

開発者は、ブラウザー・ベースのユーザー・インターフェースを使用して {{site.data.keyword.cloud_notm}} のインフラストラクチャーと対話することができます。 また、cf という、Cloud Foundry コマンド・ライン・インターフェースを使用して、Web アプリをデプロイすることもできます。

クライアント (モバイル・アプリ、外部で稼動するアプリ、{{site.data.keyword.cloud_notm}} でビルドされるアプリ、あるいはブラウザーを使用している開発者) は {{site.data.keyword.cloud_notm}} でホストされているアプリと対話します。 クライアントは、REST API または HTTP API を使用し、{{site.data.keyword.cloud_notm}} を経由して要求をアプリ・インスタンスまたはコンポジット・サービスのいずれかに経路指定します。

以下の図は、{{site.data.keyword.cloud_notm}} 上の Cloud Foundry アーキテクチャーの概要を示したものです。

![{{site.data.keyword.cloud_notm}} アーキテクチャー](images/arch.png)

図 4.{{site.data.keyword.cloud_notm}} 上の Cloud Foundry アーキテクチャー

待ち時間またはセキュリティーを考慮して、アプリはさまざまな {{site.data.keyword.cloud_notm}} の地域にデプロイすることができます。 1 つの地域にデプロイすることも、複数地域にまたがってデプロイすることも選択できます。


![複数地域のアプリケーション開発](images/multi-region.png)

図 5. 複数地域のアプリケーション・デプロイメント

{{site.data.keyword.Bluemix_notm}} インフラストラクチャー・レイヤー
{: #infralayers}


{{site.data.keyword.Bluemix_notm}} は、オペレーティング・システムおよびインフラストラクチャーのレイヤーを管理する必要がなくなるように、それらを要約するか非表示にします。 ただし、オペレーティング・システムやアプリのミドルウェアについて詳細に知る必要がある状況が発生する場合もあります。
{:shortdesc}

### {{site.data.keyword.Bluemix_notm}} インフラストラクチャー・レイヤーの表示
{: #viewinfra}

**bluemix app stacks** コマンドを実行して、アプリがデプロイされる先の使用可能なスタック (つまり、ルート・ファイル・システム) を表示することができます。 また、*-s* オプションと *stack_name* を指定して **bluemix app push** コマンドを使用する場合もスタックを指定できます。ここで、stack_name は、`lucid64` や `cflinuxfs2` などのルート・ファイル・システムです。

```
bluemix app push appName -s stack_name
```

`cf buildpacks` コマンドを使用して、WebSphere Liberty profile や SDK for Node.js など、アプリを実行するランタイムとして使用可能なミドルウェア・コンポーネントを表示できます。 また、次のコマンドを使用して、アプリのランタイム環境を指定できます。

```
bluemix app push appName -b buildpackname
```
