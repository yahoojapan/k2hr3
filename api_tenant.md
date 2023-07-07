---
layout: contents
language: en-us
title: TENANT API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_tenantja.html
lang_opp_word: To Japanese
prev_url: api_policy.html
prev_string: POLICY API
top_url: api.html
top_string: REST API
next_url: api_service.html
next_string: SERVICE API
---

# TENANT API

This page describes the K2HR3 TENANT API. The purpose of the TENANT API is to create and update and get and delete a Local Tenant of K2HR3 Cluster. See the [Feature](feature.html) about the TENANT.

### Note
The TENANT API is an API to operate K2HR3 cluster Local Tenant.  
The TENANT of the K2HR3 system uses tenants cooperated with IaaS (OpenStack tenant/project, Kubernetes namespace).  
If the K2HR3 cluster Local Tenant function is enabled in the K2HR3 REST API configuration(`localtenants` value is `true`), you can create/edit/delete your own TENANT.  

## POST (Create)
Specify Unscoped User Token or Scoped User Token and create a new K2HR3 cluster Local Tenant(TENANT).

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

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
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
- desc  
Specify a description of the K2HR3 cluster Local Tenant(TENANT).  
This value is optional and defaults to the descriptive text if omitted.  
- display  
Specify the display name for the K2HR3 cluster Local Tenant(TENANT) in the K2HR3 Web Application.  
This value can be omitted, and if omitted, the TENANT name is set.  
- users  
Specify the USER names who can use the K2HR3 cluster Local Tenant(TENANT) as an array.  
The USER name indicated by the (Un)Scoped User Token sending this request cab be omit.  
It is necessary to specify the USER name registered in the K2HR3 system, and if the USER is not existed, it is ignored.  
And the USER name can not set as [YRN](detail_variousen.html) full path.  

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
True if success. False otherwise
- message  
An error message if the result if false

## PUT (Create)
Specify Unscoped User Token or Scoped User Token and create a new K2HR3 cluster Local Tenant(TENANT).

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant{?name=...}

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### URL Arguments
- name  
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
- desc  
Specify a description of the K2HR3 cluster Local Tenant(TENANT).  
This value is optional and defaults to the descriptive text if omitted.  
- display  
Specify the display name for the K2HR3 cluster Local Tenant(TENANT) in the K2HR3 Web Application.  
This value can be omitted, and if omitted, the TENANT name is set.  
- users  
Specify the USER names who can use the K2HR3 cluster Local Tenant(TENANT) as an array.  
The USER name indicated by the (Un)Scoped User Token sending this request cab be omit.  
It is necessary to specify the USER name registered in the K2HR3 system, and if the USER is not existed, it is ignored.  
And the USER name can not set as [YRN](detail_variousen.html) full path.  

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
True if success. False otherwise
- message  
An error message if the result if false

## POST (Update)
Specify Unscoped User Token or Scoped User Token and update the K2HR3 cluster Local Tenant(TENANT).

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
If the specified the K2HR3 cluster Local Tenant(TENANT) does not exist, it is failure.  

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
Specify the _ID_ of the K2HR3 cluster Local Tenant(TENANT).  
If the K2HR3 Cluster Local Tenant(TENANT) name and this _ID_ value do not match, it will be failure.  
- desc  
Specify a description of the K2HR3 cluster Local Tenant(TENANT).  
This value is optional and defaults to the descriptive text if omitted.  
- display  
Specify the display name for the K2HR3 cluster Local Tenant(TENANT) in the K2HR3 Web Application.  
This value can be omitted, and if omitted, the TENANT name is set.  
- users  
Specify the USER names who can use the K2HR3 cluster Local Tenant(TENANT) as an array.  
The USER name indicated by the (Un)Scoped User Token sending this request cab be omit.  
It is necessary to specify the USER name registered in the K2HR3 system, and if the USER is not existed, it is ignored.  
And the USER name can not set as [YRN](detail_variousen.html) full path.  

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
True if success. False otherwise
- message  
An error message if the result if false

## PUT (Update)
Specify Unscoped User Token or Scoped User Token and update the K2HR3 cluster Local Tenant(TENANT).

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_{?id=...}

- tenant name  
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
If the specified the K2HR3 cluster Local Tenant(TENANT) does not exist, it is failure.  

### Header
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token> or <Scoped User Token>
```

### URL Arguments
- id  
Specify the _ID_ of the K2HR3 cluster Local Tenant(TENANT).  
If the K2HR3 Cluster Local Tenant(TENANT) name and this _ID_ value do not match, it will be failure.  
- desc  
Specify a description of the K2HR3 cluster Local Tenant(TENANT).  
This value is optional and defaults to the descriptive text if omitted.  
- display  
Specify the display name for the K2HR3 cluster Local Tenant(TENANT) in the K2HR3 Web Application.  
This value can be omitted, and if omitted, the TENANT name is set.  
- users  
Specify the USER names who can use the K2HR3 cluster Local Tenant(TENANT) as an array.  
The USER name indicated by the (Un)Scoped User Token sending this request cab be omit.  
It is necessary to specify the USER name registered in the K2HR3 system, and if the USER is not existed, it is ignored.  
And the USER name can not set as [YRN](detail_variousen.html) full path.  

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
True if success. False otherwise
- message  
An error message if the result if false

## GET (List)
Specify Unscoped User Token or Scoped User Token and list the K2HR3 cluster Local Tenant(TENANT).  
The list of TENANTs that can be obtained is limited to the TENANT that the USER is permitted to use.  

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant{?expand=true/false}

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL argument
- expand=_true or false_
Specifies whether to expand the list of TENANTs.  
Specify _true_ as this value to expand.  
When specify _true_, it contains all information for each TENANT.  

### Response status
200、40x

### Response Body(JSON) 
- 展開する場合（expand=true）  
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
- 展開しない場合（expand=false）  
```
{
    result:   <true/false>
    message:  <null or error message string>
    tenants:  [<tenant name>, ...]
}
```
- result  
True if success. False otherwise
- message  
An error message if the result if false
- tenants  
An array of K2HR3 cluster Local Tenants(TENANTs).  
When expanding(`expand=true`), the TENANT information is returned as an array.  
If not expanded(`expand=false`), returns the TENANT name as an array.  
- tenants[*]:name  
The TENANT name is set.  
- tenants[*]:id  
The TENANT _ID_ is set.  
- tenants[*]:desc  
The description of TENANT is set.  
- tenants[*]:display  
The display name of TENANT is set.  
- tenants[*]:user  
Set the array of USER names who are permitted to use the TENANT.  

## GET (Tenant)
Specify Unscoped User Token or Scoped User Token and get the K2HR3 cluster Local Tenant(TENANT) information.  
The list of TENANTs that can be obtained is limited to the TENANT that the USER is permitted to use.  

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
If the specified the K2HR3 cluster Local Tenant(TENANT) does not exist, it is failure.  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
200、40x

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
True if success. False otherwise
- message  
An error message if the result if false
- tenant:name  
The TENANT name is set.  
- tenant:id  
The TENANT _ID_ is set.  
- tenant:desc  
The description of TENANT is set.  
- tenant:display  
The display name of TENANT is set.  
- tenant:user  
Set the array of USER names who are permitted to use the TENANT.  

## HEAD
Specify Unscoped User Token or Scoped User Token and check the existence of the K2HR3 cluster Local Tenant(TENANT).  
The list of TENANTs that can be obtained is limited to the TENANT that the USER is permitted to use.  

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_

- tenant name  
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
If the specified the K2HR3 cluster Local Tenant(TENANT) does not exist, it is failure.  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)
Empty

## DELETE
Specify Unscoped User Token or Scoped User Token and make the USER unavailable to the K2HR3 cluster Local Tenant(TENANT).  
As a result of this process, if there are no more USER that can use the K2HR3 cluster Local Tenant(TENANT), the TENANT will be deleted.  
The list of TENANTs that can be obtained is limited to the TENANT that the USER is permitted to use.  

#### Note
All TENANT APIs require an Unscoped User Token or a Scoped User Token.  
If a Scoped User Token is specified, the tenant indicated by that token will be ignored and only the USER information will be used as with the Unscoped User Token.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/tenant/_tenant name_{?id=<tenant id>}

- tenant name  
Specify the K2HR3 cluster Local Tenant(TENANT) name.  
If this value does not have the `local@` prefix, it will automatically be changed to the TENANT name with the `local@` prefix.  
If the specified the K2HR3 cluster Local Tenant(TENANT) does not exist, it is failure.  

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL argument
- id  
Specify the _ID_ of the K2HR3 cluster Local Tenant(TENANT).  
If the K2HR3 Cluster Local Tenant(TENANT) name and this _ID_ value do not match, it will be failure.  

### Response status
204、40x

### Response Body(JSON)
Empty
