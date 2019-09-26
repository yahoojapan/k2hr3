---
layout: contents
language: en-us
title: TOKEN API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_tokenja.html
lang_opp_word: To Japanese
prev_url: api_version.html
prev_string: VERSION API
top_url: api.html
top_string: REST API
next_url: api_list.html
next_string: LIST API
---

# TOKEN API

This page describes the [K2HR3](index.html) TOKEN API. The purpose of the TOKEN API is to create a token and show details for a token and validate a token. A token is a string generated for authorization to permit access to a [K2HR3](index.html) environment. The [K2HR3](index.html) REST APIs accept both a request with a token and a tokenless request to restricted resources. As of a request with a token, clients must send each request with a token in the right place correctly, so that the K2HR3 REST APIs can identify the type of a request. See the each API page for details.

## POST
#### Unscoped user token
Creates an unscoped user token, which is a token without an explicit scope of authorization. Credentials are required. See the information below for request parameters.

#### Scoped user token
Creates a scoped user token, which is a token scoped to a tenant(or project). Credentials or unscoped user token is required. See the information below for request parameters. 

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens

### Header
#### with credentials
```
Content-Type: application/json
```
#### with an unscoped user token
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token>
```

### Request Body
#### With credentials
```
{
    auth: {
        tenantName:      <tenant name>,
        passwordCredentials:    {
            username:    <user name>
            password:    <pass phrase>
        }
    }
}
```
#### with an unscoped user token
```
{
    auth: {
        tenantName:      <tenant name>,
    }
}
```

- tenant name  
A tenant name(required when creating a scoped user token)
- user name  
A user name
- passwd  
A password

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    scoped:     <true/false>
    token:      <token string>
}
```

- result  
True if success. False otherwise
- message  
An error message if the result if false
- scoped  
True if a token with an explicit scope. False otherwise
- token  
A token


## PUT
#### Unscoped user token
Creates an unscoped user token, which is a token without explicit scope of authorization. Credentials are required. See the information below for request parameters.

#### Scoped user token
Creates a scoped user token, which is a token scoped to a tenant(or project). Credentials or unscoped user token is required. See the information below for request parameters. 

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens?_urlarg_

### Header
#### With credential
```
Content-Type: application/json
```
#### With unscoped user token
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token>
```

### URL Arguments
#### With Credential
- tenantname=_tenant name_  
A tenant name(required when creating a scoped user token)
- username=_user name_  
A user name
- password=_pass phrase_  
A password

#### With unscoped user token
- tenantname=_tenant name_  
A tenant name

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    scoped:     <true/false>
    token:      <token string>
}
```
- result  
True if success. False otherwise
- message  
An error message if the result if false
- scoped  
True if a token with an explicit scope. False otherwise
- token  
A token


## GET
Validates and shows information for a token, including its authorization scope. An unscoped user token or a scoped user token is required.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token or Scoped User Token>
```

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    scoped:     <true/false>
    user:       <user name>
    tenants:    [
        {
            name:       <tenant name>
            display:    <display tenant name>
        },
        ...
    ]
}
```
- result  
True if success. False otherwise
- message  
An error message if the result if false
- scoped  
True if a token with an explicit scope. False otherwise
- user  
The user who owns the parameter token
- tenants  
An array of tenants with display names, which is available from the user identified by the token in request parameters
A tenant if the request token is a scoped user token.

## HEAD
Validates a token.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/user/tokens

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token or Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)


