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
K2HR3 works as RBAC in cooperation with **OpenStack** and **kubernetes** which is one of **IaaS**(Infrastructure as a Service), and also provides useful functions for using RBAC.  

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

#### Demonstration site
You can access the [demonstration site](https://demo.k2hr3.antpick.ax/) of K2HR3 Web Application by accessing here.  
You can learn about Resource, Roles, policy Rules and SERVICE provided by K2HR3 on this site now.  
The data operated on this site can not be saved.  

### K2HR3 Command Line Interface
**K2HR3 Command Line Interface**(CLI) provides an interface that allows you to operate the [K2HR3 REST API](api.html) provided by K2HR3 from the command line.  
It provides the same function as [K2HR3 Web Application](usage_appja.html) for manipulating the data of the K2HR3 system as a **Command Line Interface**(CLI).

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

### K2HR3 Container Registration Sidecar
**K2HR3 Container Registration Sidecar** is a sidecar docker image for container registration to K2HR3 systems.  
This is a repository for creating docker images and publishing it on dockerhub.  
If you use the K2HR3 system to register a container, you can use the K2HR3 Web Application and get yaml to register a Sidecar that uses this image.  
You can start sidecar using the obtained yaml from K2HR3 Web Application.  

### K2HR3 Get Resource
**K2HR3 Get Resource** can be used in an environment where virtual computing(Virtual Machine) is started using User Data Script(for OpenStack) and automatically registered in the ROLE.  
**K2HR3 Get Resource** is a **Systemd timer service** that periodically acquires the RESOURCE corresponding to the ROLE in which the virtual computing(Virtual Machine) is registered.  
By using this, you can periodically acquire RESOURCE data and output it to a file or the like.  

### K2HR3 Helm Chart
**K2HR3 Helm Chart** is a **Helm Chart** for building a K2HR3 system using [Helm(The package manager for Kubernetes)](https://helm.sh/) in a kubernetes environment.  
By using this **Helm Chart**, you can easily build a K2HR3 system in a kubernetes environment.  
This can be used to build a K2HR3 system before using the [K2HDKC Helm Chart](https://dbaas.k2hdkc.antpick.ax/usage_helm_chart.html) to build a [K2HDKC DBaaS](https://dbaas.k2hdkc.antpick.ax/index.html) in a kubernetes environment.  

## Documents
[K2HR3 Document](https://k2hr3.antpick.ax/index.html)  
[K2HR3 Web Application Usage](https://k2hr3.antpick.ax/usage_app.html)  
[K2HR3 Command Line Interface Usage](https://k2hr3.antpick.ax/cli.html)  
[K2HR3 REST API Usage](https://k2hr3.antpick.ax/api.html)  
[K2HR3 Helm Chart Usage](https://k2hr3.antpick.ax/helm_chart.html)  
[K2HR3 OpenStack Notification Listener Usage](https://k2hr3.antpick.ax/detail_osnl.html)  
[K2HR3 Watcher Usage](https://k2hr3.antpick.ax/tools.html)  
[K2HR3 Get Resource Usage](https://k2hr3.antpick.ax/tools.html)  
[K2HR3 Utilities for Setup](https://k2hr3.antpick.ax/setup.html)  
[K2HR3 Demonstration](https://demo.k2hr3.antpick.ax/)

[About k2hdkc](https://k2hdkc.antpick.ax/)  
[About k2hash](https://k2hash.antpick.ax/)  
[About chmpx](https://chmpx.antpick.ax/)  
[About k2hash transaction plugin](https://k2htpdtor.antpick.ax/)  

[About AntPickax](https://antpick.ax/)  

## Repositories
[K2HR3 main repository](https://github.com/yahoojapan/k2hr3)  
[K2HR3 Web Application repository](https://github.com/yahoojapan/k2hr3_app)  
[K2HR3 Command Line Interface repository](https://github.com/yahoojapan/k2hr3_cli)  
[K2HR3 REST API repository](https://github.com/yahoojapan/k2hr3_api)  
[K2HR3 Helm Chart repository](https://github.com/yahoojapan/k2hr3_helm_chart)  
[K2HR3 OpenStack Notification Listener](https://github.com/yahoojapan/k2hr3_osnl)  
[K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils)  
[K2HR3 Container Registration Sidecar](https://github.com/yahoojapan/k2hr3_sidecar)  
[K2HR3 Get Resource](https://github.com/yahoojapan/k2hr3_get_resource)  

[k2hdkc](https://github.com/yahoojapan/k2hdkc)  
[k2hash](https://github.com/yahoojapan/k2hash)  
[chmpx](https://github.com/yahoojapan/chmpx)  
[k2hash transaction plugin](https://github.com/yahoojapan/k2htp_dtor)  

## Packages
[k2hr3-app(npm packages)](https://www.npmjs.com/package/k2hr3-app)  
[k2hr3-api(npm packages)](https://www.npmjs.com/package/k2hr3-api)  
[k2hr3-cli(packages)](https://packagecloud.io/app/antpickax/stable/search?q=k2hr3-cli)  
[k2hr3 helm chart(artifact hub)](https://artifacthub.io/packages/helm/k2hr3/k2hr3)
[k2hr3-osnl(python packages)](https://pypi.org/project/k2hr3-osnl/)  
[k2hr3-get-resource(packages)](https://packagecloud.io/app/antpickax/stable/search?q=k2hr3-get-resource)  

[k2hr3-app (dockerhub)](https://hub.docker.com/r/antpickax/k2hr3-app)  
[k2hr3-api (dockerhub)](https://hub.docker.com/r/antpickax/k2hr3-api)  
[k2hr3.sidecar(dockerhub)](https://hub.docker.com/r/antpickax/k2hr3.sidecar)  

### License
This software is released under the MIT License, see the license file.

### AntPickax
K2HR3 is one of [AntPickax](https://antpick.ax/) products.

Copyright(C) 2017 Yahoo Japan Corporation.
