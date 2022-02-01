---
layout: contents
language: ja
title: REST API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api.html
lang_opp_word: To English
prev_url: usage_appja.html
prev_string: Web Application
top_url: usageja.html
top_string: Usage
next_url: usage_rbacja.html
next_string: RBAC Usage
---

# K2HR3 REST API
K2HR3システムのAPIサーバーは、Webアプリケーション、Webサーバー、K2HR3 OpenStack Notification Listenerと、ユーザ（USER）の管理するホスト（HOST）からアクセスされる **REST API** を提供します。  
このREST APIの説明をします。

## トークン（TOKEN）について
K2HR3システムは、**REST API**の利用方法として、トークン（**TOKEN**）の**未指定**・**指定**の2つのアクセス方法を提供します。  
**REST API**へトークン（**TOKEN**）を指定してアクセスする場合、REST APIは、トークン（TOKEN）を読み取り、**アクセス元を認可**します。  
_K2HR3システムの提供するRBAC機能の特徴は、**トークン（TOKEN）を使わず、リソース（RESOURCE）にアクセスできる**ことです。よって、ROLEから利用されるREST APIはトークン（TOKEN）を使わず利用できるように設計されています。_  

このトークン（**TOKEN**）の種類と内容、およびREST APIとの関係について、以下に説明します。  

### トークン（TOKEN）の種類
K2HR3 APIサーバーの提供するREST APIで使うトークン（TOKEN）には以下の種類があります。

#### ユーザ（USER）トークン（TOKEN）
K2HR3のユーザ（USER）別に発行されるトークン（TOKEN）です。  
このトークン（TOKEN）は、REST APIにアクセスするとき、対象となるデータ・操作に対してユーザ（USER）が権限を持つか確認するために使用されます。

#### ロール（ROLE）トークン（TOKEN）
ロール（ROLE）別に発行されるトークン（TOKEN）です。  
このトークン（TOKEN）は、REST APIにアクセスするとき、対象となるデータ・操作に対してロール（ROLE）が権限を持つか確認するために使用されます。

### REST APIへのアクセス
REST APIへのアクセスは、以下のように3種類の方法があります。  

- ユーザ（USER）トークン（TOKEN）を指定したアクセス
- ロール（ROLE）トークン（TOKEN）を指定したクセス
- トークン（TOKEN）を使わないアクセス  
このアクセス方法は、ロール（ROLE）に登録されているメンバーのホスト（HOST）からAPIサーバーのREST APIを利用する場合に使います。  
主に、ホスト（HOST）からトークン（TOKEN）なしでリソース（RESOURCE）を取得する場合に使います。  
これは、K2HR3システムにおける**主目的**の機能になります。  
_認証・認可のためのトークン（TOKEN）なしでホスト（HOST）からリソース（RESOURCE）が取得できる_

![K2HR3 REST API - Token Access](images/usage_rbac_token_all.png)

## REST API説明
K2HR3システムが提供するREST APIを説明します。  
_REST APIによっては、上述のトークン（TOKEN）の内容を事前に理解しておく必要があります。_

### [VERSION API](api_versionja.html)
K2HR3 REST APIのAPIリスト（バージョン別）を取得するAPI群です。

### [TOKEN API](api_tokenja.html)
K2HR3 REST APIのトークン（TOKEN）に関連するAPI群です。

### [LIST API](api_listja.html)
K2HR3 REST APIのリソース（RESOURCE）、ロール（ROLE）、ポリシー/ルール（POLICY）のパスリストに関連するAPI群です。

### [ROLE API](api_roleja.html)
K2HR3 REST APIのロール（ROLE）に関連するAPI群です。

### [RESOURCE API](api_resourceja.html)
K2HR3 REST APIのリソース（RESOURCE）に関連するAPI群です。

### [POLICY API](api_policyja.html)
K2HR3 REST APIのポリシー/ルール（POLICY）に関連するAPI群です。

### [SERVICE API](api_serviceja.html)
K2HR3 REST APIのサービス（SERVICE）に関連するAPI群です。

### [ACR(ACCESS CROSS ROLE) API](api_acrja.html)
K2HR3 REST APIの+サービス（+SERVICE）機能で利用するACR(ACCESS CROSS ROLE)に関連するAPI群です。

### [USERDATA API](api_userdataja.html)
K2HR3 REST APIのUSER DATA SCRIPTに関連するAPI群です。

### [EXTDATA API](api_extdataja.html)
K2HR3 REST APIのEXT(RA) DATA SCRIPTに関連するAPI群です。

