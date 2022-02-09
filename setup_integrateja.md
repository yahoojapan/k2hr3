---
layout: contents
language: ja
title: Integrated installation
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_integrate.html
lang_opp_word: To English
prev_url: setup_manualja.html
prev_string: Installation step by step
top_url: setupja.html
top_string: Setup
next_url: setup_helm_chartja.html
next_string: Setup by Helm
---

# 統合セットアップ

このページでは、OpenStackの環境に K2HR3サブシステム全てを一括で設定する方法を説明します。

## IaaS環境

このドキュメントで説明するK2HR3システムは、[OpenStack](https://www.openstack.org/)および[kubernetes](https://kubernetes.io/ja/)の環境へK2HR3システムのセットアップができます。  
以下に各IaaSの構築に関するドキュメントを紹介します。  

### OpenStack

二つのOpenStackの構築及び設定方法を紹介します。

- [OpenStackドキュメントページ](https://docs.openstack.org) の `Installation Guides` 
  - OpenStackの各サービスごとに構築していく場合は、こちらをご覧ください。
- [DevStack](https://docs.openstack.org/devstack/latest/)
  - 最新版のOpenStackをテストと開発のために構築するため場合は、こちらをおすすめします。

### kubernetes 設定

kubernetesの構築に関して、参考サイトを紹介します。

- **minikube**を使って簡単なテスト環境（`minikube`）を構築する場合は[こちら](https://kubernetes.io/ja/docs/tutorials/hello-minikube/)を参照してください。  
`minikube`を利用する場合には、適切にproxyの設定を行ってください。
- **kubeadm**を使って構築する場合は[こちら](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#)を参照してください。
- **Rancher**を使って構築する場合は[こちら](https://rancher.com/)を参照してください。

## システム要件

K2HR3 システムには、以下のソフトウエアおよび環境で動作確認をしています。

- Linux
  - Debian buster and Stretch
  - Fedora 32, 31 and 30
  - CentOS 7 and 8
  - Ubuntu 16.04, 18.04, and 20.04
- OpenStack
  - Ussuri
- Kubernetes
- Node.js
  - Node.js 10.x, 12.x and 14.x
- Python
  - Python 3.6 and 3.8 

## K2HR3 システム 一括構築

ここでは、K2HR3のサブシステム全てを一括で設定する方法を説明します。  
_以下の例は、OpenStackと連携する環境を構築するための内容です。kubernetesと連携する場合には、以下のOpenStackに関連した項目は必要ありません。_

設定用プログラム（`cluster.sh`）に次の情報を与えて起動すると、設定が完了します。

* OpenStackコントローラのIPアドレス
- メッセージングバックエンドへログインするためのログインID
- メッセージングバックエンドへログインするためのパスワード
- メッセージングバックエンドへのIPアドレス

例として、次の情報を与えて、K2HR3システムを構築します。

- OpenStackコントローラのIPアドレス: 192.168.1.1
- メッセージングバックエンドへログインするためのログインID: stackrabbit
- メッセージングバックエンドへログインするためのパスワード: devstack
- メッセージングバックエンドへのIPアドレス: 192.168.1.1

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh cluster.sh \
 -s http://192.168.1.1/identity \
 -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

`cluster.sh`のログは、**journalctl**で確認できます。以下、例です。

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

## 動作確認

ここでは、上記で構築したK2HR3システムの動作確認方法を説明します。

次の6つのプロセスが起動していることを確認してください。

- chmpx(server)  
  - AntPickax メッセージングサーバープロセス
- chmpx(slave) 
  - chmpx(server)にリクエストを送信するスレーブプロセス
- k2hdkc 
  - 分散KVSクラスタ
- node(k2hr3-api) 
  - k2hr3 REST APIサーバープロセス
- node(k2hr3-app) 
  - 管理コンソール表示用Web Applicationサーバープロセス
- python3(k2hr3-osnl) 
  * OpenStack メッセージキュー購読プロセス

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

### chmpx(server)プロセスの状態

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

### chmpx(slave)プロセスの状態

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

### k2hdkcプロセスの状態

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

### node(k2hr3-api)プロセスの状態

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

### node(k2hr3-app)プロセスの状態

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

### python(k2hr3-osnl)プロセスの状態

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

## 完了
以上の手順で、K2HR3 システムの一括構築ができます。
