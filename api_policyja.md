---
layout: contents
language: ja
title: POLICY API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_policy.html
lang_opp_word: To English
prev_url: api_resourceja.html
prev_string: RESOURCE API
top_url: apija.html
top_string: REST API
next_url: api_serviceja.html
next_string: SERVICE API
---

# POLICY API

K2HR3 REST APIのポリシー/ルール（POLICY）に関連するAPI群です。

## POST
Scoped User Tokenを指定して、リソース（RESOURCE）の情報を設定（新規作成、更新）します。  
Role Tokenを指定して、リソース（RESOURCE）の情報を設定（更新）します。  
Token未指定で、リソース（RESOURCE）の情報を設定（更新）します。  
Scoped User Tokenの場合に限り、エリアス（ALIAS）の設定ができます。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Request Body
```
{
    policy:    {
        name:      <policy name>
        effect:    <allow or deny>
        action:    [<action yrn full path>,...]
        resource:  [<resource yrn full path>,...]
        condition: null or undefined
        alias:     [<policy yrn full path>,...]
    }
}
```
- name  
ポリシー/ルール（POLICY）へのパス名もしくは、[YRN](detail_variousja.html)フルパスを指定します。
- effect  
対象のポリシー/ルール（POLICY）に設定する効果（EFFECT）を指定します。値は、"allow"、"deny"のいずれかを指定します。  
省略した場合、空文字の場合には"deny"となります。
- action  
アクセス方法（ACTION）を指定します。  
アクセス方法（ACTION）は、"yrn:yahoo::::action:read" もしくは "yrn:yahoo::::action:write" を1つ、もしくは両方指定することができ、配列として設定します。  
1つの場合には、文字列としての指定ができます。
- resource  
リソース（RESOURCE）の[YRN](detail_variousja.html)フルパスを指定します。  
指定しない場合には、未指定、null、空文字として設定します。  
1つの指定の場合には文字列としての指定が可能です。  
複数指定する場合には、配列として指定します。
- alias  
エリアス（ALIAS）として指定する他ポリシー/ルール（POLICY）への[YRN](detail_variousja.html)フルパスを指定します。  
指定しない場合には、未指定、null、空文字として設定します。  
1つの指定の場合には文字列としての指定が可能です。  
複数指定する場合には、配列として指定します。

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
Scoped User Tokenを指定して、リソース（RESOURCE）の情報を設定（新規作成、更新）します。  
Role Tokenを指定して、リソース（RESOURCE）の情報を設定（更新）します。  
Token未指定で、リソース（RESOURCE）の情報を設定（更新）します。  
Scoped User Tokenの場合に限り、エリアス（ALIAS）の設定ができます。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- name=_policy path or yrn full policy path_  
ポリシー/ルール（POLICY）へのパス名もしくは、[YRN](detail_variousja.html)フルパスを指定します。
- effect=_json effect array_  
対象のポリシー/ルール（POLICY）に設定する効果（EFFECT）を指定します。値は、"allow"、"deny"のいずれかを指定します。  
省略した場合、空文字の場合には"deny"となります。
- action=_json action array_  
アクセス方法（ACTION）を指定します。  
アクセス方法（ACTION）は、"yrn:yahoo::::action:read" もしくは "yrn:yahoo::::action:write" を1つ、もしくは両方指定することができ、配列として設定します。  
1つの場合には、文字列としての指定ができます。
- resource=_json yrn full resource path array_  
リソース（RESOURCE）の[YRN](detail_variousja.html)フルパスを指定します。  
指定しない場合には、未指定、null、空文字として設定します。  
1つの指定の場合には文字列としての指定が可能です。  
複数指定する場合には、配列として指定します。
- alias=_json yrn full policy path array_  
エリアス（ALIAS）として指定する他ポリシー/ルール（POLICY）への[YRN](detail_variousja.html)フルパスを指定します。  
指定しない場合には、未指定、null、空文字として設定します。  
1つの指定の場合には文字列としての指定が可能です。  
複数指定する場合には、配列として指定します。

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
ポリシー/ルール（POLICY）のデータを取得するためのAPIです。  
サービス（SERVICE）が指定された場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のポリシー/ルール（POLICY）の情報が返されます。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy/_policy path or yrn full policy path_{?service=service name}

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
### URL argument
- service=_service name_
サービス名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のPolicyを返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでpolicyを指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    policy:    {
        name:       <policy name>,
        effect:     <allow or deny>,
        action:     [<action yrn full path>, ...],
        resource:   [<resource yrn full path>, ...],
        alias:      [<policy yrn full path>, ...]
    }
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- policy:name  
ポリシー/ルール（POLICY）名が返されます。
- policy:effect  
ポリシー/ルール（POLICY）のeffectの値（"allow"、"deny"）が格納されます。
- policy:action  
ポリシー/ルール（POLICY）のactionの配列が格納されます。
- policy:resource  
ポリシー/ルール（POLICY）に設定されているリソース（RESOURCE）の[YRN](detail_variousja.html)フルパスが配列で返されます。
- policy:alias  
ポリシー/ルール（POLICY）に設定されているエリアス（ALIAS）である他ポリシー/ルール（POLICY）の[YRN](detail_variousja.html)フルパスが配列で返されます。

## HEAD
ポリシー/ルール（POLICY）の内容を確認するためのAPIです。  
テナント（TENANT）名とリソース（RESOURCE）の（[YRN](detail_variousja.html)フルパス）を指定して、特定のアクセス方法（ACTION）が実行できるか確認します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy/_yrn full policy path_?_urlarg_

### Header
```
Content-Type: application/json
```

### URL Arguments
- tenant=_tenant name_  
テナント（TENANT）名を指定します。
- resource=_yrn full resource path_  
確認したいリソース（RESOURCE）への[YRN](detail_variousja.html)フルパスを指定します。
- action=_action type_
確認したいアクセス方法（ACTION）を指定します。"yrn:yahoo::::action:read"もしくは、"yrn:yahoo::::action:write"を指定します。
- service=_service name_
サービス名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のPolicyを返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでpolicyを指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

### Response status
204、40x

### Response Body(JSON)
なし
## DELETE
ポリシー/ルール（POLICY）を削除します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy/_policy path or yrn full policy path_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)
なし

