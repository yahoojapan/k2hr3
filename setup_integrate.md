---
layout: contents
language: ja
title: Integrated installation
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_integrateja.html
lang_opp_word: To Japanese
prev_url: setup_manual.html
prev_string: Installation step by step
top_url: setup.html
top_string: Setup
next_url: 
next_string: 
---

# Integrated installation

This chapter instructs the simplest way to install your K2HR3 system in localhost.

## About IaaS

The K2HR3 system described in this document can set up the K2HR3 system on the [OpenStack](https://www.openstack.org/) and [kubernetes](https://kubernetes.io/) IaaS environments.  
Below are the documents related to the construction of each IaaS.  

### OpenStack installation

This section describes OpenStack installation.

OpenStack is required for K2HR3 system. If you have no OpenStack environment, see the following installation guides. [DevStack](https://docs.openstack.org/devstack/latest/) is a useful tool to quickly prepare an OpenStack environment for local development environment.

- `Installation Guides` in [OpenStack Documentation](https://docs.openstack.org)
  - These guides show you how to get started with the most commonly used OpenStack services.
- [DevStack](https://docs.openstack.org/devstack/latest/)
  - This guide shows you how to get started with the latest OpenStack services.

### kubernetes installation

This section describes kubernetes installation.

- If you build kubernetes by [**minikube**](https://kubernetes.io/docs/tutorials/hello-minikube/) for simple test.  
When you are using `minikube`, set the proxy appropriately.
- If you build kubernetes by [**kubeadm**](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#).
- If you build kubernetes by [**Rancher**](https://rancher.com/).

## About System requirements

K2HR3 system currently depends on the following software.
- Linux
  - Debian buster and Stretch
  - Fedora 32, 31 and 30
  - CentOS 7 and 8
  - Ubuntu 16.04, 18.04, and 20.04
- OpenStack
  - Ussuri
- kubernetes
- Node.js
  - Node.js 10.x, 12.x and 14.x
- Python
  - Python 3.6 and 3.8 

## K2HR3 Integrated installation

This section instructs how to install all K2HR3 subsystems by executing only one command, `cluster.sh`.  
_The following documents are for building an environment that links with OpenStack. When linking with kubernetes only, the following work for OpenStack is not required._  

Running `cluster.sh` with the following parameters will complete installation.

- The IP address of the Linux box where OpenStack services are running
- The username to login the messaging backend.
- The password to login the messaging backend.
- The IP address of the Linux box where the messaging backend is running
  - This IP address is identical with the Linux box if you install your OpenStack by using [DevStack](https://docs.openstack.org/devstack/latest/).

In this document, we assume that:

- The IP address of the Linux box where OpenStack services are running is *192.168.1.1*.
- The username to login the messaging backend is *stackrabbit*
- The password to login the messaging backend is *devstack*
- The IP address of the Linux box where the messaging backend is running is *192.168.1.1*

To start installation, run the following commands in the Linux box:

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh cluster.sh \
 -s http://192.168.1.1/identity \
 -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

You can see the log messages of `cluster.sh` by using *journalctl*. For example:

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

## Confirmation of K2HR3 system

Make sure that the following six processes are running.

- chmpx(server)
  - An AntPickax messaging proxy server process, which accepts requests from chmpx(slave) and forwards them to k2hdkc
- chmpx(slave) 
  - An AntPickax messaging proxy server process, which forwards requests from k2hr3-api
- k2hdkc 
  - A distributed KVS server process
- node(k2hr3-api) 
  - An REST ASPI server process
- node(k2hr3-app) 
  - A Web Application server process
- python3(k2hr3-osnl) 
  - A process to listen to OpenStack notification messages

Here is an example to check if those processes exist:

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

**systemctl** provides information about the status of each process. 

### **chmpx(server)**'s process status

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

### **chmpx(slave)**'s process status

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

### **k2hdkc**'s process status

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

### **node(k2hr3-api)**'s process status

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

### **node(k2hr3-app)**'s process status

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

### **python(k2hr3-osnl)**'s process status

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

## Completion
With the above procedure, you can build the K2HR3 system all at once.
