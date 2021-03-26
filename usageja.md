---
layout: contents
language: ja
title: Usage
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage.html
lang_opp_word: To English
prev_url: detailja.html
prev_string: Detail
top_url: indexja.html
top_string: TOP
next_url: setupja.html
next_string: Setup
---

# 使い方
K2HR3システムの使い方を説明します。

# 基本的な流れ
K2HR3システムの提供する**RBAC**（**R**ole **B**ased **A**ccess **C**ontrol）として、リソース（RESOURCE）へのアクセスをする[基本的な流れ](usage_baseja.html)を説明します。

## K2HR3テンプレートエンジン
K2HR3システムは、動的なリソース（RESOURCE）を定義することができます。  
この動的リソース（RESOURCE）提供をサポートするための[**K2HR3テンプレートエンジン**](usage_templateja.html)について説明します。

# +サービス（+SERVICE）機能の使い方
K2HR3は、**+サービス**（**+SERVICE**）と呼ぶ機能を提供します。  
この機能を利用するためにサービス（SERVICE）を作り、連携します。  
[**+サービス**（**+SERVICE**）機能の使い方](usage_serviceja.html)を説明します。  
_基本的な流れで説明した内容を理解した前提となっています。まず、基本的な流れを参照してからみてください。_

# ブラウザからの操作
K2HR3システムのコントロールパネルとして、ユーザ（USER）がブラウザからアクセスし、ロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）の操作・設定をします。  
ユーザ（USER）がブラウザからK2HR3システムを利用するための[Webからのアクセス方法と使い方](usage_appja.html)を説明します。  

![K2HR3 Usage - Application overview](images/usage_top_app_overview.png)

## デモンストレーションサイト
[K2HR3 デモンストレーション](https://demo.k2hr3.antpick.ax/indexja.html) で **K2HR3 Webアプリケーション** の体験ができます。  
K2HR3システムが提供するロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）の操作を学ぶことができます。  

# REST APIの利用
K2HR3の、ロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）等の操作・設定を REST APIから行えます。  
このK2HR3システムが提供する[K2HR3 REST API](apija.html)を説明します。  

# Command Line Interface(CLI) の利用
K2HR3の、ロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）等の操作・設定を Command Line Interface(CLI)から行えます。  
このK2HR3が提供する[Command Line Interface(CLI)](clija.html)を説明します。  

# 主機能 RBAC の使い方
K2HR3システムを使うことで、リソース（RESOURCE）へのロール（ROLE）ベースのアクセス制御 **RBAC**（**R**ole **B**ased **A**ccess **C**ontrol）ができます。  
このリソース（RESOURCE）に対してロール（ROLE）がアクセスし、その制御をRBACとして提供することがK2HR3システムの主機能です。  
この提供されるRBAC機能を使うことで、ロール（ROLE）に登録されたメンバーであるホスト（HOST）上のプログラムからK2HR3システムにアクセスし、リソース（RESOURCE）へのアクセスが設定された権限に基づき制御できます。  

RBAC機能の説明は、[RBAC機能としてリソース（RESOURCE）にアクセスする方法](usage_rbacja.html)で説明します。  

# その他の使い方
上記以外のK2HR3システムの[使い方や事例](usage_otherja.html)などを説明します。

