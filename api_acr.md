---
layout: contents
language: en-us
title: ACR API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_acrja.html
lang_opp_word: To Japanese
prev_url: api_service.html
prev_string: SERVICE API
top_url: api.html
top_string: REST API
next_url: api_userdata.html
next_string: USERDATA API
---

# ACR API

This page describes the K2HR3 ACR(ACCESS CROSS ROLE) API. The purpose of the ACR API is to provide the +SERVICE functionality. See the [Service Usage](usage_service.html) for the +SERVICE details.

## POST
Adds a tenant as a service member to the service by creating the **yrn:yahoo:_service name_::_tenant name_**.

The ACR API internally adds **acr_role**, **acr_policy**, and the resources owned by the service owner to the service member.

## Resource in service

The service owner provides a resource as a service to the service members. The resource value is a external url(VERIFY URL) or a static JSON object. Adding a new resource to the service means that the owner starts providing the resource to the service member. When the service owner defines the resource, the ACR API requires a token without an explicit scope of authorization or a tenant-scoped token. See the [Usage +SERVICE](usage_service.md) page for the resource details. 

Before providing a new resource to a tenant as a service member, the service owner must add the tenant to the service member. . Here is the flow to add a resource to the service.
- Firstly a client requests the POST API. Then, the POST API generates a tenant-scoped token from the given token. 
- Secondary, it reaches the url that the service owner defines with a valid token only during the read request. 
- Then, the program on the service owner side will validate the token and get the user information identified by the token by invoking ACR GET API.
- Then, it creates the data that associated with the user, the tenant of a service member, and the service. 
- Then, it returns the newly created resource data to K2HR3. 
- Finally, K2HR3 associates the data with the service member.

The value of the "VERIFY URL" variable in the service definition settings is not always in URL form but it is alternatively a static data. In this case, K2HR3 will skip some steps above and associate the static data with the service member.

The following figure shows the overview of the flow.
![K2HR3 REST API - ACR Register Flow](images/api_acr_register_flow.png)

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/acr/_service name_

### Header
#### Unscoped token specified
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token>
```
#### Tenant scoped token specified
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
### Request Body
#### Unscoped token specified in request header
If a token is unscoped, configure the following request body. The API internally generates a tenant-scoped token from the given token.
```
{
    "tenant":  <tenant name>
}
```
- tenant  
A tenant as a service member.

#### Tenant scoped token specified in request header
If you specify a tenant token in request header, configure the empty request body.

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
Adds a tenant as a service member to the service by creating the **yrn:yahoo:_service name_::_tenant name_**.

K2HR3 ACR API internally adds **acr_role**, **acr_policy**, and the resources owned by the service owner to the service member.

The service owner provides a resource as a service to the service members. The resource value is a external url(VERIFY URL) or a static JSON object. Adding a new resource to the service means that the owner starts providing the resource to the service member. When the service owner defines the resource, the ACR API requires a token without an explicit scope of authorization or a tenant-scoped token. See the [Usage +SERVICE](usage_service.md) page for the resource details. 

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/acr/_service name_  
http(s)://_API SERVER:PORT_/v1/acr/_service name_?_urlarg_

### Header
#### Unscoped token specified
```
Content-Type: application/json
x-auth-token: U=<Unscoped User Token>
```
#### Tenant scoped token specified
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
### URL Arguments
#### Unscoped token specified in request header
- tenant=_tenant name_  
A tenant that the token scoped to. If a token is unscoped, configure the following request body. The API internally generates a tenant-scoped token from the given token.

#### Tenant scoped token specified in request header
If you specify a tenant token in request header, configure the empty request body.

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
Shows credential details and gets available resources. 

To show credential details, clients must authenticate before making a request, which means a token is required. The GET API is for service owners who configure the external url(VERIFY URL) to define a dynamic resource. The POST/PUT API invokes the GET API to associate a member with a service only if the service owner optionally configure the external url(VERIFY URL). The process takes two steps. At first, The POST/PUT API internally reaches the external url(VERIFY URL) with a valid token only during the read request. Then, the program on the service owner side will validate the token and get the user information identified by the token by invoking the GET API. 

To get available resources, the GET API requires an IP address and a K2RH3 ROLE name to determine whether a request should be allowed using Role Based Access Control. The request is tokenless. The GET API is for service owners to delegate authorization and authentication of their system to K2HR3. Delegating authorization and authentication simplifies the service member's API usage. A service member usually need two steps to use the service owner's system. Firstly, a service member obtains a token by using K2HR3 Token API. Secondary it sends a request with the token to a service owner's system. If service owners implements their system by using the GET API, service members don't need to authenticate before making a request because service owners will delegate authentication and authorization to K2HR3. Note that in this case, service owners must installs the K2HR3 ROLE associated with each IP addresses optionally including port numbers. If a service member's host is a member of multiple K2HR3 ROLE, the service member should pass the K2HR3 ROLE name it want to be authorized.

The following figure shows the request overview.
![K2HR3 REST API - ACR GET for one step](images/api_acr_get_onestep.png)

### Endpoint(URL)
#### Show credential details
http(s)://_API SERVER:PORT_/v1/acr/_service name_

#### Get available resources
http(s)://_API SERVER:PORT_/v1/acr/_service name_?_urlarg_

### Header
#### Show credential details
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

#### Get available resources
Empty

### URL Arguments
#### Show credential details
Empty

#### Get available resources
- cip=_client ip address_  
  - An IP address, which is owned by a service member and the other end IP address of the service owner(a peer IP).
- cport=_client port(optional)_  
  - An port number, which is used to determine the K2HR3 ROLE name of the IP address.
- crole=_client role yrn path_  
  - A K2HR3 ROLE name. If a service member's host is a member of multiple K2HR3 ROLE, the service member should pass the K2HR3 ROLE name it want to be authorized.
- ccuk=_client container unique key_  
  - This parameter is reserved for future use. Setting this currently has no effect.
- sport=_service port(optional)_  
  - A port number of the service owner's host. The IP address of the service owner's host is not required. The peer IP of the API server is used instead.
- srole=_service role yrn path_  
  - A role name assigned to service owner's host
- scuk=_service container unique key_  
  - This parameter is reserved for future use. Setting this currently has no effect.

### Response status
200、40x

### Response Body(JSON)
#### Show credential details
```
{
    result:     <true/false>
    message:    <null or error message string>
    tokeninfo = {
        user:   <user name>
        tenant: <tenant name>
        service:<service name>
    }
}
```
- result  
True if success. False otherwise.
- message  
An error message if the result if false
- tokeninfo:user  
A user identified by the token
- tokeninfo:tenant  
A tenant that the token scoped to.
- tokeninfo:service  
A service name

#### Get available resources
```
{
    result:     <true/false>
    message:    <null or error message string>
    response:   [
        {
            name:       <resource name>
            expire:     <expire>
            type:       <resource type>
            data:       <resource data>
            keys:       {
                foo:    bar
                ...
            }
        },
        ...
    ]
}
```
- result  
True if success. False otherwise.
- message  
An error message if the result if false
- response  
Resources including each resource's name, expiration, type data and keys.

## DELETE
Deletes a tenant member who uses the service. A user token scoped to the tenant is required.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/acr/_service name_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)
Empty
