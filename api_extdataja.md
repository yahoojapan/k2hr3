---
layout: contents
language: ja
title: EXTDATA API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_extdata.html
lang_opp_word: To English
prev_url: api_userdataja.html
prev_string: USERDATA API
top_url: apija.html
top_string: REST API
next_url: 
next_string: 
---

# EXTDATA API
K2HR3 REST APIのユーザ定義のEXTRA DATA SCRIPTに関連するAPI群です。  

このAPIは、ユーザが定義したテンプレートを展開し、その展開したデータを返すAPIです。  
ユーザは、K2HR3 APIの設定（コンフィグレーション）で、EXTDATA APIのエンドポイントの情報、テンプレート等を指定します。  
テンプレートには、RoleのYRNパス、RoleToken、K2HR3 APIサーバーURIなどを変数として定義できます。  
EXTDATA APIのエンドポイントは、registerpath値（ROLE APIのRoleToken取得のAPIから返された文字列）を含むURIとなっています。  
これにより、指定されたRoleに応じ、動的にテンプレートを展開したデータを得ることができます。  

以下は、K2HR3 APIの設定（コンフィグレーション）の例です。
```
{
  ...
  ...

  'extdata': {
    'dummy': {                                                // Extra data API(key=suburi) for trove k2hdkc
      'baseuri':     'https://localhost',                     // URI
      'template':    'config/extdata-dummy.sh.templ',         // Template for Shell part
      'useragent':   'dummy-client'                           // Allowed user-agent(can be omitted: default is allowed all)
      'contenttype': 'text/x-shellscript; charset="us-ascii"' // Response Content-Type(can be omitted: default is 'text/plain')
   },
   ...
   ...
 },
 ...
 ...
}
```

このAPIは、USERDATA APIのユーザ定義版として利用できます。  

## GET（Extdata）
ユーザ定義のテンプレートをRoleに応じて展開したデータとして取得します。  
例えば、ユーザ定義のテンプレートとしてシェルスクリプトを定義することができます。  
このシェルスクリプトのテンプレートに、RoleTokenなどの変数を定義することで、Roleに応じた専用のスクリプトとして取得することができます。  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/extdata/_uripath_/_registerpath_

### Header
```
Content-Type: application/octet-stream
User-Agent: <Allowed User Agent>
Accept-Encoding: gzip
```
- Content-Type  
'application/octet-stream'を期待します。  
ただし、このヘッダーは必須ではありません。  
- User-Agent  
必須のヘッダーです。  
このヘッダーの値は、K2HR3 APIの設定（コンフィグレーション）で設定した値と合致する必要があります。  
ただし、K2HR3 APIの設定（コンフィグレーション）で未指定の場合は、任意の文字列を許可します。  
- Accept-Encoding  
任意のヘッダーであり、指定する場合には'gzip'を含む必要があります。  
レスポンスをGzip圧縮する場合に指定してください。  
このヘッダーが指定されていない（もしくはgzipを含まない）場合には、レスポンスはtextで返されます。  

### URL Path
- uripath  
K2HR3 APIの設定（コンフィグレーション）で設定したEXTDATA API名を指定します。  
- registerpath  
ROLE APIのRoleToken取得のAPIから返された文字列（registerpath値）を指定します。  

### URL Arguments
なし

### Response status
200、40x

### Response（Gzip/Text）
Gzip圧縮された場合とTextの場合は共に内容は同じです。（Gzip圧縮されたかどうかだけの違いです）  

#### レスポンス（正常）
正しいURIパスが指定され、ROLE名、ROLEトークンも問題がない場合には、テンプレートが展開されたデータが返されます。

##### 例：テンプレート
```
{% raw %}
#/bin/sh

ROLE_NAME={{= %K2HR3_ROLE_NAME% }}
ROLE_TENANT={{= %K2HR3_ROLE_TENANT% }}
ROLE_TOKEN={{= %K2HR3_ROLE_TOKEN% }}
K2HR3_API_HOST={{= %K2HR3_API_HOST_URI% }}
ERROR_MSG={{= %K2HR3_ERROR_MSG% }}

echo "ROLE_NAME:      ${ROLE_NAME}"
echo "ROLE_TENANT:    ${ROLE_TENANT}"
echo "ROLE_TOKEN:     ${ROLE_TOKEN}"
echo "K2HR3_API_HOST: ${K2HR3_API_HOST}"
echo "ERROR_MSG:      ${ERROR_MSG}"

exit 0
{% endraw %}
```

##### 例：レスポンス
```
ROLE_NAME=yrn:yahoo:::mytenant:role:myrole
ROLE_TENANT=yrn:yahoo:::mytenant
ROLE_TOKEN=9b7754271286ee8dd68fc7996937f72d788b81b28c071333ded449b2d824636b
K2HR3_API_HOST=https://localhost:3000
ERROR_MSG=null

echo "ROLE_NAME:      ${ROLE_NAME}"
echo "ROLE_TENANT:    ${ROLE_TENANT}"
echo "ROLE_TOKEN:     ${ROLE_TOKEN}"
echo "K2HR3_API_HOST: ${K2HR3_API_HOST}"
echo "ERROR_MSG:      ${ERROR_MSG}"

exit 0
```

#### レスポンス（エラー時）
エラーが発生した場合には、40x系ステータスと以下のボディを返します。
```
{
    result:       <false>
    message:      <error message string>
}
```
