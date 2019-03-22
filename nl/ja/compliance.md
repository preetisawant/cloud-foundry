---

copyright:
  years: 2018
lastupdated: "2018-10-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# コンプライアンスおよび規制
{: #compliance}

{{site.data.keyword.cfee_full}} (CFEE) は、Platform as a Service です。 そのため、お客様は、どのような目的にもサービス・インスタンスを自由に使用できます。 CFEE および従属サービスは、最小限の個人データにしかアクセスしません。

ただし、CFEE コントロール・プレーンが (UI/API/CLI 経由で) 機密データ (HIPAA データなど) を処理することがなくても、{{site.data.keyword.Bluemix_notm}} アカウント内のすべての従属関係を管理および所有するのはお客様であるため、CFEE を適切に使用する責任はお客様側にあることを明記しておきます。 

以下のベスト・プラクティスをお勧めします。
*  CFEE と一緒に作成される従属サービス (Kubernetes、Cloud Object Storage、および Compose for PostgreSQL) は変更しないでください。
*  CFEE の更新および管理は、Kubernetes サービスではなく CFEE サービス自体 (ユーザー・インターフェースまたはコマンド・ライン・インターフェース) を使用して行ってください。

Cloud Foundry セルは Kubernetes ノード上にデプロイされるので、Kubernetes クラスターが、CFEE インフラストラクチャーの大部分と、CFEE で実行されるすべてのアプリケーションを保持するために使用されます。 このクラスターは、お客様の SoftLayer アカウントによって所有および管理されます。

CFEE は、Compose for PostgreSQL データベースを使用して、組織、スペース、ユーザー、および役割に関するメタデータを保持します。 推奨どおりに CFEE インスタンスを使用している場合、機密データが公開されることはありません。 しかし、お客様が組織やスペースの名前として顧客の個人情報や機密情報を使用した場合、PostgreSQL データベースに HIPAA や他のタイプの機密情報が含まれることになります。

CFEE は、アプリケーションのドロップレットをデプロイ、停止、開始できるように、Cloud Object Storage インスタンスを使用してドロップレットを保持します。つまり、Cloud Object Storage インスタンスはアプリケーションを実行するのではなく、そのイメージを保持しているだけです。 したがって、ベスト・プラクティスに従って Cloud Object Storage インスタンスを使用している場合、HIPAA 機密情報が保持されることはありません。 お客様には、個人データ (テスト・データなど) をアプリケーションにハードコーディングしないようにする責任があります。.
