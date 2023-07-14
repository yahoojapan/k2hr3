---
layout: contents
language: ja
title: TENANT API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_tenant.html
lang_opp_word: To English
prev_url: api_policyja.html
prev_string: POLICY API
top_url: apija.html
top_string: REST API
next_url: api_serviceja.html
next_string: SERVICE API
---

# TENANT API

K2HR3 REST APIのK2HR3クラスターローカルテナント（TENANT）に関連するAPI群です。  

### 補足
K2HR3 システムのテナント（TENANT）は、連携するOpenStackのテナント（またはプロジェクト）、もしくは Kubernetes の Namespace を使います。  
K2HR3 REST APIの設定（コンフィグレーション）で、K2HR3クラスターローカルテナント（TENANT）機能を有効（`localtenants=true`）とした場合、独自のテナント（TENANT）を作成・編集・削除することができます。  
TENANT APIは、K2HR3クラスターローカルテナント（TENANT）を操作するAPIです。

## POST（新規作成）
Unscoped User Tokenもしくは、Scoped User Tokenを指定して、K2HR3クラスターローカルテナント（TENANT）を新規作成します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### Request Body
```
{
    tenant:    {
        name:     <tenant name>
        desc:     <description for tenant>
        display:  <display name for tenant>
        users:    [<user name>, ...]
    }
}
```
- name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
- desc  
K2HR3クラスターローカルテナント（TENANT）の説明文を記述します。  
この値は省略可能であり、省略された場合はデフォルトの説明文が設定されます。  
- display  
K2HR3 Web Applicationで このK2HR3クラスターローカルテナント（TENANT）を表示した時の表示名を指定します。  
この値は省略可能であり、省略された場合はテナント（TENANT）名が設定されます。  
- users  
作成する K2HR3クラスターローカルテナント（TENANT）を利用できるユーザ（USER）名を配列として設定します。  
このリクエストを送信する (Un)Scoped User Tokenで示されるユーザは、省略できます。  
K2HR3システムに登録されているユーザ（USER）名を指定する必要があります。（[YRN](detail_variousja.html)フルパスではありません。）  
ユーザ（USER）が存在しない場合には、無視されます。  

### Response status
201、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。

## PUT（新規作成）
Unscoped User Tokenもしくは、Scoped User Tokenを指定して、K2HR3クラスターローカルテナント（TENANT）を新規作成します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant?name=_tenant name_&...

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### URL Arguments
- name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
- desc  
K2HR3クラスターローカルテナント（TENANT）の説明文を記述します。  
この値は省略可能であり、省略された場合はデフォルトの説明文が設定されます。  
- display  
K2HR3 Web Applicationで このK2HR3クラスターローカルテナント（TENANT）を表示した時の表示名を指定します。  
この値は省略可能であり、省略された場合はテナント（TENANT）名が設定されます。  
- users  
作成する K2HR3クラスターローカルテナント（TENANT）を利用できるユーザ（USER）名を配列として設定します。  
複数指定する場合には、配列として指定します。  
このリクエストを送信する (Un)Scoped User Tokenで示されるユーザは、省略できます。  
K2HR3システムに登録されているユーザ（USER）名を指定する必要があります。（[YRN](detail_variousja.html)フルパスではありません。）  
ユーザ（USER）が存在しない場合には、無視されます。  

### Response status
201、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。

## POST（更新）
Unscoped User Tokenもしくは、Scoped User Tokenを指定して、K2HR3クラスターローカルテナント（TENANT）を更新します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
指定したK2HR3クラスターローカルテナント（TENANT）が存在しない場合は失敗します。  

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### Request Body
```
{
    tenant:    {
        id:       <tenant id>
        desc:     <description for tenant>
        display:  <display name for tenant>
        users:    [<user name>, ...]
    }
}
```
- id  
K2HR3クラスターローカルテナント（TENANT）の _ID_ を指定します。  
K2HR3クラスターローカルテナント（TENANT）名とこの_ID_が一致しない場合、失敗します。
- desc  
K2HR3クラスターローカルテナント（TENANT）の説明文を記述します。  
この値は省略可能であり、省略された場合はデフォルトの説明文が設定されます。  
- display  
K2HR3 Web Applicationで このK2HR3クラスターローカルテナント（TENANT）を表示した時の表示名を指定します。  
この値は省略可能であり、省略された場合はテナント（TENANT）名が設定されます。  
- users  
作成する K2HR3クラスターローカルテナント（TENANT）を利用できるユーザ（USER）名を配列として設定します。  
このリクエストを送信する (Un)Scoped User Tokenで示されるユーザは、省略できます。  
K2HR3システムに登録されているユーザ（USER）名を指定する必要があります。（[YRN](detail_variousja.html)フルパスではありません。）  
ユーザ（USER）が存在しない場合には、無視されます。  

### Response status
201、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。

## PUT（更新）
Unscoped User Tokenもしくは、Scoped User Tokenを指定して、K2HR3クラスターローカルテナント（TENANT）を更新します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_?id=_tenant id_

- tenant name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
指定したK2HR3クラスターローカルテナント（TENANT）が存在しない場合は失敗します。  

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### URL Arguments
- id  
K2HR3クラスターローカルテナント（TENANT）の _ID_ を指定します。  
K2HR3クラスターローカルテナント（TENANT）名とこの_ID_が一致しない場合、失敗します。
- desc  
K2HR3クラスターローカルテナント（TENANT）の説明文を記述します。  
この値は省略可能であり、省略された場合はデフォルトの説明文が設定されます。  
- display  
K2HR3 Web Applicationで このK2HR3クラスターローカルテナント（TENANT）を表示した時の表示名を指定します。  
この値は省略可能であり、省略された場合はテナント（TENANT）名が設定されます。  
- users  
作成する K2HR3クラスターローカルテナント（TENANT）を利用できるユーザ（USER）名を配列として設定します。  
複数指定する場合には、配列として指定します。  
このリクエストを送信する (Un)Scoped User Tokenで示されるユーザは、省略できます。  
K2HR3システムに登録されているユーザ（USER）名を指定する必要があります。（[YRN](detail_variousja.html)フルパスではありません。）  
ユーザ（USER）が存在しない場合には、無視されます。  

### Response status
201、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。

## GET（リスト）
Unscoped User Tokenもしくは、Scoped User Tokenを指定して、K2HR3クラスターローカルテナント（TENANT）のリストを取得します。  
取得するテナント（TENANT）のリストは、ユーザ（USER）が利用を許可されているテナント（TENANT）のみです。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant?expand=_true or false_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL argument
- expand=_true or false_
取得するテナント（TENANT）のリストを展開するか否かを指定します。  
展開する場合は、_true_を指定します。  

### Response status
200、40x

### Response Body(JSON) 
- 展開する場合（expand=true）  
```
{
    result:           <true/false>
    message:          <null or error message string>
    tenants: [
        {
             name:    <tenant name>,
             id:      <tenant id>,
             desc:    <description for tenant>,
             display: <display name for tenant>,
             user:    [user, ...]
         },
         ...
    ]
}
```
- 展開しない場合（expand=false）  
```
{
    result:   <true/false>
    message:  <null or error message string>
    tenants:  [<tenant name>, ...]
}
```

- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- tenants  
K2HR3クラスターローカルテナント（TENANT）の配列です。  
展開する場合（`expand=true`）は、テナント（TENANT）の情報を配列で返します。  
展開しない場合（`expand=false`）は、テナント（TENANT）名を配列で返します。  
- tenants[*]:name  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）名が設定されます。
- tenants[*]:id  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の_ID_が設定されます。
- tenants[*]:desc  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の説明文が設定されます。
- tenants[*]:display  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の表示名が設定されます。
- tenants[*]:user  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の利用が許可されているユーザ（USER）名のリストを配列で返します。

## GET（テナント指定）
Unscoped User Tokenもしくは、Scoped User Tokenを指定し、K2HR3クラスターローカルテナント（TENANT）の情報を取得します。  
ユーザ（USER）が利用を許可されていないテナント（TENANT）を指定した場合、失敗します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
指定したK2HR3クラスターローカルテナント（TENANT）が存在しない場合は失敗します。  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
200、40x

### Response Body(JSON) 
```
{
    result:        <true/false>
    message:       <null or error message string>
    tenant: {
        name:      <tenant name>,
        id:        <tenant id>,
        desc:      <description for tenant>,
        display:   <display name for tenant>,
        users:     [user, ...]
    }
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- tenant:name  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）名が設定されます。
- tenant:id  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の_ID_が設定されます。
- tenant:desc  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の説明文が設定されます。
- tenant:display  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の表示名が設定されます。
- tenant:users  
展開する場合（expand=true）に返されるテナント（TENANT）情報に含まれる要素で、テナント（TENANT）の利用が許可されているユーザ（USER）名のリストを配列で返します。

## HEAD
Unscoped User Tokenもしくは、Scoped User Tokenを指定し、K2HR3クラスターローカルテナント（TENANT）の存在を確認します。  
ユーザ（USER）が利用を許可されていないテナント（TENANT）を指定した場合、失敗します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
指定したK2HR3クラスターローカルテナント（TENANT）が存在しない場合は失敗します。  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE
Unscoped User Tokenもしくは、Scoped User Tokenを指定し、ユーザ（USER）を K2HR3クラスターローカルテナント（TENANT）の利用不可にします。  
この処理を行った結果、K2HR3クラスターローカルテナント（TENANT）の利用できるユーザ（USER）がいなくなった場合、K2HR3クラスターローカルテナント（TENANT）は削除されます。  
ユーザ（USER）が利用を許可されていないテナント（TENANT）を指定した場合、失敗します。  

#### 注意
すべてのTENANT APIには、Unscoped User Tokenもしくは、Scoped User Tokenが必要です。  
Scoped User Tokenが指定された場合、そのトークンが示すテナントは無視され、Unscoped User Tokenと同様にユーザ情報のみを使用します。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_?id=_tenant id_

- tenant name  
K2HR3クラスターローカルテナント（TENANT）名を指定します。  
この値に `local@` プレフィックスが付与されていない場合、自動的に `local@` プレフィックスが付与されたテナント（TENANT）名に変更されます。  
指定したK2HR3クラスターローカルテナント（TENANT）が存在しない場合は失敗します。  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL argument
- id  
K2HR3クラスターローカルテナント（TENANT）の_ID_を指定します。  
K2HR3クラスターローカルテナント（TENANT）名とこの_ID_が一致しない場合、失敗します。

### Response status
204、40x

### Response Body(JSON)
なし
