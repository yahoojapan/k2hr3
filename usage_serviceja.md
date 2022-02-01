---
layout: contents
language: ja
title: Service Usage
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_service.html
lang_opp_word: To English
prev_url: usage_rbacja.html
prev_string: RBAC Usage
top_url: usageja.html
top_string: Usage
next_url: usage_templateja.html
next_string: Template Engine
---

# **+サービス**（**+SERVICE**）機能の使い方
K2HR3は、**+サービス**（**+SERVICE**）と呼ぶ機能を提供します。  
この**+サービス**（**+SERVICE**）機能は、サービス（SERVICE）と呼ばれる要素を使うことで、K2HR3利用者のシステム/サービスを運営における負荷軽減をする機能です。  
この**+サービス**（**+SERVICE**）機能とサービス（SERVICE）の使い方を説明します。  

## サービス（SERVICE）について
### サービス（SERVICE）の提供と利用
**+サービス**（**+SERVICE**）機能とは、リソース（RESOURCE）をテナント（TENANT）を跨ぎ、提供・利用するための機能です。  
**+サービス**（**+SERVICE**）機能は、サービス（SERVICE）と呼ばれる要素を使います。  
要素であるサービス（SERVICE）は、テナント（TENANT）に紐付き、テナント（TENANT）別に定義します。  

サービス（SERVICE）について、以下に示す定義があります。  
- 所有側（OWNER）  
サービス（SERVICE）の所有側（OWNER）とは、リソース（RESOURCE）を他テナント（TENANT）が利用できるようにします。
- 利用側（MEMBER）  
他テナント（TENANT）が提供するリソース（RESOURCE）を利用するテナント（TENANT）であり、サービス（SERVICE）の利用者（MEMBER）です。

### +サービス（+SERVICE）機能のRBAC
K2HR3は、リソース（RESOURCE）に対するRBACを提供するシステムです。  
**+サービス**（**+SERVICE**）機能を使うことで、リソース（RESOURCE）を管理するテナント（TENANT）と、それを利用するテナント（TENANT）とロール（ROLE）のアクセスを制御できます。  
このテナント（TENANT）を跨ぐリソースに対するRBACを使うことで、連携する機能・情報を簡単に管理・運用できます。  
つまり、連携する機能・情報をリソース（RESOURCE）として、これの所有側（OWNER）・利用側（MEMBER）で管理・運用の作業・工数を軽減できます。  

#### 所有側（OWNER）のメリット
通常、リソース（RESOURCE）を提供する場合、そのリソース（RESOURCE）へアクセスするロール（ROLE）メンバー（ホスト（HOST））を個別に管理する必要があります。  
これは、アクセスするホスト（HOST）の増減に伴い、その運用負荷がかかってしまいます。  
また、アクセスするホスト（HOST）毎に異なるリソース（RESOURCE）を提供する場合には、より運用の負荷は大きくなります。  

+サービス（+SERVICE）機能を利用することにより、所有側（OWNER）はアクセスするテナント（TENANT）のみを管理することができます。  
利用側（MEMBER）のテナント（TENANT）内で紐付けられたロール（ROLE）メンバーであるホスト（HOST）の管理は、そのテナント（TENANT）に任せることができます。  
また、利用側（MEMBER）のテナント（TENANT）毎に提供するリソース（RESOURCE）を動的に変更することが可能となります。  

サービス（SERVICE）の所有側（OWNER）は、アクセスをテナント（TENANT）単位で管理するだけです。  

#### 利用側（MEMBER）のメリット
通常、リソース（RESOURCE）を利用する場合、そのリソース（RESOURCE）へアクセスするロール（ROLE）メンバー（ホスト（HOST））を個別に所有側（OWNER）に依頼しなくてはなりません。  
これは、アクセスするホスト（HOST）の増減に伴い、利用側（MEMBER）と同様に運用負荷がかかってしまいます。  

+サービス（+SERVICE）機能を利用することにより、利用側（MEMBER）はテナント（TENANT）に対してのアクセスの認可をしてもらいます。  
アクセスが認可されたテナント（TENANT）内で紐付けられたロール（ROLE）メンバーであるホスト（HOST）の管理は、利用側（MEMBER）が自由に増減することができます。  

サービス（SERVICE）の利用側（MEMBER）は、アクセスするテナント（TENANT）内のロール（ROLE）を自由に管理できます。  

# (1) サービス（SERVICE）の所有側（OWNER）
サービス（SERVICE）の所有側（OWNER）の設定について説明します。  

## 提供するリソース（RESOURCE）の定義
まず、提供するリソース（RESOURCE）を決めます。  
リソース（RESOURCE）は、所有側（OWNER）・利用側（MEMBER）にとって機能・情報です。  
どのような機能・情報（主に情報）を提供するかを決定します。  
リソース（RESOURCE）に設定できる種別は以下のいずれかです。  

### 静的リソース（RESOURCE）
リソース（RESOURCE）にアクセスするテナント（TENANT）すべてに対して共通の（静的な）データを提供する場合には、この種別となります。  
静的リソース（RESOURCE）は、JSON文字列として設定します。  
このJSON文字列は複数のリソース（RESOURCE）を表現したオブジェクトである必要があります。  
JSON文字列の内容は、後述のリソース（RESOURCE）の表現で説明します。

### 動的リソース（RESOURCE）
リソース（RESOURCE）にアクセスするテナント（TENANT）毎に異なるデータを提供する場合には、この種別となります。  
動的リソース（RESOURCE）は、テナント（TENANT）がサービス（SERVICE）を連携した時点で、呼び出される（コールバックされる）VERIFY URLを登録します。  
VERIFY URLはサービス（SERVICE）所有側（OWNER）が準備したREST APIです。  

このVERIFY URLについて以下に説明します。
#### リクエスト形式
VERIFY URLはK2HR3システムから以下のようにURL argument付きでリクエストされます。  
```
GET http://<verify host[:port]>{/<path>}?service=<service name>&tenant=<tenantname>&tenantid=<tenant id>&user=<user name>&userid=<user id>
```
Url argumentについて、以下に説明します。  
- service  
値は、連携されたサービス名です。
- tenant  
値は、連携したテナント（TENANT）名です。
- tenantid  
値は、連携したテナント（TENANT）のID（K2HR3システムで認識されているID）です。
- user  
値は、連携操作したユーザ（USER）名です。
- userid  
値は、連携操作したユーザ（USER）のID（K2HR3システムで認識されているID）です。

#### レスポンス
VERIFY URLからのレスポンスはJSON文字列を返します。  
レスポンスは、リクエストのURL argumentの値に応じて、つまり連携したテナント（TENANT）に応じて変更でき、動的なリソース（RESOURCE）を提供できます。  

レスポンスのJSON文字列は複数のリソース（RESOURCE）を表現したオブジェクトである必要があります。  
JSON文字列の内容は、後述のリソース（RESOURCE）の表現で説明します。

#### テスト用VERIFY URL
K2HR3システムの[**K2HR3 API Server**](detailja.html)には、デバッグ/確認用のVERIFY URLが組み込まれています。  
このVERIFY URLをサービス（SERVICE）に設定して、動作確認をすることができます。
```
http://<k2hr3 api server host[:port]>/v1/debug/verify
```

### リソース（RESOURCE）の表現
静的リソース（RESOURCE）、およびVERIFY URLのレスポンスで返される動的リソース（RESOURCE）は、共に同じJSON文字列で表現されたオブジェクトです。  
このJSON文字列は、以下に示すオブジェクトである必要があります。  
```
[
    {
        name:    <"resource name">
        expire:  <integer>
        type:    <"string" or "object">
        data:    <null or "string" or object>
        keys: {
            key: <value>,
            .
            .
            .
        }
    },
    .
    .
    .
]
```
レスポンスの実態である、オブジェクトはリソース（RESOURCE）データの配列です。  
リソース（RESOURCE）データは、K2HR3システムで定義される一般的なリソース（RESOURCE）の要素と同じです。  
個々の要素について以下に説明します。  
- name  
リソース（RESOURCE）を区別するための名称です。  
通常のリソース（RESOURCE）の場合にはその**[YRN](detail_variousja.html)パス**です。  
この値は、配列の中でリソース（RESOURCE）を区別するために使います。
- expire  
_この項目は予約キーワードです。現在は未使用となっています。0を設定してください。_
- type  
このリソース（RESOURCE）のdata項目の種別を示します。  
"string"もしくは"object"を指定します。
- data  
リソース（RESOURCE）の値です。  
null、文字列、もしくはオブジェクトを指定します。
- keys  
キーと値の組み合わせを複数設定できます。

## サービス（SERVICE）設定
実際に所有側（OWNER）のサービス（SERVICE）設定は、以下の手順で行います。  

#### (1-1) テナント（TENANT）を選択
#### (1-2) テナント（TENANT）にサービス（SERVICE）を追加
#### (1-3) サービス（SERVICE）のデータを設定
- サービス（SERVICE）名
- リソース（RESOURCE）  
静的リソースを設定する場合は、文字列を設定します。  
動的リソースを設定する場合は、VERIFY URLを設定します。

# (2) サービス（SERVICE）の利用側（MEMBER）
サービス（SERVICE）の利用側（MEMBER）の設定を説明します。  

## 利用するサービス（SERVICE）の認可
所有側（OWNER）に、連携するサービス（SERVICE）へのテナント（TENANT）からのアクセスを許可してもらいます。  
サービス（SERVICE）へのアクセスが許可されると、利用側（MEMBER）のテナント（TENANT）で連携するサービス（SERVICE）が利用できるようになります。  

### 連携前のサービス（SERVICE）
サービス（SERVICE）が利用できるようになると、[K2HR3 Web Application](usage_appja.html)の画面にて、以下の内容が表示されます。  

- サービス名  
連携が許可されたテナント（TENANT）のサービス（SERVICE）ツリーの中に、対象のサービス（SERVICE）名が表示されます。  

## サービス（SERVICE）の連携
アクセスが許可されたテナント（TENANT）でサービス（SERVICE）との連携をします。  
[K2HR3 Web Application](usage_appja.html)での連携開始は、サービス（SERVICE）を選択し、連携させるボタンをクリックします。  
_ダイアログが表示されます。_  
表示される連携のためのダイアログにて、OKボタンを押すだけで連携は完了します。  

### 連携後のサービス（SERVICE）
サービス（SERVICE）が連携されると、[K2HR3 Web Application](usage_appja.html)の画面にて、以下の内容が表示されます。  
_サービス（SERVICE）名のサブ項目として以下のロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）が表示されます。_
- ロール（ROLE）  
"acr-role"が一つだけ存在します。  
_このロール（ROLE）は編集できません。_
- ポリシー/ルール（POLICY）  
"acr-policy"が一つだけ存在します。  
_このポリシー/ルール（POLICY）は編集できません。_
- リソース（RESOURCE）  
所有側（OWNER）から提供されたリソースが存在します。
_これらのリソース（RESOURCE）は編集できません。_

### 連携ロール（ROLE）の設定
サービス（SERVICE）連携開始する際に、ダイアログで以下の項目を設定できます。  
_連携開始のダイアログで初期設定しなくても後からでも設定できます。_

### 連携させるロール（ROLE）
サービス（SERVICE）と連携すると、サービス（SERVICE）として提供されるリソース（RESOURCE）にアクセスすることができるロール（ROLE）が自動作成されます。  
_"acr-role"ロールが作成されます。_  
サービス（SERVICE）連携し、利用側（MEMBER）が提供されたリソース（RESOURCE）に自由にアクセスするためのロール（ROLE）を管理するために、この"acr-role"ロールが使われます。  

利用側（MEMBER）は、テナント（TENANT）内にあらかじめ作成しているロール（ROLE）を、連携開始のダイアログで指定します。  
これによって、指定したロール（ROLE）のエリアス（ALIAS）に"acr-role"ロールが設定されます。  

この指定したロール（ROLE）へのエリアス（ALIAS）の追加により、提供されたリソース（RESOURCE）に指定したロール（ROLE）メンバーのホスト（HOST）からのアクセスができるようになります。

### 連携後のロール（ROLE）追加
連携開始のダイアログで初期指定せず、連携後にロール（ROLE）を設定することができます。  
この場合は、追加したいロール（ROLE）のエリアス（ALIAS）に"acr-role"ロールの**[YRN](detail_variousja.html)フルパス**を手動で追加してください。  

## 連携ロール（ROLE）とホスト（HOST）
サービス（SERVICE）と連携するロール（ROLE）の追加・削除は前項のようにできます。  
連携ロール（ROLE）のメンバーであるホスト（HOST）の追加・削除は、通常のロール（ROLE）に対する追加・削除と同じです。  

つまり、利用側（MEMBER）は、このロール（ROLE）へのメンバーであるホスト（HOST）の管理ができます。  

## サービス（SERVICE）利用
実際に利用側（MEMBER）のサービス（SERVICE）利用開始・設定は、以下の手順で行います。  

#### (2-1) テナント（TENANT）を決定
#### (2-2) 所有側（OWNER）がテナント（TENANT）を許可
#### (2-3) 許可されたサービス（SERVICE）を確認
#### (2-4) 許可されたサービス（SERVICE）の連携を開始
連携開始時にロール（ROLE）を指定することが可能です。
#### (2-5) サービス（SERVICE）で利用するロール（ROLE）を設定
連携開始後にロール（ROLE）を追加・削除できます。
#### (2-6) 利用するロール（ROLE）メンバーの管理

