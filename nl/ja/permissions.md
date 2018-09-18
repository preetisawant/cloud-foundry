---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 許可
{: #permissions}

{{site.data.keyword.cfee_full}} サービスのインスタンスを作成して作業を開始する前に、管理者の許可と、管理者以外のチーム・メンバーの許可を正しく設定する必要があります。

## 新しい環境を作成するために必要な許可
{: #perm-creating}

{{site.data.keyword.cfee_full_notm}} サービスの新しいインスタンスを作成するには、ユーザーは、インスタンスを作成するアカウントの管理者によって以下のようなアクセス・ポリシーを付与されている必要があります。

* {{site.data.keyword.Bluemix}} アカウント内の少なくとも 1 つのリソース・グループへのアクセス権限。リソース・グループでは、リソースへのアクセス制御を可能にするために、それらのリソースをカスタマイズされたグループに編成できます。新規環境インスタンスを作成するときに、リソース・グループに関するプロンプトが出されます。

* 環境が割り当てられているリソース・グループ内の {{site.data.keyword.cfee_full_notm}} サービスに対する管理者またはエディターの役割。{{site.data.keyword.cfee_full_notm}} サービス内の管理者またはエディターの役割を持つユーザーは、環境を作成および削除できます。ただし、{{site.data.keyword.cfee_full_notm}} インスタンスにユーザーを割り当てたり、そのインスタンス内のユーザーに割り当てられている役割を変更したりできるのは、管理者役割を持つユーザーのみになります。

* CFEE サービスの必須の従属関係である IBM Cloud オブジェクト・ストレージ・サービスに対する管理者またはエディターの役割。IBM Cloud オブジェクト・ストレージ・サービスのインスタンスは、ICFEE アプリケーション・コンテナーの作成中に生成されるデータ (例えば、アップロードされたアプリケーション・パッケージ、ビルドパック、およびコンパイルされた実行可能プログラムなど) を保管するために使用されます。

* Compose for PostgreSQL サービスのインスタンスは、CFEE サービスの必須の従属関係です。Compose for PostgreSQL は、Cloud Foundry データ (例えば、アプリケーション・デプロイメント (開始イベントと停止イベント) の監査、CFEE ユーザー・メンバーシップ、組織、スペース、アプリケーション、およびサービス接続の記録) を CFEE インスタンスに保管するために使用されます。Compose for PostgreSQL サービスのそのインスタンスは、パブリック Cloud Foundry 組織 (CFEE 組織とは無関係) にデプロイされます。Compose for PostgresSQL インスタンスがデプロイされるパブリック Cloud Foundry 組織には、**_cfee-`<accountId>`_** という特定の名前があります。ここで、「accountId」は、CFEE が (Compose for PostgreSQL サービス・インスタンスとともに) プロビジョンされる IBM Cloud アカウントの ID です。パブリック Cloud Foundry 組織は、アカウント所有者が CFEE インスタンスを作成すると自動的に作成されます。アカウント所有者でないユーザーが CFEE インスタンスを作成しようとしても、組織は自動的に作成されません (したがって、CFEE の作成試行は失敗します)。したがって、CFEE インスタンスを作成するが、アカウント所有者ではない IBM Cloud アカウントのユーザーはすべて、**「管理者の役割」**で **_cfee-`<accountId>`_** パブリック Cloud Foundry 組織に追加する必要があります。   

   IBM Cloud アカウントから _cfee-`<accountId>`_ パブリック組織にユーザーを追加するには、以下のようにします。
    * [**「管理」>「アカウント」>「Cloud Foundry の組織」**](https://console.bluemix.net/account/organizations)に移動します。
    * **_cfee-`<accountId>`_** 組織をクリックします。
    * ページ上部の**「ユーザー」**タブに移動します。
    * CFEE インスタンスを作成する必要があるユーザーを見つけ、そのユーザーの**「管理者」**チェック・ボックスをクリックします。CFEE インスタンスを作成できるようにするユーザーがリストに含まれていない場合は、表の上の**「ユーザーの追加または招待」**をクリックして、ユーザーを **_cfee-`<accountId>`_** 組織に追加または招待します。

   **注**: **_cfee-`<accountId>`_** パブリック組織は、IBM Cloud アカウント所有者が CFEE インスタンスを作成したときに暗黙的および自動的に作成されますが、アカウント所有者は (そしてアカウント所有者のみが)、代わりに、CFEE インスタンスを作成せずに、パブリック Cloud Foundry 組織を手動で作成できます。IBM Cloud アカウント所有者は、**「管理」>「アカウント」>「Cloud Foundry の組織」**ページで、パブリック _cfee-`<accountId>`_ 組織を手動で作成できます。ユーザーがアカウント所有者で、パブリック _cfee-`<accountId>`_ 組織を作成する場合は、組織を正確に _cfee-`<accountId>`_ と指定するようにしてください。IBM Cloud アカウント ID を見つけるには、[**「管理」>「アカウント」>「Cloud Foundry の組織」**](https://console.bluemix.net/account/organizations)ページに移動し、ブラウザーに表示されているページ URL を確認してください。IBM Cloud アカウント ID は、ページ URL 内の `=` に続く英数字の値のセットです。あるいは、__「管理」>「アカウント」>「ユーザー」__に移動し、ページの右上隅にある_「アカウント」_名の左のツールチップの上にマウスを移動します。
   
* 環境が割り当てられているリソース・グループ内の {{site.data.keyword.Bluemix_notm}} Container サービスに対する管理者またはエディターの役割。{{site.data.keyword.cfee_full_notm}} のインスタンスは、{{site.data.keyword.Bluemix_notm}} Container サービスによって提供されているコンテナー・クラスター・インフラストラクチャーにデプロイされます。{{site.data.keyword.cfee_full_notm}} サービスのインスタンスを作成すると、サービスは、{{site.data.keyword.cfee_full_notm}} がデプロイされる Kubernetes クラスターを自動的に作成します。そのクラスター・インフラストラクチャーを作成するために、IBM Container サービス (具体的には、環境が割り当てられているリソース・グループ内) へのアクセス権が必要です。

{{site.data.keyword.cfee_full_notm}} インスタンスを作成するために必要なアクセス・ポリシーがあることを確認するには、以下のようにします。
1. {{site.data.keyword.Bluemix_notm}} ヘッダーで[**「管理」>「アカウント」>「ユーザー」**](https://console.bluemix.net/iam/#/users)メニューに移動して、**「ID およびアクセス」**ページを開きます。
2. 「アクセス・ポリシー」タブで、環境を作成するユーザーをクリックします。
3. 環境を作成するユーザーのアクセス・ポリシーが、前述のポリシーと整合していることを確認します。

以下の画面は、ユーザーが {{site.data.keyword.cfee_full_notm}} インスタンスを作成することを許可する、{{site.data.keyword.Bluemix_notm}} の「ID およびアクセス」ページに表示されるアクセス・ポリシーを示しています。

![アクセス・ポリシー](img/AccessPolicies_Creator.png)

## 環境の処理を行うために必要な許可
{: #perm-working}

{{site.data.keyword.cfee_full_notm}} のインスタンスの処理を行う場合、ユーザーには以下の条件があります。
1. {{site.data.keyword.cfee_full_notm}} インスタンスが作成された {{site.data.keyword.Bluemix_notm}} アカウントのメンバーでなければならない。
2. アカウント管理者によって以下の_アクセス・ポリシー_が付与されている必要がある ({{site.data.keyword.Bluemix_notm}} ヘッダーの[**「管理」>「アカウント」>「ユーザー」**](https://console.bluemix.net/iam/#/users)メニューの下の_「ID およびアクセス」_ページを参照して、現行アカウントのアクセス・ポリシーを確認してください)。
  - {{site.data.keyword.Bluemix_notm}} アカウント内の少なくとも 1 つのリソース・グループへのアクセス権限。リソース・グループでは、リソースへのアクセス制御を可能にするために、それらのリソースをカスタマイズされたグループに編成できます。新規環境インスタンスを作成するときに、リソース・グループに関するプロンプトが出されます。
  - ユーザーは、環境インスタンスが作成されたリソース・グループ内の {{site.data.keyword.cfee_full_notm}} サービスへのアクセス権限を割り当てられている必要がある。ユーザーが {{site.data.keyword.cfee_full_notm}} インスタンスに持っているアクセス・レベルおよび制御レベルは、アクセス・ポリシーで付与されている役割によって決まります。
     - 管理者またはエディターの役割を割り当てられているユーザーは、組織を作成し、組織およびスペースに管理者を割り当て、環境内のすべての組織およびスペースへの完全許可を持ち、Cloud Controller API を使用して操作アクションを実行できる。これらのユーザーには、Cloud Foundry の_「ユーザー・アカウントおよび認証スコープ」_で _cloud_controller.admin scope_ が自動的に付与されます。
     - ビューアーの役割が割り当てられたユーザーは、メインの {{site.data.keyword.Bluemix_notm}} ダッシュボードでその環境を表示し、そのユーザー・インターフェースを開くことができる。環境内の特定の組織およびスペースへのユーザー・アクセス権限は、それらの組織およびスペースの管理者によって割り当てられる特定の組織およびスペースの役割で管理されます。詳しくは、[組織へのユーザーの追加](add-users.html)を参照してください。

イメージは、{{site.data.keyword.cfee_full_notm}} にアクセスするために必要な最小アクセス・ポリシー ({{site.data.keyword.Bluemix_notm}} の_「ID およびアクセス」_ページに表示される) を示しています。

![アクセス・ポリシー](img/AccessPolicies_User.png)

