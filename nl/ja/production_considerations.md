---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 実稼働環境でアプリを実行するためのベスト・プラクティス
{: #production}

Cloud Foundry は、クラウド対応アプリケーションを実稼働環境で実行するためのすぐれたプラットフォームです。 {{site.data.keyword.Bluemix_notm}} で実動の Cloud Foundry アプリを実行する際に、以下のベスト・プラクティスが役立ちます。
{:shortdesc}

## 複数インスタンス
{: #multiple_instances}

クラウド対応のアプリは水平にスケーラブルのため、アプリケーション・インスタンスを動的に追加したり削除したりすることができます。 単独のインシデントの発生やプラットフォームの保守が行われた際の、予期しないダウン時間を回避するために、各アプリケーションのインスタンスを少なくとも 3 つ実行します。

## モニタリング・オプション
{: #monitoring}

{{site.data.keyword.Bluemix_notm}} は、[Monitoring and Analytics](/docs/services/monana/index.html) および [New Relic ![外部リンク・アイコン](../icons/launch-glyph.svg)](http://newrelic.com/){: new_window} などのサービスを使用してアプリケーションのモニタリングを容易にします。 詳しくは、『[統合ロギング機能](../monitor_log/logging.html#logging_for_bluemix_apps)』を確認してください。

## サポート・オプション
{: #support}

{{site.data.keyword.Bluemix_notm}} の有料プランでは、*オプションの*有料サポートを含むさまざまなアカウント・タイプが提供されています。  ご使用のアカウント・タイプに関係なく、{{site.data.keyword.Bluemix_notm}} でのアプリケーションの実稼働を予定している場合は、このオプションの登録を検討してください。

有料サポートを契約しているかどうかに関係なく、お客様は『[必要なサポートを利用するには](../get-support/howtogetsupport.html)』に記載された支援を受けることができます。ただし、有料サポートは、お客様のサービス・チケットがそれに見合った注目度を確保するうえで役立ちます。
