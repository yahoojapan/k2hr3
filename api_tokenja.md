---
layout: contents
language: ja
title: TOKEN API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_token.html
lang_opp_word: To English
prev_url: api_versionja.html
prev_string: VERSION API
top_url: apija.html
top_string: REST API
next_url: api_listja.html
next_string: LIST API
---

# TOKEN API
K2HR3 REST APIのトークン（TOKEN）に関連するAPI群です。

## POST
#### Unscoped User Tokenの生成
ユーザ（USER）の Credential 情報を指定して、Unscoped User Tokenを生成します。  
OpenStackと連携している場合は、OpenStack（Identity）の発行するUnscoped Token（Id）もしくはScoped Token（Id）を指定して、Unscoped User Tokenを生成することができます。
#### Scoped User Tokenの生成
ユーザ（USER）の Credential 情報もしくは、Unscoped User Tokenを指定し、テナント（TENANT）の権限を持つ Scoped User Tokenを生成します。  
OpenStackと連携している場合は、OpenStack（Identity）の発行するUnscoped Token（Id）もしくはScoped Token（Id）を指定して、Scoped User Tokenを生成することができます。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens

### Header
#### Credential時
```
Content-Type: application/json
```
#### Unscoped User Token指定時
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token>
```

#### OpenStack (Un)scoped Token（Id）指定時
```
Content-Type: application/json
x-auth-token: U=<OpenStack (Un)scoped Token（Id）>
```

### Request Body
#### Credential時
```
{
    auth: {
        tenantName:      <tenant name>,
        passwordCredentials:    {
            username:    <user name>
            password:    <pass phrase>
        }
    }
}
```
#### Unscoped User Token指定時
```
{
    auth: {
        tenantName:      <tenant name>,
    }
}
```
#### OpenStack (Un)scoped Token（Id）指定してUnscoped User Token生成時
```
なし
```

#### OpenStack (Un)scoped Token（Id）指定してScoped User Token生成時
```
{
    auth: {
        tenantName:      <tenant name>,
    }
}
```

- tenant name  
テナント（TENANT）名を指定します。Unscoped User Tokenを生成する場合には、テナント（TENANT）名は省略できます。
- user name  
ユーザ（USER）名を指定します。
- passwd  
パスフレーズを指定します。（認証モジュールに依存します。）

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    scoped:     <true/false>
    token:      <token string>
}
```

- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- scoped  
成功時に返されるUser TokenのScope状態を返します。
- token  
Unscoped もしくは Scoped User Token文字列を返します。


## PUT
#### Unscoped User Tokenの生成  
ユーザ（USER）の Credential 情報を指定して、Unscoped User Tokenを生成します。  
OpenStackと連携している場合は、OpenStack（Identity）の発行するUnscoped Token（Id）もしくはScoped Token（Id）を指定して、Unscoped User Tokenを生成することができます。
#### Scoped User Tokenの生成  
ユーザ（USER）の Credential 情報もしくは、Unscoped User Tokenを指定し、テナント（TENANT）権限を持つ Scoped User Tokenを生成します。  
OpenStackと連携している場合は、OpenStack（Identity）の発行するUnscoped Token（Id）もしくはScoped Token（Id）を指定して、Scoped User Tokenを生成することができます。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens?_urlarg_

### Header
#### Credential時
```
Content-Type: application/json
```
#### Unscoped User Token指定時
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token>
```

#### OpenStack (Un)scoped Token（Id）指定時
```
Content-Type: application/json
x-auth-token: U=<OpenStack (Un)scoped Token（Id）>
```

### URL Arguments
#### Credential時
- tenantname=_tenant name_  
Scoped User Tokenを生成する場合には、テナント（TENANT）名を指定します。Unscoped User Tokenを生成する場合には省略します。
- username=_user name_  
ユーザ（USER）名を指定します。
- password=_pass phrase_  
パスフレーズを指定します。（認証モジュールに依存します。）

#### Unscoped User Token指定時
- tenantname=_tenant name_  
テナント（TENANT）名を指定します。

#### OpenStack (Un)scoped Token（Id）指定してUnscoped User Token生成時
なし

#### OpenStack (Un)scoped Token（Id）指定してScoped User Token生成時
- tenantname=_tenant name_  
テナント（TENANT）名を指定します。

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    scoped:     <true/false>
    token:      <token string>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- scoped  
成功時に返されるUser TokenのScope状態を返します。
- token  
Unscoped もしくは Scoped User Token文字列を返します。


## GET
Unscoped User TokenもしくはScoped User Tokenを指定して、利用できるテナント（TENANT）リストを取得します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token or Scoped User Token>
```

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    scoped:     <true/false>
    user:       <user name>
    tenants:    [
        {
            name:       <tenant name>
            display:    <display tenant name>
        },
        ...
    ]
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- scoped  
指定されたUser TokenがScopeされたTokenであるか否かを示します。
- user  
指定されたUser Tokenのユーザ（USER）名を返します。
- tenants  
指定されたUser Tokenで利用できるテナント（TENANT）名（とその表示名）を配列で返します。  
Scoped User Tokenの場合には返されるテナント（TENANT）は、Scopeされているテナント（TENANT）1つのみとなります。


## HEAD
Unscoped User TokenもしくはScoped User Tokenを指定して、そのTokenが有効であるか確認をします。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token or Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)
なし

