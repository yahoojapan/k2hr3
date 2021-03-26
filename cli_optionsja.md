---
layout: contents
language: ja
title: CLI options
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_options.html
lang_opp_word: To English
prev_url: 
prev_string: 
top_url: clija.html
top_string: Command Line Interface
next_url: cli_configja.html
next_string: CLI config
---

# Options for Command Line Interface(CLI)
K2HR3 Command Line Interface(CLI) のオプションについて説明します。  
サブコマンドに応じて、これらのオプションを使用します。  
どのオプションが指定できるかは、各サブコマンド の説明を参照してください。  

## 共通オプション
以下のオプションは、サブコマンドに共通のオプションです。

### -\-help(-h)
ヘルプを表示します。  
サブコマンド の指定がない場合には、オプションの説明、各サブコマンドの説明を表示します。  
サブコマンド を伴う場合には、指定したサブコマンドの説明が表示されます。  

### -\-version(-v)
K2HR3 Command Line Interface(CLI)のバージョンを表示します。

### -\-config(-c) [file path]
K2HR3 Command Line Interface(CLI) 起動時にロードするコンフィグレーションファイルを指定するオプションです。  
コンフィグレーションファイルに記述されたキーワードについては、[CLI config](cli_configja.html)で確認、変更できます。  
このオプションが指定されていない場合、以下の順序でコンフィグレーションファイルが検出され、ロードされます。  
- ${HOME}/.antpickax/k2hr3.config
- /etc/antpickax/k2hr3.config

### -\-interactive(-i)
このオプションが指定された場合、いくつかのサブコマンド実行に必要とされるオプションがない場合、対話形式で確認し、動的に入力を促します。  
また、このオプションは`--nointeractive(-ni)`と一緒に指定することはできません。  

### -\-nointeractive(-ni)
このオプションを指定した場合、サブコマンドの必須オプションが見つかるとエラーを発生させます。  
これが、K2HR3 Command Line Interface(CLI)のデフォルトの動作です。  
このオプションは `--interactive(-i)` と一緒に指定することはできません。  

### -\-messagelevel(-m) [level]
このオプションは、メッセージの出力レベルを指定します。  
オプションのパラメータには、以下の値を指定できます。  
- silent, slt, 0  
メッセージを何も出力しません。
- error, err, 1  
エラーレベルのメッセージを出力します。
- warning, warn, wan, 2  
エラー、ワーニングレベルのメッセージを出力します。
- information, info, inf, 3  
エラー、ワーニング、インフォメーションレベルのメッセージを出力します。
- debug, dbg, 4  
エラー、ワーニング、インフォメーション、デバッグレベルのメッセージを出力します。

### -\-curldebug(-cd)
curlコマンドを実行するときのverboseオプションを指定します。  
このオプションを指定すると、内部で実行されたcurlコマンドの詳細情報が標準エラーで出力されます。  

### -\-curlbody(-cb)
内部で実行されたcurlコマンドの応答ボディデータを表示します。  
このオプションを指定する場合は、`-curldebug(-cd)` も指定することをお勧めします。  

### -\-nodate(-nd)
メッセージ出力に日付と時刻を表示しないように指示します。  
デフォルトでは、日付と時刻が表示されます。  

### -\-nocolor(-nc)
メッセージ出力に色を付けません。  
デフォルトでは、色付きです。  

### -\-json(-j)
コマンド結果のjson出力を、整形し、複数行のわかりやすい方法で表示します。  

### -\-apiuri(-a)  [k2hr3 rest api uri]
K2HR3 REST APIへのURIを指定します。（例： https://127.0.0.1:3000）  

## 認証系オプション
ほとんどのサブコマンドは、K2HR3 REST APIサーバと通信し、その際トークンが必要となります。  
これらのオプションは、この認証に関連するオプションです。  
トークンが必要なケースにおいて、トークンがコンフィグレーションファイルに保管されていない場合、これらのオプションを指定する必要があります。  

### -\-user(-u) [user name]
クレデンシャル情報を使い、K2HR3のトークンを取得するときに必要となるK2HR3ユーザー名を指定します。  

### -\-passphrase(-p) [passphrase]
クレデンシャル情報を使い、K2HR3のトークンを取得するときに必要となるK2HR3ユーザーのパスフレーズを指定します。  
このオプションを使用した場合、コマンド履歴にパスフレーズが残ることがあります。
このオプションを使用せず、`--interactive(-i)`を指定し、対話的にパスフレーズを入力することを推奨します。

### -\-tenant(-t) [tenant name]
K2HR3のScoped トークンを取得するときに必要となるK2HR3テナント名（プロジェクト名）を指定します。  

### -\-unscopedtoken(-utoken) [token]
K2HR3のUnscoped トークンを直接を指定します。  
K2HR3のScoped トークンを取得するときに、クレデンシャル情報から作成するか、このオプションで指定したUnscoped トークンから作成できます。

### -\-scopedtoken(-token) [token]
K2HR3のScoped トークンを直接を指定します。  

### -\-openstacktoken(-optoken) [token]
K2HR3のUnscopedおよびScopedトークンを取得する方法の一つとして、OpenStackのトークンを使うケースにおいて、OpenStackシステムによって発行されたToken（UnscopedまたはScoped）を指定します。  

### -\-saveconfig(-s)
このオプションは、K2HR3のトークンを生成する処理を行うコマンドで指定できます。  
このオプションが指定された場合、そのトークン（ScopedもしくはUnscoped）の生成に利用された要素（ユーザ名、テナント名、K2HR3 REST APIのURI、Unscopedトークン、OpenStack トークン等）がコンフィグレーションファイルに保存されます。  
保存される要素については、[CLI config](cli_config.html)コマンドを使って確認できます。  

### -\-savepassphrase(-sp)
このオプションは、K2HR3のトークンを生成する処理を行うコマンドで指定できます。  
K2HR3 トークン（ScopedもしくはUnscoped）の生成のためにパスフレーズが指定された場合、パスフレーズをコンフィグレーションファイルに保存されます。  
ただし、コンフィグレーションファイルへパスフレーズの保管は、可能な限り行うべきではありません。  

## その他のオプション
以下のオプションは、サブコマンドによって指定可能なオプションです。  
指定できるか否かは、各サブコマンドの説明を確認してください。  

### -\-expand
このオプションを指定すると、対象のAPIに対して`expand=true`のパラメータを付与します。  
それにより、展開されたレスポンスデータを受け取ることになります。  
レスポンスデータの内容については、各サブコマンドの説明を確認してください。  

### -\-policies [policies]
ポリシー（POLICY）のYRNパスを指定します。  
複数のポリシー（POLICY）を指定する場合は、JSON形式の配列としてパラメータを渡します。  

### -\-alias [alias]
エリアス（ALIAS）のYRNパスを指定します。  

### -\-host [hostname or IP address]
ホスト名（またはIPアドレス）を指定します。  

### -\-port [port number]
ポート番号を指定します。  

### -\-cuk [cuk]
CUKを指定します。  

### -\-extra [data]
Extraデータを指定します。  

### -\-tag [tag]
Tagを指定します。  

### -\-expire [value]
有効期限（秒）を指定します。  

### -\-type [type]
リソース（RESOURCE）のリソースタイプ（`string`、`object`、`null`または`undefined`）を指定します。

### -\-data [value]
リソース（RESOURCE）のデータを指定します。  
リソースタイプが`string`の場合、文字列リテラルを指定します。  
リソースタイプが`object`の場合、データはJSONオブジェクトを指定します。  

### -\-datafile [file path]
リソースタイプが、`string`の場合に、データをファイルで指定できます。  
データに改行などのエスケープされていない文字が含まれている場合は、ファイルで指定できます。  

### -\-keys [data]
リソース（RESOURCE）の`keys`の要素であるキーバリューを指定します。  
JSONオブジェクトとして複数のキーバリューを指定できます。  

### -\-service [service name]
サービス（SERVICE）名を指定します。  

### -\-keynames [keynames]
リソース（RESOURCE）の`keys`のキー名を指定します。  

### -\-aliases [aliases]
エリアス（ALIAS）のYRNパスを指定します。
複数のエリアス（ALIAS）を指定する場合は、JSON形式の配列としてパラメータを渡します。  

### -\-effect [allow or deny]
ポリシー（POLICY）の効果（EFFECT）を指定します。  
`allow`もしくは`deny`を指定します。  

### -\-action [type]
ポリシー（POLICY）のアクション（ACTION）を指定します。  
`yrn:yahoo::::action:read`と`yrn:yahoo::::action:write`のいずれか、もしくは両方を指定します。  
複数指定する場合は、JSONの配列として渡します。  

### -\-clear_tenant
サービス（SERVICE）のメンバー（MEMBER）から既存のテナントを削除する場合に指定します。  

### -\-verify [url or string]
`service` sub commandで、URLを指定した動的リソース、または文字列リテラルまたはブールリテラルを指定します。  

### -\-cip [IP address]
サービスメンバーが所有するIPアドレスと、サービス所有者のもう一方の端のIPアドレス（ピアIP）を指定します。  

### -\-cport [port number]
IPアドレスとこのポート番号でK2HR3 のロール（ROLE）が確定されます。そのためのポート番号を指定します。  

### -\-crole [role name]
K2HR3 ロール（ROLE）名を指定します。  
サービスメンバーホストが複数のK2HR3 ロール（ROLE）のメンバーである場合、サービスメンバーは、許可するK2HR3 ロール（ROLE）名を渡す必要があります。  

### -\-ccuk [cuk]
このオプションは、将来の使用のために予約されています。  
現在、このオプションを設定しても効果はありません。  

### -\-sport [port number]
SERVICE OWNERホストのポート番号を指定します。  
SERVICE OWNERホストの場合、IPアドレスの指定は必要ありません。  

### -\-srole [role name]
SERVICE OWNERホストに割り当てられたロール名を指定します。  

### -\-scuk [cuk]
このオプションは、将来の使用のために予約されています。
現在、このオプションを設定しても効果はありません。  

### -\-output [file path]
コマンド結果を出力するファイルパスを指定します。  
