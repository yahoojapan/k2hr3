---
layout: contents
language: en-us
title: LIST API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_listja.html
lang_opp_word: To Japanese
prev_url: api_token.html
prev_string: TOKEN API
top_url: api.html
top_string: REST API
next_url: api_role.html
next_string: ROLE API
---

# LIST API

This page describes the K2HR3 LIST API. The purpose of the LIST API is to list available K2HR3 SERVICEs, K2HR3 RESOURCEs, K2HR3 ROLEs and K2HR3 POLICIes. Each element is in [YRN](detail_various.html) form. See the [Service Usage](usage_service.html) for the K2HR3 SERVICEs, K2HR3 RESOURCEs, K2HR3 ROLEs and K2HR3 POLICIes.

## GET

Lists a list of the followings in [YRN](detail_various.html) form. A scoped user token is required, so that these lists are scoped to the user identified by the token.

* SERVICE
  * a list of SERVICEs that the tenant is allowed access to
* RESOURCE
  * a list of RESOURCEs that belong to the tenant
* POLICY
  * a list of POLICYs that belong to the tenant
* ROLE
  * a list of ROLEs that belong to the tenant

### Endpoint(URL)

http(s)://_API SERVER:PORT_/v1/list/service name  
http(s)://_API SERVER:PORT_/v1/list{/service name}/resource{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/policy{/_root path_}?_urlarg_  
http(s)://_API SERVER:PORT_/v1/list{/service name}/role{/_root path_}?_urlarg_  

### Header

```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- expand=_true or false(default)_  
  - False will obtain an array of objects of the first children of the root [YRN](detail_various.html) object 
  - True will obtain an array of objects of all children of the root [YRN](detail_various.html) object

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
True if success. False otherwise
- message  
An error message if the result is false
- children  
  - An array of objects of the first children of the root [YRN](detail_various.html) object if querying with 'expand=false'(this is the default dehavior)
  - An array of objects of all children of the root [YRN](detail_various.html) object if querying with 'expand=true'


## HEAD

Validates that the each root [YRN](detail_various.html) object of SERVICE, RESOURCE, POLICY and ROLE of scoped tenant exists

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
True if success. False otherwise
- message  
An error message if the result is false

