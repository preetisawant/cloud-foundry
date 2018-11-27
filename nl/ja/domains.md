---

copyright:
  years: 2018
lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# ドメインの管理
{: #domains}

Cloud Foundry ドメインには、以下の 2 つのタイプがあります。
* {{site.data.keyword.cfee_full_notm}} 内の任意のスペースで任意のアプリケーションが使用できる共有ドメイン。共有ドメインにアクセスするには、UI の左側のナビゲーション・ペインにある**「ドメイン」**ページ (*「操作」*の下) に移動します。
* 特定の組織内のアプリケーションおよびスペースのみが使用できるプライベート・ドメイン。組織内のドメインにアクセスするには、UI の左側のナビゲーション・ペインにある**「組織」** ページに移動し、組織を開き、**「ドメイン」** タブに移動します。

## ドメインの作成および削除
{: #create-domains}

共有ドメインを作成するには、{{site.data.keyword.cfee_full_notm}} の左側のナビゲーション・ペインにある**「ドメイン」** に移動します。  

プライベート・ドメインを作成するには、UI の左側のナビゲーション・ペインにある**「組織」**ページに移動し、組織を開き、**「ドメイン」**タブに移動します。

_「ドメイン」_ページ (共有ドメインの場合) または特定の組織の_「ドメイン」_タブ (プライベート・ドメインの場合) で、**「ドメインの作成」**をクリックしてドメインを作成し、固有の名前を入力します。

**注:** ドメイン名は、{{site.data.keyword.cfee_full_notm}} の範囲全体で固有でなければなりません。つまり、プライベート・ドメインに、同じ {{site.data.keyword.cfee_full_notm}} 内にある共有ドメインやプライベート・ドメインの名前を付けることはできません。

以下のコマンドを実行して、Cloud Foundry CLI から共有ドメインを作成することもできます。
  ```
  cf create-shared-domain <domain name>
  ```
  {: pre}
  
以下のコマンドを実行して、Cloud Foundry CLI からプライベート・ドメインを作成できます。
  ```
  cf create-domain my-org <domain name>
  ```
  {: pre}
  
**注:** Cloud Foundry CLI から作成したドメインはただちに UI に表示されますが、有効になるまでには最大で 1 時間かかる場合があります。

ドメインを削除するには、削除するドメインに対応する表の行の右端にあるメニューに移動し、**「ドメインの削除 (Delete domain)」**を選択します。
  
以下のコマンドを実行して、CLoud Foundry CLI から共有ドメインを削除することもできます。
  ```
  cf delete-shared-domain <domain name>
  ```
  {: pre}  
  
  ```
  cf delete-domain my-org <domain name>
  ```
  {: pre}
  
 
 ## SSL 証明書のアップロード
 {: #upload-certificates}
 
ドメイン (共有またはプライベート) の SSL 証明書をアップロードできます。証明書を追加するドメインに対応する表の行の**「アップロード」**をクリックし、証明書を含むファイルと、秘密鍵を含むファイルを選択します。
  
