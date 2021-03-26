---
layout: contents
language: ja
title: CLI acr
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_acr.html
lang_opp_word: To English
prev_url: cli_serviceja.html
prev_string: CLI service
top_url: clija.html
top_string: Command Line Interface
next_url: cli_userdataja.html
next_string: CLI userdata
---

# ACR(ACCESS CROSS ROLE) Subcommand
K2HR3 Command Line Interface(CLI) の**acr(ACCESS CROSS ROLE)** サブコマンドについて説明します。  

**acr(ACCESS CROSS ROLE)** サブコマンドは、[ACR API](api_acrja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[ACR API](api_acrja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Show
サービス（SERVICE）のテナントメンバー（MEMBER）のScopedトークンの情報を表示します。
また、サービス（SERVICE）のテナントメンバー（MEMBER）に紐づけられたリソース（RESOURCE)を表示します。

### 書式(1)
```
k2hr3 acr show tenant [service name | yrn path]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）のScopedトークンの情報を表示します。  
このコマンドでは、テナントメンバー（MEMBER）のScopedトークンを指定してください。  

### 書式(2)
```
k2hr3 acr show resource [service name | yrn path] [--cip client IP address] [--cport client port] [--crole client role] [--ccuk client CUK] [--sport service port] [--srole service role] [--scuk service CUK]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）に紐づくリソース（RESOURCE）を表示します。  
このコマンドでは、テナントメンバー（MEMBER）のScopedトークンを指定してください。  

## Add
サービス（SERVICE）のテナントメンバー（MEMBER）に、サービス（SERVICE）のロール（ROLE）、ポリシー（POLICY-RULE）、リソース（RESOURCE）を作成します。

### 書式(1)
```
k2hr3 acr add [service name | yrn path]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）として、ロール（ROLE）、ポリシー（POLICY-RULE）、リソース（RESOURCE）を作成します。
このコマンドでは、テナントメンバー（MEMBER）のScopedトークンを指定してください。  

## Delete
サービス（SERVICE）のテナントメンバー（MEMBER）としてのロール（ROLE）、ポリシー（POLICY-RULE）、リソース（RESOURCE）を削除します。

### 書式(1)
```
k2hr3 acr delete [service name | yrn path]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）としてのロール（ROLE）、ポリシー（POLICY-RULE）、リソース（RESOURCE）を削除します。
このコマンドでは、テナントメンバー（MEMBER）のScopedトークンを指定してください。  

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-cip [IP address]
- -\-cport [port number]
- -\-crole [role name or yrn path]
- -\-ccuk [cuk]
- -\-sport [port number]
- -\-srole [role name or yrn path]
- -\-scuk [cuk]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
