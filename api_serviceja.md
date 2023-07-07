---
layout: contents
language: ja
title: SERVICE API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_service.html
lang_opp_word: To English
prev_url: api_tenantja.html
prev_string: TENANT API
top_url: apija.html
top_string: REST API
next_url: api_acrja.html
next_string: ACR API
---

# SERVICE API

K2HR3 REST APIのサービス（SERVICE）に関連するAPI群です。

## POST
Scoped User Tokenを指定して、サービス（SERVICE）を作成します。  
もしくは、既存サービス（SERVICE）の利用側（MEMBER）のテナント（TENANT）の追加、VERIFY URLの更新を行います。  
Scoped User Tokenは、サービス（SERVICE）の所有側（OWNER）のテナント（TENANT）にアクセス権限のあるユーザ（USER）を指定します。
サービス（SERVICE）新規作成時は、指定されたのScoped User Tokenのテナント（TENANT）が所有側（OWNER）になります。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
### Request Body
#### サービス（SERVICE）作成時
```
{
    "name":    <service name>
    "verify":  <verify url>
}
```
#### 利用側（MEMBER）のテナント（TENANT）追加/VERIFY URL更新時
```
{
    "tenant":  <tenant name> or [<tenant name>, ...]
    "clear_tenant": true/false or undefined
    "verify":  <verify url>
}
```
- name  
サービス（SERVICE）名を指定します。
- tenant  
サービス（SERVICE）の利用側（MEMBER）のテナント（TENANT）名もしくは配列を指定します。
- clear_tenant  
この値が定義され、trueである場合、tenantを未指定なら全ての利用側（MEMBER）テナント（TENANT）を削除します。tenantを指定している場合には指定したtenant設定後、それ以外の利用側（MEMBER）のテナント（TENANT）を削除します。
- verify  
サービス（SERVICE）のVerify URLを指定します。  
この値には、URL以外にstatic文字列、false（boolean）を指定できます。

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


## PUT
Scoped User Tokenを指定して、サービス（SERVICE）を作成します。  
もしくは、既存サービス（SERVICE）の利用側（MEMBER）のテナント（TENANT）の追加、VERIFY URLの更新を行います。  
Scoped User Tokenは、サービス（SERVICE）の所有側側（OWNER）のテナント（TENANT）にアクセス権限のあるユーザ（USER）を指定します。
サービス（SERVICE）新規作成時は、指定されたのScoped User Tokenのテナント（TENANT）が所有側（OWNER）になります。

### Endpoint(URL)
#### 新規作成時
http(s)://_API SERVER:PORT_/v1/service?_name=service name_&_verify=verify url_
#### 利用側（MEMBER）のテナント（TENANT）追加時
http(s)://_API SERVER:PORT_/v1/service/_service name_?_tenant=tenant name_
#### VERIFY URL更新時
http(s)://_API SERVER:PORT_/v1/service/_service name_?_verify=verify url

### Header
```
x-auth-token: U=<Scoped User Token>
```
### URL Arguments
#### 新規作成時
- name=_service name  
新規作成するサービス名を指定します。
- verify=_verify url  
新規作成するサービス名のVERIFY URLを指定します。

#### 利用側（MEMBER）のテナント（TENANT）追加時
- tenant=_<tenant name> or [<tenant name>, ...]_  
サービス（SERVICE）に追加する利用側（MEMBER）のテナント（TENANT）名もしくは配列を指定します。
- clear_tenant=_true/false_  
この値が定義され、trueである場合、tenantを未指定なら全ての利用側（MEMBER）テナント（TENANT）を削除します。tenantを指定している場合には指定したtenant設定後、それ以外の利用側（MEMBER）のテナント（TENANT）を削除します。

#### VERIFY URL更新時
- verify=_verify URL_  
サービス（SERVICE）で利用するVERIFY URLを更新します。  
この値にはURL以外に、リソース（RESOURCE）の固定値としての文字列、もしくはfalse（boolean）を指定できます。

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

## GET
サービス（SERVICE）に設定された情報を取得します。
サービス（SERVICE）の所有側側（OWNER）のテナント（TENANT）に属するScoped User Tokenを指定します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service/_service name_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    service:    {
        verify:     <verify url> or <static string> or <false>
        tenant:	[
            <tenant yrn full path>,
            ...
        ]
    }
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- service:verify  
サービス（SERVICE）に指定されているVERIFY URLの値が返されます。
- service:tenant  
サービス（SERVICE）に登録されている利用側（MEMBER）のテナント（TENANT）の[YRN](detail_variousja.html)パスが配列で返されます。  
この値には所有側側（OWNER）のテナント（TENANT）を指定することも可能です。


## HEAD
サービス（SERVICE）の存在確認、もしくはサービス（SERVICE）の利用側（MEMBER）のテナント（TENANT）の確認をします。  
サービス（SERVICE）の所有側（OWNER）のテナント（TENANT）に属するScoped User Tokenを指定します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service/_service name_
http(s)://_API SERVER:PORT_/v1/service/_service name_?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
#### 利用側（MEMBER）のテナント（TENANT）確認時
- tenant=_tenant name_  
確認をする利用側（MEMBER）のテナント（TENANT）名を指定します。

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE
サービス（SERVICE）の削除、もしくはサービス（SERVICE）の利用側（MEMBER）のテナント（TENANT）の削除をします。  
サービス（SERVICE）の所有側（OWNER）のテナント（TENANT）に属するScoped User Tokenを指定します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service/_service name_
http(s)://_API SERVER:PORT_/v1/service/_service name_?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
#### 利用側（MEMBER）のテナント（TENANT）削除時
- tenant=_tenant name_  
削除をする利用側（MEMBER）のテナント（TENANT）名を指定します。  
所有側（OWNER）のテナント（TENANT）の削除はできません。

### Response status
204、40x

### Response Body(JSON)
なし

