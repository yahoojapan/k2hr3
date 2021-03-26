---
layout: contents
language: ja
title: CLI token
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_token.html
lang_opp_word: To English
prev_url: cli_versionja.html
prev_string: CLI version
top_url: clija.html
top_string: Command Line Interface
next_url: cli_listja.html
next_string: CLI list
---

# Token Subcommand
K2HR3 Command Line Interface(CLI) の**token** サブコマンドについて説明します。  

**token** サブコマンドは、[TOKEN API](api_tokenja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[TOKEN API](api_tokenja.html)を参照してください。

## Show
オプションで指定されたトークン、もしくはコンフィグレーションファイルに設定されているトークンの情報を表示します。

### 書式(1)
```
k2hr3 token show utoken [--unscopedtoken(-utoken) unscoped token]
```
オプションで指定されたK2HR3のUnscoped トークン、もしくはコンフィグレーションファイルに設定されているUnscoped トークンの情報を表示します。  
コンフィグレーションファイルの値を使用する場合は、オプションでトークンを指定しません。

### 書式(2)
```
k2hr3 token show token [--scopedtoken(-token) scoped token]
```
オプションで指定されたK2HR3のScoped トークン、もしくはコンフィグレーションファイルに設定されているScoped トークンの情報を表示します。  
コンフィグレーションファイルの値を使用する場合は、オプションでトークンを指定しません。

## Create
K2HR3のUnscopedもしくはScopedトークンを生成します。

### 書式(1)
```
k2hr3 token create utoken_cred [--user(-u) user name] [--passphrase(-p) passphrase]
```
ユーザクレデンシャル情報（ユーザ名、パスフレーズ）を使い、K2HR3のUnscopedトークンを生成します。  
ユーザ名、パスフレーズを省略した場合は、コンフィグレーションファイルに設定されているユーザ名、パスフレーズが使われます。
コンフィグレーションファイルにもそれらの値が設定されていない場合で、かつ`--interactive(-i)`オプションが指定されている場合には、対話形式で入力が促されます。

### 書式(2)
```
k2hr3 token create utoken_optoken [--openstacktoken(-optoken) openstack token]
```
OpenStackのトークン（UnscopedもしくはScoped）を使い、K2HR3のUnscopedトークンを生成します。  
OpenStackのトークン（UnscopedもしくはScoped）を省略した場合は、コンフィグレーションファイルに設定されているOpenStackのトークン（UnscopedもしくはScoped）が使われます。
コンフィグレーションファイルにもその値が設定されていない場合で、かつ`--interactive(-i)`オプションが指定されている場合には、対話形式で入力が促されます。

### 書式(3)
```
k2hr3 token create token_cred [--user(-u) user name] [--passphrase(-p) passphrase] [--tenant(-t) tenant]
```
ユーザクレデンシャル情報（ユーザ名、パスフレーズ）とテナント名を使い、K2HR3のScopedトークンを生成します。  
ユーザ名、パスフレーズ、テナント名を省略した場合は、コンフィグレーションファイルに設定されているユーザ名、パスフレーズ、テナント名が使われます。
コンフィグレーションファイルにもそれらの値が設定されていない場合で、かつ`--interactive(-i)`オプションが指定されている場合には、対話形式で入力が促されます。

### 書式(4)
```
k2hr3 token create token_utoken [--unscopedtoken(-utoken) unscoped token] [--tenant(-t) tenant]
```
K2HR3のUnscopedトークンとテナント名を使い、K2HR3のScopedトークンを生成します。  
K2HR3のUnscopedトークン、テナント名を省略した場合は、コンフィグレーションファイルに設定されているK2HR3のUnscopedトークン、テナント名が使われます。
コンフィグレーションファイルにもそれらの値が設定されていない場合で、かつ`--interactive(-i)`オプションが指定されている場合には、対話形式で入力が促されます。

### 書式(5)
```
k2hr3 token create token_optoken [--openstacktoken(-optoken) openstack token] [--tenant(-t) tenant]
```
OpenStackのトークン（UnscopedもしくはScoped）とテナント名を使い、K2HR3のScopedトークンを生成します。  
OpenStackのトークン（UnscopedもしくはScoped）、テナント名を省略した場合は、コンフィグレーションファイルに設定されているOpenStackのトークン（UnscopedもしくはScoped）、テナント名が使われます。
コンフィグレーションファイルにもそれらの値が設定されていない場合で、かつ`--interactive(-i)`オプションが指定されている場合には、対話形式で入力が促されます。

## Check
K2HR3のUnscopedもしくはScopedトークンの確認をします。

### 書式(1)
```
k2hr3 token check [--unscopedtoken(-utoken) unscoped token]
k2hr3 token check [--scopedtoken(-token) scoped token]
```
指定されたK2HR3のUnscopedもしくはScopedトークンの確認（有効性の確認）をします。
トークンのオプションを省略した場合は、コンフィグレーションファイルに設定されているScoped トークンの確認が行われます。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-config(-c) [file]
- -\-interactive(-i)
- -\-saveconfig(-s)
- -\-savepassphrase(-sp)
