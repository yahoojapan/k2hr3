---
layout: contents
language: en-us
title: RESOURCE API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_resourceja.html
lang_opp_word: To Japanese
prev_url: api_role.html
prev_string: ROLE API
top_url: api.html
top_string: REST API
next_url: api_policy.html
next_string: POLICY API
---

# RESOURCE API

This page describes the K2HR3 RESOURCE API. The purpose of the RESOURCE API is to create and update and get and delete a K2HR3 RESOURCE. See the [Basic Usage](usage_base.html) about the K2HR3 RESOURCE.

## POST

Creates or updates a K2HR3 RESOURCE.

* Creates or updates a RESOURCE(a scoped user token is required)
* Updates a RESOURCE(a user token is required)
* Updates a RESOURCE 
* Creates alias settings(a scoped user token is required)

### Endpoint(URL)
#### If a scoped user token request header is specified
http(s)://_API SERVER:PORT_/v1/resource
#### If a role token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_
#### No token specified in the request headers
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_

### Header
#### Scoped user token
The following header contains a scoped user token.
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### A role Token
The following header contains a role token.
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No tokens
The following header contains no token.
```
Content-Type: application/json
```
### Request Body
#### A Scoped User Token 
```
{
    resource:    {
        name:    <resource name>
        type:    <data type>
        data:    <resource data>
        keys:    {
            foo:    bar,
            ...
        }
        alias:    [
            <resource yrn full path>,
            ...
        ]
    }
}
```
- name  
A resource name in [YRN](detail_various.html) form.
- type  
A resource type of the resource. A valid value is "string", "object", null, or undefined. The existing value will not be changed if this value is null or undefined.
- data  
A data of the resource. If the resource type is "string", data must be a string literal. If the resource type is "object", data must be a JSON object. The existing value will not be changed if this value is null or undefined.
- keys  
A pair of a key and a value of the resource. The existing value will not be changed if this value is null or undefined.
- alias  
An resource name aliased to in [YRN](detail_various.html) form. The value can be an array of aliases or comma separated string if multiple aliases. The value can be a string if the alias is single. The existing value will not be changed if this value is null or undefined.


#### Role Token
```
{
    resource:    {
        type:    <data type>
        data:    <resource data>
        keys:    {
            foo:    bar,
            ...
        }
    }
}
```
- type  
A resource type of the resource. A valid value is "string", "object", null, or undefined. The existing value will not be changed if this value is null or undefined.
- data  
A data of the resource. If the resource type is "string", data must be a string literal. If the resource type is "object", data must be a JSON object. The existing value will not be changed if this value is null or undefined.
- keys  
A pair of a key and a value of the resource. The existing value will not be changed if this value is null or undefined.

#### No tokens
```
{
    resource:    {
        port:    <port number>
        cuk:     <container unique key>
        role:    <role full yrn>
        type:    <data type>
        data:    <resource data>
        keys:    {
            foo:    bar,
            ...
        }
    }
}
```
- port  
A port number. A role member is identified by this value and the source IP address. Undefined (including null value) will be interpreted as *any*.
- cuk  
This parameter is reserved for future use. Setting this currently has no effect.
- role  
A role name in [YRN](detail_various.html)form. A role member is identified by this value and the source IP address.
- type  
A resource type of the resource. A valid value is "string", "object", null, or undefined. The existing value will not be changed if this value is null or undefined.
- data  
A data of the resource. If the resource type is "string", data must be a string literal. If the resource type is "object", data must be a JSON object. The existing value will not be changed if this value is null or undefined.
- keys  
A pair of a key and a value of the resource. Undefined(including null value) will not affect the existing value.

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


## PUT

Creates or updates a K2HR3 RESOURCE.

Note: The POST method can be used here as well

* Creates or updates a RESOURCE(a scoped user token is required)
* Updates a RESOURCE(a user token is required)
* Updates a RESOURCE 
* Creates alias settings(a scoped user token is required)

### Endpoint(URL)
#### If a scoped user token request header is specified
http(s)://_API SERVER:PORT_/v1/resource?_urlarg_
#### If a role token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### No token specified in the request headers
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No Tokens
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token specified in request headers
- name=_resource name_  
A resource name in [YRN](detail_various.html) form.
- type=_data type_  
A resource type of the resource. A valid value is "string", "object", null, or undefined. The existing value will not be changed if this value is null or undefined.
- data=_resource data_  
A data of the resource. If the resource type is "string", data must be a string literal. If the resource type is "object", data must be a JSON object. The existing value will not be changed if this value is null or undefined.
- keys=_json key value object_  
A pair of a key and a value of the resource. The existing value will not be changed if this value is null or undefined.
- alias=_json alias array_
  - An alias of the resource. Each alias value is in [YRN](detail_various.html) form. The value can be an array of aliases or comma separated string if multiple aliases. The value can be a string if the alias is single. The existing value will not be changed if this value is null or undefined.


#### Role Token specified in request headers
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", null, or undefined. The existing value will not be changed if this value is null or undefined.
- data=_resource data_  
  - A data of the resource. If the resource type is "string", data must be a string literal. If the resource type is "object", data must be a JSON object. The existing value will not be changed if this value is null or undefined.
- keys=_json key value object_  
  - A pair of a key and a value of the resource. The existing value will not be changed if this value is null or undefined.


#### No Token in request headers
- port=_port number_  
  - A port number. A role member is identified by this value and the source IP address. Undefined (including null value) will be interpreted as *any*.
- cuk=_container unique key_  
  - This parameter is reserved for future use. Setting this currently has no effect.
- role=_yrn full role path_  
  - A role name in [YRN](detail_various.html)form. A role member is identified by this value and the source IP address.
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", null, or undefined. The existing value will not be changed if this value is null or undefined.
- data=_resource data_  
  - A data of the resource. If the resource type is "string", data must be a string literal. If the resource type is "object", data must be a JSON object. The existing value will not be changed if this value is null or undefined.
- keys=_json key value object_  
  - A pair of a key and a value of the resource. Undefined(including null value) will not affect the existing value.


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


## GET

Lists all available resources.

* Lists all available resources if a scoped user token request header is specified.
  * The resource data can be the data itself or the alias to the resource data.
* Lists the requested resource or the data of the requested key if a roll token request header is specified or no token specified in the request headers

### Endpoint(URL)
#### If a scoped user token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### If a role token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### No token specified in the request headers
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### Token
```
Content-Type: application/json
```

### URL Arguments
#### If a scoped user token request header is specified
- expand=_true or false_  
  - Indicates whether the alias value should be expanded. If set to true, aliased value shows, If set to false, only alias name shows. Default is true.

- service=_service name_
  - A service name. If the service name is provided, the RESOURCE API lists the all resources under the service in [YRN](detail_various.html) form. The RESOURCE API will match them with the requested resource in the URL path in [YRN](detail_various.html) form.

#### If a role token request header is specified
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", "keys".
- keyname=_key name_
  - A key name. You must also specify the type with "keys".
- service=_service name_
  - A service name. If the service name is provided, the RESOURCE API lists the all resources under the service in [YRN](detail_various.html) form. The RESOURCE API will match them with the requested resource in the URL path in [YRN](detail_various.html) form.

#### No token specified in the request headers
- port=_port number_  
  - A port number. A role member is identified by this value and the source IP address. Undefined (including null value) will be interpreted as *any*.
- cuk=_container unique key_  
  - This parameter is reserved for future use. Setting this currently has no effect.
- role=_yrn full role path_  
  - A role name in [YRN](detail_various.html)form. A role member is identified by this value and the source IP address.
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", "keys".
- keyname=_key name_
  - A key name. You must also specify the type with "keys".
- service=_service name_
  - A service name. If the service name is provided, the RESOURCE API lists the all resources under the service in [YRN](detail_various.html) form. The RESOURCE API will match them with the requested resource in the URL path in [YRN](detail_various.html) form.


### Response status
200、40x

### Response Body(JSON)
#### If a scoped user token request header is specified
```
{
    result:     <true/false>
    message:    <null or error message string>
    resource:   {
        string:     <string>,
        object:     <object>,
        keys:       <object>,
        aliases:    <array>
    }
}
```
- result  
  - True if success. False otherwise
- message  
  - An error message if the result if false
- resource:string  
  - A resource name in a string literal
- resource:object  
  - A resource object
- resource:keys  
  - An object of a pair of a key and a value of the resource
- resource:aliases  
  - An array of the alias of the resource

#### a role token request header is specified or No token specified in the request headers
```
{
    result:     <true/false>
    message:    <null or error message string>
    resource:   <data>
}
```
- result  
True if success. False otherwise
- message  
An error message if the result if false
- resource  
A resource


## HEAD
Validates that a RESOURCE (including in a SERVICE if specified) exists.

### Endpoint(URL)
#### If a scoped user token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### If a role token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### No token specified in the request headers 
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No token
```
Content-Type: application/json
```

### URL Arguments
#### If a scoped user token request header is specified
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", "keys".
- keyname=_key name_
  - A key name. You must also specify the "type" url argument with "keys".
- service=_service name_
  - A service name. If the service name is provided, the RESOURCE API lists the all resources under the resource in the service in [YRN](detail_various.html) form. The RESOURCE API will validate them with the requested resource in the URL path in [YRN](detail_various.html) form.

#### If a role token request header is specified
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", "keys".
- keyname=_key name_
  - A key name. You must also specify the "type" url argument with "keys".
- service=_service name_
  - A service name. If the service name is provided, the RESOURCE API lists the all resources under the resource in the service in [YRN](detail_various.html) form. The RESOURCE API will validate them with the requested resource in the URL path in [YRN](detail_various.html) form.

#### No token specified in the request headers
- port=_port number_  
  - A port number. A role member is identified by this value and the source IP address. Undefined (including null value) will be interpreted as *any*.
- cuk=_container unique key_  
  - This parameter is reserved for future use. Setting this currently has no effect.
- role=_yrn full role path_  
  - A role name in [YRN](detail_various.html)form. A role member is identified by this value and the source IP address.
- type=_data type_  
  - A resource type of the resource. A valid value is "string", "object", "keys".
- keyname=_key name  
  - A key name. You must also specify the "type" url argument with "keys".
- service=_service name_
  - A service name. If the service name is provided, the RESOURCE API lists the all resources under the resource in the service in [YRN](detail_various.html) form. The RESOURCE API will validate them with the requested resource in the URL path in [YRN](detail_various.html) form.



### Response status
204、40x

### Response Body(JSON)
Empty

## DELETE
Deletes a part of a RESOURCE or a RESOURCE.

* Deletes a RESOURCE(a scoped user token is required)
* Deletes a part of a RESOURCE(no token required)

### Endpoint(URL)
#### If a scoped user token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### If a role token request header is specified
http(s)://_API SERVER:PORT_/v1/resource/_resource path or yrn full resource path_?_urlarg_
#### No token specified in the request headers
http(s)://_API SERVER:PORT_/v1/resource/_yrn full resource path_?_urlarg_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No Token
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token
- type=_data type_  
  - A resource type of the resource. A valid value is "anytype", “string”, “object”, “keys”, "aliases", null or undefined.
  - "anytype" will be will be interpreted as the "type" of the RESOURCE.
  - Undefined and null will be will be interpreted as everything, which means delete all of the RESOURCE.
- keynames=_key name_  
  - A key name. You must also specify the “type” url argument with “keys”.
  - The value can be a string literal of an JSON array object.
- aliases=_json alias array_  
  - alias names. You must also specify the “type” url argument with “aliases”.
  - The value can be an array of aliases or comma separated string if multiple aliases. The value can be a string if the alias is a single value.
#### Role Token
- type=_data type_  
  - A resource type of the resource. A valid value is "anytype", “string”, “object”, “keys”.
  - "anytype" will be will be interpreted as the "type" of the RESOURCE.
- keynames=_key name_  
  - A key name. You must also specify the “type” url argument with “keys”.
  - The value can be a string literal of an JSON array object.
#### No token
- port=_port number_  
  - A port number. A role member is identified by this value and the source IP address. Undefined (including null value) will be interpreted as *any*.
- cuk=_container unique key_  
  - This parameter is reserved for future use. Setting this currently has no effect.
- role=_yrn full role path_  
  - A role name in [YRN](detail_various.html)form. A role member is identified by this value and the source IP address.
- type=_data type_  
  - A resource type of the resource. A valid value is "anytype", "string", "object", "keys".
  - "anytype" will be will be interpreted as the "type" of the RESOURCE.
- keyname=_key name  
  - A key name. You must also specify the "type" url argument with "keys".
  - The value can be a string literal of an JSON array object.

### Response status
204、40x

### Response Body(JSON)
Empty

