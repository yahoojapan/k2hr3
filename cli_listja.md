---
layout: contents
language: ja
title: CLI list
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_list.html
lang_opp_word: To English
prev_url: cli_tokenja.html
prev_string: CLI token
top_url: clija.html
top_string: Command Line Interface
next_url: cli_roleja.html
next_string: CLI role
---

# List Subcommand
K2HR3 Command Line Interface(CLI) の**list** サブコマンドについて説明します。  

**list** サブコマンドは、[LIST API](api_listja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[LIST API](api_listja.html)を参照してください。  

## List
サービス（SERVICE）、ロール（ROLE）、ポリシー（POLICY-RULE）もしくはリソース（RESOURCE）のリストを表示します。  
このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

### 書式(1)
```
k2hr3 list service [service name]
```
指定されたサービス名以下の情報を表示します。

### 書式(2)
```
k2hr3 list role [yrn path] [service name]
```
指定されたロール（ROLE）以下の情報を表示します。
サービス名が指定された場合は、サービス（SERVICE）以下の指定されたロール（ROLE）の情報を表示します。

### 書式(3)
```
k2hr3 list policy [yrn path] [service name]
```
指定されたポリシー（POLICY-RULE）以下の情報を表示します。
サービス名が指定された場合は、サービス（SERVICE）以下の指定されたポリシー（POLICY-RULE）の情報を表示します。

### 書式(4)
```
k2hr3 list ressource [yrn path] [service name]
```
指定されたリソース（RESOURCE）以下の情報を表示します。
サービス名が指定された場合は、サービス（SERVICE）以下の指定されたリソース（RESORUCE）の情報を表示します。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-expand
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
