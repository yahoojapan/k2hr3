---
layout: contents
language: ja
title: Setup
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup.html
lang_opp_word: To English
prev_url: usageja.html
prev_string: Usage
top_url: indexja.html
top_string: TOP
next_url: developerja.html
next_string: Developer
---

# セットアップ

このページは、K2HR3 システムのセットアップ方法を説明しています。

## 構築するシステムの構成

本セットアップ手順により構築されるシステムの構成例を以下に示します。

![K2HR3 Setup overview](images/setup_overview.png)

後段では、つぎの二つのセットアップの方法を説明しています。

* 自動セットアップ
  * K2HR3サブシステム全てを一括で設定する方法
* 手動セットアップ
  * K2HR3サブシステムごとに設定する方法

## 確認用自動セットアップ

この章では、K2HR3サブシステム全てを一括で設定する方法を説明しています。

### OpenStack 設定

ここでは、二つのOpenStackの構築及び設定方法を紹介します。

* [OpenStackドキュメントページ](https://docs.openstack.org) の 'Installation Guides' 
  * OpenStackの各サービスごとに構築していく場合は、こちらをご覧ください。
* [DevStack](https://docs.openstack.org/devstack/latest/)
  * 最新版のOpenStackをテストと開発のために構築するため場合は、こちらをおすすめします。

### kubernetes 設定

ここでは、kubernetesの構築に関して、参考サイトを紹介します。

* **minikube**を使って簡単なテスト環境を構築する場合は[こちら](https://kubernetes.io/ja/docs/tutorials/hello-minikube/)を参照してください。  
minikubeを利用する場合には、適切にproxyの設定を行ってください。
* **kubeadm**を使って構築する場合は[こちら](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#)を参照してください。
* **Rancher**を使って構築する場合は[こちら](https://rancher.com/)を参照してください。

### K2HR3 設定

ここでは、K2HR3のサブシステム全てを一括で設定する方法を説明しています。  
_以下のドキュメントは、OpenStackと連携する環境を構築するための内容です。kubernetesのみと連携する場合には、特に以下のOpenStackのための作業は必要ありません。_

設定用プログラム（cluster.sh）に次の情報を与えて起動すると、設定が完了します。

* OpenStackのIPアドレス
* メッセージングバックエンドへログインするためのログインID
* メッセージングバックエンドへログインするためのパスワード
* メッセージングバックエンドへのIPアドレス

例として、次の情報を与えて、K2HR3を設定します。

* OpenStackのIPアドレス: 192.168.1.1
* メッセージングバックエンドへログインするためのログインID: stackrabbit
* メッセージングバックエンドへログインするためのパスワード: devstack
* メッセージングバックエンドへのIPアドレス: 192.168.1.1

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh cluster.sh \
 -s http://192.168.1.1/identity \
 -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

cluster.shのログは、**journalctl**で確認できます。以下、例です。

```bash
$ journalctl -t cluster.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 03:17:01 UTC. --
Feb 06 00:13:04 ubuntu18 cluster.sh[1580]: cluster.sh 0.0.1
Feb 06 00:13:04 ubuntu18 cluster.sh[1582]: sh dkc/setup_dkc.sh
Feb 06 00:14:41 ubuntu18 cluster.sh[13802]: sh api/setup_api.sh -i http://192.168.1.1/identity
Feb 06 00:16:55 ubuntu18 cluster.sh[20490]: sh app/setup_app.sh
Feb 06 00:17:37 ubuntu18 cluster.sh[22739]: sh osnl/setup_osnl.sh -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
Feb 06 00:19:26 ubuntu18 cluster.sh[26121]: completed in 382 seconds
```

### 動作確認

ここでは、動作確認の方法を説明しています。

次の6つのプロセスが起動していることを確認してください。

* chmpx(server)  
  * メッセージプロキシサーバ
* chmpx(slave) 
  * chmpx(server)にリクエストを送信するプロセス
* k2hdkc 
  * 分散KVSクラスタ
* node(k2hr3-api) 
  * k2hr3 APIサーバー
* node(k2hr3-app) 
  * 管理コンソール表示用Webサーバープロセス
* python3(k2hr3-osnl) 
  * メッセージキュー購読プロセス

以下、例です。

```bash
$ ps -U k2hr3 -o cmd
CMD
/usr/bin/chmpx -conf /etc/k2hdkc/slave.ini -d err
/usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
/usr/bin/chmpx -conf /etc/k2hdkc/server.ini -d err
/usr/bin/k2hdkc -conf /etc/k2hdkc/server.ini -d err
/usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
/usr/bin/python3 /usr/local/bin/k2hr3-osnl -c /usr/local/etc/k2hr3/k2hr3-osnl.conf
```

プロセスの稼働状態は、**systemctl**で確認できます。以下、例です。

chmpx(server)プロセスの状態

```bash
$ systemctl status chmpx.service
● chmpx.service - chmpx
   Loaded: loaded (/etc/systemd/system/chmpx.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:14:41 UTC; 1 day 2h ago
 Main PID: 13790 (chmpx)
    Tasks: 20 (limit: 1152)
   CGroup: /system.slice/chmpx.service
           └─13790 /usr/bin/chmpx -conf /etc/k2hdkc/server.ini -d err

Feb 06 00:14:41 ubuntu18 systemd[1]: Started chmpx.
```

chmpx(slave)プロセスの状態

```bash
$ systemctl status chmpx-slave.service
● chmpx-slave.service - chmpx
   Loaded: loaded (/etc/systemd/system/chmpx-slave.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 03:40:00 UTC; 23h ago
 Main PID: 11210 (chmpx)
    Tasks: 36 (limit: 1152)
   CGroup: /system.slice/chmpx-slave.service
           └─11210 /usr/bin/chmpx -conf /etc/k2hdkc/slave.ini -d err

Feb 06 03:40:00 ubuntu18 systemd[1]: Starting chmpx...
Feb 06 03:40:00 ubuntu18 sysctl[11206]: fs.mqueue.msg_max = 1024
Feb 06 03:40:00 ubuntu18 systemd[1]: Started chmpx.
```

k2hdkcプロセスの状態

```bash
$ systemctl status k2hdkc.service
● k2hdkc.service - k2hdkc
   Loaded: loaded (/etc/systemd/system/k2hdkc.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:14:41 UTC; 1 day 2h ago
 Main PID: 13796 (k2hdkc)
    Tasks: 3 (limit: 1152)
   CGroup: /system.slice/k2hdkc.service
           └─13796 /usr/bin/k2hdkc -conf /etc/k2hdkc/server.ini -d err

Feb 06 00:14:41 ubuntu18 systemd[1]: Starting k2hdkc...
Feb 06 00:14:41 ubuntu18 systemd[1]: Started k2hdkc.
```

node(k2hr3-api)プロセスの状態

```bash
$ systemctl status k2hr3-api.service
● k2hr3-api.service - k2hr3-api
   Loaded: loaded (/etc/systemd/system/k2hr3-api.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 04:01:41 UTC; 23h ago
 Main PID: 11428 (node)
    Tasks: 23 (limit: 1152)
   CGroup: /system.slice/k2hr3-api.service
           ├─11428 /usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
           └─11452 /usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www

Feb 06 04:01:41 ubuntu18 systemd[1]: Started k2hr3-api.
```

node(k2hr3-app)プロセスの状態

```bash
$ systemctl status k2hr3-app.service
● k2hr3-app.service - k2hr3-app
   Loaded: loaded (/etc/systemd/system/k2hr3-app.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:17:37 UTC; 1 day 2h ago
 Main PID: 22733 (node)
    Tasks: 22 (limit: 1152)
   CGroup: /system.slice/k2hr3-app.service
           ├─22733 /usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
           └─22783 /usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www

Feb 06 00:17:37 ubuntu18 systemd[1]: Started k2hr3-app.
```

python(k2hr3-osnl)プロセスの状態

```
$ systemctl status k2hr3-osnl.service
● k2hr3-osnl.service - K2HR3 OpenStack Notification Listener
   Loaded: loaded (/etc/systemd/system/k2hr3-osnl.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:19:26 UTC; 1 day 2h ago
 Main PID: 26108 (k2hr3-osnl)
    Tasks: 14 (limit: 1152)
   CGroup: /system.slice/k2hr3-osnl.service
           └─26108 /usr/bin/python3 /usr/local/bin/k2hr3-osnl -c /usr/local/etc/k2hr3/k2hr3-osnl.conf

Feb 06 00:19:26 ubuntu18 systemd[1]: Started K2HR3 OpenStack Notification Listener.
```

## 個別設定

この章では、K2HR3サブシステムごとの設定方法を説明しています。

### データーサーバー（K2HDKC）

ここでは、データーサーバーの設定方法を説明しています。

設定用プログラム（setup_dkc.sh）を起動すると、設定が完了します。

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh dkc/setup_dkc.sh
```

setup_dkc.shのログは、**journalctl**で確認できます。以下、例です。

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

### APIサーバー

ここでは、APIサーバーの設定方法を説明しています。

設定用プログラム（setup_api.sh）に次の情報を与えて起動すると、設定が完了します。

* OpenStackのIPアドレス

以下、例です。

* OpenStackのIPアドレス: 192.168.1.1

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh api/setup_api.sh -i http://192.168.1.1/identity
```

setup_api.shのログは、**journalctl**で確認できます。以下、例です。

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

### K2HR3 OpenStack Notification Listener

ここでは、K2HR3 OpenStack Notification Listenerの設定方法を説明しています。

設定用プログラム（setup_osnl.sh）に次の情報を与えて起動すると、設定が完了します。

* メッセージングバックエンドへログインするためのログインID
* メッセージングバックエンドへログインするためのパスワード
* メッセージングバックエンドへのIPアドレス

以下、例です。

* メッセージングバックエンドへログインするためのログインID: stackrabbit
* メッセージングバックエンドへログインするためのパスワード: devstack
* メッセージングバックエンドへのIPアドレス: 192.168.1.1

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh osnl/setup_osnl.sh -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

setup_osnl.shのログは、**journalctl**で確認できます。以下、例です。

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

### Webサーバー

ここでは、Webサーバーの設定方法を説明しています。

設定用プログラム（setup_app.sh）を起動すると、設定が完了します。

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh app/setup_app.sh
```

setup_app.shのログは、**journalctl**で確認できます。以下、例です。

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
