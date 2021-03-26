---
layout: contents
language: ja
title: CLI extdata
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_extdata.html
lang_opp_word: To English
prev_url: cli_userdataja.html
prev_string: CLI userdata
top_url: clija.html
top_string: Command Line Interface
next_url: 
next_string: 
---

# EXTDATA Subcommand
K2HR3 Command Line Interface(CLI) の**extdata** サブコマンドについて説明します。  

**exitdata** サブコマンドは、[EXTDATA API](api_extdataja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[EXTDATA API](api_extdataja.html)を参照してください。  

このコマンドには、K2HR3のScopedトークンが必要となります。K2HR3のScopedトークンは、オプションもしくはコンフィグレーションファイルで指定するか、`--interactive(-i)`オプションを指定してください。  

## Get
ユーザが定義したEXTRA DATA SCRIPTを取得し、表示します。

### 書式(1)
```
k2hr3 extdata [extdata name] [registerpath] [user agent] [--output file path]
```
ロールトークンを生成したときに取得される **registrepath**を指定して、ユーザが定義したEXTRA DATA SCRIPTの中身を取得します。
ロールトークンの操作については、[Role Subcommand](cli_roleja.html)を参照してください。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-output [file path]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
