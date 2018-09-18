---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 組織およびスペースの作成
{: #create_orgs}

{{site.data.keyword.cfee_full}} 内のアプリは、特定のスペース内にスコープ宣言されます。そして、スペースは特定の組織内に存在します。組織のメンバーは、割り当て量プラン、アプリ、サービス・インスタンス、およびカスタム・ドメインを共有します。組織とスペースが作成されたら、それらへのアクセスおよび制御のレベルを決定する特定の役割とともに、ユーザーをそれらの組織およびスペースに追加できます。組織を作成して、それらの組織に管理者を割り当てるには、{{site.data.keyword.cfee_full_notm}} サービスと、ユーザーを追加する特定の環境インスタンスの両方に対する管理者役割が必要です。これらの許可は、{{site.data.keyword.Bluemix}} ヘッダーの**「管理」>「ユーザー」**メニューの下の_「ID およびアクセス」_ページで設定できます。
{: shortdesc}

## 組織の作成
{: #create-org}

{{site.data.keyword.cfee_full_notm}} で組織を作成するには、以下のようにします。

1. [{{site.data.keyword.Bluemix_notm}} Cloud Foundry 環境ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments){: new_window}に移動し、組織を作成する {{site.data.keyword.cfee_full_notm}} を開きます。
2. {{site.data.keyword.cfee_full_notm}} ユーザー・インターフェースで、ナビゲーション・ペインの**「組織」**項目に移動し、_組織_ ページを開きます。
3. **「新規追加」**をクリックします。
4. 新しい組織の**「名前」**を入力します。
5. **「管理者」**の下で、少なくとも 1 人のユーザーを指定します。管理者の役割を持つユーザーのみがその組織にメンバーを追加できます。
6. **「割り当てプラン」**の下で、使用可能なプランを選択します。割り当てプランは、組織内のアプリに使用可能なメモリー、ホストされるアプリ・インスタンスの最大数、および経路の最大数を制限します。

組織の管理者は、組織のメンバーシップを管理することに加え、組織内のスペースを作成、表示、編集、または削除できます。また、組織の管理者は組織の使用量と割り当て量を表示し、ユーザーを組織に招待し、組織内のメンバーシップと役割を管理し、組織のカスタム・ドメインを管理できます。

組織内にスペースを作成するには、_「組織」_ページで**「スペース」**タブに移動し、**「新規追加」**をクリックします。組織のメンバーも、組織内の独自のスペースを作成および管理することができます。Cloud Foundry の役割について詳しくは、[Cloud Foundry アクセス権限](https://console.bluemix.net/docs/iam/cfaccess.html#cfroles){: new_window}を参照してください。

**注**: {{site.data.keyword.cfee_full_notm}} 内の組織およびスペースへのアクセスでは、ユーザーはその環境自体へのアクセス権限を持っている必要があります。{{site.data.keyword.cfee_full_notm}} へのアクセス権限がなければ、ユーザーは、その環境内の組織およびスペースでのメンバーシップおよび役割に関係なく、それらの組織およびスペースにアクセスすることはできません。
