---
layout: contents
language: ja
title: Build a trial environment
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_trialja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: setup.html
top_string: Setup
next_url: 
next_string: 
---

# Build a trial environment
Describes how to build an environment for easily trying out the K2HR3 system.  
By following the steps below, you can start the processes that make up the core of the K2HR3 system on one host(or `Virtual Machine`) and build a trial environment.  

## Required environment
An OpenStack system that works with the K2HR3 system is required.  
For the OpenStack system, an environment built with `devstack` is sufficient, and there is no problem as long as the environment where OpenStack's `Identity(Keystone)` is working.  

And, prepare the host to build the trial environment.  
This host can be `Bare Metal` or` Virtual Machine`.  

## Tools
The tool for building and stopping the trial environment is [devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack) of [K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils/) is used.  
You can easily build and stop the trial environment by expanding this repository(directory) and executing the script.  

## Information required before construction
Before building the trial environment, please check the information below.  

### Execution user
Decide who will run the processes in your K2HR3 system.  
For example, run the process with `nobody`.  

### HOST to startup the K2HR3 system on
Check the `hostname` or `IP address` of the host(or `Virtual Machine`) that builds the trial environment.  

### Host accessed from a browser
In order to access the trial environment from a browser, you need to access this host from a browser.  
In an environment where direct access is not possible, a host(proxy) etc. that goes through when accessing from the outside is required.  
When using such a host environment, check the `hostname` or `IP address` of the host(proxy) that you go through when accessing from the outside.  

For example, when using an instance(`Virtual Machine`) such as OpenStack as a host, it is necessary to set a security group(OpenStack) or run a proxy in order to access this instance directly from the outside.  
The tool for building a trial environment can output a configuration file( [HAProxy](http://www.haproxy.org/) ) that assumes that [HAProxy](http://www.haproxy.org/) will be started as a proxy for such an environment.  
You can run [HAProxy](http://www.haproxy.org/) with this configuration file to build an environment even if you cannot access it directly.  

### OpenStack Region
Check the region name of the OpenStack system with which the K2HR3 system works.  
For OpenStack built with `devstack`, it is mainly `RegionOne`.  

### Identity(Keystone) URL
Check the URL of `Identity(Keystone)` of the OpenStack system with which the K2HR3 system works.  

### The port number for K2HR3 Web Application
Decide the port number of `K2HR3 Web Application` in the trial environment.  
If your environment requires a proxy as described above, also determine the port number of `K2HR3 Web Application` on the proxy.  

### The port number for K2HR3 REST API
Decide the port number of `K2HR3 REST API` in the trial environment.  
If your environment requires a proxy as described above, also determine the port number for the `K2HR3 REST API` on the proxy.  
The `K2HR3 REST API` is accessed from the` K2HR3 Web Application` loaded by the browser, so it must be accessible from the outside(`K2HR3 Web Application`).  

## Build
This section describes how to build a trial environment.  
The construction procedure may be built on a host that can be accessed directly from the outside, or it may be built on a host that can be accessed using a proxy or the like.  
Below description will explain each case separately.  

### Build on a host that does not require a proxy
In the following example, the above parameters are set as follows to run the tool.  

- Execution user : `nobody`
- HOST to startup the K2HR3 system on : `192.168.10.20`
- OpenStack Region : `RegionOne`
- Identity(Keystone) URL : `http://192.168.10.10/identity`
- Port number for K2HR3 Web Application : `80`
- Port number for K2HR3 REST API : `8080`

_Since no proxy is used, no parameters other than the above are required._  

First, clone the [K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils) repository.
```
$ git clone https://github.com/yahoojapan/k2hr3_utils.git
```
Then go to the [devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack) directory and run the following command.
```
$ cd k2hr3_utils/devpack
$ bin/devpack.sh -ni -nc --run_user nobody --openstack_region RegionOne  --keystone_url http://192.168.10.10/identity --app_host localhost --app_port 80 --api_host localhost --api_port 8080
```
If the `devpack.sh` script is executed successfully, the trial environment has been built.  

To check the operation, access the following URL from your browser.
```
http://192.168.10.20:80/
```
_The trial environment does not support `HTTPS`._

### Build on a host that requires a proxy
In the following example, the above parameters are set as follows to run the tool.  

- Execution user : `nobody`
- HOST to startup the K2HR3 system on : `192.168.10.20`
- HOST accessed from a browser : `172.16.16.16`
- OpenStack Region : `RegionOne`
- Identity(Keystone) URL : `http://192.168.10.10/identity`
- Port number for K2HR3 Web Application(on HOST) : `80`
- Port number for K2HR3 Web Application(on Proxy) : `28080`
- Port number for K2HR3 REST API(on HOST) : `8080`
- Port number for K2HR3 REST API(on Proxy) : `18080`

First, clone the [K2HR3 Utilities](https://github.com/yahoojapan/k2hr3_utils) repository.
```
$ git clone https://github.com/yahoojapan/k2hr3_utils.git
```
Then go to the [devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack) directory and run the following command.
```
$ cd k2hr3_utils/devpack
$ bin/devpack.sh -ni -nc --run_user nobody --openstack_region RegionOne --keystone_url http://192.168.10.10/identity --app_host 192.168.10.20 --app_port 80 --app_host_external 172.16.16.16 --app_port_external 28080 --api_host 192.168.10.20 --api_port 8080 --api_host_external 172.16.16.16 --api_port_external 18080
```
If the `devpack.sh` script is executed successfully, the trial environment has been built.  

After the `devpack.sh` script has completed execution, the [HAProxy](http://www.haproxy.org/) configuration file( `k2hr3_utils/devpack/conf/haproxy_example.cfg` ) has been created.  
Use this file to start [HAProxy](http://www.haproxy.org/) as follows.
```
$ haproxy -f k2hr3_utils/devpack/conf/haproxy_example.cfg
```
When [HAProxy](http://www.haproxy.org/) starts, access the following URL from your browser and check the operation.  
```
http://172.16.16.16:28080/
```

## Stop and Clear
To stop the K2HR3 system in the started trial environment, execute the script as follows.  
```
$ cd k2hr3_utils/devpack
$ bin/stopdevpack.sh
```
If you want to stop and delete all the files automatically created when you start the trial environment, execute as follows.
```
$ cd k2hr3_utils/devpack
$ bin/stopdevpack.sh --clear
```
