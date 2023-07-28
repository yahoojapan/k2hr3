---
layout: contents
language: ja
title: CLI service
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_service.html
lang_opp_word: To English
prev_url: cli_resourceja.html
prev_string: CLI resource
top_url: clija.html
top_string: Command Line Interface
next_url: cli_tenantja.html
next_string: CLI tenant
---

# Service Subcommand
K2HR3 Command Line Interface(CLI) の**service** サブコマンドについて説明します。  

**service** サブコマンドは、[SERVICE API](api_serviceja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[SERVICE API](api_serviceja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Show
サービス（SERVICE）の情報を表示します。

### 書式(1)
```
k2hr3 service show [service name | yrn path]
```
指定されたサービス（SERVICE）の情報を表示します。

## Create
サービス（SERVICE）を生成します。

### 書式(1)
```
k2hr3 service create [service name | yrn path] [--verify verify url]
```
サービス（SERVICE）を付随情報とともに生成します。

## Delete
サービス（SERVICE）を削除します。

### 書式(1)
```
k2hr3 service delete [service name | yrn path]
```
指定されたサービス（SERVICE）を削除します。

## Update Verify URL
サービス（SERVICE）のVerify URLを更新します。

### 書式(1)
```
k2hr3 service verify [service name | yrn path] [verify url]
```
指定されたサービス（SERVICE）のVerify URLを更新します。

## Tenant Member
サービス（SERVICE）のテナントメンバー（MEMBER）を操作します。  

### 書式(1)
```
k2hr3 service tenant add [service name | yrn path] [member tenant] [--clear_tenant]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）を追加します。  
`--clear_tenant`を指定した場合は、既存のテナントメンバー（MEMBER）は削除されます。  

### 書式(2)
```
k2hr3 service tenant delete [service name | yrn path] [member tenant]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）を削除します。  

### 書式(3)
```
k2hr3 service tenant check [service name | yrn path] [member tenant]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）であるか確認します。

## Tenant Member's Service
サービス（SERVICE）のテナントメンバー（MEMBER）側のサービス（SERVICE）を操作します。  

### 書式(1)
```
k2hr3 service member clear [service name | yrn path] [member tenant]
```
指定されたサービス（SERVICE）のテナントメンバー（MEMBER）側のサービス（SERVICE）を削除します。  
このコマンドを実行する場合、テナントメンバー（MEMBER）側のK2HR3のScopedトークンを指定してください。  

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-verify [string or verify url]
- -\-clear_tenant
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
