---
layout: contents
language: en-us
title: SERVICE API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_serviceja.html
lang_opp_word: To Japanese
prev_url: api_policy.html
prev_string: POLICY API
top_url: api.html
top_string: REST API
next_url: api_acr.html
next_string: ACR API
---

# SERVICE API

This page describes the K2HR3 SERVICE API. The purpose of the SERVICE API is for a tenant to create, show details, update, and delete a information of the K2HR3 SERVICEs of the tenant. Therefore, each method requires a tenant-scoped token. See the [+SERVICE Usage](usage_service.html) page for the K2HR3 SERVICE details.

## POST
Provides the following functions. A user token scoped to the service owner's tenant in the HTTP request header is required.

* Creates a K2HR3 SERVICE.
  * The tenant scoped to the token will be the owner of the new SERVICE
* Adding new members(or Tenants) to an existing K2HR3 SERVICE.
* Modifying a url to define a dynamic resource(or VERIFY URL) of an existing K2HR3 SERVICE.
  * See the [+SERVICE Usage](usage_service.html) page for the dynamic resource.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service

### Header
Requires a user token scoped to a tenant who owns the service.
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
### Request Body
#### Create SERVICE
```
{
    "name":    <service name>
    "verify":  <verify url>
}
```
#### Add MEMBER to SERVICE / Modify VERIFY URL
```
{
    "tenant":  <tenant name> or [<tenant name>, ...]
    "clear_tenant": true/false or undefined
    "verify":  <verify url>
}
```
- name  
A service name.  
- tenant  
A tenant as a service member or an array of tenants as members.
- clear_tenant(optional)  
True with a tenant if deletes a tenant from the service member. True without a tenant if delete all tenants from the service member after adding the tenant.
- verify  
A url to define a dynamic resource or a string literal or a boolean literal. See the [+SERVICE Usage](usage_service.html) page for the dynamic resource.

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
True if success. False otherwise.
- message  
An error message if the result if false


## PUT
This method provides the following functions. A user token scoped to the service owner's tenant in the HTTP request header is required.

* Creates a K2HR3 SERVICE.
  * The tenant of the scoped user token will be the owner of the created SERVICE is the tenant
* Adding new members(or Tenants) to an existing K2HR3 SERVICE.
* Modifying a url to define a dynamic resource(or VERIFY URL) of an existing K2HR3 SERVICE.
  * See the [+SERVICE Usage](usage_service.html) page for the dynamic resource.


### Endpoint(URL)
#### Create SERVICE
http(s)://_API SERVER:PORT_/v1/service?_name=service name_&_verify=verify url_
#### Add MEMBER to SERVICE 
http(s)://_API SERVER:PORT_/v1/service/_service name_?_tenant=tenant name_
#### Modify VERIFY URL
http(s)://_API SERVER:PORT_/v1/service/_service name_?_verify=verify url

### Header
Requires a user token scoped to a tenant who owns the service.
```
x-auth-token: U=<Scoped User Token>
```
### URL Arguments
#### Create SERVICE
- name=_service name  
A service name.  
- verify=_verify url  
A url to defines a dynamic resource. See the [+SERVICE Usage](usage_service.html) page for the dynamic resource.

#### Add MEMBER to SERVICE 
- tenant=_<tenant name> or [<tenant name>, ...]_  
A tenant as a service member or an array of tenants as service members
- clear_tenant=_true/false_  
True with a tenant if deletes a tenant from the service member. True without a tenant if delete all tenants from the service member after adding the tenant.

#### Modify VERIFY URL
- verify=_verify URL_  
A url to defines a dynamic resource or a string literal or a boolean literal. See the [+SERVICE Usage](usage_service.html) page for the dynamic resource.

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
True if success. False otherwise.
- message  
An error message if the result if false

## GET
Lists the information relevant to the service.  A user token scoped to the service owner's tenant in the HTTP request header is required.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service/_service name_

### Header
Requires a user token scoped to a tenant.

```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    service:    {
        verify:     <verify url> or <static string> or <false>
        tenant:	[
            <tenant yrn full path>,
            ...
        ]
    }
}
```
- result  
True if success. False otherwise.
- message  
An error message if the result if false
- service:verify  
A url to defines a dynamic resource or a string literal or a boolean literal. See the [+SERVICE Usage](usage_service.html) page for the dynamic resource.
- service:tenant  
A tenant in [YRN](detail_various.html) form as a service member or an array of tenants [YRN](detail_various.html) as service members


## HEAD
Validates a service, including the service member.  A user token scoped to the service owner's tenant in the HTTP request header is required.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service/_service name_
http(s)://_API SERVER:PORT_/v1/service/_service name_?_urlarg_

### Header
Requires a user token scoped to a tenant who owns the service.
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
#### Validate MEMBER(Optional)
- tenant=_tenant name_  
A tenant as a service member or an array of tenants as service members.

### Response status
204、40x

### Response Body(JSON)
Empty

## DELETE
Provides the following functions. A user token scoped to the service owner's tenant in the HTTP request header is required.

* Deletes a service
* Deletes a service member(or a tenants)

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/service/_service name_
http(s)://_API SERVER:PORT_/v1/service/_service name_?_urlarg_

### Header
Requires a user token scoped to a tenant who owns the service.
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
#### Delete MEMBER(Optional)
- tenant=_tenant name(optional)_  
A tenant as a service member. Deleting the member(or tenant) who owns the service is impossible.

### Response status
204、40x

### Response Body(JSON)
Empty

