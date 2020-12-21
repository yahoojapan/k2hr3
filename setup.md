---
layout: contents
language: en
title: Setup
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setupja.html
lang_opp_word: To Japanese
prev_url: usage.html
prev_string: Usage
top_url: index.html
top_string: TOP
next_url: developer.html
next_string: Developer
---

# Quick Start

This page provides information about quickly bringing up a complete K2HR3 system in a Linux host.  

If you want to easily build and try a minimal K2HR3 system, see [Build a Trial Environment](setup_trial.html).  

## System requirements

K2HR3 currently depends on the following software.

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

## K2HR3 System Overview

The following figure shows the K2HR3 system overview. Remember this guide assumes all subsystems are running within one Linux box.

![K2HR3 Setup overview](images/setup_overview.png)

The following chapters instructs two ways to install K2HR3 system subsystems.

* Integrated installation
  * Installation is complete by executing only one command
* Installation step by step
  * Installation is complete by executing a series of commands per each subsystem.

## Integrated installation

This chapter instructs the simplest way to install your K2HR3 system in localhost.


### OpenStack installation

This section describes OpenStack installation.

OpenStack is required for K2HR3 system. If you have no OpenStack environment, see the following installation guides. [DevStack](https://docs.openstack.org/devstack/latest/) is a useful tool to quickly prepare an OpenStack environment for local development environment.

* 'Installation Guides' in [OpenStack Documentation](https://docs.openstack.org)
  * These guides show you how to get started with the most commonly used OpenStack services.
* [DevStack](https://docs.openstack.org/devstack/latest/)
  * This guide shows you how to get started with the latest OpenStack services.

### kubernetes installation

This section describes kubernetes installation.

* If you build kubernetes by [**minikube**](https://kubernetes.io/docs/tutorials/hello-minikube/) for simple test.  
When you are using minikube, set the proxy appropriately.
* If you build kubernetes by [**kubeadm**](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#).
* If you build kubernetes by [**Rancher**](https://rancher.com/).

### K2HR3 installation

This section instructs how to install all K2HR3 subsystems by executing only one command, 'cluster.sh'.  
_The following documents are for building an environment that links with OpenStack. When linking with kubernetes only, the following work for OpenStack is not required._  

Running 'cluster.sh' with the following parameters will complete installation.

* The IP address of the Linux box where OpenStack services are running
* The username to login the messaging backend.
* The password to login the messaging backend.
* The IP address of the Linux box where the messaging backend is running
  * This IP address is identical with the Linux box if you install your OpenStack by using [DevStack](https://docs.openstack.org/devstack/latest/).

In this document, we assume that::

* The IP address of the Linux box where OpenStack services are running is *192.168.1.1*.
* The username to login the messaging backend is *stackrabbit*
* The password to login the messaging backend is *devstack*
* The IP address of the Linux box where the messaging backend is running is *192.168.1.1*

To start installation, run the following commands in the Linux box::

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh cluster.sh \
 -s http://192.168.1.1/identity \
 -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

You can see the log messages of 'cluster.sh' by using *journalctl*. For example::

```bash
$ journalctl -t cluster.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 03:17:01 UTC. --
Feb 06 00:13:04 ubuntu18 cluster.sh[1580]: cluster.sh 0.0.1
Feb 06 00:13:04 ubuntu18 cluster.sh[1582]: sh dkc/setup_dkc.sh
Feb 06 00:14:41 ubuntu18 cluster.sh[13802]: sh api/setup_api.sh -i http://192.168.1.1/identity
Feb 06 00:16:55 ubuntu18 cluster.sh[20490]: sh app/setup_app.sh
Feb 06 00:17:37 ubuntu18 cluster.sh[22739]: sh osnl/setup_osnl.sh -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
Feb 06 00:19:26 ubuntu18 cluster.sh[26121]: completed in 382 seconds
```

### Monitoring processes

Make sure that the following six processes are running.

* chmpx(server)
  * A messaging proxy server process, which accepts requests from chmpx(slave) and forwards them to k2hdkc
* chmpx(slave) 
  * A messaging proxy server process, which forwards requests from k2hr3-api
* k2hdkc 
  * A distributed KVS server process
* node(k2hr3-api) 
  * An api server process
* node(k2hr3-app) 
  * A web server process
* python3(k2hr3-osnl) 
  * A process to listen to OpenStack notification messages

Here is an example to check if those processes exist::

```bash
$ ps -U k2hr3 -o cmd
CMD
/usr/bin/chmpx -conf /etc/k2hdkc/slave.ini -d err
/usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
/usr/bin/chmpx -conf /etc/k2hdkc/server.ini -d err
/usr/bin/k2hdkc -conf /etc/k2hdkc/server.ini -d err
/usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
/usr/bin/python3 /usr/local/bin/k2hr3-osnl -c /usr/local/etc/k2hr3/k2hr3-osnl.conf
```

*systemctl* provides information about the status of each process. 

Here is an example of the *chmpx(server)*'s process status::

```bash
$ systemctl status chmpx.service
● chmpx.service - chmpx
   Loaded: loaded (/etc/systemd/system/chmpx.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:14:41 UTC; 1 day 2h ago
 Main PID: 13790 (chmpx)
    Tasks: 20 (limit: 1152)
   CGroup: /system.slice/chmpx.service
           └─13790 /usr/bin/chmpx -conf /etc/k2hdkc/server.ini -d err

Feb 06 00:14:41 ubuntu18 systemd[1]: Started chmpx.
```

Here is an exam-pl of the *chmpx(slave)*'s process status::

```bash
$ systemctl status chmpx-slave.service
● chmpx-slave.service - chmpx
   Loaded: loaded (/etc/systemd/system/chmpx-slave.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 03:40:00 UTC; 23h ago
 Main PID: 11210 (chmpx)
    Tasks: 36 (limit: 1152)
   CGroup: /system.slice/chmpx-slave.service
           └─11210 /usr/bin/chmpx -conf /etc/k2hdkc/slave.ini -d err

Feb 06 03:40:00 ubuntu18 systemd[1]: Starting chmpx...
Feb 06 03:40:00 ubuntu18 sysctl[11206]: fs.mqueue.msg_max = 1024
Feb 06 03:40:00 ubuntu18 systemd[1]: Started chmpx.
```

Here is an exam-pl of the *k2hdkc*'s process status::

```bash
$ systemctl status k2hdkc.service
● k2hdkc.service - k2hdkc
   Loaded: loaded (/etc/systemd/system/k2hdkc.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:14:41 UTC; 1 day 2h ago
 Main PID: 13796 (k2hdkc)
    Tasks: 3 (limit: 1152)
   CGroup: /system.slice/k2hdkc.service
           └─13796 /usr/bin/k2hdkc -conf /etc/k2hdkc/server.ini -d err

Feb 06 00:14:41 ubuntu18 systemd[1]: Starting k2hdkc...
Feb 06 00:14:41 ubuntu18 systemd[1]: Started k2hdkc.
```

Here is an exam-pl of the *node(k2hr3-api)*'s process status::

```bash
$ systemctl status k2hr3-api.service
● k2hr3-api.service - k2hr3-api
   Loaded: loaded (/etc/systemd/system/k2hr3-api.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 04:01:41 UTC; 23h ago
 Main PID: 11428 (node)
    Tasks: 23 (limit: 1152)
   CGroup: /system.slice/k2hr3-api.service
           ├─11428 /usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
           └─11452 /usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www

Feb 06 04:01:41 ubuntu18 systemd[1]: Started k2hr3-api.
```

Here is an exam-pl of the *node(k2hr3-app)*'s process status::

```bash
$ systemctl status k2hr3-app.service
● k2hr3-app.service - k2hr3-app
   Loaded: loaded (/etc/systemd/system/k2hr3-app.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:17:37 UTC; 1 day 2h ago
 Main PID: 22733 (node)
    Tasks: 22 (limit: 1152)
   CGroup: /system.slice/k2hr3-app.service
           ├─22733 /usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
           └─22783 /usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www

Feb 06 00:17:37 ubuntu18 systemd[1]: Started k2hr3-app.
```

Here is an exam-pl of the *python(k2hr3-osnl)*'s process status::

```
$ systemctl status k2hr3-osnl.service
● k2hr3-osnl.service - K2HR3 OpenStack Notification Listener
   Loaded: loaded (/etc/systemd/system/k2hr3-osnl.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2019-02-06 00:19:26 UTC; 1 day 2h ago
 Main PID: 26108 (k2hr3-osnl)
    Tasks: 14 (limit: 1152)
   CGroup: /system.slice/k2hr3-osnl.service
           └─26108 /usr/bin/python3 /usr/local/bin/k2hr3-osnl -c /usr/local/etc/k2hr3/k2hr3-osnl.conf

Feb 06 00:19:26 ubuntu18 systemd[1]: Started K2HR3 OpenStack Notification Listener.
```

## Installation step by step

This chapter instructs each K2HR3 subsystem installation in step-by-step manner. 

K2HR3 consists of four subsystems. Installation should be done from a subsystem in lower layer.

* Data server(K2HDKC)
  * K2HDKC provides data storage.
  * You should install this subsystem at the first step because it exists the lowest layer.
* API server(k2hr3-api)
  * k2hr3-api forwards requests from web server and K2HR3 OpenStack Notification Listener.
  * You should install this subsystem at the second step.
* K2HR3 OpenStack Notification Listener
  * k2hr3-osnl listens to notification messages from OpenStack messaging backend.
  * k2hr3-osnl submits requests to API server.
  * You should install this subsystem after installing OpenStack and installing API server.
* Web server(k2hr3-app)
  * k2hr3-app accepts requests from users.
  * You should install this subsystem at the final step.

### Data server(K2HDKC)

This section instructs how to install the data server(K2HDKC).

Running 'setup_dkc.sh' will complete installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh dkc/setup_dkc.sh
```

You can see the log messages of 'setup_dkc.sh' by using *journalctl*. For example::

```bash
$ journalctl -t setup_dkc.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:13:04 ubuntu18 setup_dkc.sh[1590]: setup_dkc.sh 0.0.1
Feb 06 00:13:04 ubuntu18 setup_dkc.sh[1591]: 1. Initializes environments
Feb 06 00:13:05 ubuntu18 setup_dkc.sh[1596]: 2. Ensures that the k2hdkc data directory exists
Feb 06 00:13:05 ubuntu18 setup_dkc.sh[1629]: 3. Ensures that the k2hdkc configuration directory exists
Feb 06 00:13:05 ubuntu18 setup_dkc.sh[1634]: 4. Adds a new package repository
Feb 06 00:13:43 ubuntu18 setup_dkc.sh[2484]: 5. Installs OS dependent packages
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13650]: 6. Configures the default chmpx configuration
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13655]: 7. Installs the configured chmpx config file
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13659]: 8. Configures the chmpx's service manager default configuration
Feb 06 00:14:39 ubuntu18 setup_dkc.sh[13666]: 9. Installs the chmpx service manager configuration and enables it
Feb 06 00:14:40 ubuntu18 setup_dkc.sh[13722]: 10. Configures the k2hdkc's service manager default configuration
Feb 06 00:14:40 ubuntu18 setup_dkc.sh[13729]: 11. Installs the k2hdkc service manager configuration and enables it
Feb 06 00:14:41 ubuntu18 setup_dkc.sh[13800]: completed in 97 seconds
```

### API server

This section instructs how to install the api server(k2hr3-api).

Running 'setup_api.sh' with the following parameter will complete installation.

* The IP address of the Linux box where OpenStack services are running

We assume the IP address of the Linux box where OpenStack services are running is *192.168.1.1*. Here is an example of installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh api/setup_api.sh -i http://192.168.1.1/identity
```

You can see the log messages of 'setup_api.sh' by using *journalctl*. For example::

```bash
$ journalctl -t setup_api.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:14:41 ubuntu18 setup_api.sh[13810]: setup_api.sh 0.0.1
Feb 06 00:14:41 ubuntu18 setup_api.sh[13811]: 1. Initializes environments
Feb 06 00:14:41 ubuntu18 setup_api.sh[13825]: 2. Ensures that the k2hr3_api data directory exists
Feb 06 00:14:41 ubuntu18 setup_api.sh[13836]: 3. Ensures that the k2hdkc configuration directory exists
Feb 06 00:14:41 ubuntu18 setup_api.sh[13839]: 4. Adds a new package repository
Feb 06 00:15:10 ubuntu18 setup_api.sh[15687]: 5. Installs OS dependent packages
Feb 06 00:15:30 ubuntu18 setup_api.sh[15995]: 6. Configures the default chmpx slave configuration
Feb 06 00:15:30 ubuntu18 setup_api.sh[15998]: 7. Installs the configured chmpx slave config file
Feb 06 00:15:30 ubuntu18 setup_api.sh[16002]: 8. Configures the chmpx slave's service manager default configuration
Feb 06 00:15:30 ubuntu18 setup_api.sh[16009]: 9. Installs the chmpx-slave service manager configuration and enables it
Feb 06 00:15:31 ubuntu18 setup_api.sh[16065]: 10. Installs devel packages to build the k2hdkc node module
Feb 06 00:16:18 ubuntu18 setup_api.sh[19987]: 11. Installs npm packages
Feb 06 00:16:54 ubuntu18 setup_api.sh[20405]: 14. Configures the k2hr3-api's service manager default configuration
Feb 06 00:16:54 ubuntu18 setup_api.sh[20413]: 15. Installs the k2hr3-api service manager configuration and enables it
Feb 06 00:16:55 ubuntu18 setup_api.sh[20483]: completed in 134 seconds
```

### K2HR3 OpenStack Notification Listener

This section instructs how to install K2HR3 OpenStack Notification Listener(k2hr3-osnl).

Running 'setup_osnl.sh' with the following parameters will complete installation.

* The username to login the messaging backend.
* The password to login the messaging backend.
* The IP address of the Linux box where the messaging backend is running
  * This IP address is identical with the Linux box if you install your OpenStack by using [DevStack](https://docs.openstack.org/devstack/latest/).

In this document, we assume that::

* The username to login the messaging backend is *stackrabbit*
* The password to login the messaging backend is *devstack*
* The IP address of the Linux box where the messaging backend is running is *192.168.1.1*

Here is an example of installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh osnl/setup_osnl.sh -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

You can see the log messages of 'setup_osnl.sh' by using *journalctl*. For example::

```bash
$ journalctl -t setup_osnl.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22750]: setup_osnl.sh 0.0.1
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22754]: 1. Initializes environments
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22759]: 2. Adds a new package repository
Feb 06 00:17:37 ubuntu18 setup_osnl.sh[22760]: 3. Installs system packages
Feb 06 00:19:21 ubuntu18 setup_osnl.sh[26010]: 4. Installs the k2hr3-osnl pypi package
Feb 06 00:19:25 ubuntu18 setup_osnl.sh[26027]: 5. Configures the k2hr3-osnl.conf and Installs it
Feb 06 00:19:25 ubuntu18 setup_osnl.sh[26043]: 6. Installs a systemd configuration for k2hr3_osnl
Feb 06 00:19:25 ubuntu18 setup_osnl.sh[26048]: 7. Registers and enables k2hr3_osnl to systemd
Feb 06 00:19:26 ubuntu18 setup_osnl.sh[26112]: completed in 109 seconds
```

### Web server

This section instructs how to install web server(k2hr3-app).

Running 'setup_app.sh' will complete installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh app/setup_app.sh
```

You can see the log messages of 'setup_app.sh' by using *journalctl*. For example::

```bash
$ journalctl -t setup_app.sh -p info
-- Logs begin at Tue 2019-02-05 10:34:05 UTC, end at Thu 2019-02-07 02:45:30 UTC. --
Feb 06 00:16:55 ubuntu18 setup_app.sh[20505]: setup_app.sh 0.0.1
Feb 06 00:16:55 ubuntu18 setup_app.sh[20506]: 1. Initializes environments
Feb 06 00:16:55 ubuntu18 setup_app.sh[20511]: 2. Adds a new package repository
Feb 06 00:17:17 ubuntu18 setup_app.sh[22479]: 3. Installs OS dependent packages
Feb 06 00:17:18 ubuntu18 setup_app.sh[22485]: 4. Install the k2hr3-app npm package
Feb 06 00:17:36 ubuntu18 setup_app.sh[22665]: 7. Configures the k2hr3-app's service manager default configuration
Feb 06 00:17:36 ubuntu18 setup_app.sh[22673]: 8. Installs the k2hr3-app service manager configuration and enables it
Feb 06 00:17:37 ubuntu18 setup_app.sh[22737]: completed in 42 seconds
```
