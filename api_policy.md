---
layout: contents
language: en-us
title: POLICY API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_policyja.html
lang_opp_word: To Japanese
prev_url: api_resource.html
prev_string: RESOURCE API
top_url: api.html
top_string: REST API
next_url: api_service.html
next_string: SERVICE API
---

# POLICY API

This page describes the K2HR3 POLICY API. The purpose of the POLICY API is to define and list ACLs associated with K2HR3 RESOURCES. ACLs determine K2HR3 RESOURCE usage. Each ACL consists of a group of actions(READ, WRITE and EXECUTE) over a K2HR3 RESOURCE and a permission(ALLOW or DENY) to the group of actions. See the [Basic usage](usage_base.html) page about how to apply K2HR3 POLICIes to K2HR3 ROLE's members.

## POST

Creates or updates a K2HR3 POLICY.

* Creates or updates a POLICY(a scoped user token is required)
* Updates a POLICY(a user token is required)
* Updates a POLICY
* Creates aliases to the other policies(a scoped user token is required)

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Request Body
```
{
    policy:    {
        name:      <policy name>
        effect:    <allow or deny>
        action:    [<action yrn full path>,...]
        resource:  [<resource yrn full path>,...]
        condition: null or undefined
        alias:     [<policy yrn full path>,...]
    }
}
```
- name  
  - A policy name in [YRN](detail_various.html) form.
- effect  
  - A EFFECT type that resource members are allowed(or denied) to use the policy. A valid value is "allow" or "deny". Default is "deny".
- action  
  - An ACTION type or ACTION types that how resource members are allowed to use the resource". A valid value is "yrn:yahoo::::action:read" or "yrn:yahoo::::action:write" or both. 
  - A string literal if a single value. A valid value is "read" or "write".
- resource  
  - A resource name in [YRN](detail_various.html) form. Undefined(including empty value) will be interpreted as null.
  - A single value in a string literal. 
  - Multiple values in an array form.
- alias  
  - A policy name aliased to in [YRN](detail_various.html) form. Undefined(including empty value) will be interpreted as null.
  - A single value in a string literal. 
  - Multiple values in an array form.

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
Creates or updates a K2HR3 POLICY.

* Creates or updates a POLICY(a scoped user token is required)
* Updates a POLICY(a user token is required)
* Updates a POLICY
* Creates aliases to the other policies(a scoped user token is required)

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy?_urlarg_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### URL Arguments
- name=_policy path or yrn full policy path_  
  - A policy name in [YRN](detail_various.html) form.
- effect=_json effect array_  
  - A EFFECT type that resource members are allowed(or denied) to use the policy. 
  - A valid value is "allow" or "deny". Default is "deny".
- action=_json action array_  
  - An ACTION type or ACTION types that how resource members are allowed to use the resource". 
  - A valid value is "yrn:yahoo::::action:read" or "yrn:yahoo::::action:write" or both. 
  - A string literal if a single value. A valid value is "read" or "write".
- resource=_json yrn full resource path array_  
  - A resource name in [YRN](detail_various.html) form. Undefined(including empty value) will be interpreted as null.
  - A single value in a string literal. 
  - Multiple values in an array form.
- alias=_json yrn full policy path array_  
  - A policy name aliased to in [YRN](detail_various.html) form. Undefined(including empty value) will be interpreted as null.
  - A single value in a string literal. 
  - Multiple values in an array form.

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
Lists all available policies if a scoped user token request header is specified. If the service name is provided, the POLICY API lists the all policies under the service in [YRN](detail_various.html) form. The POLICY API will match them with the requested policy in the URL path in [YRN](detail_various.html) form.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy/_policy path or yrn full policy path_{?service=service name}

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```
### URL argument
- service=_service name_
  - A service name.
  - the POLICY API lists the all policies under the service in [YRN](detail_various.html) form. 
  - The POLICY API will match them with the requested policy in the URL path in [YRN](detail_various.html) form.

### Response status
200、40x

### Response Body(JSON)
```
{
    result:     <true/false>
    message:    <null or error message string>
    policy:    {
        name:       <policy name>,
        effect:     <allow or deny>,
        action:     [<action yrn full path>, ...],
        resource:   [<resource yrn full path>, ...],
        alias:      [<policy yrn full path>, ...]
    }
}
```
- result  
True if success. False otherwise.
- message  
An error message if the result if false
- policy:name  
A policy name.
- policy:effect  
An effect type. The value is either "allow" or "deny".
- policy:action  
An array of actions.
- policy:resource  
An array of resources in [YRN](detail_various.html) form.
- policy:alias  
An array of a policy aliased to in [YRN](detail_various.html) form.

## HEAD
Validates information of a policy(including the actions if a TENANT name and a resource are specified in [YRN](detail_various.html) form)

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy/_yrn full policy path_?_urlarg_

### Header
```
Content-Type: application/json
```

### URL Arguments
- tenant=_tenant name_  
A tenant(or project) name.
- resource=_yrn full resource path_  
A resource name in [YRN](detail_various.html) form.
- action=_action type_
An action name or action names. Each value is either "yrn:yahoo::::action:read" or "yrn:yahoo::::action:write".
- service=_service name_(optional)
  - A service name. 
  - If the service name is provided, the POLICY API validates the all policies under the tenant and the service in [YRN](detail_various.html) form. 
  - The POLICY API will match them with the requested policy in the URL path in [YRN](detail_various.html) form.

### Response status
204、40x

### Response Body(JSON)
Empty

## DELETE
Deletes a policy.

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/policy/_policy path or yrn full policy path_

### Header
```
Content-Type: application/json
x-auth-token: U=<Scoped User Token>
```

### Response status
204、40x

### Response Body(JSON)


