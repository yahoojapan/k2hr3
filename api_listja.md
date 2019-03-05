---
layout: contents
language: ja
title: LIST API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_list.html
lang_opp_word: To English
prev_url: api_tokenja.html
prev_string: TOKEN API
top_url: apija.html
top_string: REST API
next_url: api_roleja.html
next_string: ROLE API
---

# LIST API
K2HR3 REST APIのLISTに関連するAPI群です。

## GET
Scoped User Tokenを指定し、Scopeされているテナント（TENANT）のサービス（SERVICE）リスト、またはリソース（RESOURCE）、ポリシー/ルール（POLICY）、ロール（ROLE）いずれかの[YRN](detail_variousja.html)パスを取得します。  
テナント（TENANT）がアクセスできるサービス（SERVICE）のリストを取得するAPIです。  
もしくは、テナント（TENANT）に設定されているRESOURCE名、ポリシー/ルール（POLICY）名、ロール（ROLE）名を取得するAPIです。  
取得時にルートとなるリソース（RESOURCE）、ポリシー/ルール（POLICY）、ロール（ROLE）の[YRN](detail_variousja.html)パスを指定し、その下位層の[YRN](detail_variousja.html)パスのリストを取得できます。  
また、ルート[YRN](detail_variousja.html)パス以下の階層化された[YRN](detail_variousja.html)パスを一度に取得することもできます。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/list/service name  
http(s)://_API SERVER:PORT_/v1/list{/service name}/resource{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/resource{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/policy{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/role{/_root path_}?_urlarg_  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- expand=_true or false_  
階層化された[YRN](detail_variousja.html)パスを一度に取得する場合にはtrueを指定します。省略された場合にはfalseとして動作します。

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    children:   [
        {
            name:        <path name>
            children:    [
                {
                    ...
                },
                ...
            ]
        },
        ...
    ]
}
```

- result  
APIの処理結果をtrue/falseで返します。
- message  
処理結果がfalse（失敗）のときに、エラーメッセージが格納されます。
- children  
指定されたルート[YRN](detail_variousja.html)パス直下にある[YRN](detail_variousja.html)パス名のリストをオブジェクト配列で返します。  
expand=falseの場合には、第一階層のみが返されます。  
expand=trueの場合には、各階層ごとに[YRN](detail_variousja.html)パス名とchildren配列としてツリー構成のリストが返されます。


## HEAD
Scoped User Tokenを指定し、Scopeされているテナント（TENANT）のサービス（SERVICE）、リソース（RESOURCE）、ポリシー/ルール（POLICY）、ロール（ROLE）の[YRN](detail_variousja.html)パスも指定し、アクセスが可能であるか確認します。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/list/service name  
http(s)://_API SERVER:PORT_/v1/list{/service name}/resource{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/resource{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/policy{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/role{/_root path_}?_urlarg_  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204、40x

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

