---
layout: contents
language: ja
title: Tools
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: tools.html
lang_opp_word: To English
prev_url: environmentsja.html
prev_string: Environments/Settings
top_url: indexja.html
top_string: TOP
next_url: 
next_string: 
---

# ツール

このページでは、各種ツールについて説明しています。

## K2HR3提供のツール

この章では、K2HR3システムで提供しているツールを説明しています。

### Watcher

ここでは、**Watcher** の用途と使い方を説明しています。

**Watcher**は、K2HR3 OpenStack Notification Listenerが利用できない環境において、仮想コンピューティング（Virtual Machine）削除の監視、およびロール（ROLE）へのメンバーから対象のホスト（HOST）の自動削除を行うためのシステム（プログラム）です。
* OpenStackからインスタンスが削除されたとき、K2HR3のデータベースからそのインスタンスのIPアドレスを削除する必要があります。
* K2HR3からのIPアドレス削除は、K2HR3 OpenStack Notification Listener を使って実施することをおすすめします。
* K2HR3 OpenStack Notification Listener を利用できない場合は、**Watcher** を起動し、削除することができます。
* **Watcher** は、 APIサーバー（npmのk2hr3-apiパッケージ） に含まれています。

**Watcher** とK2HR3システム全体と **Watcher** の構成イメージを以下に示します。  
![K2HR3 Watcher overview](images/tool_watcher.png)

Watcherの使い方は次の通りです。

```
$ git clone https://github.com/yahoojapan/k2hr3_api.git && cd k2hr3_api
$ ./bin/run.sh -h
Usage:   run.sh [--production(default) | --development]
            [--stop]
            [--background(-bg) | --foreground(-fg)]
            [--debug(-d) | --debug-nobrk(-dnobrk)]
            [--debuglevel DBG/MSG/WARN/ERR/(custom debug level)]
            [--watcher [--oneshot]]

Option:  --production           : Set 'production' to NODE_ENV environment
                                  (This option is default and exclusive with
                                  the '--development' option)
         --development          : Set 'development' to NODE_ENV environment
                                  (exclusive with the '--production' option)
         --stop                 : Stop www or watcher nodejs process
         --debug(-d)            : Run with nodejs inspector option
         --debug-nobrk(-dnobrk) : Run with nodejs inspector option
                                  (no break at start)
         --debuglevel           : Specify the level of debug output.
                                  (DBG/MSG/WARN/ERR/custom debug level)
         --watcher              : Run IP watcher process as daemon
         --oneshot              : Run watcher process only once
```

* --watcher
  * 常駐プロセスとして起動し、IPアドレス削除処理を定常的に実行する。
  
* -os または --oneshot
  * IPアドレス削除処理を一回だけ実行する。


### devcluster

ここでは、**devcluster** の用途と使い方を説明します。

**devcluster**は、K2HR3の全サブシステムをlocalhostに構築します。主に開発＆テストのためのツールです。

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh cluster.sh -h
usage : cluster.sh [-d] [-f file] [-o file] [-p file] [-h] [-t url] [-v]
    -d        print debug messages
    -i file   k2hr3-api package file path(or URL)
    -o file   k2hr3-osnl package file path(or URL)
    -p file   k2hr3-app package file path(or URL)
    -h        display this message and exit
    -s url    OpenStack Identity Service Endpoint(Default: 'http://127.0.0.1/identity')
    -t url    TransportURL(Default: 'rabbit://guest:guest@127.0.0.1:5672/')
    -v        display version and exit
```

* -d
  * デバッグモードで起動します。
  
* -i
  * tgz形式のk2hr3-apiパッケージのファイルパスもしくは、URLを指定します。
  * このパラメータは、k2hr3-apiパッケージの開発者用途で使用します。
  * 通常k2hr3-apiパッケージは、npmレポジトリからインストールされるので指定は不要です。
  
* -d
  * デバッグモードを指定します。
  
* -o
  * tgz形式のk2hr3-osnlパッケージのファイルパスもしくは、URLを指定します。
  * このパラメータは、k2hr3-osnlパッケージの開発者用途で使用します。
  * 通常k2hr3-osnlパッケージは、PyPIレポジトリからインストールされるので指定は不要です。
  
* -p
  * tgz形式のk2hr3-appパッケージのファイルパスもしくは、URLを指定します。
  * このパラメータは、k2hr3-appパッケージの開発者用途で使用します。
  * 通常k2hr3-appパッケージは、npmレポジトリからインストールされるので指定は不要です。
  
* -h
  * ヘルプ文言を表示します。
  
* -s
  * OpenStack IdentityサービスのAPIエンドポイント(URL)を指定します。
  
* -t
  * MessageQueueサーバのURLを指定します。
  
* -v
  * バージョンを表示します。
  

## その他のツール

この章では、K2HR3のサブシステムに付属する管理ツールを紹介します。

### k2hdkclinetool

k2hdkclinetoolは、データーサーバー（K2HDKC）に格納されているデータへの参照、更新、削除など全ての操作を対話形式で実行するツールです。

詳しい使い方は、[K2HDKCのツール](https://k2hdkc.antpick.ax/k2hdkclinetoolja.html) をご覧ください。

### chmpxlinetool

chmpxlinetoolは、chmpxプロセスを制御する対話形式で実行できます。

詳しい使い方は、[CHMPXのツール](https://chmpx.antpick.ax/toolsja.html) をご覧ください。

### chmpxstatus

chmpxstatusは、CHMPXクラスタ内のホストの状態を表示するツールです。

詳しい使い方は、[CHMPXのツール](https://chmpx.antpick.ax/toolsja.html) をご覧ください。

### k2hlinetool

k2hlinetoolは、K2HASHデータベースへの参照、更新、削除など全ての操作を対話形式で実行できます。 

詳しい使い方は、[K2HASHのツール](https://k2hash.antpick.ax/toolsja.html) をご覧ください。

