---

copyright:
  years: 2018
lastupdated: "2018-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# アカウントの準備
{: #prepare}

CFEE インスタンスは、IBM Cloud アカウントに請求されるインフラストラクチャー・リソース (IBM Container サービスの Kubernetes ワーカー・ノード) にデプロイされます。 つまり、CFEE インスタンスが作成される IBM Cloud アカウントは、有料アカウント (従量課金 (PAYG) アカウントまたはサブスクリプション・アカウント) でなければなりません。  CFEE インスタンスの作成を予定している IBM Cloud アカウントがトライアル・アカウントの場合は、CFEE インスタンスを作成しようとしたときにアカウントのアップグレードを要求されます。  IBM Cloud アカウントが (トライアル・アカウントから従量課金 (PAYG) アカウントまたはサブスクリプション・アカウントに) アップグレードされると、IBM Cloud アカウントは、SoftLayer アカウントにリンクされます (そのアカウントを通じてインフラストラクチャー・リソースを作成できます)。 詳しくは、[アカウント・タイプ](https://cloud.ibm.com/docs/account/index.html#accounts)を参照してください。 これらのインフラストラクチャー・リソースのコストは、IBM Cloud の送り状に示されます。

## IBM Cloud アカウントが CFEE インスタンスを作成できるかどうかの判別方法
{: #account-check}

IBM Cloud アカウントがトライアル・アカウントか有料アカウントか、および SoftLayer アカウントにリンクされているかどうかは、IBM Cloud バナーの右上隅のアカウント情報を確認することによって判別できます。

以下の例では、ユーザー_「Mary Smith」_が IBM Cloud アカウント_「MyCompany」_にログインしています。このアカウントはトライアル・アカウントです。
![アカウントの確認](img/AccountExample_1.png)

以下の例では、同じ IBM Cloud アカウント_「MyCompany」_が有料アカウントにアップグレードされています。  アップグレードの結果として、アカウントは現在、SoftLayer アカウント_「1684806」_にリンクされています。  両方のアカウントが「アカウント (Account)」フィールドに表示されています。
![アカウントの確認](img/AccountExample_2.png)

IBM Cloud アカウントがトライアル・アカウントの場合は、CFEE インスタンスを作成しようとしたときにアカウントのアップグレードを求めるプロンプトが出されます。 以下の画面を参照してください。

![アカウントの確認](img/UpgradeAccountPage_1.png)

## IBM Cloud アカウントをアップグレードする代わりに SoftLayer アカウントを使用
{: #account-linkswitching}

IBM Cloud アカウントで管理者の役割を持っている場合は、IBM Cloud アカウントをアップグレードせずに、SoftLayer アカウントを使用して CFEE インスタンスを作成できます。


**警告:** ここで SoftLayer アカウントを使用し、将来 IBM Cloud アカウントを (従量課金 (PAYG) アカウントまたはサブスクリプション・アカウントに) 更新する場合、将来のインフラストラクチャー・リソースを作成するときに、更新された IBM Cloud アカウントがまだ Softlayer アカウント (ここで資格情報を設定するもの) を使用する可能性があります。 さらに、将来、Cloud Foundry Enterprise Environment を作成するために、異なる SofLayer アカウントを使用した場合、IBM Cloud アカウントのユーザーは、現在資格情報を設定している SoftLayer アカウントで作成したインフラストラクチャー・リソースにアクセスできない可能性があります。 それよりも IBM Cloud アカウントをアップグレードすることをお勧めします。

IBM Cloud アカウントをアップグレードせずに SoftLayer アカウントを使用するには、以下のようにします (図示については以下の画面を参照してください)。
1. IBM Cloud アカウントをアップグレードしない場合に表示される画面で、**「SoftLayer アカウントを使用 (Use a SoftLayer account)」**をクリックします。
2. SoftLayer アカウントの**「ユーザー名」**と**「API キー」**を入力します。 SoftLayer のユーザー名と API キーを取得するには、[SoftLayer コンソール](https://control.softlayer.com)にアクセスします。 SoftLayer にログインしたら、{{site.data.keyword.Bluemix_notm}} アカウントにリンクするアカウントを選択します。 アカウントを選択すると、アカウントのプロファイル・ページが開きます。 ページの最後までスクロールダウンして、アカウントのユーザー名と API キーを見つけます。 API キーがない場合は、ユーザーがアカウント所有者であれば生成できます。 アカウント所有者でない場合は、アカウント所有者に API キーを生成するよう依頼してください。
3. **「資格情報の設定」**をクリックします。

![アカウントの確認](img/UpgradeAccountPage_2.png)

**注:** IBM Container サービスから通常の Kubernetes クラスターを作成するには、SoftLayer アカウントに十分な許可を持っている必要があります。 持っていない場合は、SoftLayer アカウントの管理者、または SoftLayer アカウントへのアクセス権を付与したユーザーに、それらの追加許可を付与するよう依頼してください。
