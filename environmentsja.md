---
layout: contents
language: ja
title: Environments/Settings
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: environments.html
lang_opp_word: To English
prev_url: developerja.html
prev_string: Developer
top_url: indexja.html
top_string: TOP
next_url: toolsja.html
next_string: Tools
---

このページでは、K2HR3システムの中で使われている環境変数と設定項目を説明しています。

# 環境変数

K2HR3システムの中で使われている環境変数を説明しています。

## APIサーバー

この章は、APIサーバで使われている環境変数を説明しています。

### HOME

HOME環境変数は、k2hr3-api Node.jsモジュールを起動するユーザのホームディレクトリとして使用されます。

**devcluster** を使って、K2HR3を構築した場合は、 **/home/k2hr3** がデフォルト値となっています。

### NODE_CONFIG_DIR

NODE_CONFIG_DIR環境変数は、k2hr3-api Node.jsモジュールの設定ファイルのインストール先ディレクトリとして使われます。

**devcluster** を使って、K2HR3を構築した場合は、 **/home/k2hr3/etc/k2hr3-api** がデフォルト値となっています。

### NODE_DEBUG

NODE_DEBUG環境変数は、ログレベルとして使われます。指定可能なレベルと動作概要は次の通りです。

* LOGLEVEL_DBG
  * アプリケーション動作の詳細ログを出力。デバッグ用途で使われます。
* LOGLEVEL_MSG
  * アプリケーション動作概要ログを出力します。
* LOGLEVEL_WAN
  * 警告メッセージ、エラーのみ出力します。
* LOGLEVEL_ERR
  * エラーのみ出力します。
* LOGLEVEL_SLT　
  * ログは出力されません。

**devcluster** を使って、K2HR3を構築した場合は、 **LOGLEVEL_ERR** がデフォルト値となっています。

### NODE_ENV

NODE_ENV環境変数は、nodeプロセスの動作環境として表す環境変数として使用されます。指定可能な名前と動作概要は次の通りです。

* development
  * 開発用途に最適化された状態で動作します。
* production
  * 通常と同じ状態で動作します。

**devcluster** を使って、K2HR3を構築した場合は、 **development** がデフォルト値となっています。


### 補足：systemd使用時の環境変数の指定について

ここでは、[systemd](https://www.freedesktop.org/wiki/Software/systemd/)を使ってプロセスを起動する場合の環境変数の指定方法について説明しています。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) は、OS起動または終了時に、常駐プロセスの起動・停止を制御することができる、OS付属のサービスマネージャーです。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定は、必須ではありません。OS起動（または終了）時に、自動的にプロセスを起動（または停止）したい場合は、次のように設定しておくこともできます。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) を使って APIサーバを起動する場合は、 [systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定ファイルの[Environment変数](https://www.freedesktop.org/software/systemd/man/systemd.exec.html#Environment)に、環境変数を指定します。

**devcluster** を使って、APIサーバを構築した場合は、 APIサーバのsystemd設定ファイルは、/etc/systemd/system/k2hr3-api.service にインストールされます。

/etc/systemd/system/k2hr3-api.service の環境変数をエディタなどで更新し、次のように実行すると、環境変数がプロセスに反映されます。

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-api.service
```

## Webサーバー

この章は、Webサーバーで使われている環境変数を説明しています。

### HOME

HOME環境変数は、k2hr3-app Node.jsモジュールを起動するユーザのホームディレクトリとして参照されています。

**devcluster** を使って、K2HR3を構築した場合は、 **/home/k2hr3** がデフォルト値となっています。

### NODE_CONFIG_DIR

NODE_CONFIG_DIR環境変数は、k2hr3-app Node.jsモジュールの設定ファイルのインストール先ディレクトリとして使われます。

**devcluster** を使って、K2HR3を構築した場合は、 **/home/k2hr3/etc/k2hr3-app** がデフォルト値となっています。

### NODE_ENV

NODE_ENV環境変数は、nodeプロセスの動作環境として表す環境変数として使用されます。指定可能な名前と動作概要は次の通りです。

* development
  * 開発用途に最適化された状態で動作します。
* production
  * 通常と同じ状態で動作します。

**devcluster** を使って、K2HR3を構築した場合は、 **development** がデフォルト値となっています。


### 補足：systemd使用時の環境変数の指定について

ここでは、[systemd](https://www.freedesktop.org/wiki/Software/systemd/)を使ってプロセスを起動する場合の環境変数の指定方法について説明しています。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) は、OS起動または終了時に、常駐プロセスの起動・停止を制御することができる、OS付属のサービスマネージャーです。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定は、必須ではありません。OS起動（または終了）時に、自動的にプロセスを起動（または停止）したい場合は、次のように設定しておくこともできます。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) を使って Webサーバを起動する場合は、 [systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定ファイルの[Environment変数](https://www.freedesktop.org/software/systemd/man/systemd.exec.html#Environment)に、環境変数を指定します。

**devcluster** を使って、Webサーバを構築した場合は、 Webサーバのsystemdの設定ファイルは、/etc/systemd/system/k2hr3-app.service にインストールされます。

/etc/systemd/system/k2hr3-app.service の環境変数をエディタなどで更新し、次のように実行すると、環境変数がプロセスに反映されます。

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-app.service
```

# 設定

K2HR3システムの中で使われている設定ファイルの項目を説明しています。

## データーサーバー（K2HDKC）

この章では、データーサーバー（K2HDKC）の設定ファイルとその項目説明します。

* ここでは、データーサーバー（K2HDKC）の起動に最低限必要な項目のみについて説明しています。
* K2HDKCの説明は、[K2HDKC](https://chmpx.antpick.ax/) を見てください。
* K2HDKCの設定ファイルの全項目は、 [CHMPXの詳細ページ](https://chmpx.antpick.ax/detailsja.html) を見てください。

データーサーバー（K2HDKC）は、複数のホストから構成されるクラスタです。各ホスト上には、chmpxプロセスとk2hdkcプロセスが起動します。

* chmpxプロセス
  * このプロセス、複数のホストを一つの分散KVSクラスタとして構成するためのサーバプロセスです。
  * 設定ファイルは /etc/k2hdkc/server.ini にインストールされます。
* k2hdkcプロセス
  * このプロセスは、ネットワーク経由でk2hr3データベースへの参照・更新などのリクエストを受けるサーバプロセスです。
  * 設定ファイルは、chmpxプロセスと共通です。

/etc/k2hdkc/server.ini の **[SVRNODE]** セクションの **NAME** に、データーサーバー（K2HDKC）のホスト名が記述されています。サーバ名が複数の場合は、正規表現に似た表記で記述することも可能です。

例：データーサーバー（K2HDKC）が、dkc01~dkc04.example.comというホストで構成されていた場合、次のように記述することも可能です。
```
...
#
# SERVER NODES SECTION
#
[SVRNODE]
NAME                            = dkc[1-4].example.com
PORT                            = 8020
CTLPORT                         = 8021
SSL                             = no
...
```

### 補足：サービスマネージャ(systemd)の設定

ここでは、[systemd](https://www.freedesktop.org/wiki/Software/systemd/)を使ってデーターサーバー（K2HDKC）のプロセスを制御する方法を説明しています。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) は、OS起動または終了時に、常駐プロセスの起動・停止を制御することができる、OS付属のサービスマネージャーです。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定は、必須ではありません。OS起動（または終了）時に、自動的にプロセスを起動（または停止）したい場合は、次のように設定しておくこともできます。

次の内容を /etc/systemd/system/chmpx.service に保存します。
```
[Unit]
Description=chmpx
After=network-online.target

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStartPre=/sbin/sysctl fs.mqueue.msg_max=1024
ExecStart=/usr/bin/chmpx -conf /etc/k2hdkc/server.ini -d err
Restart=on-failure
PIDFile=/var/run/chmpx.pid

[Install]
WantedBy=multi-user.target
```

次のように実行し、上で保存した設定ファイルをsystemdに反映させ、chmpxプロセスをchmpxというサービスとして起動します。
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart chmpx.service
```

続いて、k2hdkcプロセスをサービスとして起動する設定をします。次の内容を /etc/systemd/system/k2hdkc.service に保存します。
```
[Unit]
Description=k2hdkc
Requires=chmpx.service
After=chmpx.service

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStartPre=/sbin/sysctl fs.mqueue.msg_max=1024
ExecStart=/usr/bin/k2hdkc -conf /etc/k2hdkc/server.ini -d err
Restart=on-failure
PIDFile=/var/run/k2hdkc.pid

[Install]
WantedBy=multi-user.target
```

次のように実行し、上で保存した設定ファイルをsystemdに反映させ、k2hdkcプロセスをk2hdkcサービスとして起動します。
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hdkc.service
```

## APIサーバー

この章は、APIサーバで動作するプロセスとその設定ファイルについて説明しています。

APIサーバーの設定ファイルの項目を説明します。APIサーバーには、次の三つのプロセスが起動します。

* HTTPサーバープロセス
  * HTTPサーバーは、[Node.js](https://nodejs.org/)で実装されています。
* chmpx-slaveプロセス
  * HTTPサーバーとデーターサーバー（K2HDKC）との接続を仲介するプロセスです。
  * 設定ファイルは、/etc/k2hdkc/slave.ini です。
  * データーサーバー（K2HDKC）のサーバ名を設定します。
* watcherプロセス
  * OpenStackインスタンスのIPアドレスを死活監視するプロセスです。
  * Node.jsプロセスの設定ファイルの中に設定を記述します。

### HTTPサーバー設定

ここでは、HTTPサーバーの設定項目を説明しています。

* 設定ファイルは、 /home/k2hr3/node_modules/k2hr3-api/config の下にインストールされます。
* default.json ファイルの設定項目の中から、変更したい項目のみを抜き出して、自分専用のファイル(local.jsonなど)に保存してお使いください。
* 自分専用のファイル名は、[configモジュールのルール](https://github.com/lorenwest/node-config/wiki/Configuration-Files#file-load-order) にしたがって作成してください。
* 命名ルールをよく理解できない場合は、local.json にしておけば問題ありません。
* default.jsonと自分専用のファイルを /home/k2hr3/etc/k2hr3-api の下にコピーしてください。

以下は、設定項目のサンプルとその説明です。

```
{
    "keystone": {
        "type": "openstackapiv3",                              // keystoneエンドポイントのバージョン(openstackapiv3 または openstackapiv2)
        "eptype": "list",                                      // keystoneエンドポイントの指定方法(listまたはfile)
        "epfile": null,                                        // keystoneエンドポイントのファイル名(listの場合はnull)
        "eplist": {
            "myregion": "https://dummy.keystone.openstack/"    // keystoneエンドポイント名及びURL
        }
    },
    "k2hdkc": {
        "config": "/etc/k2hdkc/slave.ini",                     // chmpx-slaveの設定ファイル名
        "port": 8031                                           // chmpx-slaveのサービスポート番号
    },
    "multiproc": true,                                         // 複数プロセス起動の有無
    "scheme": "https",                                         // APIサーバープロトコル（http/https)
    "runuser": "nobody",                                       // 起動ユーザ名
    "privatekey": "config/key.pem",                            // 秘密鍵ファイル名
    "cert": "config/cert.pem",                                 // サーバ証明書ファイル名
    "ca": "/etc/pki/tls/certs/ca-bundle.crt",                  // ルート認証局証明書ファイル名
    "logdir": "log",                                           // ログディレクトリ名
    "accesslogname": "access.log",                             // 標準出力ファイル名
    "consolelogname": "error.log",                             // 標準エラー出力ファイル名
    "watcherlogname": "watcher.log",                           // 標準出力ファイル名(watcher用)
    "wconsolelogname": "watchererror.log",                     // 標準エラー出力ファイル名(watcher用)
    "logrotateopt": {                                          // ログローテーション関連設定
        "compress": "gzip",                                    // ローテーション時のログ圧縮方式(gzipのみ)
        "interval": "6h",                                      // ローテーション期間
        "initialRotation": true                                // ローテーション期間以降の初回起動時におけるローテーション実行の有無
    },
    "userdata": {                                              // UserData取得API関連設定
        "baseuri": "https://localhost",                        // APIエンドポイントの基本パス
        "cc_templ": "config/k2hr3-cloud-config.txt.templ",     // cloud configのテンプレートファイルパス
        "script_templ": "config/k2hr3-init.sh.templ",          // cloud init用シェルスクリプトテンプレートファイル名
        "errscript_templ": "config/k2hr3-init-error.sh.templ", // cloud init用エラー出力用シェルスクリプトテンプレートファイル名
        "algorithm": "aes-256-cbc",                            // 暗号アルゴリズム名
        "passphrase": "k2hr3_regpass"                          // 暗号化パスフレーズ
    },
    "k2hr3admin": {
        "tenant": "admintenant",                               // テナント(プロジェクト)名
        "delhostrole": "delhostrole"                           // ホスト削除用サーバ用のロール名
    },
    "confirmtenant": false,                                    // 未登録のテナント(プロジェクト)のサービスへの追加確認の有無
    "chkipconfig": {                                           // IPアドレス死活監視
        "type": "Listener"                                     // IPアドレス死活監視の方式名(後述)
        "pendingsec": 864000,                                  // 最初に未検出となった時刻から削除されるまでの時間(秒)
        "intervalms": 4320000,                                 // 死活監視の実行間隔時間(ミリ秒)
        "parallelcnt": 32,                                     // 死活監視実行処理の並列数
        "command4": "ping",                                    // UNIXコマンドパス名(IPv4アドレス用)
        "command6": "ping6",                                   // UNIXコマンドパス名(IPv6アドレス用)
        "params": "-c 1",                                      // UNIXコマンド引数(ICMPによるリクエスト回数)
        "timeoutparam": "-W",                                  // UNIXコマンド引数(タイムアウト時間指定用)
        "timeoutms": 5000                                      // UNIXコマンド引数(タイムアウト時間)
    },
    "allowcredauth": true                                      // クレデンシャル認証のみによるアクセス許可
}
```

### chmpx-slaveの設定

ここでは、chmpx-slaveプロセスの設定について説明しています。

chmpx-slaveプロセスは、HTTPサーバとデーターサーバー（K2HDKC）との接続を仲介するプロセスです。設定ファイルは、/etc/k2hdkc/slave.ini です。

`[SVRNODE]`セクションの`NAME`に、データーサーバー（K2HDKC）のホスト名を記述します。サーバ名を正規表現に似た表記で記述することも可能です。

例：データーサーバー（K2HDKC）が、dkc01~dkc04.example.comというホストで構成されていた場合、次のように記述することも可能です。
```
...
#
# SERVER NODES SECTION
#
[SVRNODE]
NAME                            = dkc[1-4].example.com
PORT                            = 8020
CTLPORT                         = 8021
SSL                             = no
...
```

設定ファイルの項目は、 [CHMPXの詳細ページ](https://chmpx.antpick.ax/detailsja.html) に説明されています。

### Watcher(IPアドレス死活監視)の設定

ここでは、**Watcher**の設定について説明しています。

OpenStackからインスタンスが削除されたとき、K2HR3のデータベースからそのインスタンスのIPアドレスを削除する必要があります。

K2HR3からのIPアドレス削除は、K2HR3 OpenStack Notification Listener（k2hr3-osnl）を使って実施することをおすすめします。

k2hr3-osnl を利用できない場合は、IPアドレス死活監視プログラム（Watcher) を起動し、削除されたインスタンスのIPアドレスをK2HR3のデータベースから削除できます。

Watcher には、以下のタイプを指定できます。

* Listenerタイプ
  * このタイプが指定された場合には、k2hr3-osnl が動作している前提となります。  
  * 現時点でWatcherが動作する内容がないため、Watcherは何も処理をしません。

* Basic{And/Or}タイプ
  * このタイプが指定された場合には、DNS登録の有無の確認、Ping（ICMP）確認を行います。  
  * AndとOrの違いは、これらの確認項目の全て(And)で、1つでも（Or）未検出となった場合にIPアドレスの削除の条件が整うことを意味しています。

* NoCheckタイプ
  * このタイプが指定された場合には、Watcherは何も処理をしません。


### 補足：サービスマネージャ(systemd)の設定

この章は、[systemd](https://www.freedesktop.org/wiki/Software/systemd/)を使ってAPIサーバーの各プロセスを制御する方法を説明しています。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) は、OS起動または終了時に、常駐プロセスの起動・停止を制御することができる、OS付属のサービスマネージャーです。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定は、必須ではありません。OS起動（または終了）時に、自動的にプロセスを起動（または停止）したい場合は、次のように設定しておくこともできます。

次の内容を /etc/systemd/system/chmpx-slave.service に保存します。
```
[Unit]
Description=chmpx
After=network-online.target

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStartPre=/sbin/sysctl fs.mqueue.msg_max=1024
ExecStart=/usr/bin/chmpx -conf /etc/k2hdkc/slave.ini -d err
Restart=on-failure
PIDFile=/var/run/chmpx.pid

[Install]
WantedBy=multi-user.target
```

設定ファイルをsystemdに反映させ、chmpx-slaveをサービスとして起動します。
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart chmpx-slave.service
```

次の内容を /etc/systemd/system/k2hr3-api.service に保存します。
```
[Unit]
Description=k2hr3-api
Requires=chmpx-slave.service
After=chmpx-slave.service

[Service]
Type=simple
WorkingDirectory=/home/k2hr3
Environment=HOME=/home/k2hr3
Environment=NODE_CONFIG_DIR=/home/k2hr3/etc/k2hr3-api
Environment=NODE_DEBUG=LOGLEVEL_ERR
Environment=NODE_ENV=production
ExecStart=/usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
Restart=on-failure
PIDFile=/var/run/k2hr3-api.pid

[Install]
WantedBy=multi-user.target
```

設定ファイルをsystemdに反映させ、k2hr3-apiをサービスとして起動します。
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-api.service
```

## Webサーバーの設定

この章は、Webサーバの設定ファイルについて説明しています。

* Webサーバーは、[Node.js](https://nodejs.org/)で実装されています。
* 設定ファイルは、 /home/k2hr3/node_modules/k2hr3-app/config の下にインストールされます。
* default.json ファイルの設定項目の中から、変更したい項目のみを抜き出して、自分専用のファイル(local.jsonなど)に保存してお使いください。
* 自分専用のファイル名は、[configモジュールのルール](https://github.com/lorenwest/node-config/wiki/Configuration-Files#file-load-order) にしたがって作成してください。
* 命名ルールをよく理解できない場合は、local.json にしておけば問題ありません。
* default.jsonと自分専用のファイルを /home/k2hr3/etc/k2hr3-app の下にコピーしてください。

以下は、設定項目のサンプルとその説明です。
```
{
    "scheme": "http",                               // Webサーバープロトコル(http/https)
    "port": 3000,                                   // Webサーバーポート
    "multiproc": true,                              // 複数プロセス起動の有無
    "runuser": "nobody",                            // 起動ユーザ名
    "privatekey": "config/key.pem",                 // 秘密鍵ファイル名
    "cert": "config/cert.pem",                      // サーバ証明書ファイル名
    "ca": "/etc/pki/tls/certs/ca-bundle.crt",       // ルート認証局証明書ファイル名
    "validator": "userValidateCredential",          // ユーザトークン検査用JavaScriptモジュール名
    "lang": "en",                                   // 言語ロケール

    "logdir": "log",                                // ログディレクトリ名
    "accesslogname": "access.log",                  // 標準出力ファイル名
    "consolelogname": "error.log",                  // 標準エラー出力ファイル名
    "logrotateopt": {                               // ログローテーション関連設定
        "compress": "gzip",                         // ローテーション時のログ圧縮方式(gzipのみ)
        "interval": "6h",                           // ローテーション期間
        "initialRotation": true                     // ローテーション期間以降の初回起動時におけるローテーション実行の有無
    },


    "apischeme": "http",                            // APIサーバープロトコル(http/https)
    "apihost": "localhost",                         // APIサーバー名
    "apiport": 3001,                                // APIサーバーポート

    "appmenu": [                                    // メニューリスト
        {
            "name": "Document",                     // メニューの名前
            "url": "https://k2hr3app.antpick.ax/"   // メニューのURL
        }
    ],

    "userdata": "\
#include\n\
{{= %K2HR3_API_HOST_URI% }}/v1/userdata/{{= %K2HR3_USERDATA_INCLUDE_PATH% }}\n\
"                                                   // UserDataのURL
}
```

### 補足：サービスマネージャ(systemd)の設定

ここでは、[systemd](https://www.freedesktop.org/wiki/Software/systemd/)を使ってWebサーバーの各プロセスを制御する方法を説明しています。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) は、OS起動または終了時に、常駐プロセスの起動・停止を制御することができる、OS付属のサービスマネージャーです。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定は、必須ではありません。OS起動（または終了）時に、自動的にプロセスを起動（または停止）したい場合は、次のように設定しておくこともできます。

次の内容を /etc/systemd/system/k2hr3-app.service に保存します。
```
[Unit]
Description=k2hr3-app
After=network-online.target

[Service]
Type=simple
WorkingDirectory=/home/k2hr3
Environment=HOME=/home/k2hr3
Environment=NODE_CONFIG_DIR=/home/k2hr3/etc/k2hr3-app
Environment=NODE_DEBUG=LOGLEVEL_ERR
Environment=NODE_ENV=production
ExecStart=/usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
Restart=on-failure
PIDFile=/var/run/k2hr3-app.pid

[Install]
WantedBy=multi-user.target
```

設定ファイルをsystemdに反映させ、k2hr3-appをサービスとして起動します。
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-app.service
```


## K2HR3 OpenStack Notification Listener

この章は、K2HR3 OpenStack Notification Listenerの設定ファイルについて説明しています。

* K2HR3 OpenStack Notification Listenerは、[OpenStack](https://www.openstack.org/)とK2HR3システムとデータを同期させる常駐プロセスです。
* [OpenStack](https://www.openstack.org/)の各サービスからの通知メッセージを、メッセージングバックエンド経由で受け取ります。
* K2HR3 OpenStack Notification Listenerの動作確認は、[OpenStack Rocky](https://docs.openstack.org/rocky/) を使って行なっています。
* K2HR3 OpenStack Notification Listenerの動作確認は、[RabbitMQ](http://www.rabbitmq.com/)（RabbitMQ 3.6.5（rabbitmq_amqp1_0拡張は不使用））を使って行なっています。

K2HR3 OpenStack Notification Listenerの設定ファイルは、 /usr/local/etc/k2hr3/k2hr3-osnl.conf にインストールされます。

以下は、設定項目のサンプルとその説明です。

```
[DEFAULT]
log_file = sys.stderr                                 # ログファイル名
debug_level = error                                   # ログレベル
libs_debug_level = warning                            # 依存モジュールのログのログレベル

[oslo_messaging_notifications]
event_type = ^port\.delete\.end$                      # 通知メッセージのイベントのタイプ
publisher_id = ^network.*$                            # 通知メッセージの発行者
transport_url = rabbit://guest:guest@127.0.0.1:5672/  # メッセージキューブローカーサーバのURL
topic = notifications                                 # 購読トピック名
exchange = neutron                                    # OpenStackサービス名(通知メッセージをキューに送信)
executor = threading                                  # 受け取った通知メッセージの処理方式(threading, blocking, eventlet)
pool = k2hr3_osnl                                     # キューの名前
allow_requeue = True                                  # キューの書き戻し許容の可否

[k2hr3]
api_url = https://localhost/v1/role                   # APIサーバーのURL
timeout_seconds = 30                                  # APIサーバーのリクエストタイムアウト時間(秒)
retries = 3                                           # リクエストエラー時の再送回数
retry_interval_seconds = 60                           # リクエストエラー時のリクエスト再送待機時間(秒)
allow_self_signed_cert = False                        # 自己署名のサーバ証明書許容の可否
requeue_on_error = False                              # リクエストエラー時のキューの書き戻しの可否
```

### 補足：通知メッセージのフォーマットと設定

ここでは、K2HR3 OpenStack Notification Listenerが、[OpenStack](https://www.openstack.org/)の各サービスから受け取る通知メッセージのフォーマットについて説明しています。

k2hr3-osnlが解析可能な通知メッセージのフォーマットは主に2種類あり、フォーマットに合わせて設定します。

* OpenStack neutronからの通知メッセージを取得する場合
  * メッセージを受け取るメッセージキューの指定
	* topicに **topic = notifications** を設定してください（デフォルトの設定です）
	* exchangeに **exchange = neutron** を設定してください（デフォルトの設定です）
  * メッセージのフィルタリングの指定
	* キューには様々なメッセージが届きます。インスタンスが削除されたメッセージだけにマッチするように、次のように指定します。
		* event_type
			* 通知メッセージの内容です。**event_type = ^port\.delete\.end$** を指定してください（デフォルトの設定です）
		* publisher_id
			* 通知メッセージを発行者です。**publisher_id = ^network.*$** を指定してください（デフォルトの設定です）
* OpenStack novaからの通知メッセージを解析する場合
  * デフォルトの設定が使えないときは、novaからの通知メッセージを解析するように設定することもできます。
  * メッセージを受け取るメッセージキューの指定
	* topicに **topic = versioned_notifications** を設定してください
	* exchangeに **exchange = nova** を設定してください
  * メッセージのフィルタリングの指定
	* キューには様々なメッセージが届きます。インスタンスが削除されたメッセージだけにマッチするように、次のように指定します。
		* event_type
			* 通知メッセージの内容です。**event_type = ^instance\.delete\.end$** を指定してください（デフォルトの設定です）
		* publisher_id
			* 通知メッセージを発行者です。**publisher_id = ^nova-compute:.*$** を指定してください（デフォルトの設定です）

次の設定は、neutronからの通知メッセージを解析する設定例です。

```
...
[oslo_messaging_notifications]
event_type = ^port\.delete\.end$
publisher_id = ^network.*$
transport_url = rabbit://user:pass@127.0.0.1:5672/
topic = notifications
exchange = neutron
...
```

上記設定は、neutronの通知メッセージドライバが、 **messagingv2** を使っていることを想定しています。

/etc/neutron/neutron.confが次のように設定されていることを確認してください。

```
[oslo_messaging_notifications]
#
# From oslo.messaging
#
# The Drivers(s) to handle sending notifications. Possible values are
# messaging, messagingv2, routing, log, test, noop (multi valued)
# Deprecated group/name - [DEFAULT]/notification_driver
driver = messagingv2
```

neutronからの通知メッセージを解析できない場合は、novaからの通知メッセージを解析するように設定することもできます。以下設定例です。

```
[oslo_messaging_notifications]
event_type = ^instance\.delete\.end$
publisher_id = ^nova-compute:.*$
transport_url = rabbit://user:pass@127.0.0.1:5672/
topic = versioned_notifications
exchange = nova
```

novaが送信する通知メッセージのtopicとevent_typeは、[こちら](https://docs.openstack.org/nova/latest/reference/notifications.html#existing-versioned-notifications)をみてください。

### 補足：サービスマネージャ(systemd)の設定

ここでは、[systemd](https://www.freedesktop.org/wiki/Software/systemd/)を使ってK2HR3 OpenStack Notification Listenerのプロセスを制御する方法を説明しています。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) は、OS起動または終了時に、常駐プロセスの起動・停止を制御することができる、OS付属のサービスマネージャーです。

[systemd](https://www.freedesktop.org/wiki/Software/systemd/)の設定は、必須ではありません。OS起動（または終了）時に、自動的にプロセスを起動（または停止）したい場合は、次のように設定しておくこともできます。

次の内容を /etc/systemd/system/k2hr3-osnl.service に保存します。
```
[Unit]
Description=K2HR3 OpenStack Notification Listener
After=network-online.target

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStart=/opt/rh/rh-python36/root/usr/bin/k2hr3-osnl -c /usr/local/etc/k2hr3/k2hr3-osnl.conf
Restart=on-failure
PIDFile=/var/run/k2hr3-osnl.pid

[Install]
WantedBy=multi-user.target
```

設定ファイルをsystemdに反映させ、k2hr3-osnlをサービスとして起動します。
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-osnl.service
```
