---
layout: contents
language: en-us
title: Service Usage
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_serviceja.html
lang_opp_word: To Japanese
prev_url: usage_rbac.html
prev_string: RBAC Usage
top_url: usage.html
top_string: Usage
next_url: usage_template.html
next_string: Template Engine
---

# +SERVICE Usage
The K2HR3 system provides a feature called **+SERVICE**.  
This **+SERVICE** feature uses elements of **SERVICE** to cooperate with systems and services between users of the K2HR3 system.  
Using the **+SERVICE** feature, USER can lower the operation load of systems and services operated by **USER**.  

This section explains the functions of **+SERVICE** and how to use SERVICE.  

## SERVICE element

### Defining and using SERVICE
**+SERVICE** feature is a function for providing and using **RESOURCE** across **TENANT**.  
The **+SERVICE** feature uses an element called **SERVICE**.  
**SERVICE** is defined and registered in each **TENANT**.  

**SERVICE** has the following two types.
- OWNER : **SERVICE** of the **providing side**  
**TENANT** that provides **RESOURCE** using the **+SERVICE** feature is called **OWNER**.  
In other words, **OWNER** owns and **provides SERVICE**.  
**OWNER** uses **SERVICE** to make **RESOURCE** available to other **TENANT**s.
- **MEMBER** : **SERVICE** on the **side of use**  
**MEMBER** is **TENANT** that uses **RESOURCE** as **SERVICE** provided by **OWNER**.

### RBAC provided by +SERVICE
The K2HR3 system provides the **RBAC** function for **RESOURCE**.  
**+SERVICE** feature enables access control by **TENANT** which manages **RESOURCE** for **TENANT** and **ROLE** using **RESOURCE**.  
Thus, **+SERVICE** provides **RBAC** for **RESOURCE** across **TENANT**.  
And **+SERVICE** makes it easy for **USER** to manage and operate functions and information to be cooperated between **TENANT**s.  
**USER** defines cooperating functions and information as **RESOURCE**, and can reduce the work related to cooperation between **OWNER** and **MEMBER** of **SERVICE**.

#### Benefits of OWNER
Normally in the K2HR3 system, when providing **RESOURCE**, USER need to manage the **HOST** of the **ROLE member** accessing the **RESOURCE**.  
This task can be done easily if RESOURCE and ROLE are owned by the **same TENANT**.(Due to cooperation between IaaS(OpenStack or kubernetes))  
However, if RESOURCE and ROLE are owned by **different TENANTs**, coordination between **OWNER** and **MEMBER** becomes **difficult**.  
In particular, if OWNER want to provide **different RESOURCE** for each MEMBER, it becomes more difficult.  

By using the **+SERVICE** feature, OWNER manages **only TENANT(MEMBER)** to be accessed and does not manage ROLE.  
ROLE is only managed by MEMBER which is the TENANT to which it belongs.  
And **+SERVICE** can also make OWNER provide **different RESOURCE** for each MEMBER.  

The benefit of OWNER using +SERVICE is that OWNER only need to manage access to RESOURCE in units of TENANT(MEMBER).  

#### Benefits of MEMBER
As explained in Benefits of OWNER, by using the **+SERVICE** feature, MEMBER accessing RESOURCE provided by other TENANT(OWNER) only defines **ROLE** and manages that **ROLE member HOST**.  
**MEMBER** is only to have **OWNER allow** its TENANT to access RESOURCE.

**MEMBER** can only **manage HOST** that accesses authorized RESOURCE freely by MEMBER.

# (1) Settings for OWNER
Describe the settings that SERVICE OWNER does.  

## Definition of provided RESOURCE
First, OWNER decides which RESOURCE to provide.  
RESOURCE is a **function or information** shared by OWNER and MEMBER.
Therefore, OWNER decides what functions or information (mainly information) to provide.

The contents that can be set as RESOURCE are shown below.

### Static RESOURCE
This type of RESOURCE is used to provide **common(static) data** to all TENANT(MEMBER).  
OWNER needs to set an **object(string formatted by JSON)** to RESOURCE as static RESOURCE.  

This RESOURCE object(string formatted by JSON) is an array object of JavaScript.  
Each element of that array needs to be **RESOURCE expressed object** used in K2HR3 system.  

The contents of this object is described in **Contents of the RESOURCE object** described later.  

### Dynamic RESOURCE
The type of RESOURCE is used to provide **different data** for each TENANT(MEMBER) accessing RESOURCE.  
OWNER registers the **VERIFY URL** to be called(callback) to **dynamic RESOURCE** when TENANT (MEMBER) cooperates with SERVICE.  
**VERIFY URL** is **REST API** prepared by **OWNER** of SERVICE.  

This **VERIFY URL** is explained below.  

#### Request format
The **VERIFY URL** is called from the K2HR3 system with the following **URL arguments**.
```
GET http://<verify host[:port]>{/<path>}?service=<service name>&tenant=<tenantname>&tenantid=<tenant id>&user=<user name>&userid=<user id>
```
The URL arguments are explained below.
- service  
The value is a cooperating SERVICE name.
- tenant  
The value is the TENANT name who cooperates with SERVICE.
- tenantid  
The value is the TENANT ID(known by the K2HR3 system).
- user  
The value is the USER name that instructed SERVICE cooperation.
- userid  
The value is USER ID (known by the K2HR3 system).

#### Response
The response from the **VERIFY URL** returns the **JSON string of the JavaScript Object**.  
OWNER can change the contents of the response according to the cooperating **TENANT** and **USER** according to the contents of the URL arguments of the request.  
That is, it responds with **dynamic RESOURCE**.  
A response object(string formatted by JSON) is an object representing multiple RESOURCEs.  

The contents of this object is described in **Contents of the RESOURCE object** described later.  

#### VERIFY URL prepared for testing
The [**K2HR3 API Server**](detail.html) of the K2HR3 system incorporates the **VERIFY URL** for debugging and testing used by OWNER.  
OWNER can check the operation by setting this VERIFY URL to SERVICE.
```
http://<k2hr3 api server host[:port]>/v1/debug/verify
```

### Contents of the RESOURCE object
Static RESOURCE and dynamic RESOURCE returned in the response of VERIFY URL are both JavaScript objects represented by the same JSON string.  
This JSON string must be a JavaScript object shown below.  
```
[
    {
        name:    <"resource name">
        expire:  <integer>
        type:    <"string" or "object">
        data:    <null or "string" or object>
        keys: {
            key: <value>,
            .
            .
            .
        }
    },
    .
    .
    .
]
```
The response JavaScript object is an array of RESOURCE data.  
The RESOURCE data is the same as the RESOURCE used in the K2HR3 system.  
Each element is described below.  
- name  
It is the name of RESOURCE.  
This value is used to distinguish RESOURCE in the array.
- expire  
_This item is a reservation keyword. Currently it is unused. Please set to 0._
- type  
Indicates the type of this RESOURCE data item.  
Specify "string" or "object".
- data  
It is data of RESOURCE.  
A null, string, or object is specified.
- keys  
You can set multiple combinations of keys and values.

## Procedure for setting SERVICE by OWNER
The actual procedure for setting up SERVICE of OWNER is shown below.

#### (1-1) Select TENANT
#### (1-2) Register SERVICE in TENANT
#### (1-3) Register contents of SERVICE
- SERVICE name
- RESOURCE provided by SERVICE  
To set static RESOURCE, set a character string.  
To set dynamic RESOURCE, set the VERIFY URL.

# (2) Settings for MEMBER
Describe the settings that SERVICE MEMBER does.  

## Authorization to use SERVICE
MEMBER has permission to access SERVICE linked to OWNER from TENANT.
When access to SERVICE is permitted, SERVICE which cooperates with TENANT of MEMBER becomes available.

### SERVICE before cooperation
When SERVICE becomes available, you can check the following contents with [K2HR3 Web Application](usage_app.html).

- SERVICE name  
The target SERVICE name is displayed in the SERVICE tree of TENANT that is allowed to cooperate with.

## SERVICE starts cooperation
MEMBER can cooperate with SERVICE at TENANT where access is permitted.  
To start cooperation using the [K2HR3 Web Application](usage_app.html), select SERVICE and click the button for cooperating.
_ Dialog will be displayed. _
In this dialog, you can complete the cooperation by pressing the OK button.

### SERVICE after cooperation
When SERVICE is cooperated with, the following contents can be confirmed on the screen of [K2HR3 Web Application](usage_app.html).  
_The following ROLE, POLICY-RULE, RESOURCE are displayed as subitems of SERVICE name._  
- ROLE  
There is only one "acr-role".  
_This ROLE can not be edited._
- POLICY-RULE  
There is only one "acr-policy".  
_This POLICY-RULE can not be edited._
- RESOURCE  
RESOURCE provided by OWNER exists.  
_These RESOURCEs can not be edited._

### Setting of associating ROLE
The following items can be set in the dialog displayed when starting SERVICE cooperation.  
_You can set it even after you do not initialize it in dialog of starting cooperation._

#### Associating ROLE at cooperating
When cooperating with SERVICE, ROLE which can access RESOURCE provided as SERVICE is automatically created.  
_This ROLE is "acr-role"._  
This "acr-role" is used to manage the ROLE for MEMBER to freely access the provided RESOURCE.  

MEMBER can specify the ROLE registered in TENANT in the dialog for starting cooperation.  
This automatically sets "acr-role" to ALIAS of the specified ROLE.  

Adding "acr-role" to ALIAS of MEMBER 's ROLE makes it possible to access the RESOURCE provided from HOST of this ROLE member.  

### Associating ROLE after cooperation
MEMBER can associate ROLE after cooperation, for example when ROLE is not initially specified at start cooperating.
Please manually add **[YRN](detail_various.html) full path** of "acr-role" to ALIAS of ROLE which MEMBER want to add.

## Associative HOST
Associating or Unassociating of ROLE cooperated with SERVICE can be done as described in the previous section.
Adding/deleting HOST in ROLE member is the same as ordinary procedure.

That is MEMBER can manage HOST accessing RESOURCE as this ROLE member.

## Procedure for setting SERVICE by MEMBER
Start and set up MEMBER SERVICE using the following procedure.

#### (2-1) Select TENANT
#### (2-2) OWNER allows MEMBER TENANT
#### (2-3) MEMBER confirms SERVICE permitted to cooperate with
#### (2-4) Started to cooperate with SERVICE
Here, you can specify ROLE of MEMBER to be associated.
#### (2-5) Set ROLE to be associated to SERVICE of MEMBER.
You can add/delete HOST to/from ROLE at anytime after starting cooperation.
#### (2-6) Management of associating ROLE members

