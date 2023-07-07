---
layout: contents
language: ja
title: TENANT API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_tenant.html
lang_opp_word: To English
prev_url: api_policyja.html
prev_string: POLICY API
top_url: apija.html
top_string: REST API
next_url: api_serviceja.html
next_string: SERVICE API
---

# TENANT API

K2HR3 REST API¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿API¿¿¿¿  

### ¿¿
K2HR3 ¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿OpenStack¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ Kubernetes ¿ Namespace ¿¿¿¿¿¿  
K2HR3 REST API¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿`localtenants=true`¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
TENANT API¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿API¿¿¿

## POST¿¿¿¿¿¿
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### Request Body
```
{
    tenant:    {
        name:     <tenant name>
        desc:     <description for tenant>
        display:  <display name for tenant>
        users:    [<user name>, ...]
    }
}
```
- name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
- desc  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
- display  
K2HR3 Web Application¿ ¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
- users  
¿¿¿¿ K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿ (Un)Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿[YRN](detail_variousja.html)¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Response status
201¿40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
API¿¿¿¿¿¿true/false¿¿¿¿¿¿
- message  
¿¿¿¿¿false¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

## PUT¿¿¿¿¿¿
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant{?name=...}

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### URL Arguments
- name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
- desc  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
- display  
K2HR3 Web Application¿ ¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
- users  
¿¿¿¿ K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿ (Un)Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿[YRN](detail_variousja.html)¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Response status
201¿40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
API¿¿¿¿¿¿true/false¿¿¿¿¿¿
- message  
¿¿¿¿¿false¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

## POST¿¿¿¿
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### Request Body
```
{
    tenant:    {
        id:       <tenant id>
        desc:     <description for tenant>
        display:  <display name for tenant>
        users:    [<user name>, ...]
    }
}
```
- id  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿ _ID_ ¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿_ID_¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿
- desc  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
- display  
K2HR3 Web Application¿ ¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
- users  
¿¿¿¿ K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿ (Un)Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿[YRN](detail_variousja.html)¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Response status
201¿40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
API¿¿¿¿¿¿true/false¿¿¿¿¿¿
- message  
¿¿¿¿¿false¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

## PUT¿¿¿¿
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_{?id=...}

- tenant name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### URL Arguments
- id  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿ _ID_ ¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿_ID_¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿
- desc  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
- display  
K2HR3 Web Application¿ ¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
- users  
¿¿¿¿ K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿¿ (Un)Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿[YRN](detail_variousja.html)¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Response status
201¿40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
}
```
- result  
API¿¿¿¿¿¿true/false¿¿¿¿¿¿
- message  
¿¿¿¿¿false¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

## GET¿¿¿¿¿
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant{?expand=true/false}

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL argument
- expand=_true or false_
¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿_true_¿¿¿¿¿¿¿  

### Response status
200¿40x

### Response Body(JSON) 
- ¿¿¿¿¿¿¿expand=true¿  
```
{
    result:           <true/false>
    message:          <null or error message string>
    tenants: [
        {
             name:    <tenant name>,
             id:      <tenant id>,
             desc:    <description for tenant>,
             display: <display name for tenant>,
             user:    [user, ...]
         },
         ...
    ]
}
```
- ¿¿¿¿¿¿¿¿expand=false¿  
```
{
    result:   <true/false>
    message:  <null or error message string>
    tenants:  [<tenant name>, ...]
}
```

- result  
API¿¿¿¿¿¿true/false¿¿¿¿¿¿
- message  
¿¿¿¿¿false¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿
- tenants  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿`expand=true`¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿`expand=false`¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿  
- tenants[*]:name  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿
- tenants[*]:id  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿_ID_¿¿¿¿¿¿¿¿
- tenants[*]:desc  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿
- tenants[*]:display  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿
- tenants[*]:user  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

## GET¿¿¿¿¿¿¿¿
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
200¿40x

### Response Body(JSON) 
```
{
    result:        <true/false>
    message:       <null or error message string>
    tenant: {
        name:      <tenant name>,
        id:        <tenant id>,
        desc:      <description for tenant>,
        display:   <display name for tenant>,
        user:      [user, ...]
    }
}
```
- result  
API¿¿¿¿¿¿true/false¿¿¿¿¿¿
- message  
¿¿¿¿¿false¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿
- tenant:name  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿
- tenant:id  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿_ID_¿¿¿¿¿¿¿¿
- tenant:desc  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿
- tenant:display  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿
- tenant:user  
¿¿¿¿¿¿¿expand=true¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

## HEAD
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204¿40x

### Response Body(JSON)
¿¿

## DELETE
Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿¿¿¿USER¿¿ K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿¿¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿USER¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

#### ¿¿
¿¿¿¿TENANT API¿¿¿Unscoped User Token¿¿¿¿¿Scoped User Token¿¿¿¿¿¿  
Scoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿Unscoped User Token¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_{?id=<tenant id>}

- tenant name  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿  
¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿ `local@` ¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿  
¿¿¿¿K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL argument
- id  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿_ID_¿¿¿¿¿¿¿  
K2HR3¿¿¿¿¿¿¿¿¿¿¿¿¿¿TENANT¿¿¿¿¿_ID_¿¿¿¿¿¿¿¿¿¿¿¿¿¿¿

### Response status
204¿40x

### Response Body(JSON)
¿¿
