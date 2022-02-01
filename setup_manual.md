---
layout: contents
language: ja
title: Installation step by step
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_manualja.html
lang_opp_word: To Japanese
prev_url: setup_trial.html
prev_string: Build a trial environment
top_url: setup.html
top_string: Setup
next_url: setup_integrate.html
next_string: Integrated installation
---

# Installation step by step

This chapter instructs each K2HR3 subsystem installation in step-by-step manner. 

K2HR3 consists of four subsystems. Installation should be done from a subsystem in lower layer.

- K2HDKC Server
  - K2HDKC provides data storage.
  - You should install this subsystem at the first step because it exists the lowest layer.
- REST API Server
  - k2hr3-api forwards requests from web server and K2HR3 OpenStack Notification Listener.
  - You should install this subsystem at the second step.
- K2HR3 OpenStack Notification Listener
  - k2hr3-osnl listens to notification messages from OpenStack messaging backend.
  - k2hr3-osnl submits requests to REST API server.
  - You should install this subsystem after installing OpenStack and installing REST API server.
- Web Application Server
  - k2hr3-app accepts requests from users.
  - You should install this subsystem at the final step.

## K2HDKC Server

This section instructs how to install the data server(K2HDKC cluster).

Running `setup_dkc.sh` will complete installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh dkc/setup_dkc.sh
```

You can see the log messages of `setup_dkc.sh` by using **journalctl**. For example:

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

## REST API Server

This section instructs how to install the REST API server(k2hr3-api).

Running `setup_api.sh` with the following parameter will complete installation.

* The IP address of the Linux box where OpenStack services are running

We assume the IP address of the Linux box where OpenStack services are running is **192.168.1.1**. Here is an example of installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh api/setup_api.sh -i http://192.168.1.1/identity
```

You can see the log messages of `setup_api.sh` by using **journalctl**. For example:

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

## K2HR3 OpenStack Notification Listener

This section instructs how to install K2HR3 OpenStack Notification Listener(k2hr3-osnl).

Running `setup_osnl.sh` with the following parameters will complete installation.

- The username to login the messaging backend.
- The password to login the messaging backend.
- The IP address of the Linux box where the messaging backend is running
  - This IP address is identical with the Linux box if you install your OpenStack by using [DevStack](https://docs.openstack.org/devstack/latest/).

In this document, we assume that:
- The username to login the messaging backend is **stackrabbit**
- The password to login the messaging backend is **devstack**
- The IP address of the Linux box where the messaging backend is running is **192.168.1.1**

Here is an example of installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh osnl/setup_osnl.sh -t rabbit://stackrabbit:devstack@192.168.1.1:5672/
```

You can see the log messages of `setup_osnl.sh` by using **journalctl**. For example:

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

## Web Application Server

This section instructs how to install Web Application server(k2hr3-app).

Running `setup_app.sh` will complete installation.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh app/setup_app.sh
```

You can see the log messages of `setup_app.sh` by using **journalctl**. For example:

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

## Completion
With the above procedure, you can manually boot each subsystem for K2HR3 system.
