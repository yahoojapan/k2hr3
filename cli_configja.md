---
layout: contents
language: ja
title: CLI config
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_config.html
lang_opp_word: To English
prev_url: cli_optionsja.html
prev_string: CLI options
top_url: clija.html
top_string: Command Line Interface
next_url: cli_versionja.html
next_string: CLI version
---

# Config Subcommand
K2HR3 Command Line Interface(CLI) の**config** サブコマンドについて説明します。  

**config** サブコマンドは、K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）の内容を表示・操作する機能です。  

## Show
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）の内容を表示します。

### 書式(1)
```
k2hr3 config show
```
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）に設定できる変数の一覧を表示します。

### 書式(2)
```
k2hr3 config show all
```
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）に設定されている変数とその値を表示します。

### 書式(3)
```
k2hr3 config show [variable name]
```
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）に設定されている指定された変数とその値を表示します。

## Set
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）の変数に値を設定します。

### 書式(1)
```
k2hr3 config set [variable name] [value]
```
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）の指定した変数に値を設定します。

## Clear
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）の変数の値を消去します。

### 書式(1)
```
k2hr3 config clear [variable name]
```
K2HR3 Command Line Interface(CLI)のコンフィグレーション（ファイル）の指定した変数の値を消去（未設定）します。

## オプション
以下のオプションを指定することができます。
- -\-help(-h)
- -\-config(-c) [file]
