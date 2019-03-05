K2HR3
-----
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/yahoojapan/k2hr3/master/LICENSE)
[![GitHub forks](https://img.shields.io/github/forks/yahoojapan/k2hr3.svg)](https://github.com/yahoojapan/k2hr3/network)
[![GitHub stars](https://img.shields.io/github/stars/yahoojapan/k2hr3.svg)](https://github.com/yahoojapan/k2hr3/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/yahoojapan/k2hr3.svg)](https://github.com/yahoojapan/k2hr3/issues)

## **K2HR3** - **K2H**dkc based **R**esource and **R**oles and policy **R**ules

![K2HR3 system](https://k2hr3.antpick.ax/images/top_k2hr3.png)

## K2HR3 system overview
**K2HR3** (**K2H**dkc based **R**esource and **R**oles and policy **R**ules) is one of extended **RBAC** (**R**ole **B**ased **A**ccess **C**ontrol) system.  
K2HR3 works as RBAC in cooperation with **OpenStack** which is one of **IaaS**(Infrastructure as a Service), and also provides useful functions for using RBAC.  

K2HR3 is a system that defines and controls **HOW**(policy Rule), **WHO**(Role), **WHAT**(Resource), as RBAC.  
Users of K2HR3 can define **Role**(WHO) groups to access freely defined **Resource**(WHAT) and control access by **policy Rule**(HOW).  
By defining the information and assets required for any system as a **Resource**(WHAT), K2HR3 system can give the opportunity to provide access control in every situation.  

K2HR3 provides **+SERVICE** feature, it **strongly supports** user system, function and information linkage.

![K2HR3 system overview](https://k2hr3.antpick.ax/images/overview_abstract.png)

K2HR3 is built [k2hdkc](https://github.com/yahoojapan/k2hdkc), [k2hash](https://github.com/yahoojapan/k2hash), [chmpx](https://github.com/yahoojapan/chmpx) and [k2hash transaction plugin](https://github.com/yahoojapan/k2htp_dtor) components by [AntPickax](https://antpick.ax/).

## K2HR3 Systems/Components
The K2HR3 system consists of several subsystems and components.  
They are registered as **submodules in this repository**.  
Below is a brief description of each submodule.  

### K2HR3 Web Application
**K2HR3 Web Application** is one subsystem of K2HR3 system.  
This is accessed from the browser by users and operates as the control panel of the K2HR3 system.  
This is a JavaScript based web application that can manipulate all of the data required by users.  
_K2HR3 Web Application is created with [React.js](https://reactjs.org/) and [Node.js](https://nodejs.org/)._  

User can manipulate **Roles**, **policy Rules**, **Resource**, **Service** data using this **K2HR3 Web Application**.  

![K2HR3 Web Application](https://k2hr3.antpick.ax/images/usage_top_app_overview.png)

### K2HR3 REST API
**K2HR3 REST API** provides for manipulating data such as **ROLE**, **POLICY RULE**, **RESOURCE** and **SERVICE** stored in the K2HR3 Data Server([k2hdkc](https://github.com/yahoojapan/k2hdkc)).  

Using the K2HR3 REST API provided by this K2HR3 API server, the [K2HR3 Web Application](https://k2hr3.antpick.ax/usage_app.html) and its Web Server communicates with the K2HR3 Data Server([k2hdkc](https://github.com/yahoojapan/k2hdkc)).  
And users and hosts of the ROLE member directly call this K2HR3 REST API on this K2HR3 API Server, and get/put RESOURCE data.  

K2HR3 REST API and K2HR3 API Server is the server side JavaScript program running on [Node.js](https://nodejs.org/).  

![K2HR3 system overview](https://k2hr3.antpick.ax/images/detail_system_overview.png)

### K2HR3 OpenStack Notification Listener
**K2HR3 OpenStack Notification Listener** is an OpenStack Notification Listener that listens to notifications from OpenStack services.  
OpenStack services emit notifications to the message bus, which is provided by oslo.messaging transports notification messages to a message broker server.  
The default broker server is RabbitMQ.  
When **K2HR3 OpenStack Notification Listener** catches a notification message from RabbitMQ, it sends the payload to the K2hR3 system.  

![K2HR3 OpenStack Notificatoin Listener overview](https://k2hr3.antpick.ax/images/detail_osnl_details.png)

### K2HR3 Utilities
**K2HR3 Utilities** is a utility for the quick setup K2HR3 system.  
This will easily set up all the subcomponents of the K2HR3 system([K2HR3 Web Application](https://k2hr3.antpick.ax/usage_app.html) and Web Server, [K2HR3 REST API](https://k2hr3.antpick.ax/api.html), K2HR3 Data Server([k2hdkc](https://github.com/yahoojapan/k2hdkc)), [K2HR3 OpenStack Notification Listener](https://k2hr3.antpick.ax/detail_osnl.html)).
You can test the K2HR3 system in this environment.
**Before using K2HR3 Utilities**, OpenStack must be set up in the your environment.

**How to use K2HR3 Utilities** is explained in [K2HR3 Setup](https://k2hr3.antpick.ax/setup.html).

## Documents
[K2HR3 Document](https://k2hr3.antpick.ax/index.html)  
[K2HR3 Web Application Usage](https://k2hr3.antpick.ax/usage_app.html)  
[K2HR3 REST API Usage](https://k2hr3.antpick.ax/api.html)  
[K2HR3 OpenStack Notification Listener Usage](https://k2hr3.antpick.ax/detail_osnl.html)  
[K2HR3 Watcher Usage](https://k2hr3.antpick.ax/tools.html)  
[K2HR3 Utilities for Setup](https://k2hr3.antpick.ax/setup.html)  

[About k2hdkc](https://k2hdkc.antpick.ax/)  
[About k2hash](https://k2hash.antpick.ax/)  
[About chmpx](https://chmpx.antpick.ax/)  
[About k2hash transaction plugin](https://k2htpdtor.antpick.ax/)  

[About AntPickax](https://antpick.ax/)  

## Repositories
[K2HR3 main repository](https://github.com/yahoojapan/k2hr3)  
[K2HR3 Web Application repository](https://github.com/yahoojapan/k2hr3_app)  
[K2HR3 REST API repository](https://github.com/yahoojapan/k2hr3_api)  
[K2HR3 OpenStack Notification Listener](https://github.com/yahoojapan/k2hr3_osnl)  
[K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils)  

[k2hdkc](https://github.com/yahoojapan/k2hdkc)  
[k2hash](https://github.com/yahoojapan/k2hash)  
[chmpx](https://github.com/yahoojapan/chmpx)  
[k2hash transaction plugin](https://github.com/yahoojapan/k2htp_dtor)  

## Packages
[k2hr3-app(npm packages)]()  
[k2hr3-api(npm packages)]()  
[k2hr3-osnl(python packages)]()  

### License
This software is released under the MIT License, see the license file.

### AntPickax
K2HR3 is one of [AntPickax](https://antpick.ax/) products.

Copyright(C) 2017 Yahoo Japan Corporation.
