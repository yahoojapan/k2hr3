---
layout: contents
language: en-us
title: Introduce
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: introduceja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: whatnew.html
top_string: What's new
next_url: 
next_string: 
---

# Introduction of K2HR3

[AntPickax](https://antpick.ax/), which is an open source team in [Yahoo Japan Corporation](https://www.yahoo.co.jp/), has released [**K2H**dkc based **R**esource and **R**oles and policy **R**ules(**K2HR3**)](https://k2hr3.antpick.ax/) under the MIT license. K2HR3 is a **RBAC** (**R**ole **B**ased **A**ccess **C**ontrol) system. The primary feature is called **+SERVICE** that enables service owners in cloud environments to control their resources. K2HR3 is designed to primarily work in a private cloud environment, which is dedicated to deliver services to a single organization. For the K2HR3 0.9.0 version, K2HR3 works with [OpenStack](https://www.openstack.org/).

![K2HR3 system overview](images/overview_abstract.png)

## Background

Every system and service consists of subsystems, hosts, and processes. For example, database and RESTful HTTP service are mostly classified as a backend system. On the other hand, GUI applications that use the backend are classified as a frontend system. Backend system must commonly permits access to its resource only for authenticated and authorized applications by using some types of ACL system.

Virtualization and containerization technology enable hardware resources to use more efficiently than before. Every system and service in cloud environments should run on servers flexibly provisioned on demand by using Infrastructure-as-a-service.

To cover the points above, RBAC systems are commonly used in cloud environments. Each cloud native program naturally works with RBAC systems.

## Goal of K2HR3

The primary purpose of K2HR3 as a RBAC system is to minimize developer's hardship and to reducing operations between service providers and users.

### Minimize developer's hardship

The primary purpose of K2HR3 as a RBAC system is to minimize developer's hardship. To achieve this purpose, K2HR3 use tokens as well as IP addresses to authorize permissions to restricted resources because authorization by using IP address is so simple that application developers may remove additional code to authentication and authorization.

For example, most of RBAC system use a token, which is generated for authorization to permit access to a restricted resource. A token is a string to identify a user or a some type of group. System(or service) administrators assign a role to the user or the group. Therefore, a user or a group with no assigned roles will not access any resources. To integrate this type of RBAC system with cloud environments, frontend application developers will firstly write code to request a token. After that, they write code to send requests with the token. Backend server developers will write code to validate the token. If the token grants authorization for the requested resource, servers will permit access to the requested resource. IAM([AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)) is a famous RBAC in AWS([Amazon Web Services](https://aws.amazon.com/)), which enables users to utilize tokens very easily. However Write code to manage tokens is always required.

The integration process of K2HR3 tokenless authorization is different from the above. Frontend applications directly send requests without tokens. Backend server will grant authorization for the requested resource by using the IP address of the other end of the server. As a result, frontend developer need not think of tokens and backend developer is simply required to get the source IP address. Moreover, frontend applications code is independent of RBAC system. This means applications will easily work with RBAC system as they are.


### Reducing operations between service providers and users

K2HR3 reduces operations between service providers and service members(or users). K2HR3 enables programs(or systems) of service providers and service members to be loosely coupled with each other.
- In K2HR3, a service member is a tenant that has its own roles. 
  - A role in the tenant is a collection of hosts or IP addresses that are members of the tenant.
  - The tenant administrator will add a new host to a role.
- A service provider grant permission by tenant. 
- After granted permissions, service members(or users) need not to obtain permissions for additional member of the tenant. 
- A service provider is simply required approves access to the resource by the role only once.

This feature is called as "+SERVICE" in K2HR3. Backend service providers should use this feature when they provides frontend servers with their resources. For example, when the number of frontend instances increases on demand, additional hostnames or IP addresses will be automatically allowed to access the backend services by using the "+SERVICE" functionality.


## K2HR3 RBAC feature

A RBAC system controls access to restricted resources by defining and using a role. K2HR3 as a RBAC system defines the three primary elements: role, rule(or policy rule) and resource. 

- Role  
Defines a collection of a host(or an IP address) that access assets in a service.
- Rule(or Policy Rule)  
Defines a group of actions(read and write) over assets in a service and a permission(allow or deny) to the group of actions.
- Resource  
Defines a value(string or object) as an asset in a service. A value can contains data in any form: text or binary. A text data can be a key, a token or an URL.

Every host is defined as a member of roles in K2HR3 and a host can access resources in a way followed by rules. 

Service providers can dynamically generate data as a resource corresponding to the roles if the providers use K2HR3 template engine. The K2HR3 template engine is designed to autoscaling service in cloud environments. For example, a service provider defines service server's hostnames as a resource and role members. The resource will change if the service provider increase instances(or decreasing) service servers. Of course programs on the service member side is required to track updates of the resource because they should send requests to new servers and they should not to send requests to old(deleted) servers.

Tokenless requests and dynamic resources will enable current programs on-premises environments to move to cloud environments easily because they will work with K2HR3 as they are. All the steps you need to do is mainly the followings.
- Ask service providers to grant permission to the resources
- Wait for the permission
- Add a host or IP address of your server to the authorized role.

![K2HR3 RBAC](images/feature_overview.png)

## K2HR3 working with OpenStack

As of K2HR3 as a RBAC system, every tenant defines a role, which is a collection of hosts and IP addresses. That is, in K2HR3, a host is a member of a role. Adding a host to a role or deleting a host from a role is automatically done by cooperating with IaaS.

We have tested K2HR3 integration with [OpenStack Rocky](https://docs.openstack.org/rocky/). K2HR3 system is almost independent of OpenStack. K2HR3 maintains an IP address relevant to roles by using [cloud-init](https://cloudinit.readthedocs.io/en/latest/index.html) and a message queue service. After an instance is created, the IP address of the instance will be assigned to a role in K2HR3. After the instance is terminated, the IP address of the instance will be removed from assigned role members.

Try K2HR3 by using **devcluster**, which is a tool to install all K2HR3 subsystems in a Linux host for development and test purpose. See the [setup](https://k2hr3.antpick.ax/setup.html) page for details.

![K2HR3 ](images/feature_iaas.png)

## K2HR3 +SERVICE feature

K2HR3 provides the **+SERVICE** feature that enables programs(or systems) of service providers and service members to be loosely coupled with each other. Every service provider defines its service. A service administrator defines permissions to service users(or service members).

[IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) of [AWS](https://aws.amazon.com/) provides a similar feature to the +SERVICE though [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) has many other features.
[IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) provides a function to permit access to service for users as a role. 

That is the almost same function with +SERVICE. By using +SERVICE, K2HR3 users can define their own services and introduce them to their current environments.

![K2HR3 +SERVICE](images/feature_service.png)

## Benefits of K2HR3

As a RBAC system, K2HR3 in cloud environments has unique features that enable developers and service providers to integrate K2HR3 with the current programs(or systems) with minimizing the amount of modification of them.

## Future of K2HR3

The current version of K2HR3 is 0.9.0. It is still in the beta stage. Give us feedback or submit a pull request through the [GitHub website](https://github.com/yahoojapan/k2hr3) for a stable version. We have currently tested K2HR3-0.9.0 on the following environments:
* Linux
  * Debian buster and Stretch
  * Fedora 32, 31 and 30
  * CentOS 7 and 8
  * Ubuntu 16.04, 18.04, and 20.04
* OpenStack
  * Ussuri
* Node.js
  * Node.js 10.x, 12.x and 14.x
* Python
  * Python 3.6 and 3.8

We also want your request for comments on the future K2HR3. We will improve the current **+SERVICE** and the other features. For example, we have a plan to support [Kubernetes](https://kubernetes.io/) to manage containers as a member of a role. We also plan to provide developers and service administrators with a simple way to start K2HR3 cluster. 


