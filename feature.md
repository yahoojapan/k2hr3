---
layout: contents
language: en-us
title: Feature
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: featureja.html
lang_opp_word: To Japanese
prev_url: home.html
prev_string: Overview
top_url: index.html
top_string: TOP
next_url: whatnew.html
next_string: What's new
---

# Feature

**K2HR3** (**K2H**dkc based **R**esource and **R**oles and policy **R**ules) is one of extended **RBAC** (**R**ole **B**ased **A**ccess **C**ontrol) system.  
This section explains the features of the **RBAC** system and **unique functions** provided by the K2HR3 system.  

## RBAC(Role Based Access Control)
The K2HR3 system controls access to **RESOURCE** as a RBAC system.  
The K2HR3 system defines "WHO(**ROLE**) access to WHAT(**RESOURCE**) controlled by HOW(**POLICY-RULE**)" and provides a function to make it easier to manage this.  

### TENANT
**TENANT** is a group of users who use the K2HR3 system.  
The K2HR3 system is designed to work with IaaS(Infrastructure as a Service).  
K2HR3 system can work together IaaS like [OpenStack](https://www.openstack.org/) and [kubernetes](https://kubernetes.io/).  
If you use [OpenStack](https://www.openstack.org/), K2HR3's **TENANT** matches OpenStack tenant(or project).  
In the case of [kubernetes](https://kubernetes.io/), it is necessary to link with the user management system used in the kubernetes system.  

The **ROLE**, **RESOURCE**, **POLICY-RULE**, and **SERVICE** described below are data belonging to the **TENANT**.  
A user of K2HR3 system belongs to some TENANT and can edit the data of those TENANT.  

### ROLE
**ROLE** of the K2HR3 system means **WHO** described above.  
Then **ROLE** is a grouping of sets that access **RESOURCE**(**WHAT**).  

**ROLE** is a group that accesses **RESOURCE**, and the user registers host information(IP address etc.) in this group and permits access to **RESOURCE**.  
And the users can also include other ROLEs in ROLE.  
In this way, the user can create a minimum unit **ROLE** according to the role and define a large unit **ROLE** containing these **ROLE**s.  
And you can define flexible **ROLE** according to accessed **RESOURCE** by using this **ROLE** registration function.  

The K2HR3 system automatically registers/deletes members(IP address, etc) to ROLE by working with IaaS([OpenStack](https://www.openstack.org/), [kubernetes](https://kubernetes.io/)).  
K2HR3 user can register automatically as **ROLE** member by simply starting a Virtual Machine or Container with IaaS already in use.  

### RESOURCE
**RESOURCE** of the K2HR3 system means **WHAT** described above.  
The users can register any data as **RESOURCE** in the K2HR3 system.  

Users can register data of any format in **RESOURCE** without relying on formats such as strings and binaries.  

Also, users can register as static and dynamic data(**RESOURCE**).
If dynamic data is registered in **RESOURCE**, the user can read it as data to be confirmed when accessing it.  

The user can read out the result of combining multiple **RESOURCE**.  
**RESOURCE** can be defined and registered in minimum units, and a large unit **RESOURCE** containing them can be defined and registered.  
This allows users to divide and manage complex **RESOURCE** data into simple **RESOURCE**s, and the user can create any data set.  

K2HR3 system provides the [**K2HR3 Template Engine**](usage_template.html) to enable users to use dynamic **RESOURCE**.  

### POLICY-RULE
**POLICY-RULE** of the K2HR3 system means **HOW** described above.  
**POLICY-RULE** defines how to access **RESOURCE** by **ROLE**.  

The K2HR3 system defines the following **POLICY-RULE** value.  
The user combines these values and registers **POLICY-RULE**.
- **READ**(readable)
- **WRITE**(writable)
- EXECUTE(executable) _reserved_

The user registers target **RESOURCE** to which the access type defined by **POLICY-RULE** is applied in **POLICY-RULE**.  
By registering **POLICY-RULE** in **ROLE**, the access type of **POLICY-RULE** is applied when accessing the target **RESOURCE** from **ROLE**.

### Schematic block diagram

![K2HR3 Feature(Schematic block diagram)](images/feature_overview.png)

## +SERVICE
In addition to RBAC function, K2HR3 provides **+SERVICE** function that works with it.  
This **+SERVICE** function is used on the RBAC function, supports the cooperation between the K2HR3 user's system and service provider and user, and helps the operation of it.  

### Background
When providing a system or service as a backend to its users, the backend provider needs to control the user's access to those systems.  
The provider may also construct systems and functions for this access control.  

This access control system requires functions such as provider, user, access type, authorization setting management of those, and also requires administrative functions to grant and revoke privileges between providers and users.  
In addition, each time a provider's system is added, removed, or modified, both the provider and the user occur as operational costs.  

The **+SERVICE** of K2HR3 provides these adjustments and settings at low cost for the system and service provider and users based on the RBAC function.  

We believe that operating costs can be reduced by preparing the following conditions.  
- The provider can manage the increase and decrease of the access side by the group.
- The provider can dynamically set the system and service provided on a group basis.
- The provider can decide the scope of the system and service to be used.
- Users can freely set the increase and decrease of the access source within the permitted group.

**+SERVICE** will use the RBAC function to link system/services providers and users.  

### Collaboration by +SERVICE
**+SERVICE** defines system service providers and users as **OWNER** and **MEMBER** respectively.  
**+SERVICE** creates and uses data called **SERVICE** to support cooperation between **OWNER** and **MEMBER**.  

**+SERVICE** is used as shown below.  

![K2HR3 Feature +SERVICE(overview)](images/feature_service.png)

1. **[ OWNER ]** Create a SERVICE for the system/service OWNER provide.
1. **[ OWNER ]** Register **RESOURCE** in SERVICE.
1. **[ OWNER ]** Register **TENANT of MEMBER** that uses SERVICE.
1. **[ MEMBER ]** Create **ROLE** as a group that uses provided system/service.
1. **[ MEMBER ]** Check SERVICE registered as **MEMBER in TENANT**.
1. **[ MEMBER ]** Register **ROLE** to collaborate SERVICE.
1. **[ MEMBER ]** **RESOURCE of SERVICE** provided from **OWNER** is automatically set.

Operation work after OWNER's SERVICE registration is only registering TENANT of MEMBER according to increase/decrease.  
MEMBER who will start using existing SERVICE will be only register MEMBER's TENANT by OWNER.  
After that, MEMBER can freely increase/decrease ROLE associated with SERVICE and also increase/decrease host (based IP address/hostname) in this ROLE.  
OWNER can freely change the RESOURCE being provided/registered to SERVICE MEMBER, regardless of whether SERVICE is used or not.  

**+SERVICE** separates authority of OWNER and MEMBER so that each can manage data(RESOURCE/ROLE) freely within authority and reduce administrative cost.  

## Collaboration with IaaS
The K2HR3 system works in cooperation with IaaS(Infrastructure as a Service).  
_Currently, [**OpenStack**](https://www.openstack.org/) and [**kubernetes**](https://kubernetes.io/) are available as IaaS for K2HR3 system._  

By collaborating with [**OpenStack**](https://www.openstack.org/) and [**kubernetes**](https://kubernetes.io/), the K2HR3 system cooperates with instance startup/deletion of the OpenStack **Virtual Machine** or kubernetes **Pod(Container)** and automatically registers/deletes those as a member of **ROLE**.  

The link between K2HR3 system and IaaS([OpenStack](https://www.openstack.org/) and [kubernetes](https://kubernetes.io/)) is **loosely coupled** and can be installed without affecting the existing [OpenStack](https://www.openstack.org/) and [kubernetes](https://kubernetes.io/) system.  
And you can use RBAC of K2HR3 system with the same OpenStack and kubernetes operation as before.  

![K2HR3 Feature IaaS(overview)](images/feature_iaas.png)

The user of the K2HR3 system only prepares **ROLE** before starting/creating the instance or Pod(container) by [OpenStack](https://www.openstack.org/) or [kubernetes](https://kubernetes.io/).  
And just by starting/creating an instance, the instance is automatically registered to that **ROLE**.  
Even if you deleted an instance, it will be deleted automatically from **ROLE** just like when registering.
