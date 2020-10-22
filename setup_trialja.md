---
layout: contents
language: ja
title: Build a trial environment
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_trial.html
lang_opp_word: To English
prev_url: 
prev_string: 
top_url: setupja.html
top_string: Setup
next_url: 
next_string: 
---

# 試用環境
K2HR3システムを簡単に試用するための環境の構築について説明します。  
以下の手順により、K2HR3システムの基幹を構成するプロセスを一つのホスト（もしくは`Virtual Machine`）で起動し、試用環境を構築することができます。  

## 実行環境
K2HR3システムが連携するOpenStackシステムが必要となります。  
OpenStackシステムは、`devstack`で構築された環境でも十分であり、OpenStackの`Identity(Keystone)`が機能している環境であれば、問題ありません。  

次に、試用環境を構築するホストを準備してください。  
このホストは、`Bare Metal`でも`Virtual Machine`でも構いません。  

## ツール
試用環境を構築・停止するためにツールは、[K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils) の [devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack) を使います。  
このリポジトリ（ディレクトリ）を展開し、スクリプトを実行することで簡単に試用環境の構築・停止ができます。  

## 事前準備
試用環境を構築する前に、以下に示す情報を確認してください。  

### プロセス実行ユーザ
K2HR3システムのプロセスを実行するユーザを確認してください。  
例えば、`nobody`でプロセスを実行します。  

### ホスト
試用環境を構築するホスト（もしくは`Virtual Machine`）の`hostname`もしくは`IPアドレス`を確認してください。  

### ブラウザからアクセスされるホスト
試用環境にブラウザからアクセスするためには、このホストにブラウザからアクセスする必要があります。  
直接アクセスできない環境では、外部からアクセスするときに経由するホスト（プロキシ）などが必要となります。  
このようなホスト環境を使う場合には、外部からアクセスするときに経由するホスト（プロキシ）の`hostname`もしくは`IPアドレス`を確認してください。  

例えば、OpenStackなどのインスタンス（`Virtual Machine`）をホストとして使う場合、このインスタンスへ外部から直接アクセスするためにはセキュリティグループ（OpenStack）を設定したり、プロキシを準備する必要があります。  
試用環境を構築するツールでは、このような環境のためにプロキシとして[HAProxy](http://www.haproxy.org/)を起動することを想定した設定ファイル（[HAProxy](http://www.haproxy.org/)用のコンフィグレーションファイル）を出力することができます。  
直接アクセスできない環境であっても、この設定ファイルと[HAProxy](http://www.haproxy.org/)を使って環境を構築できます。  

### リージョン名
K2HR3システムが連携するOpenStackシステムのリージョン名を確認してください。  
`devstack`で構築したOpenStackの場合、主に`RegionOne`です。  

### Identity(Keystone) URL
K2HR3システムが連携するOpenStackシステムの`Identity(Keystone)`のURLを確認してください。  

### K2HR3 Web Application ポート番号
試用環境の`K2HR3 Web Application`のポート番号を決めておきます。  
もし、上述するようなプロキシを必要とする環境の場合、プロキシ上での`K2HR3 Web Application`のポート番号も決めておいてください。  

### K2HR3 REST API ポート番号
試用環境の`K2HR3 REST API`のポート番号を決めておきます。  
もし、上述するようなプロキシを必要とする環境の場合、プロキシ上での`K2HR3 REST API`のポート番号も決めておいてください。  
`K2HR3 REST API`には、ブラウザがロードした`K2HR3 Web Application`からアクセスしますので、`K2HR3 Web Application`と同様に外部からアクセスできる必要があります。  

## 構築
試用環境の構築について説明します。  
構築手順は、外部から直接アクセスできるホスト上に構築する場合と、プロキシなどを利用してアクセスが可能なホスト上に構築する場合があります。  
それぞれのケースに分けて説明します。  

### プロキシが不要なホストに構築
例として、事前準備で説明した以下のパラメータを使用します。

- プロセス実行ユーザ : `nobody`
- ホスト : `192.168.10.20`
- リージョン名 : `RegionOne`
- Identity(Keystone) URL : `http://192.168.10.10/identity`
- K2HR3 Web Application ポート番号 : `80`
- K2HR3 REST API ポート番号 : `8080`

プロキシを使用しないので、上記以外のパラメータは不要です。

まず、[K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils) リポジトリを展開します。
```
$ git clone https://github.com/yahoojapan/k2hr3_utils.git
```
次に、[devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack) ディレクトリに移動し、以下のコマンドを実行します。
```
$ cd k2hr3_utils/devpack
$ bin/devpack.sh -ni -nc --run_user nobody --openstack_region RegionOne  --keystone_url http://192.168.10.10/identity --app_host localhost --app_port 80 --api_host localhost --api_port 8080
```
`devpack.sh`スクリプトの実行が成功すれば、試用環境の構築は完了しています。  

動作を確認するには、以下のURLにブラウザからアクセスしてください。
```
http://192.168.10.20:80/
```
_試用環境では、`HTTPS`をサポートしていません。_  

### プロキシが必要なホストに構築
例として、事前準備で説明した以下のパラメータを使用します。

- プロセス実行ユーザ : `nobody`
- ホスト : `192.168.10.20`
- ブラウザからアクセスされるホスト : `172.16.16.16`
- リージョン名 : `RegionOne`
- Identity(Keystone) URL : `http://192.168.10.10/identity`
- K2HR3 Web Application ポート番号（ホスト） : `80`
- K2HR3 Web Application ポート番号（プロキシ） : `28080`
- K2HR3 REST API ポート番号（ホスト） : `8080`
- K2HR3 REST API ポート番号（プロキシ） : `18080`

まず、[K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils) リポジトリを展開します。
```
$ git clone https://github.com/yahoojapan/k2hr3_utils.git
```
次に、[devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack) ディレクトリに移動し、以下のコマンドを実行します。
```
$ cd k2hr3_utils/devpack
$ bin/devpack.sh -ni -nc --run_user nobody --openstack_region RegionOne --keystone_url http://192.168.10.10/identity --app_host 192.168.10.20 --app_port 80 --app_host_external 172.16.16.16 --app_port_external 28080 --api_host 192.168.10.20 --api_port 8080 --api_host_external 172.16.16.16 --api_port_external 18080
```
`devpack.sh`スクリプトの実行が成功すれば、試用環境の構築は完了しています。  

`devpack.sh`スクリプトの実行完了後、[HAProxy](http://www.haproxy.org/)設定ファイル（`k2hr3_utils/devpack/conf/haproxy_example.cfg`）が作成されています。  
このファイルを使い、以下のように[HAProxy](http://www.haproxy.org/)を起動してください。
```
$ haproxy -f k2hr3_utils/devpack/conf/haproxy_example.cfg
```
[HAProxy](http://www.haproxy.org/)が起動したら、以下のURLにブラウザからアクセスし、動作確認してください。
```
http://172.16.16.16:28080/
```

## 停止
起動した試用環境のK2HR3システムを停止するには、以下のようにスクリプトを実行します。
```
$ cd k2hr3_utils/devpack
$ bin/stopdevpack.sh
```
もし、試用環境を起動したときに自動的に作成されたファイルなどを全て削除したい場合は、以下のように実行します。
```
$ cd k2hr3_utils/devpack
$ bin/stopdevpack.sh --clear
```
