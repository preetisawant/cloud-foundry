---



copyright:

  years: 2018

lastupdated: "2019-01-08"



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:tip: .tip}

# よくある質問
{: #cfeefaq}

## IBM Cloud Foundry Enterprise Environment (CFEE) とパブリック Cloud Foundry の違いは何ですか?
{: #cfee_diff}

{{site.data.keyword.cloud}} Foundry パブリックでは、Cloud Foundry を使用するクラウド・ネイティブ・アプリケーションを実行して、単純なセットアップ、強力なスケーリング、トラフィック管理を利用できます。 また、すべての {{site.data.keyword.cloud}} サービスに簡単にアクセスできます。

{{site.data.keyword.cfee_full}} では、Cloud Foundry パブリックでできるすべてのことに加えて、分離した環境を作成および管理してお客様の企業専用の Cloud Foundry アプリケーションをホストできます。


## 新しいオファリングと前の IBM Cloud Foundry オファリングの違いは何ですか?
{: #cfOfferings_diff}

パブリックのマルチテナントについて言えば、最も注目すべき違いは、確実に分離プロパティーです。 IBM Cloud インフラストラクチャーの既存の単一テナント・オファリングについて言えば、インフラストラクチャーの占有スペースが削減 (つまりコストも削減) したことと、そのような単一テナント環境に統合されたサービス・モデルが主な 2 つの違いです。

## CFEE サービスはどこにありますか?
{: #where}

{{site.data.keyword.cfee_full}} サービスは、{{site.data.keyword.Bluemix_notm}} [カタログ](https://cloud.ibm.com/catalog)で検索してインスタンス化できます。

## 1 つの地域データ・センター内に複数の CFEE 環境を持つことはできますか?
{: #multiple-cfees}

はい。[これらの地域](https://dev.console.test.cloud.ibm.com/docs/cloud-foundry/index.html#provisioning-targets){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") で、必要な数の CFEE インスタンスをオンデマンドで作成できます。

## 複数のデータ・センターをまたいで (マルチゾーンで) CFEE 環境をプロビジョンできますか?
{: #multizone}
はい。 CFEE v2.2.0 以降、CFEE インフラストラクチャー (Kubernetes クラスター・ノード) を、所定の地域の複数のデータ・センター (ゾーン) 間で分散できるようになりました。 

## 開始時に必要な最小容量は決まっていますか?
{: #minimum-capacity}

はい。 CFEE インスタンスを作成するには、少なくとも 2 つの Cloud Foundry セルが必要です。各セルは、RAM 16 GB、SSD 1 次ディスク 25 GB、SSD 2 次ディスク 100 GB、およびネットワーク速度 1000 Mbps のコア 4 つで構成されます。

## CFEE がデプロイされる基礎 IaaS は何ですか?
{: #why-kubs}

CFEE サービスは Kuberneters コンテナーで実行されます。Kubernetes は多くの操作アクティビティーを自動化する非常にスマートな IaaS ですので、インフラストラクチャー・コストは低く、運用効率は高くなります。 

## CFEE の作成にはどのような分離オプションがありますか?
{: #isolation}

CFEE インスタンスがデプロイされる Kubernetes インフラストラクチャーのタイプには、_仮想共有_ハードウェアと_仮想専用_ハードウェアという 2 つのハードウェア・オプションがあります。 _仮想共有_ハードウェアの場合、ワーカー・ノード (Cloud Foundry プラットフォーム・コンテナーがデプロイされるところ) がお客様と他の IBM のお客様の間で分配されます。  _仮想専用_の場合、ワーカー・ノードは、お客様のアカウントに専用のハードウェア上でホストされます。  _仮想共有_ と_仮想専用_ のどちらの場合も、各ワーカー・ノードはお客様の単一テナントであることに注意してください。  つまり、アプリケーションが実行されている Cloud Foundry セルが他のお客様と共有されることはありません。

## 分離されたネットワーク内で CFEE を操作できますか?
{: #isolation}

はい。 バージョン 2.2.0 以降、IBM® Cloud Foundry Enterprise Environment (CFEE) インスタンスは、外部の脅威から環境を防御して保護する分離ネットワーク内で操作できるようになりました。詳しくは、[分離ネットワークでの操作](https://cloud.ibm.com/docs/cloud-foundry?topic=cloud-foundry-isolated-network#isolated-network)の資料を参照してください。

## CFEE の容量をスケーリングできますか?
{: #scaling}

はい。CFEE の容量は、Cloud Foundry セルを追加または削除することで、ニーズの変化に合わせて拡大縮小できます。

## CFEE を新規バージョンにアップグレードできますか? それはどのような方法で行われますか?
{: #upgrading}
はい。 新しい CFEE バージョンがあると CFEE ユーザー・インターフェースに通知が表示されます。  新しいバージョンに更新するタイミングはお客様が決められます。 CFEE バージョン更新プログラムは、CFEE 管理者がユーザー・インターフェースで実行します。 CFEE バージョン更新プログラムには、コンポーネントや補助サービス (Cloud Foundry や Kubernetes など) の新規バージョンが含まれている場合があります。  まず CFEE コントロール・プレーンを更新してから、Cloud Foundry セルを更新します。  更新処理は、中断時間が最短になるように最適化されています。

## CFEE インスタンスの作成にはどれくらいの時間がかかりますか?
{: #create}

CFEE サービスは {{site.data.keyword.Bluemix_notm}} カタログにリストされています。  アップグレードした {{site.data.keyword.Bluemix_notm}} アカウントと、CFEE サービスおよび補助サービス (Kubernetes、Cloud Object Storage、および Compose for PostgreSQL) に対する権限が必要です。  これらの権限を持っていれば、環境の名前を指定して_「作成」_をクリックするだけです。  作成には約 90 分かかります。

## CFEE で {{site.data.keyword.Bluemix_notm}} サービスを使用できますか?
{: #Services-ibmcloud}

もちろんです。  {{site.data.keyword.Bluemix_notm}} に統合されたので、CFEE 内の開発者は、{{site.data.keyword.Bluemix_notm}} サービス・インスタンスを作成し (または既存のインスタンスを使用し)、CFEE スペースにデプロイされたアプリケーションにそれらのインスタンスをバインドできます。

## 自分の CFEE 内に独自のサービスを作成できますか?
{: #Services-ibmcloud}

はい。  管理者が CFEE にサービス・ブローカーを登録し、その CFEE 内のユーザーにカスタム・サービス・プランを提供することができます。  ローカルの MCFEE マーケットプレイスには、{{site.data.keyword.Bluemix_notm}} カタログのサービスに加えて、CFEE のローカル・サービス・ブローカーで管理されるお客様のサービスが含まれます。

## どのような方法で CFEE へのユーザー・アクセスを制御できますか?
{: #Services}

他の {{site.data.keyword.Bluemix_notm}} サービスと同様に、CFEE へのアクセスも _ID およびアクセス管理_ (IAM) によって制御されます。 特定の役割にユーザー・アクセス・ポリシーを (個別に、またはアクセス・グループを使用して) 割り当てることで、CFEE に対する特定のアクセス・レベルを付与できます。  CFEE サービスへのアクセス以外にも、CFEE 内の Cloud Foundry 組織およびスペースへのアクセスが、特定の組織およびスペースのユーザーに割り当てられた Cloud Foundry メンバーシップおよび役割によって制御されます。

