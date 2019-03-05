---
layout: contents
language: en-us
title: VERSION API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_versionja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: api.html
top_string: REST API
next_url: api_token.html
next_string: TOKEN API
---

# VERSION API
This page describes the [K2HR3](index.html) VERSION API. The purpose of the VERSION API is to list all versions, endpoints and methods in the [K2HR3](index.html) REST APIs.

## GET(/)
Lists all versions in the [K2HR3](index.html) REST APIs.

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
Lists all of the endpoints and methods in the Version1 of [K2HR3](index.html) REST APIs.

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
