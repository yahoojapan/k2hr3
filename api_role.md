---
layout: contents
language: en-us
title: ROLE API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_roleja.html
lang_opp_word: To Japanese
prev_url: api_list.html
prev_string: LIST API
top_url: api.html
top_string: REST API
next_url: api_resource.html
next_string: RESOURCE API
---

# ROLE API

This page describes the K2HR3 ROLE API. The purpose of the ROLE API is to create and update and get and delete a K2HR3 ROLE. See the [Basic Usage](usage_base.html) about the K2HR3 ROLE in the K2HR3.

## POST(Create ROLE)

Creates a K2HR3 ROLE.

### Endpoint(URL)

http(s)://_API SERVER:PORT_/v1/role

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Request Body
```
{
    role:    {
        name:        <role name or yrn full path>
        policies:    [
                         <policy yrn full path>,
                         ...
                     ]
        alias:       [
                         <role yrn full path>,
                         ...
                     ]
    }
}
```

- name  
  - A role name in a string literal. The role will belongs to the scoped tenant(project).
  - A role name in [YRN](detail_various.html) form is also acceptable. In this case, the ROLE API will validate both the scoped tenant in [YRN](detail_various.html) form and the role name in [YRN](detail_various.html) form.
- policies  
  - A policy rule for the role
  - A policy rule name should be in [YRN](detail_various.html) form or in a string literal.
  - An array of policy rules is acceptable.
  - Empty policy rule with a role is acceptable. In this case, the policy rule of the role will be empty.
  - undefined or null value is also acceptable. In this case, the current policy rule settings of the role will not updated.
- alias  
  - An alias to the other roles. 
  - An alias should be in [YRN](detail_various.html) form or in a string literal.
  - An array of aliases is acceptable.
  - Empty alias with a role is acceptable. In this case, the alias of the role will be empty.
  - undefined or null value is also acceptable. In this case, the current alias settings of the role will not updated.

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


## PUT(Create ROLE)

Creates a K2HR3 ROLE.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- name=_role name or yrn full path_  
  - A role name in a string literal. The role will belongs to the scoped tenant(project).
  - A role name in [YRN](detail_various.html) form is also acceptable. In this case, the ROLE API will validate both the scoped tenant in [YRN](detail_various.html) form and the role name in [YRN](detail_various.html) form.
- policies=_policy yrn full path_  
  - A policy rule for the role
  - A policy rule name should be in [YRN](detail_various.html) form as a JSON object or in a string literal.
  - An array of policy rules is acceptable.
  - Empty policy rule with a role is acceptable. In this case, the policy rule of the role will be empty.
  - undefined or null value is also acceptable. In this case, the current policy rule settings of the role will not updated.
- alias=_role yrn full path_  
  - An alias to the other roles. 
  - An alias should be in [YRN](detail_various.html) form as a JSON object or in a string literal.
  - An array of aliases is acceptable.
  - Empty alias with a role is acceptable. In this case, the alias of the role will be empty.
  - undefined or null value is also acceptable. In this case, the current alias settings of the role will not updated.

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


## POST(Add HOST to ROLE)

Adds a member(aka a hostname or an IP address) to a K2HR3 ROLE.

### Endpoint(URL)

#### Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path_
#### Role Token
http(s)://_API SERVER:PORT_/v1/role/_yrn full path to role_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token

API server will add a source IP address to a role if it finds a role token in request parameters.

```
Content-Type: application/json
x-auth-token: R=<Role Token>
```

### Request Body

#### Scoped User Token

One request body includes only one host.

```
{
    host:    {
        host:            <hostname / ip address>
        port:            <port number>
        cuk:             <container unique key: reserved>
        extra:           <extra string data>
    }
    clear_hostname:      <true/false>
    clear_ips:           <true/false>
}
```

One request body includes multiple hosts.

```
{
    host:    [
        {
            host:        <hostname / ip address>
            port:        <port number>
            cuk:         <container unique key: reserved>
            extra:       <extra string data>
        },
        ...
    ]
    clear_hostname:      <true/false>
    clear_ips:           <true/false>
}
```

#### Role Token
```
{
    host:    {
        port:            <port number>
        cuk:             <container unique key: reserved>
        extra:           <extra string data>
    }
}
```

#### Parameters

- host  
  - Must a FQDN or an IP address. You can write multiple hostnames in a regex-like form. 
  - ex) 'dkc[1-2].example.com' means dkc1.example.com and dkc2.example.com.
- port  
  - A port number.
  - undefined, null value or "0" value is identical with "any".
- cuk
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey. 
- extra  
  - extra information of the host. undefined or null value is acceptable.
- clear_hostname  
  - True if delete all hostnames.
- clear_ips  
  - True if delete all IP addresses.

### Note: Port assignment

You need to pay special attention in case you add a hostname or IP address that already exists with a different port.

- An existing hostname or IP address with non-ANY port will NOT be deleted if you add a hostname or IP address with non-ANY port.
- An existing hostname or IP address with ANY port will be deleted if you add a hostname or IP address with non-ANY port.
- An existing hostname or IP address with non-ANY port will be deleted if you add a hostname or IP address with ANY port.

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


## PUT(Add HOST to ROLE)

Adds a member(aka a hostname or an IP address) to a K2HR3 ROLE.

### Endpoint(URL)
#### Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path_?_urlarg_
#### Role Token
http(s)://_API SERVER:PORT_/v1/role/_yrn full path to role_?_urlarg_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### Role Token

API server will add a source IP address to a role if it finds a role token in request parameters.

```
Content-Type: application/json
x-auth-token: R=<Role Token>
```

### URL Arguments
#### Scoped User Token
- host=_hostname or ip address_  
  - Must a FQDN or an IP address. You can write multiple hostnames in a regex-like form. 
  - ex) 'dkc[1-2].example.com' means dkc1.example.com and dkc2.example.com.
- port=_port number_  
  - A port number.
  - undefined, null value or "0" value is identical with "any".
- cuk=_container unique key_  
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey.
- extra=_extra string data_  
  - extra information of the host. undefined or null value is acceptable.

#### Role Token

- port=_port number_  
  - A port number.
  - undefined, null value or "0" value is identical with "any".
- cuk=_container unique key_  
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey.
- extra=_extra string data_  
  - extra information of the host. undefined or null value is acceptable.

### Note

If you add a hostname or IP address that already exists with a different port, you should know the followings:

- An existing hostname or IP address with non-ANY port will NOT be deleted if you add a hostname or IP address with non-ANY port.
- An existing hostname or IP address with ANY port will be deleted if you add a hostname or IP address with non-ANY port.
- An existing hostname or IP address with non-ANY port will be deleted if you add a hostname or IP address with ANY port.

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


## GET(Show ROLE details)
Shows details for a role.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- expand=_true or false_  
  - False will not show aliased roles.(default)
  - True will show aliased roles.

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    role:       {
        policies:   array,
        aliases:    array
        hosts: {
            hostnames: [
                "<hostname> <port> <cuk>",
                ...
            ],
            ips: [
                "<ip address> <port> <cuk>",
                ...
            ]
        }
    }
}
```
- result  
True if success. False otherwise
- message  
An error message if the result if false.
- role:policies  
An array of policy objects.
- role:aliases  
An array of alias objects if the 'expand' request parameter is false
- role:hosts  
An array of hostname and IP address objects if the 'expand' request parameter is false.

## GET(Create ROLE Token)

Create a role token. Role API creates a role token in the following three cases.

- The source IP address has member assignment on the role.
* A scoped user token exists in request parameters.
* A role token exists in request parameters.

### Endpoint(URL)
#### A Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/token/_role path or yrn full role path_
#### A Role Token
http(s)://_API SERVER:PORT_/v1/role/token/_role path or yrn full role path_
#### No Tokens
http(s)://_API SERVER:PORT_/v1/role/token/_yrn full role path_

### Header
#### A Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### A Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No Tokens
```
Content-Type: application/json
```

### Response status
200、40x

### Response Body(JSON)
```
{
    result:       <true/false>
    message:      <null or error message string>
    token:        <role token string>
    registerpath: <URI path for userdata API>
}
```
- result  
True if success. False otherwise
- message  
An error message if the result if false.
- token  
A role token
- registerpath  
A string by using JSON stringify() method for the following json object. 
```
{
    role:         <role name>
    token:        <role token string>
}
```
In addition, the string is encrypted, base64 encoded and encodeURI（+'/',':','?'） encoded. The string is used as a part of userdata API（/v1/userdata） URI Path string.

## HEAD(Validate ROLE)
Validates the client's source IP address, a scoped user token or a role token.

* Check whether the source IP address has member assignment on the role in [YRN](detail_various.html) form.
* Check whether the requested role exists and the user identified by the scoped user token can manage the role.
* Check whether the requested role identified by the role token exists.


### Endpoint(URL)
#### A Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### A Role Token
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### A No Tokens
http(s)://_API SERVER:PORT_/v1/role/_yrn full role path_

### Header
#### A Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### A Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No Tokens
```
Content-Type: application/json
```

### Response status
204、40x

### Response Body(JSON)
The server will not return a message-body in the response in the HEAD method.


## DELETE(Delete ROLE)

Deletes a role, a hostname(or an IP address) from a role, a role token.

* Delete the source IP address from the role in the requested URI path if the IP address has member assignment on the role in [YRN](detail_various.html) form.
* Delete a requested role, a requested hostname(or an IP address) from a requested role with a scoped user token parameter.
* Disable a requested role token if a role in the requested URI path exists.


### Note: Port assignment

You need to pay special attention in case you request to delete a hostname or IP address with a port.

- An existing hostname or IP address with ANY port will be deleted.
- An existing hostname or IP address with a different port will NOT be deleted.

This means that if an existing hostname or IP address with a port matches with requested hostname or IP address with a port port will be deleted.

### Endpoint(URL)
#### A Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_?_urlarg_
#### A Role Token
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_
#### No Token
http(s)://_API SERVER:PORT_/v1/role/_yrn full role path_?_urlarg_

### Header
#### A Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### A Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```
#### No Token
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token(Delete ROLE)

A role identified by the scoped user token will be deleted if ROLE API find no URL args.

#### Scoped User Token(Delete Hostnames or IP addresses)
- host=_hostname or ip address_  
  - Must be a FQDN or an IP address. You can write multiple hostnames in a regex-like form. 
  - ex) 'dkc[1-2].example.com' means dkc1.example.com and dkc2.example.com.
- port=_port number_  
  - A port number. undefined, null or "0" value is acceptable.
- cuk=_container unique key_  
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey. 

#### A Role Token
Empty

#### No Token
- port=_port number_  
  - A port number. undefined, null or "0" value is acceptable.
  - If the requested port number is undefined, null or "0" value, ROLE API will delete a hostname with 'ANY' port.


### Response status
204、40x

### Response Body(JSON)
Empty.

## DELETE(Delete Hostname or IP address)

Delete an IP address(or a hostname).

* [K2HR3 OpenStack Notification Listener](detail_osnl.html) will invoke this API.
* The IP addresses to be deleted in this API should be added by using OpenStack 'Customization Script' in Launch Instance form.
* *CUK*, which is semantically same with OpenStack Instance ID, is required. You will find the ID in OpenStack Horizon UI.
  * ROLE API will delete all IP addresses with the same *CUK*.
  * *extra* should be *openstack-auto-v1*.

In addition, to allow the specific role members to delete IP addresses, add the client host in 'delhostrole' role member. Make sure that the following settings exists in your K2HR3 API configuration file.
```
{
  'k2hr3admin': {
     'tenant':      'admintenant',
     'delhostrole': 'delhostrole'
  }
}
```

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/role?_urlarg_

### Header
```
Content-Type: application/json
```

### URL Arguments
#### cuk
*CUK*（Cloud Unique Key = *Instance ID*）, which is semantically same with OpenStack Instance ID, is required. You will find the ID in OpenStack Horizon UI. ROLE API will delete all IP addresses with the same *CUK*.

#### host
IP addresses in a JSON array object or in a string literal.

* ROLE API will delete IP addresses matched with requested IP addresses and the requested *CUK*.
* ROLE API will delete all IP addresses matched with the requested *CUK* if no IP addresses are requested.
  * The 'host' parameter should be optional because an IP address is assigned with only one instance ID.
  


#### extra
*openstack-auto-v1* It is currently a fixed value because We support 'OpenStack' only.

### Response status
204、40x

### Response Body(JSON)
Empty
