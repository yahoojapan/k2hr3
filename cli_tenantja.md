---
layout: contents
language: ja
title: CLI tenant
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_tenant.html
lang_opp_word: To English
prev_url: cli_serviceja.html
prev_string: CLI service
top_url: clija.html
top_string: Command Line Interface
next_url: cli_acrja.html
next_string: CLI acr
---

# Tenant Subcommand
K2HR3 Command Line Interface(CLI) の**tenant** サブコマンドについて説明します。  

**tenant** サブコマンドは、[TENANT API](api_tenantja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[TENANT API](api_tenantja.html)を参照してください。  

このコマンドには、K2HR3の Unscopedトークン が必要となります。K2HR3の Uncopedトークン は、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Show
ローカルテナント（TENANT）の情報を表示します。

### 書式(1)
```
k2hr3 tenant show [--expand]
```
ユーザに紐づけられているローカルテナント（TENANT）の名前（もしくは名前を含む全情報）をリスト表示します。  

### 書式(2)
```
k2hr3 tenant show <tenant name>
```
指定されたローカルテナント（TENANT）の情報を表示します。

## Create
ローカルテナント（TENANT）を新規作成します。

### 書式(1)
```
k2hr3 tenant create <tenant name> [--display <display name>] [--description <description>] [--users '["user","user",...]']
```
ローカルテナント（TENANT）を付随情報とともに作成します。  
テナント名（`tenant name`）は、`local@`プレフィックスで指定してください。（これが省略された場合、自動的に付与されます。）

## Update
ローカルテナント（TENANT）の情報を更新します。

### 書式(1)
```
k2hr3 tenant update <tenant name> --tenantid <tenant id> [--display <display name>] [--description <description>] [--users '["user","user",...]']
```
ローカルテナント（TENANT）の情報を更新します。  
テナント名（`tenant name`）は、`local@`プレフィックスで指定してください。  
テナントID（`tenant id`）は、正しい値を指定しなければなりません。  

## Delete
ローカルテナント（TENANT）を完全に削除します。

### 書式(1)
```
k2hr3 tenant delete <tenant name> --tenantid <tenant id>
```
指定されたローカルテナント（TENANT）を削除します。  
テナントID（`tenant id`）は、正しい値を指定しなければなりません。  


## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-tenantid [tenant name]
- -\-display [display name for tenant]
- -\-description [description of tenant]
- -\-users [user name array as JSON string]
- -\-expand
