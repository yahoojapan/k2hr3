---
layout: contents
language: ja
title: VERSION API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_version.html
lang_opp_word: To English
prev_url: 
prev_string: 
top_url: apija.html
top_string: REST API
next_url: api_tokenja.html
next_string: TOKEN API
---

# VERSION API
K2HR3 REST APIのAPIリスト（バージョン別）を取得するAPI群です。

## GET(/)
K2HR3 REST APIのサポートしているバージョン一覧（VERSION APIの種類）を返します。
### Endpoint(URL)
http(s)://_API SERVER:PORT_/
### Header
```
Content-Type: application/json
```
### Response status
200
### Response Body(JSON)
```
{
	version: ['v1']
}
```

## GET(/v1)
Version1でサポートしているREST APIのエンドポイントとメソッドを返します。
### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1
### Header
```
Content-Type: application/json
```
### Response status
200
### Response Body(JSON)
```
{
																
    version:    {   '/':                                        ['GET'],
                    '/v1':                                      ['GET']},
    user token: {   '/v1/user/tokens':                          ['HEAD', 'GET', 'POST']},
    host:       {   '/v1/host':                                 ['GET', 'PUT', 'POST', 'DELETE'],
                    '/v1/host/{port}':                          ['PUT', 'POST', 'DELETE'],
                    '/v1/host/FQDN':                            ['DELETE'],
                    '/v1/host/FQDN:{port}':                     ['DELETE'],
                    '/v1/host/IP':                              ['DELETE'],
                    '/v1/host/IP:{port}':                       ['DELETE']},
    role:       {   '/v1/role':                                 ['PUT', 'POST'],
                    '/v1/role/{role}':                          ['HEAD', 'GET', 'PUT', 'POST', 'DELETE'],
                    '/v1/role/token/{role}':                    ['GET']},
    resource:   {   '/v1/resource':                             ['PUT', 'POST'],
                    '/v1/resource/{resource}':                  ['HEAD', 'GET', 'DELETE']},
    policy:     {   '/v1/policy':                               ['PUT', 'POST'],
                    '/v1/policy/{policy}':                      ['HEAD', 'GET', 'DELETE']},
    list:       {   '/v1/list':                                 ['HEAD', 'GET'],
                    '/v1/list/{role, resource, policy}/{path}': ['HEAD', 'GET']}
}
```
