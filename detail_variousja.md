---
layout: contents
language: ja
title: Various
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: detail_various.html
lang_opp_word: To English
prev_url: detail_osnlja.html
prev_string: K2HR3 OSNL
top_url: detailja.html
top_string: Detail
next_url: 
next_string: 
---

# 詳細（その他）
K2HR3システムの仕様に関して、共通内容を説明します。

## Yahoo Resource Names (YRN) 
K2HR3システムで参照、登録されるデータ（ユーザ（USER）、テナント（TENANT）、ロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）など）は、一意に識別できる必要があります。  
K2HR3では、これらを一意に識別するために **Yahoo Resource Names(YRN)** を定義し、利用します。  

### 書式
**Yahoo Resource Names(YRN)**は、以下の書式で定義されており、K2HR3システムを使うときにこれをパス（一部分）、フルパス（すべて）として使います。  
```
yrn:<provider(domain)>:<service>:<region>:<tenant>:<type>{:<paths>}
```
各パーツは、セパレーターとして**":"**文字で区切られています。  

以下に各パーツの説明をします。

#### **yrn**
**Yahoo Resource Names (YRN)**を示すパーツであり、すべてのYRNパスはこの文字列から開始されます。

#### < provider(domain) >
K2HR3システムを提供するプロバイダを示すパーツであり、今のところ**"yahoo"**固定となっています。  
_将来的には可変になる予定です。_

#### < service >
+サービス（+SERVICE）機能を使う場合のサービス（SERVICE）のためのパーツであり、サービス（SERVICE）名となります。  
所有側（OWNER）が設定したサービス（SERVICE）のデータを示すパスを表現する場合に指定します。  
このパーツが**空でない**場合、< tenant >はサービス（SERVICE）の所有側（OWNER）が属するテナント（TENANT）が指定されます。  

#### < region >
K2HR3システムを提供するリージョン（その名のとおり地方、地域 、範囲、領域などを意味します）を示すパーツです。  
このパーツは、現在**未定義（reserved）**であり、常に**空**となります。  
_将来的には定義される予定です。_

#### < tenant >
テナント（TENANT）を一意に識別するためのパーツであり、テナント（TENANT）の**ID**となります。  
K2HR3システムは、IaaS（OpenStack）と連携します。
よって、K2HR3システムのテナント（TENANT）は、IaaS（OpenStack）のテナント（もしくはプロジェクト）と同じです。  
つまり、テナント（TENANT）の**ID**は、IaaS（OpenStack）のテナント（もしくはプロジェクト）のIDと同じになります。  
テナント（TENANT）に関係しないデータをYRNパスで指定する場合、このパーツの値は**空**となります。

#### < type >
K2HR3システムのデータ（ユーザ（USER）、ロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）他）種別を示すパーツです。  
このパーツには、以下の値のいずれかを指定します。  
_太字以外の値はK2HR3システムの内部のみで使用しますので、ユーザ（USER）が直接利用することはありません。_
- **user**
- **service**
- **role**
- **policy**
- **resource**
- desc
- display
- id
- action
- token
- keystone
- iaas

#### < paths >
< type >までで示されるデータ種別に登録されているデータを、その種別の中で一意に示すパスです。  

このパーツの値は、**YRN部分パス**と呼ばれます。また、YRNパスの先頭（**"yrn"**）から最後までで示される値は、**YRNフルパス**と呼ばれます。  

このパーツの値には、階層化したパスを設定・利用することができます。  
階層化されたデータの場合、**"/"**文字で区切られた親子関係をPATHと同等に表現されます。

### 用途
K2HR3システムにおいて、この**Yahoo Resource Names (YRN)**は、データの設定・読み出しなどで使用されます。  
主に、ユーザ（USER）はロール（ROLE）、ポリシー/ルール（POLICY）、リソース（RESOURCE）、サービス（SERVICE）の参照・設定時にこの**YRNパス**を使用します。
ユーザ（USER）は、[K2HR3 Webアプリケーション](usage_appja.html)を使って、データの属性情報を表示するダイアログ内で**YRNフルパス**を確認することができます。

## 付属情報（AUX）
付属情報（AUX）とは、ロール（ROLE）に登録されるメンバーであるホスト（HOST）に付加される情報のことです。  

### 一意性
ロール（ROLE）メンバーのホスト（HOST）は、一意に識別される必要があります。  
しかし、K2HR3システムでは、ホスト（HOST）をFQDNもしくはIPアドレスで指定していますが、この情報だけでは一意とならないケースがあります。  
このような場合のために、付属情報（AUX）を付加できるようになっています。  
現在、自由にユーザ（USER）が利用できる付属情報（AUX）は、**PORT**要素のみになります。

### IaaS（OpenStack）連携
K2HR3システムは、ロール（ROLE）メンバーのホスト（HOST）の登録・削除をIaaS(OpenStack)と連携し、自動で実行できます。  
この機能を利用した場合、登録されるホスト（HOST）の付属情報（AUX）に、**CUK**、**EXTRA**という要素が付与されます。  
この要素は、直接設定することは避けてください。

### 付属情報（AUX）の要素
上述のとおり付属情報（AUX）にはいくつかの要素があります。  
現時点で付与可能、もしくは自動的に付与される要素を以下に説明します。  
- PORT  
ユーザ（USER）が設定することができる唯一の要素であり、ポート番号を表しています。  
この値には数値を指定してください。  
K2HR3システムを利用する上で一意に識別するためにのみ利用するようにしてください。
- CUK  
IaaS(OpenStack)連携時に自動的に設定されます。  
この値の編集・追加などは行わないようにしてください。
- EXTRA  
IaaS(OpenStack)連携時に自動的に設定されます。  
この値の編集・追加などは行わないようにしてください。

