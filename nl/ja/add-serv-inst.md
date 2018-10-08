---

copyright:
  years: 2018
lastupdated: "2018-09-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# サービスの処理
{: #workingwith-services}

{{site.data.keyword.cfee_full_notm}} にデプロイされているアプリケーションは、以下の 2 つのタイプのサービス・インスタンスにバインドできます。
1. {{site.data.keyword.Bluemix}} カタログから作成され、{{site.data.keyword.Bluemix}} アカウントで使用可能なパブリック・サービス・インスタンス。
  
{{site.data.keyword.Bluemix}} アカウントで使用可能なパブリック・サービス・インスタンスは、それだけでは、CFEE 環境で使用できません。  パブリック・サービス・インスタンス ({{site.data.keyword.Bluemix}} アカウントで使用可能) が CFEE 環境内のスペースで使用可能になるためには、ターゲット CFEE スペースに明確に追加される必要があります。CFEE スペースに追加された {{site.data.keyword.Bluemix}} サービス・インスタンスは、その CFEE スペース内のアプリケーションにバインドできます。これにより、開発者は {{site.data.keyword.Bluemix}} サービスの膨大なカタログを CFEE 環境にデプロイしたアプリケーションで利用でき、それらの {{site.data.keyword.Bluemix}} サービスへのアクセス制御も可能になります。

   既存の {{site.data.keyword.Bluemix}} サービス・インスタンスを CFEE スペースに追加することに加えて、新規 {{site.data.keyword.Bluemix}} サービス・インスタンスを CFEE スペース内から作成することもでき、そうすると、そのサービス・インスタンスは自動的にその CFEE スペースに追加されます。

2. ローカル Cloud Foundry サービス・ブローカー (CFEE に対してローカル) によって管理されているサービス・インスタンス。 これは、以下の 2 つのタイプのいずれかです。
   *  2a. 現在の {{site.data.keyword.cfee_full_notm}} インスタンスの Cloud Foundry マーケットプレイスから作成されたサービス・オファリングのインスタンス。 このタイプのサービス・インスタンスでは、環境内で使用可能な登録されたサービス・ブローカーが必要です。 サービス・ブローカーにより、サービス・オファリングおよびプランのカタログが示されるとともに、該当するサービス・オファリングからのインスタンスを作成、削除、バインド、およびアンバインドできます。 詳しくは、Cloud Foundry 資料の『[Managing Service Brokers](https://docs.cloudfoundry.org/services/managing-service-brokers.html)』を参照してください。
   * 2b. ユーザー提供のサービス・インスタンス。 このタイプの作成は、CLI でサポートされますが、ユーザー・インターフェースではサポートされません。 それにもかかわらず、ユーザー提供のサービス・インスタンスは、ユーザー・インターフェースにリストされます。
   

## すべての CFEE 環境の {{site.data.keyword.Bluemix_notm}} サービス・インスタンスの表示
{: #viewing-services_across}

[Cloud Foundry サービス・ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/services)に移動して、{{site.data.keyword.Bluemix_notm}} アカウント内の (アクセス権限を持っている) すべての {{site.data.keyword.Bluemix_notm}} サービス・インスタンスの統合ビューを表示し、どのサービス・インスタンスがどの CFEE スペースに追加済みなのかを確認することができます。

このビューには、アカウント内のすべての使用可能な {{site.data.keyword.Bluemix_notm}} が表示され、どれがどの CFEE スペースに追加済み (別名割り当て済み) なのかが示されます。サービス・インスタンスを展開すると、そのサービス・インスタンスが追加された CFEE スペースが表示されます。さらに展開すると、サービス・インスタンスがバインドされた先の、それらの CFEE スペース内のアプリケーションを表示することができます。  

このビューから、CFEE スペースにデプロイされたアプリケーションを、追加されたそれらのサービス・インスタンスにバインドすることもできます。対応するサービス (特定の CFEE スペースで使用可能) の表の行の右端にあるメニューに進み、**「アプリケーションにバインド」**を選択します。

## CFEE スペースへの既存の {{site.data.keyword.Bluemix_notm}} サービス・インスタンスの追加
{: #adding-services_inspace}

{{site.data.keyword.Bluemix_notm}} サービス・インスタンスを、CFEE スペースにデプロイされたアプリケーションにバインドできます。IBM Cloud サービス・インスタンスを CFEE にデプロイされたアプリケーションにバインドするには、その前に、そのサービス・インスタンスを、そのアプリケーションがデプロイされている CFEE スペースに追加する必要があります。{{site.data.keyword.Bluemix_notm}} サービス・インスタンスを CFEE スペースに追加するためには、前もって以下の要件が満たされている必要があります。
* その {{site.data.keyword.Bluemix_notm}} サービスは、CFEE インスタンスがあるのと同じ {{site.data.keyword.Bluemix_notm}} アカウント内で使用可能である必要があります。
* その {{site.data.keyword.Bluemix_notm}} サービス・インスタンス自体に対するアクセス権限を持っている必要があります。詳しくは、{{site.data.keyword.Bluemix_notm}} ヘッダーの**「管理」>「ユーザー」** メニューにある「ID およびアクセス」ページを参照して、現在のアカウント・アクセス・ポリシーを確認してください。

既存の {{site.data.keyword.Bluemix_notm}} サービス・インスタンスを CFEE スペースに追加するには、次のようにします。
1. [Cloud Foundry サービス・ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/services)に移動します。  
2. リスト内で対象の {{site.data.keyword.Bluemix_notm}} サービス・インスタンスを見つけて、対応する表の行の右端にあるメニューを起動します。
3. **「サービスの追加」**を選択します。
4. _「サービスの追加」_ダイアログで、サービスを追加する先の CFEE、組織、およびスペースを選択し、**「追加」**をクリックします。
5. ターゲット {{site.data.keyword.Bluemix_notm}} サービスを展開して、サービスが追加された新しい CFEE を確認します。


代わりに以下のようにして、{{site.data.keyword.Bluemix_notm}} サービス・インスタンスを、それを追加したい CFEE スペース内から追加することができます。
1. {{site.data.keyword.Bluemix_notm}} [ダッシュボード](https://console.bluemix.net/dashboard)または [Cloud Foundry サービス・ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/services)で、アプリケーションがホストされている Cloud Foundry Enterprise Environment を見つけます。
2. ナビゲーション・ペインで**「組織」**に移動し、アプリケーションがある組織およびスペースを開きます。
3. **「スペース」**タブに移動し、アプリケーションが含まれているスペースを見つけます。
4. ターゲット・スペースのページで、**「サービス」**タブに移動し、**「サービスの追加」**をクリックします。これにより、__「サービスの追加」__ダイアログが開きます。{{site.data.keyword.Bluemix_notm}} アカウント内で使用可能なサービス・インスタンスのリストがページに表示されます。
5. 使用可能なサービス・インスタンスから CFEE スペースに追加するものを見つけて選択します。 
6. CFEE スペース内で使用可能なサービスのリストにそのサービス・インスタンスが追加されます。

   **注:** {{site.data.keyword.Bluemix_notm}} サービスを CFEE スペースに追加すると、そのサービス・インスタンスの別名がそのスペース内で作成されます。サービス・インスタンスを CFEE スペースから**削除**する (表内の対応するサービス・インスタンス行の右端にあるメニューから行えます) 場合、サービスはパブリック・アカウントからは削除されません。この操作は、特定の CFEE アカウントからの削除を行うだけであり、その CFEE スペース内のアプリケーションへのバインドができなくなります。また、サービス・インスタンス自体を {{site.data.keyword.Bluemix_notm}} アカウントから削除すると、そのサービスはどの CFEE スペースでも使用可能ではなくなります。 

## CFEE スペース UI からの {{site.data.keyword.Bluemix_notm}} サービス・インスタンスの作成
{: #creating-services_inspace}
CFEE スペース内から {{site.data.keyword.Bluemix_notm}} サービス・インスタンスを作成できます。{{site.data.keyword.Bluemix_notm}} サービス・インスタンスの作成の結果、次のようになります。
* {{site.data.keyword.Bluemix_notm}} サービス・インスタンスが IBM Cloud 内に作成されます。これは、{{site.data.keyword.Bluemix_notm}} [カタログ](https://console.bluemix.net/catalog)からのサービス・インスタンスの作成と等価です。
* {{site.data.keyword.Bluemix_notm}} サービス・インスタンスが、作成操作が開始された CFEE スペースに追加 (別名割り当て) されます。


CFEE スペース内からサービス・インスタンスを作成するには、次のようにします。
1. ターゲット・スペース・ページで、**「サービス」**タブに移動し、**「サービスの作成」**をクリックします。  これにより、{{site.data.keyword.cfee_full_notm}} の**「マーケットプレイス」**ビューが開きます。このビューでは、以下の 2 つのソースからのサービス・オファリングがリストされます (「__ソース__」列を参照)。
   * {{site.data.keyword.Bluemix_notm}} カタログからのオファリング。
   * ローカル {{site.data.keyword.cfee_full_notm}} マーケットプレイスからのオファリング。
5. 使用可能なサービス・オファリングからインスタンスを生成するものを見つけて選択します。 
6. サービス・オファリングのソース (IBM Cloud カタログまたはローカル CFEE マーケットプレイス) に応じて、以下のいずれかに進みます。
   * 選択したサービス・オファリングが {{site.data.keyword.Bluemix_notm}} カタログからのオファリングである場合、IBM Cloud サービス・オファリング作成ページに進むための**「続行」**ボタンが表示されます。これは、{{site.data.keyword.Bluemix_notm}} カタログから使用できるのと同じページです。このページで、新規サービス・インスタンスの名前、地域、プラン、および IBM Cloud 内でサービスを作成するために必要なその他の特性を指定します。サービス・インスタンスを作成すると、それは IBM Cloud 内に作成され、自動的に現行 CFEE スペースに追加されます。
   * 選択したサービス・オファリングがローカル CFEE カタログからのものである場合、サービス・インスタンスを作成するための**「作成」**ボタンが表示されます。サービス・インスタンスが作成される現行 CFEE 内の組織およびスペースを指定するように求めるプロンプトが出されます。

## CLI を使用した CFEE スペースからの {{site.data.keyword.Bluemix_notm}} サービス・インスタンスの作成
{: #creating-services_cli}

CFEE 内のスペースから CLI を使用してサービス・インスタンスを作成できます。CFEE スペースからの CLI を使用したサービスの作成は、そのスペース内での UI を使用した作成と等価です。つまり、サービスを作成すると、以下の 2 つの結果が生じます。
* {{site.data.keyword.Bluemix_notm}} サービス・インスタンスが IBM Cloud 内に作成されます。これは、{{site.data.keyword.Bluemix_notm}} [カタログ](https://console.bluemix.net/catalog)からのサービス・インスタンスの作成と等価です。
* {{site.data.keyword.Bluemix_notm}} サービス・インスタンスが、作成操作が開始された CFEE スペースに追加 (別名割り当て) されます。

サービス・インスタンスの作成を CFEE スペース内から行うことと CLI から行うことの相違点は、作成されたサービス・インスタンスのライフサイクルの違いです。CFEE スペース UI でサービス・インスタンスを作成した場合、作成されたサービス・インスタンスのライフサイクルは、{{site.data.keyword.Bluemix_notm}} アカウント内のサービス・インスタンス自体から制御されます。これは、サービス・プランの更新が、CFEE スペースからではなく、{{site.data.keyword.Bluemix_notm}} アカウント内のインスタンスから制御されることを意味します。代わりに、サービス・インスタンスが CLI から作成された場合、サービスのライフサイクルは CFEE スペースから制御されます (サービスは CFEE スペースから更新されます)。

CLI から作成されたサービス・インスタンスは UI でも表示され、サービス・インスタンス名の横の ` * ` で示されます。

CLI を使用してサービス・インスタンスを作成するには、以下の手順に従います。

1. まだ行っていない場合、{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェースをダウンロードしてインストールします ([Cloud Foundry CLI のダウンロード](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください)。

2. {{site.data.keyword.cfee_full}} の概要ページに移動し、環境の API エンドポイントを見つけます。

3. コマンド・ライン・インターフェースで、以下のように API エンドポイントを CFEE 環境のエンドポイントに設定します。

  ```
  cf api <api_enpoint>
  ```
  {: pre}

4. CFEE 環境にログインします。

  ```
  cf login -u <username> -o <org_name> -s <space_name>
  ```
  {: pre}

  フェデレーテッド ID を使用する場合、`-sso` オプションを使用してください。

  ```
  cf login -o <org_name> -s <space_name> -sso
  ```
  {: pre}
  
5. サービスを作成します。
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c '{"name":"value","name":"value"}'
  ```
  {: pre}

  オプションで、特定のサービスを作成するために必要な有効な JSON オブジェクトのパラメーターを含んでいるファイルを提供することができます。
  このパラメーター・ファイルへのパスはファイルへの絶対パスまたは相対パスとすることができます。
  
  ```
  cf create-service SERVICE PLAN SERVICE_INSTANCE -c PATH_TO_FILE
  ```
  {: pre}
   
  以下に、有効な JSON オブジェクトの例を示します。
   
  ```
   {
      "cluster_nodes": {
         "count": 5,
         "memory_mb": 1024
      }
   }
  ```
  {: pre}
  
   CLI からのサービスの作成のヘルプを見るには、以下を実行します。
  
  ```
  cf cs -help
  ```
詳細情報については、Cloud Foundry 資料の [cf CLI を使用したサービス・インスタンスの管理](https://docs.cloudfoundry.org/devguide/services/managing-services.html){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。
  
## アプリケーションへのサービスのバインド
{: #bind_services}

[Cloud Foundry サービス・ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/services)から、または、CFEE スペース・ページの「サービス」タブから、CFEE にデプロイされたアプリケーションにサービス・インスタンスをバインドできます。  

アプリケーションへのサービス・インスタンスのバインドを [Cloud Foundry サービス・ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/services)から行うには、次のようにします。
1. [Cloud Foundry サービス・ダッシュボード](https://console.bluemix.net/dashboard/cloudfoundry/services)に移動して、{{site.data.keyword.Bluemix_notm}} アカウント内の使用可能なすべての {{site.data.keyword.Bluemix_notm}} サービス・インスタンスの統合ビューを表示します。どの {{site.data.keyword.Bluemix_notm}} サービス・インスタンスがどの CFEE スペース内で使用可能である (別名が割り当てられている) のかを表示することもこのビューの目的です。サービス・インスタンスを展開して、そのサービス・インスタンスが追加された CFEE スペースを表示することができます。さらに展開すると、サービス・インスタンスがバインドされた先の、それらの CFEE スペース内のアプリケーションを表示することができます。 
2. バインドする {{site.data.keyword.Bluemix_notm}} サービス・インスタンスを見つけます。
3. 対応するビューを展開して、サービス・インスタンスが追加されたすべての CFEE スペースを表示します。そのサービス・インスタンスが、アプリケーションがデプロイされた CFEE スペースに追加されていない場合、ターゲット CFEE スペース内でそのサービス・インスタンスを使用可能にするため、行の右端にあるメニューから**「追加」**を選択します。
4. サービス・インスタンスが使用可能な CFEE スペースに対応している行の右端にあるメニューに移動し、**「アプリケーションのバインド」**を選択します。
5. __「アプリケーションのバインド」__ダイアログで、バインドするアプリケーションを選択します。
6. そのアプリケーションが、それがデプロイされている CFEE スペース内のサービス・インスタンスにバインドされます。表内の対応する行を展開して、CFEE スペース内のバインドされたアプリケーションを表示できます。


サービス・インスタンスへのアプリケーションのバインドを CFEE スペースの__「サービス」__ページから行うには、次のようにします。

1. アプリケーションがデプロイされた CFEE ユーザー・インターフェースを開きます。
2. 左側のナビゲーション・ペインで**「組織」**に移動し、アプリケーションがデプロイされた組織およびスペースを開きます。
3. **「スペース」**タブに移動し、アプリケーションが含まれているスペースを見つけます。
4. ターゲット・スペース・ページで**「サービス」**タブに移動します。
5. **「サービス・インスタンス」**の表で、バインドしたいサービス・インスタンスに対応している行の右端にある__「アクション」__メニューに移動し、**「バインド」**を選択します。
6. サービス・インスタンスにバインドするアプリケーションを選択します。

アプリケーションをサービス・インスタンスからアンバインドするには、以下のようにします。

1. スペースの**「サービス」**タブで、ターゲット・サービス・インスタンスを展開して、そのインスタンスにバインドされているアプリを表示します。
2. アプリケーションの行にある「アクション」メニューに移動し、**「サービスのアンバインド」**を選択します。

CLI を使用したアプリケーションのバインドについて詳しくは、Cloud Foundry 資料で[サービス・インスタンスのバインド](https://docs.cloudfoundry.org/devguide/services/application-binding.html){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") を参照してください。


