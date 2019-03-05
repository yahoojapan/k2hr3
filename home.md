---
layout: contents
language: en-us
title: Overview
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: homeja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: index.html
top_string: TOP
next_url: feature.html
next_string: Feature
---

# K2HR3
**K2HR3** (**K2H**dkc based **R**esource and **R**oles and policy **R**ules) is one of extended **RBAC** (**R**ole **B**ased **A**ccess **C**ontrol) system.  

**K2HR3** is a system that defines and controls HOW(POLICY-RULE), WHO(ROLE), WHAT(RESOURCE), as RBAC.  

Users of K2HR3 can define **ROLE(WHO)** groups to access freely defined **RESOURCE(WHAT)** and control access by **POLICY-RULE(HOW)**.  

By defining the information and assets required for any system as a RESOURCE(WHAT), K2HR3 system can give the opportunity to provide access control in every situation.  

![K2HR3 Overview(abstract)](images/overview_abstract.png)

## Background
Every system combines systems, servers, hosts, processes to provide services.  

Programs of these minimum units require settings, information, etc. for their own operation, which change depending on the environment.  

Especially in the cloud environment, it is necessary to create and use information(RESOURCE) corresponding to each environment.  

For example, this information(RESOURCE) is host connection, program setting, authentication related information, etc.  

This information(RESOURCE) is accessed from the group(ROLE) handling it.  

Currently, AWS( [Amazon Web Services](https://aws.amazon.com/) ) IAM( [AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) ) is famous for the cloud world as a system to manage and control the RESOURCE.  

We made **K2HR3** system with the purpose of providing an RBAC system that can cooperate with IaaS([OpenStack](https://www.openstack.org/), etc), can be used in environments other than AWS, and can easily use it.  

Now, **K2HR3** can work with [OpenStack](https://www.openstack.org/) and control access to RESOURCE.

**K2HR3** will **eliminate unique authentication system**(ex. authentication by token) to get RESOURCE, and will reduce the work of building the user's system.  

## Purpose
K2HR3 is purpose at providing tools to users who provide services and systems using IaaS(Infrastructure as a Service) in cloud environments, and to assist in system development and construction.  
K2HR3 will reduce costs for developers and service providers in building systems in cloud and non-cloud environments.  

Then using K2HR3 system do **NOT** need **authentication/authorization such as token authorization**, and you will make it easy for user's system development and construction.  

## K2HR3 RBAC
**K2HR3** defines the following as elements of **RBAC**.
#### **WHO**(who, what group)
#### **WHAT**(What, what kind of information)
#### **HOW**(What to do, what kind of access)

K2HR3 is an RBAC system that clearly defines these and controls access to information(RESOURCE) to handle.

## +SERVICE
K2HR3 can register information(RESOURCE) and groups(ROLE) that manage and handle it as RBAC system.  

In general Web services, it is sometimes necessary for administrators(RESOURCE owner ROLE) to provide resources(RESOURCE) of the backend system to other groups(user ROLE).  

The controller in this case can be distinguished between the SERVICE OWNER side that provides functions and information(RESOURCE) and the SERVICE MEMBER side that uses them.  

In a general example, there are a group that provides an Web APIs and a group that uses those APIs, and these groups work together to provide a Web service that users use.  

On the side that provides these function and information(RESOURCE) and the side using these require Access authorization, group management, group member management, etc.  

**With +SERVICE** provided by K2HR3, it can be easy to separate and manage the authority of the side providing the function/information(RESOURCE) and the side using those.  

