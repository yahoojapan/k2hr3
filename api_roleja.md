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
        tag:             <tag string data>
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
- cuk=_custom unique key_  
OpenStackのVirtualMachineの登録の場合には、その**Instance ID**を指定してください。  
kubernetesのPodからの登録の場合は、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
それ以外の場合には未指定もしくはnullを指定します。
- extra  
現在、登録種別を指定します。この値を直接指定することはほとんどありません。  
OpenStackのVirtualMachineの登録の場合には、**openstack-auto-v1**を指定してください。  
kubernetesのPodからの登録の場合には、**k8s-auto-v1**を指定します。それ以外の場合には未指定もしくはnullを指定します。
- tag  
任意の文字列を設定できます。  
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
- cuk=_custom unique key_  
OpenStackのVirtualMachineの登録の場合には、その**Instance ID**を指定してください。  
kubernetesのPodからの登録の場合は、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
それ以外の場合には未指定もしくはnullを指定します。
- extra  
現在、登録種別を指定します。この値を直接指定することはほとんどありません。  
OpenStackのVirtualMachineの登録の場合には、**openstack-auto-v1**を指定してください。  
kubernetesのPodからの登録の場合には、**k8s-auto-v1**を指定します。それ以外の場合には未指定もしくはnullを指定します。
- tag  
任意の文字列を設定できます。  

#### Role Token
- port=_port number_  
ポート番号を指定します。この値は、未指定、nullを指定することができます。  
未指定、null、"0"を指定した場合には、対象のホストのポート番号がanyとして登録されます。
- cuk=_custom unique key_  
OpenStackのVirtualMachineの登録の場合には、その**Instance ID**を指定してください。  
kubernetesのPodからの登録の場合は、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
それ以外の場合には未指定もしくはnullを指定します。
- extra  
現在、登録種別を指定します。この値を直接指定することはほとんどありません。  
OpenStackのVirtualMachineの登録の場合には、**openstack-auto-v1**を指定してください。  
kubernetesのPodからの登録の場合には、**k8s-auto-v1**を指定します。それ以外の場合には未指定もしくはnullを指定します。
- tag  
任意の文字列を設定できます。  

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
- expand=_true or false_  
ロール（ROLE）に設定されているエリアスを展開するかどうかを指定します。  
省略された場合には展開します（true）。

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

### URL Arguments(Scoped User Tokenの場合のみ)
- expire=_0 または 有効期限秒数（10進数）_  
発行するRoleTokenの有効期限を秒で指定することができます。未指定の場合には、デフォルトの値（configに設定されている値か、24Hを有効期限とします）が使われます。0を指定した場合には、無期限（正確には10年、configで指定可能）のTokenを発行します。

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

### 注意
#### RoleTokenの有効期限について
Scoped User Tokenによる発行する場合は、有効期限を指定することが可能です。未指定の場合はデフォルト値が使われます。（デフォルト値はconfigで指定できます）  
Role Tokenを指定する場合、その指定したRoleTokenに設定された有効期限と同じ有効期限で発行されます。  
Tokenが未指定の場合には、常にデフォルト値が使われます。
#### RoleTokenの再発行について
Role Tokenを指定した場合、新たに発行されるRoleTokenは、再発行されたRoleTokenであり、指定されたRoleTokenは再発行後には利用できなく（無効）なります。


## GET（Role Token List）
ロールに対して発行されているRole Tokenのリストを取得するためのAPIです。このAPIを利用するためには、Scoped User Tokenを指定する必要があります。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/role/token/list/_role path or yrn full role path_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- expand=_true or false_  
Role Tokenのリストを取得した結果を展開するか否かを指定します。  
省略された場合には展開します（true）。

### Response status
200、40x

### Response Body(JSON)
#### 展開しない場合
```
{
    result:       <true/false>
    message:      <null or error message string>
    tokens: [
                  <role token striong>,
                  ...
    ]
}
```
#### 展開する場合
```
{
    result:       <true/false>
    message:      <null or error message string>
    tokens:	{
        <role token string>: {
            date:		  <create date(UTC ISO 8601)>
            expire:		  <expire date(UTC ISO 8601)>
            user:		  <user name if user created this token>
            hostname:	  <hostname if this token was created by host(name)>
            ip:			  <ip address if this token was created by ip>
            port:		  <port number, if specified port when created token>
            cuk:		  <cuk, if specified cuk when created token>
            registerpath: <register path in user data script>
        },
        ...
    }
}
```
- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- tokens(展開しない場合)  
Role Token文字列を配列として返します。
- tokens(展開する場合)  
Role Token文字列をキーとして値にはそのRole Tokenの属性情報をオブジェクトとしてもった、オブジェクトのリストを返します。

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
ロールの削除を行うAPIです。  
Scoped User Tokenを指定する必要があります。

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
URL Argumentsとして何も指定しません。  
hostなどのURL Argumentsを伴う場合には、ロールメンバーのhostの削除として動作しますので、注意してください。

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE（Hostname/IPアドレス削除 - ロール指定）
HostnameもしくはIPアドレスを削除するAPIです。  
Scoped User Tokenを指定するか、ロールのメンバーであるホストから呼び出すようにしてください。  
(Role Tokenを指定してDELETEメソッドを呼び出すと別の処理となります。)

### Endpoint(URL)
#### Scoped User Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### Token未指定
http(s)://_API SERVER:PORT_/v1/role/_yrn full role path_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Token未指定
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token指定
- host  
ロールから削除するhostanmeもしくはIPアドレスを指定します。  
- port  
ロールから削除するhostanmeもしくはIPアドレスを特定するために必要なポート番号を指定します。  
特定が不要な場合には、未指定もしくは0とします。
- cuk=_custom unique key_  
ロールから削除するhostanmeもしくはIPアドレスを特定するために必要なCUKを指定します。  
OpenStackのVirtualMachineの登録の場合には、その**Instance ID**を指定してください。kubernetesのPodからの登録の場合は、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
特定が不要な場合には、未指定もしくはnullとします（kubernetes以外は未指定が可能）。

#### Token未指定
- port  
このリクエストを送信したホスト（IPアドレス）をロールから削除するために必要なポート番号を指定します。  
特定が不要な場合には、未指定もしくは0とします。
- cuk=_custom unique key_  
このリクエストを送信したホスト（IPアドレス）をロールから削除するために必要なCUKを指定します。  
OpenStackのVirtualMachineの登録の場合には、その**Instance ID**を指定してください。kubernetesのPodからの登録の場合は、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
特定が不要な場合には、未指定もしくはnullとします（kubernetes以外は未指定が可能）。

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE（Hostname/IPアドレス削除 - ロール未指定）
本APIは、IPアドレスが自動登録されたときに指定される **CUK**（Custom Unique Key）を指定し、同じ**CUK**で登録されたIPアドレスを、ROLEキー以下のHOST情報から削除します。  

このAPIは、OpenStackおよびkubernetesから自動登録されたIPアドレス（もしくはHostname）を削除するために使用するAPIです。  
K2HR3では、OpenStack対応として、USER DATA SCRIPTによるIPアドレスの自動登録をサポートしています。  
kubernetesのPodの登録のためにK2HR3システムは、専用のSidecarを提供しています。  
これらの自動登録は、CUKを指定して各々のIPアドレスが登録される仕組みです。  
そして、このAPIはCUKを指定してIPアドレスの削除ができるために提供されます。  

本APIは、K2HR3 Web Applicationからの操作や、APIを直接利用することを想定したものではなく、OpenStackのRabbitMQにHookするNeutron Notification Listnerからの呼び出し、もしくはkubernetesによるPodsの削除に連動することを想定しています。  

OpenStack Neutron Notification Listnerから本APIの呼び出しは、K2HR3 Web Applicationのconfigとして以下の設定がなされているTenant/Roleに登録されているIPアドレスからのみ許可されます。  
_default.jsonやlocal.jsonに設定してください_
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
- cuk=_custom unique key_  
OpenStackのVirtualMachineの登録の場合、その**Instance ID**を指定してください。  
kubernetesのPodからの登録の場合、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
この値に紐づくIPアドレスを削除の対象として動作します。
- host  
削除したいIPアドレスを指定するパラメータです。  
**CUK**に紐づくIPアドレスのうち、このパラメータで指定されたIPアドレスのみが削除の対象となります。  
IPアドレスを複数指定する場合には、JSONオブジェクトで文字列配列として指定します。  
一つのIPアドレスの場合には、文字列を指定します。  
このパラメータを指定せず、**CUK**のみを指定した場合には、**CUK**に紐づくすべてのIPアドレスが削除の対象となります。  
_OpenStackやkubernetsで登録した場合、CUKに紐づくIPアドレスは1つであることが前提であり、hostパラメータは通常指定する必要はありません。_

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE（RoleToken削除 - ロール指定）
Role Tokenを削除（無効化）するAPIです。  
Role Tokenを指定し、URLパスで指定されるロール（YRNフルパスで指定されている）であることが確認され、またリクエストの送信元IPアドレスがロールのメンバーであることも確認し、そのRole Tokenを無効化します。  

### Endpoint(URL)
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_

### Header
#### Role Token指定
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```

### URL Arguments
- port=_port number_  
リクエストの送信元IPアドレスがロールのメンバーであることを確認するために必要な場合に、ポート番号を指定します。  
特定が不要な場合には、未指定もしくは0とします。
- cuk=_custom unique key_  
リクエストの送信元IPアドレスがロールのメンバーであることを確認するために必要な場合に、CUKを指定します。  
OpenStackのVirtualMachineの登録の場合には、その**Instance ID**を指定してください。kubernetesのPodからの登録の場合は、登録用に計算されたCUK文字列（K2HR3システムが提供するSidecarで自動的に計算されます）を指定します。  
特定が不要な場合には、未指定もしくはnullとします（kubernetes以外は未指定が可能）。

### Response status
204、40x

### Response Body(JSON)
なし

## DELETE（RoleToken削除 - ロール未指定）
Scoped User Tokenを指定して、Role Tokenを削除（無効化）するAPIです。  
Role Tokenの管理をするために必要となるAPIであり、主にK2HR3 Web Applicationから利用されます。

### Endpoint(URL)
#### Role Token指定
http(s)://_API SERVER:PORT_/v1/role/token/_role token string_

### Header
#### Scoped User Token指定
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
なし

### Response status
204、40x

### Response Body(JSON)
なし

