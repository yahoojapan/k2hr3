---
layout: contents
language: en-us
title: Basic Usage
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_baseja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: usageja.html
top_string: Usage
next_url: usage_service.html
next_string: Service Usage
---

# Basic Usage
This section explains the basic usage of the K2HR3 system.  

The sections after here explains how to define and set the contents of data in order of **RESOURCE**, **POLICY-RULE** and **ROLE**.  
Please refer to these procedures and use the K2HR3 system.  

# (1) RESOURCE Usage
The primary purpose of **USER** using K2HR3 system is to control access to **RESOURCE**.  
In other words, when you start using the K2HR3 system, you **first** need to start with defining and registering **RESOURCE** to be controlled as **RBAC**. 

## RESOURCE Definition and Design
At first you need to find out **data**(or information) in your system, that data should be controlled as **RBAC** provided by K2HR3 system.  
You aggregate, divide, and synthesize this data(or information) and create definitions and units for the **RESOURCE**.  
To extract and define the **RESOURCE**, you can use indexes such as a set accessing data, a unit/range to be accessed, etc.  

For example, the following data unit could be used as indexes for **RESOURCE** definition.  
- Configuration file for application and program
- URL list.
- List of hosts providing the same functionality(such as Web servers)

Next, consider the unit of **RESOURCE** data with reference to the following.  
- Grouping the access sources and assigning data units accessed from each group
- Data units that can be shared
- Dynamic or static data units
- Data unit according to access type(READ, WRITE, EXECUTE)

Please refer to the above and decide data to be registered in **RESOURCE** as shown in the next section.  

## RESOURCE Contents
You can set any of the following, or a combination of them for **RESOURCE**.

### Static string or Object(JSON string)
**RESOURCE** can be either a **static string** or **JavaScript Object**.  
When registering a JavaScript Object, specify it as a character string formatted by **JSON**.  
For a static string, you can set an arbitrary character string.  
To set **dynamic RESOURCE** using **TEMPLATE**, select static text and register strings written by **TEMPLATE**.  
For the **TEMPLATE**, please see [K2HR3 Template Engine](usage_template.html).

### KEYS
For **RESOURCE KEYS**, you can set arbitrary key names and values as **key-value** as a set.
You can set multiple sets of this key and value in one **RESOURCE**.

### ALIAS
**RESOURCE** can include **other RESOURCE** set as **ALIAS**.  
**RESOURCE** can synthesize all the contents of **other RESOURCE** specified by ALIAS into **its own data**.  
That means you can read this **synthesized data** when you read RESOURCE.  
USER and the system access RESOURCE through the **REST API**.  
The **REST API** can detect ALIAS and return RESOURCE as **a result of combining**.  
With **ALIAS**, you can split the RESOURCE into small units and manage them.  
In other words, you can use ALIAS to subdivide and group RESOURCE and **ALIAS makes it easy to manage RESOURCE**.  

## Unit of RESOURCE
It is recommended to register **RESOURCE** in minimum units.  
The RESOURCE data can be defined using the ALIAS described above or the hierarchy described below and can include other RESOURCEs.  
Therefore, by registering USER as a minimum unit, you can easily manage **RESOURCE**s.
Because RESOURCE can be aggregated, it is recommended to divide RESOURCE by data type and group being updated at the same time.  

Consolidating and managing RESOURCE makes it easy to create aggregate patterns and define **flexible RESOURCE**.  

### Hierarchize RESOURCE
The name of RESOURCE is a character string, it becomes part of [YRN](detail_various.html) full path.  
String of RESOURCE name can be expressed in **PATH format**(concatenated with **"/"** character), and **hierarchical parent-child relationship** like directory can be created.  

### Inheritance of RESOURCE
In the **hierarchical RESOURCE**, the RESOURCE data of the parent PATH is **imported** into the RESOURCE of the child PATH, and its RESOURCE data can be **inherited**.  
In other words, when you access RESOURCE, you can get RESOURCE data that contains RESOURCE data set in the upper layer PATH of that RESOURCE.  

By using inheritance by this hierarchy, you can register **common data** in RESOURCE of the upper hierarchy and **share the data**.  
And you can create several different RESOURCEs, including common RESOURCE.  

![K2HR3 Usage - Resource hierarchy](images/usage_base_resource_hierarchy.png)

## How to set the RESOURCE
Once you have defined the definition and unit of RESOURCE, you consider the hierarchy of that RESOURCE and register.  

#### (1-1) Select TENANT
#### (1-2) Register RESOURCE in TENANT (note the RESOURCE PATH hierarchy)
#### (1-3) Set contents of RESOURCE

# (2) POLICY-RULE Usage
After registering RESOURCE, define how to access the RESOURCE as **POLICY-RULE** and register it.  
**POLICY-RULE** is registered in units of RESOURCE to be accessed.  
_You do not need to set POLICY-RULE for RESOURCE not directly accessed(ex. common RESOURCE)._  

## POLICY-RULE Contents
The items to be set for POLICY-RULE are shown below.  

### EFFECT
Select **EFFECT** type for the **ACTION** element set to **POLICY-RULE**.  
- ALLOW
- DENY

### ACTION
Select the access method(**ACTION**) for RESOURCE from the following values and define them in combination.  
- READ
- WRITE
- EXECUTE  
_Currently, this value is reserved and not provided._

### RESOURCES
Specify one or more RESOURCE controlled by this POLICY-RULE.  
RESOURCE is specified with **[YRN](detail_various.html) full path**.  
[YRN](detail_various.html) full path is a unique PATH indicating RESOURCE.  
For explanation of this PATH, please see [YRN](detail_various.html) full path.  
USER can use the [K2HR3 Web Application](usage_app.html), select RESOURCE, display the **Selected Path Information** dialog, and know the PATH.  

If this **POLICY-RULE** is applied to access the registered RESOURCE, ACTION and EFFECT are confirmed by the K2HR3 system, and access authorization judgment is done.

### ALIAS
**POLICY-RULE** can include **other POLICY-RULE** set as **ALIAS**.  
**POLICY-RULE** can synthesize all the contents of **other POLICY-RULE** specified by ALIAS into **its own data**.  
That means K2HR3 system uses this **synthesized data** for checking authorization at accessing **RESOURCE**.
With **ALIAS**, you can split the POLICY-RULE into small units and manage them.  
In other words, you can use ALIAS to subdivide and group POLICY-RULE and **ALIAS makes it easy to manage POLICY-RULE**.  

## How to set POLICY-RULE
Once you have defined the definition and unit of POLICY-RULE, you register that POLICY-RULE.  

#### (2-1) Select TENANT
#### (2-2) Register POLICY-RULE in TENANT
#### (2-3) Set contents of POLICY-RULE

# (3) ROLE Usage
Finally, we define **ROLE** in units accessing **RESOURCE**.  
**ROLE** is registered in units of one or more units of **POLICY-RULE** which sets resources to be accessed.  

## ROLE Contents
The items to be set for ROLE are shown below.  

### HOST NAME
To distinguish **HOST** registered in **ROLE** by **hostname**, you can register it manually.  
Register the hostname(**FQDN**) and the **Auxiliary Information(AUX)** of the **HOST** together.  
_Please refer to [Auxiliary Information(AUX)](detail_various.html) for AUX._  

### IP ADDRESSES
To distinguish **HOST** registered in **ROLE** by **IP address**, you can register it manually.  
Register the IP address and the **Auxiliary Information(AUX)** of the **HOST** together.  
_Please refer to [Auxiliary Information(AUX)](detail_various.html) for AUX._  

#### Automatic registration
When cooperating with IaaS(OpenStack) and automatically registering/deleting **ROLE member HOST**, manually registering **HOST** with IP address is **unnecessary**.  
This is because IP addresses are automatically registered/deleted when they are worked with IaaS(OpenStack).  
If you do not work with IaaS(OpenStack) or do not use it, please use manual registration of IP address.  

### POLICIES
Please list **POLICY-RULE** which defines access method to **RESOURCE** accessed by **ROLE** member's **HOST**.  
You can register more than one **POLICY-RULE**.  

### ALIAS
**ROLE** can include **other ROLE** set as **ALIAS**.  
**ROLE** can synthesize all the contents of **other ROLE** specified by ALIAS into **its own data**.  
That means you can read this **synthesized data** when you read ROLE.  
USER and the system access ROLE through the **REST API**.  
The **REST API** and K2HR3 system can detect ALIAS and return ROLE as **a result of combining**.  
With **ALIAS**, you can split the ROLE into small units and manage them.  
In other words, you can use ALIAS to subdivide and group ROLE and **ALIAS makes it easy to manage ROLE**.  

## Unit of ROLE
It is recommended to register **ROLE** in minimum unit.  
The **ROLE** data can be defined using the above ALIAS or the following hierarchy and can include **other ROLE**s.  
Therefore, you can easily manage **ROLE** by registering it as the smallest unit.  
Since **ROLE** can be aggregated, it is recommended to divide ROLE according to the **role**.  
By aggregating and managing ROLE, you can easily create and define **flexible patterns**.  

### Hierarchize ROLE
The name of ROLE is a character string, it becomes part of [YRN](detail_various.html) full path.  
String of ROLE name can be expressed in **PATH format**(concatenated with **"/"** character), and **hierarchical parent-child relationship** like directory can be created.  

### Collection of ROLE
Hierarchical ROLE can be HOST of ROLE member of child PATH belong to ROLE member of parent PATH.  
In other words, the ROLE member HOST of the lower hierarchy has a role as a ROLE member of the upper hierarchy.  
By doing this, you register HOST in only one ROLE, but you can make that HOST belong to more than one ROLE.  
This makes it easy to manage HOST.  

Although it is possible to register one HOST in multiple ROLEs, management becomes cumbersome. Also, when registering HOST automatically, only one ROLE can be used.  
_Note that hierarchy of RESOURCE is inherited, but ROLE is considered as a set._

![K2HR3 Usage - Role hierarchy](images/usage_base_role_hierarchy.png)

### Examples
Suppose that there is a group(A) to be read-only, and a group(B) to only read and write for a certain RESOURCE.  
Consider the case where there is a common HOST in groups (A) and (B).  
In this case, create and register ROLE with POLICY-RULE that is common to both sides and ROLE for non-common POLICY-RULE.  

An example is shown below.
- HOST only to read RESOURCE  
Host-A, Host-B
- HOST to read and write RESOURCE only  
Host-C, Host-D, Host-E

In this case, create two ROLEs as follows.
- Read only ROLE(R-X)  
Host-A, Host-B
- Write only ROLE(R-Y)  
Host-C, Host-D, Host-E

Then, register ROLE(R-X) as the upper layer and ROLE(R-Y) in the lower level.  
With this registration, HOST will be registered in only one ROLE without duplication.  
And you can master duplicate POLICY-RULE.  

## Manual HOST registration to ROLE
After determining the unit/definition of ROLE, register ROLE according to the unit/definition and manually register member HOST.  
_Skip this item only if HOST is automatically registered._  

#### (3-1) Select TENANT
#### (3-2) Register ROLE in TENANT
#### (3-3) Register HOST in ROLE
You can register HOST in any of the following.  
- Register with **IP address**
- Register at **hostname**

_Please refer to [Auxiliary Information(AUX)](detail_various.html) for AUX. Please leave it empty here._  

## Automatic host registration to ROLE
After determining the unit/definition of ROLE, create a ROLE like a manual.  
We do not register HOST of members in ROLE.  
It starts Virtual Machine with IaaS(OpenStack) and it is registered automatically.  

#### (3'-1) Select TENANT
#### (3'-2) Register ROLE in TENANT
#### (3'-3) Get **USER DATA SCRIPT** of ROLE
When using the [K2HR3 Web Application](usage_app.html), select ROLE and display the **Selected Path Information** dialog.  
Copy (click the button) **USER DATA SCRIPT** in this dialog.
#### (3'-4) Create Virtual Machine with OpenStack
Start up the instance(Virtual Machine) with OpenStack.  
To start an instance from OpenStack's Dashboard(horizon), specify **USER DATA SCRIPT** in **after creating** in the instance setting dialog.  
The **USER DATA SCRIPT** can be obtained from **Selected Path Information** dialog of ROLE.  
When using the openstack command(CLI), specify the user data script with the **-user-data** option.  
_Depending on the version of OpenStack, screens, wordings, etc. may differ._
#### (3'-5) Automatically registered after Virtual Machine is started
When the instance(Virtual Machine) starts up, the instance is automatically registered to the member of ROLE.

## Manual HOST deleted from ROLE
You can manually delete HOST from ROLE members.  
When using the [K2HR3 Web Application](usage_app.html), you can delete it manually by specifying the HOST registered in the ROLE member.  
Please manually register in order to re-register the same HOST after deleting auto registered HOST.

## Automatic deletion by K2HR3 OpenStack Notification Listener
HOST registered automatically for ROLE members can be automatically deleted.  
[K2HR3 OpenStack Notification Listener](detail_osnl.html) is running, it is automatically deleted in cooperation with IaaS(OpenStack).  

#### (4-1) Delete Instance(Virtual Machine) with OpenStack
#### (4-2) K2HR3 OpenStack Notification Listener detects deletion
[K2HR3 OpenStack Notification Listener](detail_osnl.html) receives notification via OpenStack's RabbitMQ and checks whether the deleted instance is registered in K2HR3.  
If it is a registered HOST, it will be deleted automatically from members of ROLE that registered this HOST.  

## Automatic detection by Watcher
HOST registered automatically for ROLE members can be automatically deleted.  
Even if [K2HR3 OpenStack Notification Listener](detail_osnl.html) can not be started, instead of starting K2HR3 [Watcher](tools.html), you can automatically delete HOST.  
This [Watcher](tools.html) periodically queries IaaS(OpenStack) for the presence of automatically registered HOST, detects that it has been deleted, and automatically deletes it from the ROLE member.  

#### (4'-1) Delete Instance(Virtual Machine) with OpenStack
#### (4'-2) Watcher detects deletion
[Watcher](tools.html)'s regular OpenStack inquiry will detect deletion of target HOST.  
It automatically deletes the detected HOST from the registered ROLE member.  

