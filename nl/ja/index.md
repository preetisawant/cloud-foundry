---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-29-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# {{site.data.keyword.cfee_full_notm}} の概要
{: #about}

{{site.data.keyword.cfee_full}} サービスへようこそ。

{{site.data.keyword.cfee_full}} (CFEE) では、エンタープライズ・クラスの独立した Cloud Foundry プラットフォームを、オンデマンドでいくつもインスタンス化できます。{{site.data.keyword.Bluemix_notm}} Foundry Enterprise サービスのインスタンスは、{{site.data.keyword.Bluemix_notm}} の自分自身のアカウント内で実行されます。 環境は、分離したハードウェア (Kubernetes クラスター) 上にデプロイされます。 アクセス制御、キャパシティー、バージョンの更新、リソース使用量とモニターなど、環境を完全に制御できます。さらに、CFEE には {{site.data.keyword.Bluemix_notm}} が統合されているので、開発者は {{site.data.keyword.Bluemix_notm}} アカウントで使用可能なサービスを利用できます。ユーザーはそれらのサービスを CFEE に追加し、CFEE スペースにデプロイしたアプリケーションにバインドできます。

CFEE インスタンスの作成と使用を[**開始する**](https://console.bluemix.net/docs/cloud-foundry/getting-started.html#getting-started)方法について説明します。

{:shortdesc}

## CFEE の主な要素
{: #key-elements}

以下の表に、{{site.data.keyword.cfee_full}} サービスの主な要素の要約を示します。

| 要素   | 説明 |
|-----------|---------------|
| IBM Cloud アカウント | CFEE インスタンスは、特定の IBM Cloud アカウントの下で作成されます。そのアカウント内のユーザーは、そのユーザーに定義されている役割およびアクセス・ポリシーに従って、CFEE インスタンスを使用できます。 |
|| CFEE インスタンスが作成されるアカウントは、トライアル・アカウントではなく、従量課金 (PAYG) またはサブスクリプション・アカウント・タイプでなければなりません。  |
| CFEE | アプリケーションをホストするための IBM Cloud Foundry Enterprise Environment サービス。 |
|| IBM Cloud カタログから使用可能です。 |
| CFEE インスタンス | IBM Cloud アカウントの下で、当該アカウントにおける管理者またはエディターの役割を備えているユーザーによって作成される IBM Cloud Foundry Enterprise Environment サービスのインスタンス。 |
|| 1 つの IBM Cloud アカウントで複数の CFEE インスタンスを使用できます。 |
|| 1 つ以上の組織を含めることができます。 |
| 組織 | 1 つ以上のスペースが含まれます。 |
|| 1 人以上の組織管理者が含まれます。 |
|| 1 人以上のチーム・メンバーが含まれます。 各チーム・メンバーに、1 つ以上の役割を付与できます。 |
|| スペース内にデプロイされたアプリケーションで発生した使用料金は、組織レベルで報告されます。 |
| スペース | 1 つ以上のリソースが含まれます。 |
|| 1 つ以上のアプリが含まれます。 |
|| 1 人以上のスペース管理者が含まれます。 |
|| 1 人以上のチーム・メンバーが含まれます。 各ユーザーは、所有している組織で既にチーム・メンバーでなければなりません。 各チーム・メンバーに、1 つ以上の役割を付与できます。 |
| チーム・メンバー | 異なるアカウントをまたがって 1 つ以上の組織およびスペースに追加可能です。 |
|| 同じ組織またはスペース、あるいはその両方の中で複数の役割を付与されることが可能です。 |
| サービス別名 | IBM Cloud 内のサービス・インスタンスの別名。 |
|| これにより、開発者は、IBM Cloud アカウントで使用可能な既存のサービス・インスタンスを CFEE 内のスペースにデプロイされているアプリケーションにバインドできます。|
{:caption="表 1. 主な要素の説明" caption-side="top"}

## CFEE およびサポートされるサービスのプロビジョン・ターゲット
{: #provisioning-targets}

以下に、CFEE サービスおよび従属サービス (Kubernetes サービス、Compose for PostgreSQL サービス、および Cloud Object Storage サービス) のプロビジョンが可能な、ジオグラフィー、ロケーション、およびデータ・センターを示します。

|  **ジオグラフィー** &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;| **CFEE インスタンス & Kubernetes クラスター** | **Cloud Object Storage** | **Compose for PostgreSQL (CF 地域)** |
|----------------------------------------|-------------------|-------------------|-------------------|
|北アメリカ | モントリオール (mon01) | us-geo | us-east |
|北アメリカ | トロント (tor01) | us-geo| us-east |
|北アメリカ | ワシントン DC (wdc04) | us-geo | us-east |
|北アメリカ | ワシントン DC (wdc06) | us-geo | us-east | 
|北アメリカ | ワシントン DC (wdc07) | us-geo | us-east |
|北アメリカ | ダラス (das10) | us-geo | us-south |
|北アメリカ | ダラス (das12) | us-geo | us-south |
|北アメリカ | ダラス (das13) | us-geo |us-south |
|北アメリカ | サンノゼ (sjc03) | us-geo | us-south |
|北アメリカ | サンノゼ (sjc04) | us-geo | us-south |
|南アメリカ &nbsp; &nbsp;| サンパウロ (sao01) |  us-geo | us-south |
|ヨーロッパ | ロンドン (lon02) | eu-geo | eu-gb |
|ヨーロッパ | ロンドン (lon04) | eu-geo | eu-gb |
|ヨーロッパ | ロンドン (lon06) | eu-geo | eu-gb | 
|ヨーロッパ | アムステルダム (ams03) | eu-geo | eu-de |
|ヨーロッパ | オスロ (osl01) |eu-geo | eu-de | 
|ヨーロッパ | パリ (par01) | eu-geo | eu-de |
|ヨーロッパ | フランクフルト (fra02) | eu-geo | eu-de |
|ヨーロッパ | フランクフルト (fra04) | eu-geo | eu-de | 
|ヨーロッパ | フランクフルト (fra05) |  eu-geo | eu-de |
|アジア太平洋 | メルボルン (mel01) | ap-geo | au-syd |
|アジア太平洋 | シドニー (syd01) | ap-geo | au-syd |
|アジア太平洋 | シドニー (syd04) | ap-geo | au-syd | 
|アジア太平洋 | 香港 (hkg02) | ap-geo | au-syd |
|アジア太平洋 | 香港 (seo01) | ap-geo | au-syd |
|アジア太平洋 | シンガポール (sng01) | ap-geo | au-syd |
|アジア太平洋 | 東京 (gok02) | ap-geo | au-syd |
|アジア太平洋 | 東京 (gok04) | ap-geo | au-syd |
|アジア太平洋 | 東京 (gok05) | ap-geo | au-syd |
{: caption="表 2. CFEE およびサポートされるサービスのプロビジョン・ターゲット" caption-side="top"}

**例えば**、CFEE サービスを、ヨーロッパのアムステルダム (1 データ・センター)、フランクフルト (3 つのデータ・センター)、ロンドン (3 つのデータ・センター)、オスロ (1 データ・センター)、およびパリ (1 データ・センター) のうち、3 つのデータ・センターにプロビジョンできます。CFEE がフランクフルトにプロビジョンされる場合、Cloud Object Store サービス・インスタンスは _eu-geo_ 地域にデプロイされ、Compose for PostgreSQL サービス・インスタンスは _eu-de_ パブリック Cloud Foundry 地域にデプロイされます。

CFEE でサービスを使用する方法について詳しく説明し、実演しているビデオが、[CFEE ビデオの再生リスト](https://ibm.biz/CFEE_Playlist){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。
{:tip}
