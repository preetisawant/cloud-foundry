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

# 分離ネットワークでの作動
{: #isolated-network}


バージョン 2.2.0 以降、{{site.data.keyword.cfee_full}} (CFEE) インスタンスは、外部の脅威から環境を防御して保護する分離ネットワーク内で操作できるようになりました。分離ネットワークはプライベート VLAN および一連の制御メカニズムを介して作成し、ネットワーク境界内のリソースとの間のトラフィックをルーティング、フィルター処理、および保護します。分離ネットワークは、Virtual Router Appliances ([VRA](https://cloud.ibm.com/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started-with-ibm-virtual-router-appliance#vlans-and-the-gateway-appliance-s-role)) などのテクノロジーを使用してセットアップします。 

**注:** 分離ネットワークで作動する CFEE インスタンスは、CFEE kubernetes クラスターを v1.13 に更新することが必要です。Kubernetes クラスター v1.13 の更新は、CFEE の更新とは独立して行う必要があります。

CFEE インスタンスは、IBM Kubernetes Service からクラスターにプロビジョンされます。CFEE の Cloud Foundry セル (アプリケーションがホストされる場所) は、クラスターのワーカー・ノードにプロビジョンされます。つまり、CFEE セルとアプリケーションへのアクセスによってクラスターのワーカー・ノードのアクセスが暗黙指定されます。 

ワーカー・ノードには、ワーカー・ノード間でアプリケーションのワークロードを分散するアプリケーション・ロード・バランサー (ALB) が組み込まれています。CFEE v2.2.0 を使用すると、Kubernetes ALB をプライベート・ネットワークとパブリック・ネットワークのどちらでも利用できます。つまり、CFEE v2.2.0 はパブリック・ネットワークとプライベート・ネットワークのどちらかでもアクセスできます。

## 分離ネットワークにおける CFEE 管理
{: #control-plan-access}

v2.2.0 の CFEE 管理プレーン (プロビジョニング、更新、および他のライフサイクルのアクティビティーに使用するサブシステム) は、CFEE インスタンスを管理する点で ALB やワーカー・ノードに直接依存するわけではありません。代わりに CFEE 管理プレーンは、_Kubernetes マスターとワーカー・ノード間の VPN 接続_ を使用して CFEE インスタンスとそのリソースにアクセスします。このようにして、管理プレーンで CFEE インスタンスを制御できます。

CFEE インスタンスを作成すると、管理プレーンによってご使用のアカウントに [IAM サービス ID](https://cloud.ibm.com/docs/overview/whats-new?topic=overview-whatsnew#identity-and-access-management-application-authentication-feature) が作成され、IKS マスター・ノードに渡されます。CFEE 管理プレーンはこのサービス ID を使用して、マスター・ノードとその VPN アクセスを介して CFEE ホスト・ワーカーにアクセスし、その後のプロビジョニングや管理操作 (CFEE の Cloud Foundry メインコンポーネントのデプロイを含む) を行います。

以下に示す図は、VRA ネットワーク境界の背後にインストールされている CFEE を表わしています。   
![ネットワーク分離](img/CFEE_IsolatedNetwork.png "分離ネットワークにおける CFEE の作動方法を示す図。")

## 分離ネットワークにおける CFEE インスタンスへのアクセスの制御
{: #oppening-access-points}

CFEE インスタンスで実行される CF アプリでは、さまざまな理由によって分離ネットワーク外に出る必要がしばしば生じます。例えば、アプリケーションでパブリック RESTful サービスにアクセスしたり、Docker イメージ、NPM パッケージ、Python モジュールなどのパッケージをパブリック・レジストリーからダウンロードしたりしなければならないことがあります。そのため、特定のネットワーク・アクセスの必要性に応えるファイアウォール・ルールを構成する必要があります。

特定のプロトコル、ソース・エンドポイント、ターゲット・エンドポイントのためのルールを構成することによって、分離ネットワークとの間のインバウンド/アウトバウンド接続を制御できます。こうしたルールの作成と構成は、ネットワーク境界のセットアップに使用する特有のテクノロジー (VRA など) の制御メカニズムを使用して行えます。ただし、最も簡単な制御方法は、ホスト Kubernetes クラスター用のネットワーク・ルールを具体的に定義する [Calico ネットワーク・ポリシー](https://docs.projectcalico.org/v3.4/reference/calicoctl/resources/globalnetworkpolicy)を作成することです。段階的なガイダンスについては、[Calico ネットワーク・ポリシーの作成と適用](https://cloud.ibm.com/docs/containers?topic=containers-network_policies#adding_network_policies)を参照してください。

ネットワーク分離されている CFEE に関連するネットワーク・アクセス・ルールは、以下のいずれかのタイプにすることができます。

* **インバウンド・トラフィック・アクセス:** Kubernetes クラスターがインストールされると、[デフォルトの Calico ポリシー](https://cloud.ibm.com/docs/containers/cs_network_policy.html#default_policy)が自動的に設定および構成されます。このポリシーを使用すると、ワーカー・ノード (この場合、CFEE インスタンスをホストするノード) への管理アクセスが可能になります。

<br>
**Kubernetes クラスター**・ワーカー・ノードにアクセスするための**デフォルト**の Calico ルール:

```
allow-node-port-dnat            1500    ibm.role == 'worker_public'                        
allow-vrrp                      1600    ibm.role == 'worker_public'                        
allow-icmp                      1700    ibm.role in { 'worker_public', 'master_public' }
allow-bigfix-port               1900    ibm.role in { 'worker_public', 'master_public' }
allow-sys-mgmt                  1950    ibm.role in { 'worker_public', 'master_public' }
```
{: codeblock}
<br />
代わりのネットワーク境界実装環境を使用している場合、対応する制御メカニズムを使用して同じポリシーをセットアップする必要が生じます。
  
* **アウトバウンド・トラフィック・アクセス:** CFEE は、パブリック・エンドポイントを使用する IBM Cloud 内のいくつかのサービスに依存します。分離ネットワークでは、CFEE インスタンスがこれらのエンドポイントにアクセスできるようにする必要があります。こうしたルールをそれぞれの Calico ポリシーとともに以下に示します。

| ルール   | 説明 | エンドポイント |
|-----------|---------------|---------------|
| cfee-egress-allow-adminserver | CFEE 管理プレーンへのアウトバウンド・アクセスを許可します | 169.46.2.150/32、169.47.104.126/32、     161.156.68.46/32、130.198.90.238/32、169.46.66.254/32、169.46.186.113/32、161.156.66.118/32、130.198.90.238/32|
| cfee-egress-allow-docker | Docker レジストリーへのアウトバウンド・アクセスを許可します | `registry-1.docker.io`、`docker.io`、`production.cloudflare.docker.com`|
| cfee-egress-allow-iks | CFEE Kubernetes クラスター管理プレーンへのアウトバウンド・アクセスを許可します | [詳細はこちら](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall)|
| cfee-egress-allow-internal  | CFEE の Kubernetes クラスター・ポータブル IP アドレスへのアウトバウンド・アクセスおよびルーティングを許可します | クラスター・ポータブル・アドレスは以下を使用して検出できます: `kubectl get cm -n kube-system ibm-cloud-provider-vlan-ip-config -o json` \`jq .data."reserved_public_ip"`, `kubectl get cm -n kube-system ibm-network-interfaces -o yaml`, `kubectl get svc --all-namespaces`|
| cfee-egress-allow-postgres | CFEE の Compose for PostgreSQL データベースへのアウトバウンド・アクセスを許可します | Compose インスタンスの `<cfee-name>-postgress` のダッシュボード・ページおよび CFEE の_「プライベート・アクセス (Private Access)」_ページからエンドポイントを検出できます。|
| cfee-egress-allow-rc | サービス・シンジケーションを有効にする IBM Cloud プラットフォームへのアウトバウンド・アクセスを有効にします | `resource-controller.cloud.ibm.com` |
| cfee-egress-allow-registry | IBM Cloud Container Registry へのアウトバウンド・アクセスを許可します | [詳細はこちら](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall) |
| cfee-egress-allow-logging | (オプション) CFEE ワーカー・ノードから IBM Cloud Monitoring サービスおよび IBM Cloud Log Analysis サービスへのアウトバウンド・ネットワーク・トラフィックを許可します | [詳細はこちら](https://cloud.ibm.com/docs/containers?topic=containers-firewall#firewall_outbound) |
| cfee-egress-allow-helm-tiller | CFEE ワーカー・ノードから helm イメージ・レジストリーへのアウトバウンド・ネットワーク・トラフィックを許可します| この calico ルールは  Helm tiller の IP 用です。Helm tiller は `mage:gcr.io` ドメインと `storage.googleapis.com` ドメインにアクセスして、helm tiller イメージをプルする必要があります。|

<br>  
最後のネットワーク・セキュリティー・ルール (最**重要**なルール) は、それまでのポリシーと一致しないネットワーク・トラフィックへのアクセスをすべて拒否するルールです。
<br>
**すべてのアウトバウンド・アクセスを拒否する**ための Calico ルール (`cfee-egress-deny-all`):

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-egress-deny-all
spec:
  applyOnForward: true
  egress:
  - action: Deny
    destination: {}
    source: {}
  order: 3000
  selector: ibm.role in { 'worker_public' }
  types:
- Egress
```
{: codeblock}

<br>
**すべてのインバウンド・アクセスを拒否する** Calico ルール (`cfee-ingress-deny-all')
`):

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: cfee-ingress-deny-all
spec:
  applyOnForward: true
  ingress:
  - action: Deny
    destination: {}
    source: {}
  order: 4000
  selector: ibm.role=='worker_public'
  types:
- Ingress
```
{: codeblock}
<br>  
分離ネットワークからのアウトバウンド・アクセスで難しい部分は、一部のターゲット・エンドポイントが Cloudflare や Akamai のような_パブリック・エッジ_・ネットワークの背後にあるという状況です。この場合、頻繁に変更される数百もの IP アドレスへのアクセスを潜在的に許可しなければならない場合があります。この状態を回避する選択肢の 1 つとして、**すべてのアウトバウンド・アクセスを許可する**ことができます。その場合には、以下の Calico ルール (`cfee-egress-allow-all`) を使用します。

```
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
   name: cfee-egress-allow-http
    spec:
   egress:
   - action: Allow
     destination:
       ports:
       - 443
       - 80
     protocol: TCP
     source: {}
   order: 1611
   selector: ibm.role in { 'worker_public' }
   applyOnForward: true
   types:
   - Egress
```
{: codeblock}
  
前述の例の場合、CFEE クラスター・ワーカー・ノード (「worker_public」) に由来する HTTP 呼び出しと HTTPS 呼び出しすべて (ポート 443 および 80 上のすべての TCP トラフィック) は、パブリック・ネットワークへのアウトバウンド (「egress」) アクセスを許可されます。

## 管理コントロール・プレーンからのプライベート・アクセス
{: #private-access}

分離ネットワーク内の CFEE インスタンスを管理するには、CFEE 管理コントロール・プレーンによる CFEE インスタンスへのプライベート・アクセスが必要になります。CFEE 管理コントロール・プレーンによる CFEE インスタンスへのプライベート・アクセスはデフォルトで有効な状態です。 

_管理_ ロールを持つユーザーは、CFEE 管理コントロール・プレーンによるプライベート・アクセスを無効にすることができます。プライベート・アクセスを無効にすると、CFEE コントロール・プレーンでデータを取得したり、CFEE インスタンスを管理したりすることができなくなります (ユーザー・インターフェース、CLI、API のいずれを使用する場合でも同様です)。CFEE 管理者は、CFEE ユーザー・インターフェースにある**「プライベート・アクセス (Private Access)」**ページ (管理者のみが表示可能) でプライベート・アクセスを無効にすることができます。このページで、**「無効化」**を 1 回押します。  

分離ネットワークへのアクセスは API キーを使用して行います。デフォルトで API キーが提供されます。CFEE 管理者はデフォルトの API キーをカスタム・キーに置換できます。プライベート・アクセスを無効にした後に有効にするには、API キーが必要です。これは、*_「IBM Cloud API キー」_*(IBM Cloud ユーザー・インターフェース・ヘッダーで、_「管理」>「アクセス (IAM)」>「IBM Cloud API キー」_と移動) で生成する必要があります。

