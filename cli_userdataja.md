---
layout: contents
language: ja
title: CLI userdata
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_userdata.html
lang_opp_word: To English
prev_url: cli_acrja.html
prev_string: CLI acr
top_url: clija.html
top_string: Command Line Interface
next_url: cli_extdataja.html
next_string: CLI extdata
---

# USERDATA Subcommand
K2HR3 Command Line Interface(CLI) の**userdata** サブコマンドについて説明します。  

**userdata** サブコマンドは、[USERDATA API](api_userdataja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[USERDATA API](api_userdataja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Get
OpenStack用のUserDataScriptを取得し、表示します。

### 書式(1)
```
k2hr3 userdata [registerpath] [--output file path]
```
ロールトークンを生成したときに取得される **registrepath**を指定して、OpenStack用のUserDataScriptの中身を取得します。
ロールトークンの操作については、[Role Subcommand](cli_roleja.html)を参照してください。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-output [file path]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
