---
layout: contents
language: ja
title: CLI resource
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_resource.html
lang_opp_word: To English
prev_url: cli_policyja.html
prev_string: CLI policy
top_url: clija.html
top_string: Command Line Interface
next_url: cli_serviceja.html
next_string: CLI service
---

# Resource Subcommand
K2HR3 Command Line Interface(CLI) の**resource** サブコマンドについて説明します。  

**resource** サブコマンドは、[RESOURCE API](api_resourceja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[RESOURCE API](api_resourceja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Show
リソース（RESOURCE）の情報を表示します。

### 書式(1)
```
k2hr3 resource show [resource name | yrn path]
```
指定されたリソース（RESOURCE）の情報を表示します。

## Create
リソース（RESOURCE）を生成・更新します。

### 書式(1)
```
k2hr3 resource create [resource name | yrn path] [--type type] [--data data] [--datafile filepath] [--keys key pair] [--alias role path]
```
存在しないリソース（RESOURCE）を指定した場合は、付随情報とともに生成します。
既存リソース（RESOURCE）を指定した場合は、その付随情報を更新します。

## Delete
リソース（RESOURCE）もしくはリソース（RESOURCE）の要素を削除します。

### 書式(1)
```
k2hr3 resource delete [resource name | yrn path] [--type type] [--keynames key names] [--aliases aliases]
```
オプションを指定しない場合は、リソース（RESOURCE）を削除します。
オプションを指定した場合は、リソース（RESOURCE）の付随情報を削除します。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-type [type]
- -\-data [resource data]
- -\-datafile [resoruce data file]
- -\-keys [key value datas]
- -\-alias [aliases]
- -\-service [service name]
- -\-keynames [key names]
- -\-aliases [aliases]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
