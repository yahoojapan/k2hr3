---
layout: contents
language: ja
title: CLI policy
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_policy.html
lang_opp_word: To English
prev_url: cli_roleja.html
prev_string: CLI role
top_url: clija.html
top_string: Command Line Interface
next_url: cli_resourceja.html
next_string: CLI resource
---

# Policy Subcommand
K2HR3 Command Line Interface(CLI) の**policy** サブコマンドについて説明します。  

**policy** サブコマンドは、[POLICY API](api_policyja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[POLICY API](api_policyja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Show
ポリシー（POLICY-RULE）の情報を表示します。

### 書式(1)
```
k2hr3 policy show [policy name | yrn path]
```
指定されたポリシー（POLICY-RULE）の情報を表示します。

## Create
ポリシー（POLICY-RULE）を生成します。

### 書式(1)
```
k2hr3 policy create [policy name | yrn path] [--effect effect type] [--action action type] [--resource resource yrn path] [--alias policy yrn path]
```
ポリシー（POLICY-RULE）を付随情報とともに作成します。

## Delete
ポリシー（POLICY-RULE）を削除します。

### 書式(1)
```
k2hr3 policy delete [policy name | yrn path]
```
指定されたポリシー（POLICY-RULE）を削除します。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-effect [allow or deny]
- -\-action [yrn:yahoo::::action:read or yrn:yahoo::::action:write]
- -\-resource [resouces]
- -\-alias [aliases]
- -\-service [service name]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
