---

copyright:

  years: 2015, 2017, 2018

lastupdated: "2018-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# IBM Cloud Foundry Enterprise Environment の新機能

本書では、現在日付までにリリースされた {{site.data.keyword.cfee_full_notm}} サービスの各バージョンの新機能について説明します。

## バージョン 1.1.0
{: #v101}

_リリース日:_ 2018-11-16

{{site.data.keyword.cfee_full_notm}} サービスのバージョン 1.1.0 では、以下の変更がリリースされました。

* 新規機能:
   * CFEE インスタンスが新規バージョンに[更新](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#update)されました。
   * Cloud Foundry セルを追加または削除して、CFEE インスタンスの容量を[スケーリング](https://console.bluemix.net/docs/cloud-foundry/updating-scaling.html#update-scale#scale)できます。
   * 自動構成される IBM Cloud Activity Tracker サービス・インスタンスと統合して、Cloud Foundry のアクティビティーを[監査](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#auditing)できます。
   * 自動構成される IBM Cloud Log Analysis サービス・インスタンスで、Cloud Foundry の[ログ・イベント](https://console.bluemix.net/docs/cloud-foundry/auditing-logging.html#auditing-logging#logging)を永続化できます。
   * CFEE インスタンスを作成する権限を取得および設定するための新しい `ibmcloud cfee` [コマンド](https://console.bluemix.net/docs/cloud-foundry/permissions.html#permissions#permcli-creating)が用意されました。これらのコマンドにより、CFEE サービスおよび必要な補助サービスに対する許可の設定をまとめて単純化することができます。
   * IBM Cloud アカウント内のユーザーに対する IBM クラウド・サービスの[可視性の制御](https://console.bluemix.net/docs/cloud-foundry/add-serv-inst.html#workingwith-services#service_visibility)を簡単に行える新しい `ibmcloud catalog blacklist` コマンドが用意されました。

* 解決された問題:
   *  解決された問題: セルのメトリックへのアクセス中に断続的にエラーが発生する
   
この[短いビデオ](https://ibm.biz/CFEE-V110){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") で、CFEE v1.1.0 の新機能について説明しています。

さまざまな CFEE のトピックに関するその他のビデオが、[CFEE ビデオの再生リスト](https://ibm.biz/CFEE-Playlist){: new_window} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン") にあります。
