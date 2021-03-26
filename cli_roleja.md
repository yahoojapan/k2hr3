---
layout: contents
language: ja
title: CLI role
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_role.html
lang_opp_word: To English
prev_url: cli_listja.html
prev_string: CLI list
top_url: clija.html
top_string: Command Line Interface
next_url: cli_policyja.html
next_string: CLI policy
---

# Role Subcommand
K2HR3 Command Line Interface(CLI) の**role** サブコマンドについて説明します。  

**role** サブコマンドは、[ROLE API](api_roleja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[ROLE API](api_roleja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Show
ロール（ROLE）の情報を表示します。

### 書式(1)
```
k2hr3 role show [role name | yrn path]
```
指定されたロール（ROLE）の情報を表示します。

## Create
ロール（ROLE）を作成します。

### 書式(1)
```
k2hr3 role create [role name | yrn path] [--policies policy path] [--alias role path]
```
指定されたロール（ROLE）を生成します。

## Delete
ロール（ROLE）を削除します。

### 書式(1)
```
k2hr3 role delete [role name | yrn path]
```
指定されたロール（ROLE）を削除します。

## Host
ロール（ROLE）のホスト（HOST）メンバーを操作（追加・削除）します。

### 書式(1)
```
k2hr3 role host add [role name | yrn path] [--host hostname or ip address] [--port port number] [--cuk custom unique key] [--extra extra information] [--tag tag name]
```
指定されたロール（ROLE）に、指定したホスト（HOST）を付随情報と共にメンバーとして登録します。

### 書式(2)
```
k2hr3 role host delete [role name | yrn path] [--host hostname or ip address] [--port port number] [--cuk custom unique key]
```
指定されたロール（ROLE）のメンバーから、指定したホスト（HOST）を削除します。

## Role Token
ロール（ROLE）トークンの操作をします。

### 書式(1)
```
k2hr3 role token show [role name | yrn path]
```
指定されたロール（ROLE）のロールトークンのリストを表示します。

### 書式(2)
```
k2hr3 role token create [role name | yrn path] [--expire seconds]
```
指定されたロール（ROLE）のロールトークンを生成します。

### 書式(3)
```
k2hr3 role token delete [role token]
```
指定されたロールトークンを削除（消去）します。

### 書式(4)
```
k2hr3 role token check [role name | yrn path] [role token]
```
指定されたロールトークンが有効であるか確認します。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-policies [policies]
- -\-alias [aliases]
- -\-host [hostanme or IP address]
- -\-port [port number]
- -\-cuk [cuk string]
- -\-extra [extra data]
- -\-tag [tag]
- -\-expire [seconds]
- -\-expand
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
