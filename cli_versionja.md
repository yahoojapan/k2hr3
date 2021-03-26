---
layout: contents
language: ja
title: CLI version
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_version.html
lang_opp_word: To English
prev_url: cli_configja.html
prev_string: CLI config
top_url: clija.html
top_string: Command Line Interface
next_url: cli_tokenja.html
next_string: CLI token
---

# Version Subcommand
K2HR3 Command Line Interface(CLI) の**version** サブコマンドについて説明します。  

**version** サブコマンドは、[VERSION API](api_versionja.html)をCommand Line Interface(CLI)として提供した機能です。  
APIの詳細は、[VERSION API](api_versionja.html)を参照してください。

## k2hr3 version
[K2HR3 REST API](apija.html)の一覧を表示します。

### 書式
```
k2hr3 version
```

## k2hr3 version [version string]
[K2HR3 REST API](apija.html)の指定されたバージョンの一覧を表示します。  
現在、`v1`のみをサポートしています。

### 書式
```
k2hr3 version v1
```

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-json(-j)
