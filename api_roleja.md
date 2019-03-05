---
layout: contents
language: ja
title: ROLE API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_role.html
lang_opp_word: To English
prev_url: api_listja.html
prev_string: LIST API
top_url: apija.html
top_string: REST API
next_url: api_resourceja.html
next_string: RESOURCE API
---

# ROLE API

K2HR3 REST APIのロール（ROLE）に関連するAPI群です。

## POST（ロール設定）
Scoped User Tokenを指定して、ロール（ROLE）の情報を設定（新規作成、更新）します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Request Body
```
{
    role:    {
        name:        <role name or yrn full path>
        policies:    [
                         <policy yrn full path>,
                         ...
                     ]
        alias:       [
                         <role yrn full path>,
                         ...
                     ]
    }
}
```

- name  
ロール（ROLE）名もしくは、[YRN](detail_variousja.html)フルパスでロール（ROLE）を指定します。  
ロール（ROLE）名を指定した場合には、Scoped User Tokenで示すテナント（TENANT）以下にロール（ROLE）名（パス）が作成されます。  
[YRN](detail_variousja.html)フルパスでロール（ROLE）を指定した場合には、Scoped User Tokenで示すテナント（TENANT）名との検証がなされます。
- policies  
ポリシー/ルール（POLICY）の[YRN](detail_variousja.html)フルパスを指定します。  
ポリシー/ルール（POLICY）は、単数の場合には文字列として設定することができます。  
複数のポリシー/ルール（POLICY）を指定する場合には、配列として指定します。  
ロール（ROLE）が存在し、空の配列、空文字列を指定した場合には、指定したロール（ROLE）のポリシー/ルール（POLICY）は空に設定されます。  
この値が未指定もしくはnullの場合で、ロール（ROLE）がすでに存在している場合には、ロール（ROLE）のポリシー/ルール（POLICY）は更新されません。
- alias  
エリアスとして他ロール（ROLE）の[YRN](detail_variousja.html)フルパスを指定します。  
エリアスで指定する他ロール（ROLE）が単数の場合には文字列として設定することができます。  
複数のエリアスを指定する場合には、配列として指定します。  
ロール（ROLE）が存在し、空の配列、空文字列を指定した場合には、指定したロール（ROLE）のエリアスは空に設定されます。  
この値が未指定もしくはnullの場合で、ロール（ROLE）がすでに存在している場合には、ロール（ROLE）のエリアスは更新されません。

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


## PUT（ロール（ROLE）設定）
Scoped User Tokenを指定して、ロール（ROLE）の情報を設定（新規作成、更新）します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- name=_role name or yrn full path_  
ロール（ROLE）名もしくは、[YRN](detail_variousja.html)フルパスでロール（ROLE）を指定します。  
ロール（ROLE）名を指定した場合には、Scoped User Tokenで示すテナント（TENANT）以下にロール（ROLE）名（パス）が作成されます。  
[YRN](detail_variousja.html)フルパスでロール（ROLE）を指定した場合には、Scoped User Tokenで示すテナント（TENANT）名との検証がなされます。
- policies=_policy yrn full path(文字列、配列)_  
ポリシー/ルール（POLICY）の[YRN](detail_variousja.html)フルパスをJSONで指定します。  
ポリシー/ルール（POLICY）は、単数の場合には文字列として設定することができます。  
複数のポリシー/ルール（POLICY）を指定する場合には、配列として指定します。  
ロール（ROLE）が存在し、空の配列、空文字列を指定した場合には、指定したロール（ROLE）のポリシー/ルール（POLICY）は空に設定されます。  
この値が未指定もしくはnullの場合で、ロール（ROLE）がすでに存在している場合には、ロール（ROLE）のポリシー/ルール（POLICY）は更新されません。
- alias=_role yrn full path(文字列、配列)_  
エリアスとして他ロール（ROLE）の[YRN](detail_variousja.html)フルパスをJSONで指定します。  
エリアスで指定する他ロール（ROLE）が単数の場合には文字列として設定することができます。  
複数のエリアスを指定する場合には、配列として指定します。  
ロール（ROLE）が存在し、空の配列、空文字列を指定した場合には、指定したロール（ROLE）のエリアスは空に設定されます。  
この値が未指定もしくはnullの場合で、ロール（ROLE）がすでに存在している場合には、ロール（ROLE）のエリアスは更新されません。

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


## POST（ホスト（HOST）登録）
ロール（ROLE）メンバーにhostnameもしくはIPアドレスを設定するAPIです。呼び出しのTokenの種類により動作が異なります。  
Scoped User Tokenを指定して、ロール（ROLE）メンバーにホスト（HOST）を設定（新規作成、更新）します。  
Role Tokenを指定して、ロール（ROLE）メンバーにリクエスト送信元IPアドレスを設定（新規作成、更新）します。

### Endpoint(URL)
#### Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path_
#### Role Token
http(s)://_API SERVER:PORT_/v1/role/_yrn full path to role_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```

### Request Body
#### Scoped User Token(1 hostのみ登録)
```
{
    host:    {
        host:            <hostname / ip address>
        port:            <port number>
        cuk:             <container unique key: reserved>
        extra:           <extra string data>
    }
    clear_hostname:      <true/false>
    clear_ips:           <true/false>
}
```
#### Scoped User Token(複数host登録)
```
{
    host:    [
        {
            host:        <hostname / ip address>
            port:        <port number>
            cuk:         <container unique key: reserved>
            extra:       <extra string data>
        },
        ...
    ]
    clear_hostname:      <true/false>
    clear_ips:           <true/false>
}
```
#### Role Token
```
{
    host:    {
        port:            <port number>
        cuk:             <container unique key: reserved>
        extra:           <extra string data>
    }
}
```

#### 変数説明
- hostname  
FQDNのhostnameを指定します。hostnameには、簡易的な正規表現を指定できます。
- ip address  
IPアドレスを指定します。
- port  
ポート番号を指定します。この値は、未指定、nullを指定することができます。  
未指定、null、"0"を指定した場合には、対象のホストのポート番号がanyとして登録されます。
- extra  
任意の情報を指定します。未指定、nullなど指定可能です。
- clear_hostname  
既存hostnameの情報をすべてクリアすることを指示します。
- clear_ips  
既存IPアドレスの情報をすべてクリアすることを指示します。

### 注意
すでに存在しているhostname/IPアドレスと同じホスト（HOST）を異なるポートで指定した場合には、以下の動作に注意してください。
- 既存ホスト（HOST）のポートがANYの場合  
追加するホスト（HOST）がANY以外であるケースです。この場合には、既存ホスト（HOST）のANYは削除され、新たに追加されるポート番号のみが登録されます。
- 既存ホスト（HOST）のポートがANY以外、かつ追加するホスト（HOST）のポートがANYの場合  
この場合は、既存ホスト（HOST）のANY以外のポートは削除され、新たに追加されるANYポートのみが登録されます。
- 既存ホスト（HOST）のポートがANY以外、かつ追加するホスト（HOST）のポートがANY以外（既存とも異なる）の場合  
この場合は、既存ホスト（HOST）のANY以外のポートはそのまま残ります。新たに追加されるANY以外のポートも追加登録されます。

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


## PUT（ホスト（HOST）登録）
ロール（ROLE）メンバーにhostnameもしくはIPアドレスを設定するAPIです。呼び出しのTokenの種類により動作が異なります。  
Scoped User Tokenを指定して、ロール（ROLE）メンバーにホスト（HOST）を設定（新規作成、更新）します。  
Role Tokenを指定して、ロール（ROLE）メンバーにリクエスト送信元IPアドレスを設定（新規作成、更新）します。

### Endpoint(URL)
#### Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path_?_urlarg_
#### Role Token
http(s)://_API SERVER:PORT_/v1/role/_yrn full path to role_?_urlarg_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```

### URL Arguments
#### Scoped User Token
- host=_hostname or ip address_  
FQDNのhostnameもしくは、IPアドレスを指定します。hostnameには、簡易的な正規表現を指定できます。
- port=_port number_  
ポート番号を指定します。この値は、未指定、nullを指定することができます。  
未指定、null、"0"を指定した場合には、対象のホストのポート番号がanyとして登録されます。
- cuk=_container unique key_  
このパラメータは現在reservedです。
- extra=_extra string data_  
任意の情報を指定します。未指定、nullなど指定可能です。

#### Role Token
- port=_port number_  
ポート番号を指定します。この値は、未指定、nullを指定することができます。  
未指定、null、"0"を指定した場合には、対象のホストのポート番号がanyとして登録されます。
- cuk=_container unique key_  
このパラメータは現在reservedです。
- extra=_extra string data_  
任意の情報を指定します。未指定、nullなど指定可能です。

### 注意
すでに存在しているhostname/IPアドレスと同じホスト（HOST）を異なるポートで指定した場合には、以下の動作に注意してください。
- 既存ホスト（HOST）のポートがANYの場合  
追加するホスト（HOST）がANY以外であるケースです。この場合には、既存ホスト（HOST）のANYは削除され、新たに追加されるポート番号のみが登録されます。
- 既存ホスト（HOST）のポートがANY以外、かつ追加するホスト（HOST）のポートがANYの場合  
この場合は、既存ホスト（HOST）のANY以外のポートは削除され、新たに追加されるANYポートのみが登録されます。
- 既存ホスト（HOST）のポートがANY以外、かつ追加するホスト（HOST）のポートがANY以外（既存とも異なる）の場合  
この場合は、既存ホスト（HOST）のANY以外のポートはそのまま残ります。新たに追加されるANY以外のポートも追加登録されます。

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


## GET（ロール（ROLE）データ）
Scoped User Tokenを指定して、ロール（ROLE）のデータを取得します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
-expand=_true or false_  
ロール（ROLE）に設定されているエリアスを展開するかどうかを指定します。  
省略された場合には展開しません（false）。

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    role:       {
        policies:   array,
        aliases:    array
        hosts: {
            hostnames: [
                "<hostname> <port> <cuk>",
                ...
            ],
            ips: [
                "<ip address> <port> <cuk>",
                ...
            ]
        }
    }
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- role:policies  
ロール（ROLE）に設定されているpolicyを配列で返します。
- role:aliases  
ロール（ROLE）に設定されているエリアスがあれば、配列として返します。（expand=falseの場合のみ）
- role:hosts  
ロール（ROLE）に設定されているホスト（HOST）のIP情報を返します。詳細は上記の例を参照してください。（expand=falseの場合のみ）

## GET（Role Token）
Role Tokenを取得するためのAPIです。取得には3つの手段が準備されています。  
1つは、Scoped User Tokenを指定して、Role Tokenを取得します。  
Role Tokenを指定して、Role Token（更新された新しいRole Token）を取得します。  
最後は、Tokenを指定せず、ロール（ROLE）を指定し、そのロール（ROLE）メンバーのホスト（HOST）である確認をした上で、Role Tokenを取得します。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/role/token/_role path or yrn full role path_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/role/token/_role path or yrn full role path_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/role/token/_yrn full role path_

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

### Response status
200、40x

### Response Body(JSON)
```
{
    result:       <true/false>
    message:      <null or error message string>
    token:        <role token string>
    registerpath: <URI path for userdata API>
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- token  
Role Token文字列が返されます。
- registerpath (2018/10/10追加)  
userdata API（/v1/userdata）のURIパスとなる文字列をかえします。  
この値は、以下のJSONを文字列（stringify）として、encrypt、base64、encodeURI（+'/',':','?'）変換をした文字列です。  
```
{
    role:         <role name>
    token:        <role token string>
}
```
## HEAD
Scoped User Tokenによるロール（ROLE）へのアクセス確認、またはRole Tokenの確認、リクエスト送信元IPアドレスのロール（ROLE）メンバーの確認の3つの機能を提供します。  
Scoped User Token場合には、URLパスで指定するロール（ROLE）パスもしくは[YRN](detail_variousja.html)フルパスで指定したロール（ROLE）パスに設定されているロール（ROLE）へのアクセス、ロール（ROLE）の存在を確認します。  
Role Tokenの場合には、URLパスで指定するロール（ROLE）パスもしくは[YRN](detail_variousja.html)フルパスで指定したロール（ROLE）パスに設定されているロール（ROLE）のTokenであるか確認します。  
Token未指定の場合には、APIリクエスト元のIPアドレスがURLパスで指定した[YRN](detail_variousja.html)フルパスのロール（ROLE）メンバーであるか確認します。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/role/_yrn full role path_

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

### Response status
204、40x

### Response Body(JSON)
なし


## DELETE（ロール（ROLE）削除）
ロール（ROLE）の削除、ロール（ROLE）メンバーのHostnameの削除、ロール（ROLE）メンバーのIPアドレスの削除、Role Tokenの削除（無効化）を行うAPIです。  
Scoped User Tokenを指定した場合には、ロール（ROLE）の削除、ロール（ROLE）メンバーのHostnameの削除、ロール（ROLE）メンバーのIPアドレスの削除ができます。  
Role Tokenを指定した場合には、URLパスで指定されるロール（ROLE）（[YRN](detail_variousja.html)フルパスで指定されている）であることを確認し、そのRole Tokenを無効化します。  
Tokenが未指定の場合には、リクエスト送信元IPアドレスがURLパスで指定されるロール（ROLE）（[YRN](detail_variousja.html)フルパスで指定されている）のメンバーであることを確認し、そのIPアドレスの削除をします。  
Hostname/IPアドレスの削除するケースにおいてポート番号を指定する場合に、登録されているポート番号が0（any）であり、指定されたポート番号が0以外であってもそのHostname/IPアドレスは削除されます。逆に、登録されているポート番号が0以外であり、そのポート番号と異なるポート番号を指定した場合には、削除されません。  
これは、指定されたHostname/IPアドレス（ポート番号含む）が、登録されているHostname/IPアドレス（ポート番号含む）に含まれている場合には、登録されているHostname/IPアドレスが削除されることを意味しています。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_?_urlarg_
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/role/_yrn full role path_?_urlarg_

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
#### Scoped User Token指定（ロール（ROLE）削除）
URL Argumentsとして何も指定しない場合には、ロール（ROLE）の削除となります。
#### Scoped User Token指定（Hostname/IPアドレス削除）
- host=_hostname or ip address_  
FQDNのhostnameもしくは、IPアドレスを指定します。hostnameには、簡易的な正規表現を指定できます。
- port=_port number_  
ポート番号を指定します。この値は、未指定、nullを指定することができます。
- cuk=_container unique key_  
この値は現在reservedです。

#### Role Token指定
なし
#### Token未指定
- port=_port number_  
ポート番号を指定します。この値は、未指定、nullを指定することができます。  
未指定、null、"0"を指定した場合には、対象のホストのポート番号がanyとして削除されます。

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE（Hostname/IPアドレス削除）
IaaS（OpenStack）のインスタンスから自動登録されたIPアドレス（もしくはHostname）を削除するAPIです。  
現在、IaaSとしてOpenStackを想定しており、OpenStackにおけるインスタンス起動時のUSER DATA SCRIPTによるIPアドレスの自動登録をサポートしています。  
この自動登録されたIPアドレスを、OpenStack インスタンスが削除された時点で自動的に削除するために本APIを利用します。  

本APIは、IPアドレスが自動登録されたときに指定される、`CUK`（Cloud Unique Key）を指定し、同じ`CUK`で登録されたIPアドレスを、ROLEキー以下のホスト（HOST）情報から削除します。  
現在、IaaSとしてOpenStackのインスタンスのIPアドレスを対象としており、`CUK`はOpenStackの`Instance ID`となっています。  
_また、OpenStackからの自動登録を行ったホスト（HOST）は、`extra`（後述）値が`openstack-auto-v1`固定であり、この値である必要があります。_  

本APIは、[K2HR3 Webアプリケーション](usage_appja.html)やCLIからのリクエストを想定したものではなく、[K2HR3 OpenStack Notification Listener](detail_osnlja.html)からの呼び出しを想定しています。  

本APIの呼び出しは、K2HR3 APIのconfigとして以下の設定がなされているテナント（TENANT）やロール（ROLE）に登録されているIPアドレスからのみ許可されます。（default.jsonやlocal.jsonで設定してください）
```
{
  'k2hr3admin': {
     'tenant':      'admintenant',
     'delhostrole': 'delhostrole'
  }
}
```

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role?_urlarg_

### Header
```
Content-Type: application/json
```

### URL Arguments
#### cuk
OpenStackのUSER DATA SCRIPTにより登録されたときの`CUK`（Cloud Unique Key = `Instance ID`）を指定してください。  
この値に紐づくIPアドレスを削除の対象として動作します。
#### host
削除したいIPアドレスを指定するパラメータです。  
`CUK`に紐づくIPアドレスのうち、このパラメータで指定されたIPアドレスのみが削除の対象となります。  
IPアドレスを複数指定する場合には、JSONオブジェクトで文字列配列として指定します。  
一つのIPアドレスの場合には、文字列を指定します。  
このパラメータを指定せず、`CUK`のみを指定した場合には、`CUK`に紐づくすべてのIPアドレスが削除の対象となります。  
_OpenStack起動時に登録するだけの環境では、CUKに紐づくIPアドレスは1つであることが通常であり、hostパラメータを指定しなくてもよいことが多いはずです。_
#### extra
`openstack-auto-v1`を指定してください。  
_現在、サポートしているのは、OpenStackのみであり、この値固定です。_

### Response status
204、40x

### Response Body(JSON)
なし
