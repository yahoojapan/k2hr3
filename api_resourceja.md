---
layout: contents
language: ja
title: RESOURCE API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_resource.html
lang_opp_word: To English
prev_url: api_roleja.html
prev_string: ROLE API
top_url: apija.html
top_string: REST API
next_url: api_policyja.html
next_string: POLICY API
---

# RESOURCE API

K2HR3 REST APIのリソース（RESOURCE）に関連するAPI群です。

## POST
Scoped User Tokenを指定して、リソース（RESOURCE）の情報を設定（新規作成、更新）します。  
Role Tokenを指定して、リソース（RESOURCE）の情報を設定（更新）します。  
Token未指定で、リソース（RESOURCE）の情報を設定（更新）します。  
Scoped User Tokenの場合に限り、エリアス（ALIAS）の設定ができます。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/resource
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token指定
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### Token未指定
```
Content-Type: application/json
```
### Request Body
#### Scoped User Token指定
```
{
    resource:    {
        name:    <resource name>
        type:    <data type>
        data:    <resource data>
        keys:    {
            foo:    bar,
            ...
        }
        alias:    [
            <resource yrn full path>,
            ...
        ]
    }
}
```
- name  
リソース（RESOURCE）への[YRN](detail_variousja.html)パス名もしくは、[YRN](detail_variousja.html)フルパスを指定します。
- type  
リソース（RESOURCE）データのタイプを指定します。タイプは、"string"、"object"、null、未指定を設定できます。未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- data  
リソース（RESOURCE）データを指定します。typeが"string"の場合には文字列、"object"の場合にはJSONオブジェクトを設定します。この値が未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- keys  
リソース（RESOURCE）のキーと値のペア（KEYS）の値を指定します。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。
- alias  
リソース（RESOURCE）のエリアス（ALIAS）を指定します。エリアス（ALIAS）は、[YRN](detail_variousja.html)フルパスで他のリソース（RESOURCE）を指定し、配列で設定します。1つの値の場合には文字列として設定することができます。複数の場合は、配列もしくは","区切りの文字列で指定できます。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。

#### Role Token指定
```
{
    resource:    {
        type:    <data type>
        data:    <resource data>
        keys:    {
            foo:    bar,
            ...
        }
    }
}
```
- type  
リソース（RESOURCE）データのタイプを指定します。タイプは、"string"、"object"、null、未指定を設定できます。未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- data  
リソース（RESOURCE）データを指定します。typeが"string"の場合には文字列、"object"の場合にはJSONオブジェクトを設定します。この値が未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- keys  
リソース（RESOURCE）のキーと値のペア（KEYS）の値を指定します。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。

#### Token未指定
```
{
    resource:    {
        port:    <port number>
        cuk:     <container unique key>
        role:    <role full yrn>
        type:    <data type>
        data:    <resource data>
        keys:    {
            foo:    bar,
            ...
        }
    }
}
```
- port  
ポート番号を指定します。リクエスト送信元のIPアドレスとこの値を組み合わせて、roleで指定されたロール（ROLE）のメンバーであることが確認されます。  
未指定、nullの場合には、"0"と同じ意味である"any"として判定されます。
- cuk  
現在この値はreservedです。
- role  
ロール（ROLE）の[YRN](detail_variousja.html)フルパスを指定します。リクエスト送信元のIPアドレスとポート番号の組み合わせが、このロール（ROLE）メンバーであることが確認されます。
- type  
リソース（RESOURCE）データのタイプを指定します。タイプは、"string"、"object"、null、未指定を設定できます。未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- data  
リソース（RESOURCE）データを指定します。typeが"string"の場合には文字列、"object"の場合にはJSONオブジェクトを設定します。この値が未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- keys  
リソース（RESOURCE）のキーと値のペア（KEYS）の値を指定します。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。

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
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/resource?_urlarg_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token指定
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### Token未指定
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token指定
- name=_resource name_  
リソース（RESOURCE）へのパス名もしくは、[YRN](detail_variousja.html)フルパスを指定します。
- type=_data type_  
リソース（RESOURCE）データのタイプを指定します。タイプは、"string"、"object"、null、未指定を設定できます。未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- data=_resource data_  
リソース（RESOURCE）データを指定します。typeが"string"の場合には文字列、"object"の場合にはJSONオブジェクトを設定します。この値が未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- keys=_json key value object_  
リソース（RESOURCE）のキーと値のペア（KEYS）オブジェクトをJSON文字列で指定します。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。
- alias=_json alias array_
リソース（RESOURCE）のエリアス（ALIAS）を指定します。エリアス（ALIAS）は、[YRN](detail_variousja.html)フルパスで他のリソース（RESOURCE）を指定し、配列で指定し、JSON文字列として設定します。1つの値の場合には文字列として設定することができます。複数の場合は、配列もしくは","区切りの文字列で指定できます。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。

#### Role Token指定
- type=_data type_  
リソース（RESOURCE）データのタイプを指定します。タイプは、"string"、"object"、null、未指定を設定できます。未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- data=_resource data_  
リソース（RESOURCE）データを指定します。typeが"string"の場合には文字列、"object"の場合にはJSONオブジェクトを設定します。この値が未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- keys=_json key value object_  
リソース（RESOURCE）のキーと値のペア（KEYS）オブジェクトをJSON文字列で指定します。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。

#### Token未指定
- port=_port number_  
ポート番号を指定します。リクエスト送信元のIPアドレスとこの値を組み合わせて、roleで指定されたロール（ROLE）のメンバーであることが確認されます。  
未指定、nullの場合には、"0"と同じ意味である"any"として判定されます。
- cuk=_container unique key_  
現在この値はreservedです。
- role=_yrn full role path_  
ロール（ROLE）の[YRN](detail_variousja.html)フルパスを指定します。リクエスト送信元のIPアドレスとポート番号の組み合わせが、このロール（ROLE）メンバーであることが確認されます。
- type=_data type_  
リソース（RESOURCE）データのタイプを指定します。タイプは、"string"、"object"、null、未指定を設定できます。未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- data=_resource data_  
リソース（RESOURCE）データを指定します。typeが"string"の場合には文字列、"object"の場合にはJSONオブジェクトを設定します。この値が未指定、nullの場合には既存リソース（RESOURCE）の更新はされません。
- keys=_json key value object_  
リソース（RESOURCE）のキーと値のペア（KEYS）オブジェクトをJSON文字列で指定します。未指定、もしくはnullの場合には既存リソース（RESOURCE）の更新はされません。

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
リソース（RESOURCE）のデータを取得するためのAPIです。  
Scoped User Tokenを指定した場合には、リソース（RESOURCE）全体を取得できます。取得するリソース（RESOURCE）は、リソース（RESOURCE）データそのものか、展開（エリアス（ALIAS）など）したリソース（RESOURCE）データを取得することができます。  
Role Tokenを指定した場合、Tokenの未指定の場合には、リソース（RESOURCE）の特定データ（リソース（RESOURCE）データもしくはKeyの値）を取得することができます。  

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token指定
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### Token未指定
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token指定
- expand=_true or false_  
ロール（ROLE）に設定されているエリアス（ALIAS）を展開するかどうかを指定します。  
省略された場合には展開します（true）。
- service=_service name_
サービス（SERVICE）名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のリソース（RESOURCE）を返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでリソース（RESOURCE）を指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

#### Role Token指定
- type=_data type_  
取得するリソース（RESOURCE）のタイプを指定します。タイプは、"string"、"object"、"keys"です。
- keyname=_key name_
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を指定します。
- service=_service name_
サービス（SERVICE）名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のリソース（RESOURCE）を返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでリソース（RESOURCE）を指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

#### Token未指定
- port=_port number_  
ポート番号を指定します。リクエスト送信元のIPアドレスとこの値を組み合わせて、roleで指定されたロール（ROLE）のメンバーであることが確認されます。  
未指定、nullの場合には、"0"と同じ意味である"any"として判定されます。
- cuk=_container unique key_  
現在この値はreservedです。
- role=_yrn full role path_  
ロール（ROLE）の[YRN](detail_variousja.html)フルパスを指定します。リクエスト送信元のIPアドレスとポート番号の組み合わせが、このロール（ROLE）メンバーであることが確認されます。
- type=_data type_  
取得するリソース（RESOURCE）のタイプを指定します。タイプは、"string"、"object"、"keys"です。
- keyname=_key name_
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を指定します。
- service=_service name_
サービス（SERVICE）名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のリソース（RESOURCE）を返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでリソース（RESOURCE）を指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

### Response status
200、40x

### Response Body(JSON)
#### Scoped User Token指定
```
{
    result:     <true/false>
    message:    <null or error message string>
    resource:   {
        string:     <string>,
        object:     <object>,
        keys:       <object>,
        aliases:    <array>
    }
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- resource:string  
指定したリソース（RESOURCE）の文字列データが返されます。
- resource:object  
指定したリソース（RESOURCE）のオブジェクトデータが返されます。
- resource:keys  
指定したリソース（RESOURCE）のキーと値のペア（KEYS）のオブジェクトが返されます。
- resource:aliases  
指定したリソース（RESOURCE）のエリアス（ALIAS）が配列として返されます。

#### Role Token、Token未指定
```
{
    result:     <true/false>
    message:    <null or error message string>
    resource:   <data>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- resource  
指定したリソース（RESOURCE）のデータが返されます。


## HEAD
リソース（RESOURCE）のデータの存在を確認するためのAPIです。  
リソース（RESOURCE）のデータタイプを指定し、そのデータの確認をします。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token指定
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### Token未指定
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token指定
- type=_data type_  
取得するリソース（RESOURCE）のタイプを指定します。タイプは、"string"、"object"、"keys"です。
- keyname=_key name_
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を指定します。
- service=_service name_
サービス（SERVICE）名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のリソース（RESOURCE）を返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでリソース（RESOURCE）を指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

#### Role Token指定
- type=_data type_  
取得するリソース（RESOURCE）のタイプを指定します。タイプは、"string"、"object"、"keys"です。
- keyname=_key name_
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を指定します。
- service=_service name_
サービス（SERVICE）名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のリソース（RESOURCE）を返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでリソース（RESOURCE）を指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

#### Token未指定
- port=_port number_  
ポート番号を指定します。リクエスト送信元のIPアドレスとこの値を組み合わせて、roleで指定されたロール（ROLE）のメンバーであることが確認されます。  
未指定、nullの場合には、"0"と同じ意味である"any"として判定されます。
- cuk=_container unique key_  
現在この値はreservedです。
- role=_yrn full role path_  
ロール（ROLE）の[YRN](detail_variousja.html)フルパスを指定します。リクエスト送信元のIPアドレスとポート番号の組み合わせが、このロール（ROLE）メンバーであることが確認されます。
- type=_data type_  
取得するリソース（RESOURCE）のタイプを指定します。タイプは、"string"、"object"、"keys"です。
- keyname=_key name_
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を指定します。
- service=_service name_
サービス（SERVICE）名を指定します。指定されている場合には、サービス（SERVICE）とテナント（TENANT）で示される[YRN](detail_variousja.html)パス以下のリソース（RESOURCE）を返すことになります。  
URLパスにフル[YRN](detail_variousja.html)パスでリソース（RESOURCE）を指定している場合に、本パラメータが指定されているときにはその名前が同じであるか検証されます。

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE
リソース（RESOURCE）のデータ、リソース（RESOURCE）そのものを削除するためのAPIです。  
Scoped User Tokenを指定した場合には、リソース（RESOURCE）全体を削除できます。また、リソース（RESOURCE）内のデータタイプを指定して、指定したデータをリソース（RESOURCE）から削除できます。
Role Tokenを指定した場合、Tokenの未指定の場合には、リソース（RESOURCE）内のデータタイプを指定して、指定したデータをリソース（RESOURCE）から削除できます。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token指定
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### Token未指定
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token指定
- type=_data type_  
削除するリソース（RESOURCE）のタイプを指定します。タイプは、"anytype"、"string"、"object"、"keys"、"aliases"、未指定、nullです。  
"anytype"は、リソース（RESOURCE）に設定されている文字列かオブジェクトのタイプにしたがって、その値を削除することを意味します。
未指定、nullの場合にはリソース（RESOURCE）全体が削除されます。
- keynames=_key name_  
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を削除します。_key name_には文字列、配列（JSON）を指定することができます。
- aliases=_json alias array_  
typeが"aliases"の場合に、リソース（RESOURCE）内のエリアス（ALIAS）を削除します。  
エリアス（ALIAS）は複数指定でき、配列もしくは","区切りで指定し、JSON文字列で指定します。単数の場合には文字列として指定することができます。
#### Role Token指定
- type=_data type_  
削除するリソース（RESOURCE）のタイプを指定します。タイプは、"anytype"、"string"、"object"、"keys"です。  
"anytype"は、リソース（RESOURCE）に設定されている文字列かオブジェクトのタイプにしたがって、その値を削除することを意味します。
- keynames=_key name_  
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を削除します。_key name_には文字列、配列（JSON）を指定することができます。
#### Token未指定
- port=_port number_  
ポート番号を指定します。リクエスト送信元のIPアドレスとこの値を組み合わせて、roleで指定されたロール（ROLE）のメンバーであることが確認されます。  
未指定、nullの場合には、"0"と同じ意味である"any"として判定されます。
- cuk=_container unique key_  
現在この値はreservedです。
- role=_yrn full role path_  
ロール（ROLE）の[YRN](detail_variousja.html)フルパスを指定します。リクエスト送信元のIPアドレスとポート番号の組み合わせが、このロール（ROLE）メンバーであることが確認されます。
- type=_data type_  
削除するリソース（RESOURCE）のタイプを指定します。タイプは、"anytype"、"string"、"object"、"keys"です。  
"anytype"は、リソース（RESOURCE）に設定されている文字列かオブジェクトのタイプにしたがって、その値を削除することを意味します。
- keynames=_key name_  
typeが"keys"の場合に、リソース（RESOURCE）内のkey名を削除します。_key name_には文字列、配列（JSON）を指定することができます。

### Response status
204、40x

### Response Body(JSON)
なし

