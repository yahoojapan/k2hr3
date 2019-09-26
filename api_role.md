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
- cuk=_custom unique key_  
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey. 
  - For registering an OpenStack VirtualMachine, specify the **Instance ID**.
  - For registering from a pod of kubernetes, specify the CUK string calculated for registration(automatically calculated by Sidecar provided by the K2HR3 system).
  - Otherwise, specify unspecified or null.
- extra  
  - extra information of the host. You rarely specify this value directly.
  - Specify **openstack-auto-v1** when registering OpenStack VirtualMachine.
  - Specify **k8s-auto-v1** for kubernetes pod registration.
  - undefined or null value is acceptable.
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
- cuk=_custom unique key_  
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey. 
  - For registering an OpenStack VirtualMachine, specify the **Instance ID**.
  - For registering from a pod of kubernetes, specify the CUK string calculated for registration(automatically calculated by Sidecar provided by the K2HR3 system).
  - Otherwise, specify unspecified or null.
- extra  
  - extra information of the host. You rarely specify this value directly.
  - Specify **openstack-auto-v1** when registering OpenStack VirtualMachine.
  - Specify **k8s-auto-v1** for kubernetes pod registration.
  - undefined or null value is acceptable.

#### Role Token

- port=_port number_  
  - A port number.
  - undefined, null value or "0" value is identical with "any".
- cuk=_custom unique key_  
  - A unique id of the host. **cuk** is **C**ontainer **U**inque **K**ey. 
  - For registering an OpenStack VirtualMachine, specify the **Instance ID**.
  - For registering from a pod of kubernetes, specify the CUK string calculated for registration(automatically calculated by Sidecar provided by the K2HR3 system).
  - Otherwise, specify unspecified or null.
- extra  
  - extra information of the host. You rarely specify this value directly.
  - Specify **openstack-auto-v1** when registering OpenStack VirtualMachine.
  - Specify **k8s-auto-v1** for kubernetes pod registration.
  - undefined or null value is acceptable.

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
  - False will not show aliased roles.
  - True will show aliased roles.(default)

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

### URL Arguments(only for Scoped User Token)
- expire = _0 or expiration seconds(decimal) _  
You can specify the expiration date of the RoleToken to be issued in seconds.  
If not specified, the default value(value set in config or 24H will expire) will be used.  
If 0 is specified, a Token has no expiration(exactly 10 years as default, and configurable with config).

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

### Note
#### RoleToken expiration
When issuing with Scoped User Token, it is possible to specify the expiration date. If not specified, the default value is used. (The default value can be specified in config)  
When Role Token is specified, it is issued with the same expiration date as that set for the specified RoleToken.
If Token is not specified, the default value is always used.
#### Reissuing RoleToken
When Role Token is specified, the newly issued RoleToken is the reissued RoleToken, and the specified RoleToken cannot be used (invalid) after the reissue.

## GET (Role Token List)
API to obtain a list of Role Tokens issued for the role. In order to use this API, it is necessary to specify Scoped User Token.

### Endpoint (URL)
#### Scoped User Token specified
http(s)://_APISERVER:PORT_/v1/role/token/list/_role path or yrn full role path_

### Header
#### Scoped User Token specified
```
Content-Type: application/json
x-auth-token: U = <Scoped User Token>
```

### URL Arguments
- expand = _true or false_  
Specify whether to expand the result of acquiring the list of Role Token.  
Expands if omitted (true).

### Response status
200, 40x

### Response Body (JSON)
#### Not expanding
```
{
    result:       <true/false>
    message:      <null or error message string>
    tokens: [
                  <role token striong>,
                  ...
    ]
}
```
#### Expanding
```
{
    result:       <true/false>
    message:      <null or error message string>
    tokens:	{
        <role token string>: {
            date:		  <create date(UTC ISO 8601)>
            expire:		  <expire date(UTC ISO 8601)>
            user:		  <user name if user created this token>
            hostname:	  <hostname if this token was created by host(name)>
            ip:			  <ip address if this token was created by ip>
            port:		  <port number, if specified port when created token>
            cuk:		  <cuk, if specified cuk when created token>
            registerpath: <register path in user data script>
        },
        ...
    }
}
```
- result  
Returns the API processing result as true/false.
- message  
An error message is stored when the processing result is false(failure).
- tokens(if not expanded)  
Returns a Role Token string as an array.
- tokens (if expanded)  
Returns a list of objects with Role Token string as key and attribute information of Role Token as object.

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
Deletes a role.  
Scoped User Token must be specified.

### Endpoint(URL)
#### A Scoped User Token
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
Specify nothing as URL Arguments.  
Note that if URL Arguments such as host are accompanied, it will operate as deleting the role member host.

### Response status
204、40x

### Response Body(JSON)
Empty.

## DELETE(Hostname/IP address deletion-role specification)
This API deletes Hostname or IP address.  
Specify a Scoped User Token or call it from a host that is a member of the role.  
(If you specify the Role Token and call the DELETE method, it will be a different process.)

### Endpoint (URL)
#### Scoped User Token specified
http(s)://_APISERVER:PORT_/v1/role/_role path or yrn full role path_
#### Token not specified
http(s)://_APISERVER:PORT_/v1/role/_yrn full role path_

### Header
#### Scoped User Token
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
#### No Token
```
Content-Type: application/json
```

### URL Arguments
#### Scoped User Token
- host  
Specify the hostanme or IP address to be deleted from the role.
- port  
Specify the port number required to identify the hostanme or IP address to be deleted from the role.  
If no identification is required, it is unspecified or 0.
- cuk=_custom unique key_  
Specify CUK required to specify the hostanme or IP address to be deleted from the role.  
When registering an OpenStack VirtualMachine, specify its **Instance ID**. When registering from a pod of kubernetes, specify the CUK string calculated for registration (automatically calculated by Sidecar provided by the K2HR3 system).  
If it is not necessary to specify, it is unspecified or null(unspecified except for kubernetes).

#### No Token
- port  
Specify the port number required to delete the host (IP address) that sent this request from the role.  
If no identification is required, it is unspecified or 0.
- cuk=_custom unique key_  
Specify the CUK required to delete the host (IP address) that sent this request from the role.  
When registering an OpenStack VirtualMachine, specify its **Instance ID**. When registering from a pod of kubernetes, specify the CUK string calculated for registration (automatically calculated by Sidecar provided by the K2HR3 system).  
If it is not necessary to specify, it is unspecified or null (unspecified except for Kubernetes).

### Response status
204, 40x

### Response Body (JSON)
Empty.

## DELETE(Hostname/IP address deletion - Role not specified)
This API specifies **CUK** (Custom Unique Key) that is specified when the IP address is automatically registered.  
And remove the IP address below the ROLE key registered with the same **CUK**.  

This API is used to delete an automatically registered IP address (or Hostname) from OpenStack and kubernetes.  
K2HR3 supports automatic registration of IP addresses by USER DATA SCRIPT as OpenStack support.  
For kubernetes pod registration, the K2HR3 system offers a dedicated Sidecar.  
These automatic registrations are systems in which each IP address is registered by specifying CUK.  
This API is provided to allow you to delete an IP address by specifying CUK.  

This API is not intended to be used from K2HR3 Web Application or directly using the API.  
This API is called from Neutron Notification Listner which is hooking to RabbitMQ of OpenStack and from deletion logic of Pods by kubernetes.  

For calling this API from OpenStack Neutron Notification Listner is allowed only from the IP address registered in Tenant/Role for which the following settings have been configured as the K2HR3 Web Application config.  
_You can set in default.json or local.json_
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
-cuk = _custom unique key_  
When registering an OpenStack VirtualMachine, specify its **Instance ID**.  
When registering from a pod of kubernetes, specify the CUK string calculated for registration (automatically calculated by Sidecar provided by the K2HR3 system).  
The IP address associated with this value will be deleted.
-host  
This parameter specifies the IP address to be deleted.  
Of the IP addresses associated with **CUK**, only the IP address specified by this parameter is subject to deletion.  
When specifying multiple IP addresses, specify them as a string array in the JSON object.  
For a single IP address, specify a character string.  
If this parameter is not specified and only **CUK** is specified, all IP addresses linked to ** CUK ** will be deleted.  
_When registering with OpenStack or kubernets, it is assumed that there is only one IP address linked to CUK, and it is not usually necessary to specify the host parameter._

### Response status
204, 40x

### Response Body (JSON)
Empty.

## DELETE (RoleToken deletion - Role specified)
API to delete (invalidate) Role Token.  
This API confirms Role Token and the role(specified by the full YRN path), and that the request source IP address is a member of that role.  
And the Role Token Disable.

### Endpoint (URL)
#### Role Token specified
http(s)://_API SERVER:PORT_/v1/role/_role path or yrn full role path_

### Header
#### Role Token
```
Content-Type: application/json
x-auth-token: R=<Role Token>
```

### URL Arguments
-port = _port number_  
Specify the port number required to delete the host (IP address) that sent this request from the role.  
If no identification is required, it is unspecified or 0.

- cuk=_custom unique key_  
Specify the CUK required to delete the host(IP address) that sent this request from the role.  
When registering an OpenStack VirtualMachine, specify its **Instance ID**. When registering from a pod of kubernetes, specify the CUK string calculated for registration (automatically calculated by Sidecar provided by the K2HR3 system).  
If it is not necessary to distinguish the CUK, it will be left unspecified or null. (In the case of kubernetes, it is necessary to specify.)

### Response status
204, 40x

### Response Body (JSON)
Empty.

## DELETE(Delete RoleToken - Role not specified)
API to delete(invalidate) Role Token by specifying Scoped User Token.  
This API is required to manage Role Token and is mainly used from K2HR3 Web Application.

### Endpoint (URL)
#### Role Token specified
http(s)://_API SERVER:PORT_/v1/role/token/_role token string_

### Header
#### Scoped User Token specified
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
Empty.

### Response status
204, 40x

### Response Body (JSON)
Empty.
