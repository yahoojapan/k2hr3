---
layout: contents
language: ja
title: Installation step by step
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_manual.html
lang_opp_word: To English
prev_url: setup_trialja.html
prev_string: Build a trial environment
top_url: setupja.html
top_string: Setup
next_url: setup_integrateja.html
next_string: Integrated installation
---

# 手動セットアップ（個別設定）

このページでは、サブシステムごとにK2HR3システムを構築する設定方法を説明します。  

K2HR3 システムは4つのサブシステムで構成されています。  
インストールは、下位層のサブシステムから実行する必要があります。

- K2HDKCサーバー  
K2HDKCはデータストレージを提供します。  
このサブシステムは最下層に存在するため、最初のステップでインストールする必要があります。  
- REST APIサーバー  
K2HR3 REST APIは、Web ApplicationサーバーおよびK2HR3 OpenStack Notification Listenerからのリクエストを受け取ります。  
このサブシステムは、2番目のステップでインストールする必要があります。  
- K2HR3 OpenStack Notification Listener  
k2hr3-osnlは、OpenStack messaging バックエンドからの通知メッセージを監視します。  
k2hr3-osnlはREST APIサーバーにリクエストを送信します。  
OpenStackをインストールし、REST APIサーバーをインストールした後、このサブシステムをインストールする必要があります。  
- Web Application サーバー  
k2hr3-appはユーザーからのリクエストを受けます。  
このサブシステムは、最後のステップでインストールする必要があります。  

## データーサーバー（K2HDKC）

ここでは、データーサーバーの設定方法を説明します。

設定用プログラム（`setup_dkc.sh`）を起動すると、設定が完了します。

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh dkc/setup_dkc.sh
```

`setup_dkc.sh`のログは、**journalctl**で確認できます。以下、例です。

```bash
$ journalctl -t setup_dkc.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:13:04 ubuntu18 setup_dkc.sh[1590]: setup_dkc.sh 0.0.1
Feb 06 00:13:04 ubuntu18 setup_dkc.sh[1591]: 1. Initializes environments
Feb 06 00:13:05 ubuntu18 setup_dkc.sh[1596]: 2. Ensures that the k2hdkc data directory exists
Feb 06 00:13:05 ubuntu18 setup_dkc.sh[1629]: 3. Ensures that the k2hdkc configuration directory exists
Feb 06 00:13:05 ubuntu18 setup_dkc.sh[1634]: 4. Adds a new package repository
Feb 06 00:13:43 ubuntu18 setup_dkc.sh[2484]: 5. Installs OS dependent packages
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13650]: 6. Configures the default chmpx configuration
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13655]: 7. Installs the configured chmpx config file
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13659]: 8. Configures the chmpx's service manager default configuration
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13666]: 9. Installs the chmpx service manager configuration and enables it
Feb 06 00:14:40 ubuntu18 setup_dkc.sh[13722]: 10. Configures the k2hdkc's service manager default configuration
Feb 06 00:14:40 ubuntu18 setup_dkc.sh[13729]: 11. Installs the k2hdkc service manager configuration and enables it
Feb 06 00:14:41 ubuntu18 setup_dkc.sh[13800]: completed in 97 seconds
```

## REST APIサーバー

ここでは、REST APIサーバーの設定方法を説明します。

設定用プログラム（`setup_api.sh`）に次の情報を与えて起動すると、設定が完了します。

- OpenStackのIPアドレス

以下、例です。

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh api/setup_api.sh -i http://192.168.1.1/identity
```
_OpenStackのIPアドレスを `192.168.1.1`で指定した例です。_

`setup_api.sh`のログは、**journalctl**で確認できます。以下、例です。

```bash
$ journalctl -t setup_api.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:14:41 ubuntu18 setup_api.sh[13810]: setup_api.sh 0.0.1
Feb 06 00:14:41 ubuntu18 setup_api.sh[13811]: 1. Initializes environments
Feb 06 00:14:41 ubuntu18 setup_api.sh[13825]: 2. Ensures that the k2hr3_api data directory exists
Feb 06 00:14:41 ubuntu18 setup_api.sh[13836]: 3. Ensures that the k2hdkc configuration directory exists
Feb 06 00:14:41 ubuntu18 setup_api.sh[13839]: 4. Adds a new package repository
Feb 06 00:15:10 ubuntu18 setup_api.sh[15687]: 5. Installs OS dependent packages
Feb 06 00:15:30 ubuntu18 setup_api.sh[15995]: 6. Configures the default chmpx slave configuration
Feb 06 00:15:30 ubuntu18 setup_api.sh[15998]: 7. Installs the configured chmpx slave config file
Feb 06 00:15:30 ubuntu18 setup_api.sh[16002]: 8. Configures the chmpx slave's service manager default configuration
Feb 06 00:15:30 ubuntu18 setup_api.sh[16009]: 9. Installs the chmpx-slave service manager configuration and enables it
Feb 06 00:15:31 ubuntu18 setup_api.sh[16065]: 10. Installs devel packages to build the k2hdkc node module
Feb 06 00:16:18 ubuntu18 setup_api.sh[19987]: 11. Installs npm packages
Feb 06 00:16:54 ubuntu18 setup_api.sh[20405]: 14. Configures the k2hr3-api's service manager default configuration
Feb 06 00:16:54 ubuntu18 setup_api.sh[20413]: 15. Installs the k2hr3-api service manager configuration and enables it
Feb 06 00:16:55 ubuntu18 setup_api.sh[20483]: completed in 134 seconds
```

## K2HR3 OpenStack Notification Listener

ここでは、K2HR3 OpenStack Notification Listenerの設定方法を説明します。

設定用プログラム（`setup_osnl.sh`）に次の情報を与えて起動すると、設定が完了します。

- メッセージングバックエンドへログインするためのログインID
- メッセージングバックエンドへログインするためのパスワード
- メッセージングバックエンドへのIPアドレス

以下の値を設定した実行例を示します。
- メッセージングバックエンドへログインするためのログインID: stackrabbit
- メッセージングバックエンドへログインするためのパスワード: devstack
- メッセージングバックエンドへのIPアドレス: 192.168.1.1

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh osnl/setup_osnl.sh -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

`setup_osnl.sh`のログは、**journalctl**で確認できます。以下、例です。

```bash
$ journalctl -t setup_osnl.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22750]: setup_osnl.sh 0.0.1
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22754]: 1. Initializes environments
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22759]: 2. Adds a new package repository
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22760]: 3. Installs system packages
Feb 06 00:19:21 ubuntu18 setup_osnl.sh[26010]: 4. Installs the k2hr3-osnl pypi package
Feb 06 00:19:25 ubuntu18 setup_osnl.sh[26027]: 5. Configures the k2hr3-osnl.conf and Installs it
Feb 06 00:19:25 ubuntu18 setup_osnl.sh[26043]: 6. Installs a systemd configuration for k2hr3_osnl
Feb 06 00:19:25 ubuntu18 setup_osnl.sh[26048]: 7. Registers and enables k2hr3_osnl to systemd
Feb 06 00:19:26 ubuntu18 setup_osnl.sh[26112]: completed in 109 seconds
```

## Web Applicationサーバー

ここでは、Web Applicationサーバーの設定方法を説明します。

設定用プログラム（`setup_app.sh`）を起動すると、設定が完了します。

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh app/setup_app.sh
```

`setup_app.sh`のログは、**journalctl**で確認できます。以下、例です。

```bash
$ journalctl -t setup_app.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:16:55 ubuntu18 setup_app.sh[20505]: setup_app.sh 0.0.1
Feb 06 00:16:55 ubuntu18 setup_app.sh[20506]: 1. Initializes environments
Feb 06 00:16:55 ubuntu18 setup_app.sh[20511]: 2. Adds a new package repository
Feb 06 00:17:17 ubuntu18 setup_app.sh[22479]: 3. Installs OS dependent packages
Feb 06 00:17:18 ubuntu18 setup_app.sh[22485]: 4. Install the k2hr3-app npm package
Feb 06 00:17:36 ubuntu18 setup_app.sh[22665]: 7. Configures the k2hr3-app's service manager default configuration
Feb 06 00:17:36 ubuntu18 setup_app.sh[22673]: 8. Installs the k2hr3-app service manager configuration and enables it
Feb 06 00:17:37 ubuntu18 setup_app.sh[22737]: completed in 42 seconds
```

## 完了
以上の手順で、手動で各サブシステムごとに起動ができます。
