---
layout: contents
language: en-us
title: Various
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: detail_variousja.html
lang_opp_word: To Japanese
prev_url: detail_osnl.html
prev_string: K2HR3 OSNL
top_url: detail.html
top_string: Detail
next_url: 
next_string: 
---

# Various Details
This document explains the common contents regarding the specifications of the K2HR3 system.  

## Yahoo Resource Names (YRN) 
The data(**USER**, **TENANT**, **ROLE**, **POLICY-RULE**, **RESOURCE**, **SERVICE** etc) of the **K2HR3** system must be uniquely identifiable when referring and registered.  
**K2HR3** defines and uses **Yahoo Resource Names(YRN)** to uniquely identify these data.  

### Format
**Yahoo Resource Names(YRN)** is defined in the following **format** like a **PATH**, and the user of K2HR3 system specifies and uses a part and all of this YRN path.  
```
yrn:<provider(domain)>:<service>:<region>:<tenant>:<type>{:<paths>}
```
Each part of the **YRN path** is separated by a **":"** character as a separator.  

Each part is explained below.  

#### **yrn**
This is a part indicating that this is **Yahoo Resource Names(YRN)**, and all YRN paths start from this **"yrn"** string.

#### < provider(domain) >
This part shows the **provider** that provides the K2HR3 system.  
Currently, this part is reserved, this part is a static value **"yahoo"**.  

#### < service >
This part is showing **SERVICE** data used by **+SERVICE**, and sets a **SERVICE name** as a value.  

The user of K2HR3 system specifies this part when expressing the path indicating the **SERVICE** data set by **OWNER**.  
If this part' value is **not empty**, **< tenant >** specifies the **TENANT** to which the **OWNER of SERVICE** belongs.  

#### < region >
This part shows the **region** where the K2HR3 system exists(which means its name, region, region, range, area etc).  

This part is currently **undefined(reserved)** and the value is always **empty**.  
_It will be defined in the future._  

#### < tenant >
This is a part for uniquely identifying **TENANT**, and **TENANT ID** is set as a value.  
In collaboration with IaaS(OpenStack) of K2HR3 system, **TENANT** of K2HR3 system is the same as tenant(or project) of IaaS(OpenStack).  
That is **TENANT ID** is the same as the ID of the tenant(or project) of IaaS(OpenStack).  
 
When specifying data not related to **TENANT** by **YRN Path**, the value of this part is **empty**.  

#### < type >
This is a part indicating the type of data(**USER**, **ROLE**, **POLICY-RULE**, **RESOURCE**, **SERVICE** etc) of the K2HR3 system.  
The value of this part is one of the following.  
_Values other than bold are used only inside the K2HR3 system. USER will not use it directly._  
- **user**
- **service**
- **role**
- **policy**
- **resource**
- desc
- display
- id
- action
- token
- keystone
- iaas

#### < paths >
This last part shows data registered in the type indicated by **< type >**, and it is a **path** uniquely indicating data **under the types**.  
And the value of this part is called the **YRN partial path**.  
**YRN full path** means all string from "yrn" to end.  
The value of this part can represent a **hierarchical path** like a PATH.  
In that case, separate each hierarchy with **"/"** characters, and explicitly state parent/child relationships.  

### Usage
The K2HR3 system uniquely identifies data using **Yahoo Resource Names(YRN)** when setting/referring data.  
Mainly, **USER** uses **YRN Path** to specify **ROLE**, **POLICY**, **RESOURCE**, **SERVICE**.  
**USER** can use [K2HR3 Web Application](usage_app.html) to check **YRN full path**.  
The [K2HR3 Web Application](usage_app.html) displays the **YRN full path** in the dialog that displays the attribute information of the data.

## Auxiliary Information(AUX)
The **Auxiliary Information(AUX)** used by the K2HR3 system is the information attached to the **ROLE member HOST**.  
The K2HR3 system uniquely distinguishes ROLE members using **HOST** name(or IP address) and this **AUX**.  

### Uniqueness
In the K2HR3 system, the **HOST** of the **ROLE member** must be uniquely identified.  
However, the K2HR3 system registers **HOST** with **FQDN** or **IP address**, but there are cases where it is not unique with these.  
In that case, the K2HR3 system can add **Auxiliary Information(AUX)** to **HOST**.  
Currently, the **Auxiliary Information(AUX)** that **USER** can specify is only the **PORT** element.  

### Collaboration with IaaS(OpenStack)
The K2HR3 system can register and delete the **ROLE member**'s **HOST** with IaaS(OpenStack).  
When using this collaboration function, the elements **CUK**, **EXTRA** are added to the **Auxiliary Information(AUX)** of the registered **HOST**.  
_Please do not use these element directly._  

### Elements of AUX
As mentioned above, several elements are defined for the **Auxiliary Information(AUX)**.  
This section explains these elements of **AUX**.  
- PORT  
This is the only element that **USER** can set and this value shows the port number.  
Please specify a numerical value for this value.
- CUK  
K2HR3 cooperates with IaaS(OpenStack) and this element is automatically set to registered **HOST**.  
_Do not edit/use/add this element._
- EXTRA  
K2HR3 cooperates with IaaS(OpenStack) and this element is automatically set to registered **HOST**.  
_Do not edit/use/add this element._


