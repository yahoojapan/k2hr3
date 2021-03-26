---
layout: contents
language: ja
title: Command Line Interface
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli.html
lang_opp_word: To English
prev_url: apija.html
prev_string: REST API
top_url: usageja.html
top_string: Usage
next_url: usage_rbacja.html
next_string: RBAC Usage
---

# Command Line Interface (CLI)
K2HR3 Command Line Interface(CLI)は、K2HR3が提供する[REST API](apija.html)をコマンドラインから操作できるインターフェースを提供します。  
K2HR3システムのもつデータを操作する [K2HR3 Webアプリケーション](usage_appja.html) と同等の機能を **コマンドラインインターフェース** として提供します。  

## 概要
K2HR3 Command Line Interface(CLI) を使うには、パッケージでインストールするか、ソースコードを展開することで利用できます。  
K2HR3 Command Line Interface(CLI)は、[K2HR3 REST API](apija.html)を利用しますので、**REST APIサーバー**に接続可能なホスト上で動作することができます。  

### 使い方
K2HR3 Command Line Interface(CLI)は、ひとつのコマンド（`k2hr3`）として提供されます。  
使い方は、`--help(-h)`を渡してヘルプを表示できます。
```
$ k2hr3 --help
$ k2hr3 <sub command> --help
```

### インストール（パッケージ）
K2HR3 Command Line Interface(CLI)をパッケージとしてインストールする方法を説明します。  

K2HR3 Command Line Interface(CLI)は、[packagecloid.io](https://packagecloud.io/app/antpickax/stable/search?q=k2hr3-cli) でパッケージを頒布しています。  
K2HR3 Command Line Interface(CLI)は、**Bourne Shell**（`/bin/sh`）および`curl`が動作できる環境で利用できます。  
以下の手順でインストールできます。  

#### パッケージリポジトリの設定
インストール前に、[packagecloid.io](https://packagecloud.io/antpickax/stable) のリポジトリを設定してください。  
[ここ](https://packagecloud.io/antpickax/stable/install)を参考にして、リポジトリを登録します。  
```
# curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.deb.sh | sudo bash
 もしくは
# curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.rpm.sh | sudo bash
```
#### パッケージのインストール
以下のようにパッケージ管理ツールを使い、インストールします。
```
# apt-get install k2hr3-cli
 もしくは
# yum install k2hr3-cli
```

### ソースコード
パッケージが提供されていないOSや、パッケージを使わず利用する場合には、[github.comリポジトリ](https://github.com/yahoojapan/k2hr3_cli) から直接ソースコードをダウンロードして利用することができます。  
github.comおよびgitコマンドの使い方については、ドキュメントなどを参照してください。  

ソースコードを展開して、利用する場合には、以下の環境変数を設定する必要があります。
```
$ export K2HR3CLI_LIBEXEC_DIR <k2hr3_cli repository top dir>/src/libexec
```

K2HR3 Command Line Interface(CLI)のコマンド（`k2hr3`）は、`<k2hr3_cli repository top dir>/src/k2hr3`にありますので、このファイルを実行してください。  

## 詳細
K2HR3 Command Line Interface(CLI)の使い方を説明します。

### 共通
K2HR3 Command Line Interface(CLI)のコマンドの書式を以下に示します。  
```
$ k2hr3 --help(-h)
 もしくは
$ k2hr3 <sub command> <options...>
```
サブコマンド（**<sub command>**）は、各[K2HR3 REST API](apija.html)に対応しています。（後述）

#### ヘルプ表示
K2HR3 Command Line Interface(CLI)の使い方は、以下のようにヘルプで見ることができます。
```
$ k2hr3 --help(-h)
```
上記のように、サブコマンド（**<sub command>**）なしで、ヘルプを表示させるとK2HR3 Command Line Interface(CLI)の概要を表示します。  

各サブコマンドのヘルプを表示するには、以下のように実行します。  
```
$ k2hr3 <sub command> --help(-h)
```
各サブコマンド（**<sub command>**）の使い方が表示されます。  

#### オプション
K2HR3 Command Line Interface(CLI)には、いくつかのオプションがあります。  
各オプションの説明は、[こちら](cli_optionsja.html)を参照してください。  
サブコマンドに応じて、指定できるオプションは異なりますので、各サブコマンドの説明を参照してください。  

### サブコマンド
K2HR3 Command Line Interface(CLI)のサブコマンドの説明をします。

#### [config](cli_configja.html)
K2HR3 Command Line Interface(CLI)のコンフィグレーションに関連する操作を行うサブコマンドです。  
K2HR3 Command Line Interface(CLI)は、いくつかのオプションで指定する値をコンフィグレーションファイルに保持することができます。  
これにより、連続してコマンドを実行するときに、これらのオプションを指定せず、コンフィグレーションに保存した値を使うことができます。  

#### [version](cli_versionja.html)
[VERSION API](api_versionja.html)に対応したサブコマンドです。  
K2HR3 REST APIのバージョンを表示するサブコマンドです。  

#### [token](cli_tokenja.html)
[K2HR3 REST API](apija.html)を使うために必要となるトークンを操作するためのサブコマンドです。  
これは、[TOKEN API](api_tokenja.html)に対応したサブコマンドです。  

#### [list](cli_listja.html)
[LIST API](api_listja.html)に対応したサブコマンドです。  
K2HR3のロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）のパスリストを表示するサブコマンドです。  

#### [role](cli_roleja.html)
[ROLE API](api_roleja.html)に対応したサブコマンドです。  
K2HR3のロール（ROLE）を操作するサブコマンドです。  

#### [policy](cli_policyja.html)
[POLICY API](api_policyja.html)に対応したサブコマンドです。  
K2HR3のポリシー/ルール（POLICY）を操作するサブコマンドです。  

#### [resource](cli_resourceja.html)
[RESOURCE API](api_resourceja.html)に対応したサブコマンドです。  
K2HR3のリソース（RESOURCE）を操作するサブコマンドです。  

#### [service](cli_serviceja.html)
[SERVICE API](api_serviceja.html)に対応したサブコマンドです。  
K2HR3のサービス（SERVICE）を操作するサブコマンドです。  

#### [acr](cli_acrja.html)
[ACR(ACCESS CROSS ROLE) API](api_acrja.html)に対応したサブコマンドです。  
K2HR3の+サービス（+SERVICE）機能で利用するACR(ACCESS CROSS ROLE)を操作するサブコマンドです。  

#### [userdata](cli_userdataja.html)
[USERDATA API](api_userdataja.html)に対応したサブコマンドです。  
K2HR3のUSER DATA SCRIPTを操作するサブコマンドです。  

#### [extdata](cli_extdataja.html)
[EXTDATA API](api_extdataja.html)に対応したサブコマンドです。  
K2HR3のEXT(RA) DATA SCRIPTを操作するサブコマンドです。  
