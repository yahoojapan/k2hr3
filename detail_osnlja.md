---
layout: contents
language: ja
title: K2HR3 OSNL
short_desc: overview and details on k2hr3_osnl 
lang_opp_file: detail_osnl.html
lang_opp_word: To English
prev_url: 
prev_string: 
top_url: detailja.html
top_string: Detail
next_url: detail_variousja.html
next_string: Various
---

# 詳細（K2HR3 OpenStack Notification Listener）

K2HR3 OpenStack Notification Listenerは、OpenStackとK2HR3システムとデータを同期させる常駐プロセスです。OpenStackの各サービスからの通知メッセージを、メッセージングバックエンド経由で受け取ります。

![K2HR3 OSNL overview](images/detail_osnl.png)

ここでは、K2HR3 OpenStack Notification Listenerの動作を詳細に説明します。

## OpenStack Notification Listener

最初に[OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html)について説明します。

[OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html)は、[oslo.messaging](https://docs.openstack.org/oslo.messaging/latest/)というライブラリを使って作成された通知メッセージを処理するプログラムです。次のように動作します。

* OpenStackの各サービスは、OpenStack利用者の操作などを契機として、通知メッセージをメッセージングバックエンドに送信します。
* メッセージングバックエンドは、通知メッセージを、指定されたキューに書き込みます。
  * メッセージは、重複してキューに書き込まれることがありません。
* 指定されたキューをリスンしている[OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html)に、届いたメッセージが渡されます。
  * 複数のリスナーがキューをリスンしてる場合、一つのリスナーがランダムに選択され、メッセージが渡されます。
* [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html)は、届いたメッセージに応じて、あらかじめ定義された関数を呼び出し、メッセージを処理します。
* ある一つのメッセージに対する処理は、一つのリスナープロセスによって、一回のみ実行されます。

メッセージを作成している通知ドライバについて説明します。

* OpenStackの各サービスは、[oslo.messaging](https://docs.openstack.org/oslo.messaging/latest/)の通知ドライバを使ってメッセージを作成します。
* [OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html)が処理するメッセージは、*messaging* と *messagingv2* という通知ドライバによって作成された通知メッセージです。
* 通知ドライバの指定は、OpenStackサービスの設定ファイルを使って行われます。
* 通知ドライバの種類によって、送信されるメッセージのフォーマットが異なります。

メッセージのキューについて説明します。

* メッセージは、メッセージングバックエンドが受け取り、指定されたキューに配送されます。
* メッセージが配送されるキューの名前は、OpenStackサービスが指定します。
  * **topic** という名前で呼ばれます。
* メッセージには、オプションでメッセージが有効な範囲を指定することができます。
  * メッセージの範囲を狭め、メッセージへのアクセスを制限する効果があります。
  * **exchange** という名前で呼ばれます。
* **topic** と **exchange** の設定方法は、[環境変数・設定](environmentsja.html)をみてください。


## K2HR3 OpenStack Notification Listener

K2HR3 OpenStack Notification Listener(以下、リスナー)は、[OpenStack Notification Listener](https://docs.openstack.org/oslo.messaging/latest/reference/notification_listener.html)のプラグインです。このプラグインは次のように動作します。

![K2HR3 OSNL details](images/detail_osnl_details.png)

* メッセージキューに届いたメッセージを受信
  * メッセージは、OpenStack利用者が、削除したインスタンスの情報
* メッセージを解析
  * 削除されたインスタンスのIDとIPアドレスを抽出
* K2HR3 APIサーバの[ロールAPI](api_roleja.html)にアクセス
  * 削除されたインスタンスをロールメンバーから削除するリクエストを送信

リスナーの基本動作は次の三つの項目で制御されます。設定方法は、[環境変数・設定](environmentsja.html)をみてください。

* transport_url
  * OpenStackの各サービスの通知メッセージ送信先サーバURL
  * URLの記述方式は、**transport://user:pass@host1:port[,hostN:portN]/virtual_host** です。
    * 詳細は、[こちら](https://docs.openstack.org/oslo.messaging/latest/reference/transport.html#oslo_messaging.TransportURL)を見てください。
  * 例：rabbit://guest:guestpass@127.0.0.1:5672/
    * メッセージバックエンドは、[RabbitMQ](http://www.rabbitmq.com/)
    * ユーザ名は、`guest`
    * パスワードは、`guestpass`
    * サーバ名は、`localhost`
    * ポート番号は、`5672`
* topic
  * 通知メッセージが配送されるキューの名前を指定します。
  * OpenStackの各サービスが通知メッセージを送信するときに指定する値を指定します。
  * デフォルト設定は、notificationsです。
    * 実際の配送先キュー名は、topic設定値の末尾に、".info"が自動的に付与されます。
* exchange
  * topicの範囲です。
  * デフォルト設定は、neutronです。

**topic** と **exchange** の値は、OpenStackのサービスが送信するメッセージのフォーマットに合わせて設定する必要があります。通知メッセージのフォーマットと設定方法は、[環境変数・設定](environmentsja.html)をみてください。
