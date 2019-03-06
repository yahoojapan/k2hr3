---
layout: contents
language: en
title: Environments/Settings
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: environmentsja.html
lang_opp_word: To Japanese
prev_url: developer.html
prev_string: Developer
top_url: index.html
top_string: TOP
next_url: tools.html
next_string: Tools
---

This page provides information about environment variables and settings in K2HR3 system.

# Environment variables

The followings describes environment variables in K2HR3 system.

## Environment variables in API server

This chapter describes environment variables in K2HR3 API server.

### HOME

This variable specifies the home directory of user who executes the 'k2hr3-api' Node.js process, which is a HTTP server daemon process in API server. The default value is */home/k2hr3* when you install API server by using *devcluster*.


### NODE_CONFIG_DIR

This variable specifies the path where the configuration files of k2hr3-api Node.js module, which is a main module of API server, are installed. The default value is */home/k2hr3/etc/k2hr3-api* when you install API server by using *devcluster*.


### NODE_DEBUG

This variable specifies the log priority of 'k2hr3-api' Node.js process. These are valid values::

* LOGLEVEL_DBG
  * Use this setting to print verbose logs of API server process.
* LOGLEVEL_MSG
  * Use this setting to print informative logs of API server process.
* LOGLEVEL_WAN
  * Use this setting to print warning logs of API server process.
* LOGLEVEL_ERR(default)
  * Use this setting to print error logs of API server process.
* LOGLEVEL_SLT　
  * Use this setting to print no logs.


### NODE_ENV

This variable specifies the environment where the Node.js process runs. These are valid values::

* development
  * Use this setting when you run the API server Node.js process for development purpose.
* production
  * Use this setting when you run the API server Node.js process in production environment.

The default value is *development* when you install Web server by using *devcluster*.

### Tips: Applies environment variables to processes by using systemd

This section instructs how to apply environment variables when starting a process by using [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Settings of [systemd](https://www.freedesktop.org/wiki/Software/systemd/) are not always necessary. If you would like to control each API server process as a systemd service, this tips will help you.

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) is a service manager for Linux that controls userspace processes. It brings up userspace processes in configured order during booting a Linux installation. After starting up processes, it tries to keep them up. On shutdown, systemd terminates all the other processes.

Use [Environment variables](https://www.freedesktop.org/software/systemd/man/systemd.exec.html#Environment) in [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) configuration to apply environment variables for API server processes.

The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'k2hr3-api' service, which serves HTTP service in API server, will be installed in /etc/systemd/system/k2hr3-api.service when you install API server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'k2hr3-api' service. Note that the order to start up a service is important. The 'k2hr3-api' service must starts after the 'chmpx-slave' service, which forwards requests from HTTP server processes to Data server.
```
[Unit]
Description=k2hr3-api
Requires=chmpx-slave.service
After=chmpx-slave.service

[Service]
Type=simple
WorkingDirectory=/home/k2hr3
Environment=HOME=/home/k2hr3
Environment=NODE_CONFIG_DIR=/home/k2hr3/etc/k2hr3-api
Environment=NODE_DEBUG=LOGLEVEL_ERR
Environment=NODE_ENV=development
ExecStart=/usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
Restart=on-failure
PIDFile=/var/run/k2hr3-api.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-api.service
```

## Web server

This chapter describes environment variables in K2HR3 Web server.

### HOME

This variable specifies the home directory of user who executes the 'k2hr3-app' Node.js process, which is a HTTP server daemon process in Web server. The default value is */home/k2hr3* when you install Web server by using *devcluster*.

### NODE_CONFIG_DIR

This variable specifies the path where the configuration files of k2hr3-app Node.js module, which is a main module of Web server, are installed. The default value is */home/k2hr3/etc/k2hr3-app* when you install Web server by using *devcluster*.

### NODE_ENV

This variable specifies the environment where the Node.js process runs. These are valid values::

* development
  * Use this setting when you run the Web server Node.js process for development purpose.
* production
  * Use this setting when you run the Web server Node.js process in production environment.

The default value is *development* when you install Web server by using *devcluster*.


### Tips: Applies environment variables to processes by using systemd

This section instructs how to apply environment variables when starting a process by using [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Settings of [systemd](https://www.freedesktop.org/wiki/Software/systemd/) are not always necessary. If you would like to control each Web server process as a systemd service, this tips will help you.

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) is a service manager for Linux that controls userspace processes. It brings up userspace processes in configured order during booting a Linux installation. After starting up processes, it tries to keep them up. On shutdown, systemd terminates all the other processes.

Use [Environment variables](https://www.freedesktop.org/software/systemd/man/systemd.exec.html#Environment) in [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) configuration to apply environment variables for Web server processes.

The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'k2hr3-app' service, which serves HTTP service in Web server, will be installed in /etc/systemd/system/k2hr3-app.service when you install Web server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'k2hr3-app' service. The 'k2hr3-app' service must run after the [Network](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) is up.

```
[Unit]
Description=k2hr3-app
After=network-online.target

[Service]
Type=simple
WorkingDirectory=/home/k2hr3
Environment=HOME=/home/k2hr3
Environment=NODE_CONFIG_DIR=/home/k2hr3/etc/k2hr3-app
Environment=NODE_DEBUG=LOGLEVEL_ERR
Environment=NODE_ENV=development
ExecStart=/usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
Restart=on-failure
PIDFile=/var/run/k2hr3-app.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-app.service
```

# Settings

The followings describes settings in K2HR3 system.

## Data server(K2HDKC)

This chapter describes settings of Data server.

* Here describes the minimum settings of Data server(K2HDKC).
* See [K2HDKC](https://k2hdkc.antpick.ax/) for details.
* See [CHMPX details](https://chmpx.antpick.ax/details.html) for [K2HDKC](https://k2hdkc.antpick.ax/) settings.

Data server(K2HDKC) can be a cluster where a chmpx process and a k2hdkc process runs.
* A chmpx process
  * A server process to connect hosts together as a distributed KVS cluster through network.
  * The configuration file will be installed in /etc/k2hdkc/server.ini
* A k2hdkc process
  * A server process to accept requests to read and write the K2HR3 database through network.
  * The configuration file is same with the chmpx process.

The **NAME** setting in the **[SVRNODE]** section lists hosts of Data server. If dkc01~dkc04.example.com were the Data server hosts, you could write them in a regex-like form::
```
...
#
# SERVER NODES SECTION
#
[SVRNODE]
NAME                            = dkc[1-4].example.com
PORT                            = 8020
CTLPORT                         = 8021
SSL                             = no
...
```


### Tips: Controls processes by using systemd

This section instructs how to control processes by using [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Settings of [systemd](https://www.freedesktop.org/wiki/Software/systemd/) are not always necessary. If you would like to control each Web server process as a systemd service, this tips will help you.

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) is a service manager for Linux that controls userspace processes. It brings up userspace processes in configured order during booting a Linux installation. After starting up processes, it tries to keep them up. On shutdown, systemd terminates all the other processes.

The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'chmpx' service will be installed in /etc/systemd/system/chmpx.service when you install Data server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'chmpx' service. 

```
[Unit]
Description=chmpx
After=network-online.target

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStartPre=/sbin/sysctl fs.mqueue.msg_max=1024
ExecStart=/usr/bin/chmpx -conf /etc/k2hdkc/server.ini -d err
Restart=on-failure
PIDFile=/var/run/chmpx.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart chmpx.service
```

Then, configure the 'k2hdkc' service. The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'k2hdkc' service will be installed in /etc/systemd/system/k2hdkc.service when you install Data server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'k2hdkc' service. The 'k2hdkc' service must run after the 'chmpx' service is up.

```
[Unit]
Description=k2hdkc
Requires=chmpx.service
After=chmpx.service

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStartPre=/sbin/sysctl fs.mqueue.msg_max=1024
ExecStart=/usr/bin/k2hdkc -conf /etc/k2hdkc/server.ini -d err
Restart=on-failure
PIDFile=/var/run/k2hdkc.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hdkc.service
```

## API Server

This chapter describes settings of processes in API server.

The following three kinds of processes are up and running in API server.

* HTTP server
  * The HTTP server is implemented by [Node.js](https://nodejs.org/).
* chmpx-slave
  * chmpx-slave forwards requests from HTTP server processes to Data server.
  * The configuration file is /etc/k2hdkc/slave.ini.
	* You need update Data server setting in the configuration file.
* Watcher
  * *Watcher* is a tool to synchronize the OpenStack 'instance' metadata between OpenStack and K2HR3. It finds deleted instances from OpenStack and deletes them from K2HR3 ROLE members.
  * Node.js configuration file includes settings for *Watcher*.

### HTTP Server settings

This section describes settings for HTTP Server.

* *devcluster* will install configuration files to */home/k2hr3/node_modules/k2hr3-api/config*
* 'default.json' contains all setting items with default values. Your own setting items should be saved in your own configuration file like 'local.json'. 
  * Your settings will overwrite the default ones.
  * See [npm config module 'File Load Order'](https://github.com/lorenwest/node-config/wiki/Configuration-Files#file-load-order) for details.
* TLDR, create a 'local.json' file as your own configuration file.
* Then, copy the default.json and your own configuration file to */home/k2hr3/etc/k2hr3-api* directory.


Here are the default configuration values and the descriptions.

```
{
    "keystone": {
        "type": "openstackapiv3",                              // Keystone version(openstackapiv3 or openstackapiv2)
        "eptype": "list",                                      // The place where keystone endpoint settings exist(list or file)
        "epfile": null,                                        // The file path that contains keystone endpoints
        "eplist": {
            "myregion": "https://dummy.keystone.openstack/"    // Keystone endpoint name and the URL
        }
    },
    "k2hdkc": {
        "config": "/etc/k2hdkc/slave.ini",                     // chmpx-slave configuration file path
        "port": 8031                                           // chmpx-slave port
    },
    "multiproc": true,                                         // True if multiple node processes are up
    "scheme": "https",                                         // HTTP Protocol(http or https)
    "runuser": "nobody",                                       // The username to be run the process as 
    "privatekey": "config/key.pem",                            // The file path to the RSA private key
    "cert": "config/cert.pem",                                 // The file path to the SSL Server Certificate
    "ca": "/etc/pki/tls/certs/ca-bundle.crt",                  // Bundled certificates of root certificate authorities
    "logdir": "log",                                           // Directory where the server will log
    "accesslogname": "access.log",                             // Location where the server will log
    "consolelogname": "error.log",                             // Location where the server will log errors
    "watcherlogname": "watcher.log",                           // Location where the server will log by Watcher
    "wconsolelogname": "watchererror.log",                     // Location where the server will log errors by Watcher
    "logrotateopt": {
        "compress": "gzip",                                    // Log compression algorithm(gzip)
        "interval": "6h",                                      // Log rotation duration
        "initialRotation": true                                // See https://github.com/iccicci/rotating-file-stream/blob/master/README.md#initialrotation
    },
    "userdata": {                                              // Settings for UserData API
        "baseuri": "https://localhost",                        // BaseURL of UserData API
        "cc_templ": "config/k2hr3-cloud-config.txt.templ",     // The template file path to cloud config
        "script_templ": "config/k2hr3-init.sh.templ",          // The template file path to cloud init shell script
        "errscript_templ": "config/k2hr3-init-error.sh.templ", // The template file path to cloud init shell script used in case of errors
        "algorithm": "aes-256-cbc",                            // Encryption algorithm 
        "passphrase": "k2hr3_regpass"                          // passphrase to decrypt encrypted userdata
    },
    "k2hr3admin": {
        "tenant": "admintenant",                               // Tenant(or Project) name of K2HR3 administrator
        "delhostrole": "delhostrole"                           // A role name of Admin Tenant that can delete hosts from K2HDKC
    },
    "confirmtenant": false,                                    // False if only existent Tenants(or Projects) can be added to Services
    "chkipconfig": {                                           // Settings for Watcher
        "type": "Listener"                                     // The way how Watcher works(see below for details)
        "pendingsec": 864000,                                  // The duration from the time when a host is dead to the time to be deleted from K2HR3
        "intervalms": 4320000,                                 // The interval duration from the last command execution time(in milliseconds)
        "parallelcnt": 32,                                     // The number of concurrency of Watcher execution
        "command4": "ping",                                    // Ping command file path(for IPv4 address)
        "command6": "ping6",                                   // Ping command file path(for IPv6 address)
        "params": "-c 1",                                      // Ping command parameter(ICMP request count)
        "timeoutparam": "-W",                                  // Ping command parameter(timeout duration)
        "timeoutms": 5000                                      // Ping command parameter(timeout duration)
    },
    "allowcredauth": true                                      // True if allowing access to API server by credential
}
```

### chmpx-slave settings

This section instructs how to configure the 'chmpx-slave' process.

*chmpx-slave* forwards requests from HTTP server processes to Data server.  /etc/k2hdkc/slave.ini is the default configuration file installation path. 

You need update the 'Data server setting' in the configuration file. The **NAME** setting in the **[SVRNODE]** section lists hosts of Data server. If dkc01~dkc04.example.com were the Data server hosts, you could write them in a regex-like form::
```
...
#
# SERVER NODES SECTION
#
[SVRNODE]
NAME                            = dkc[1-4].example.com
PORT                            = 8020
CTLPORT                         = 8021
SSL                             = no
...
```

See [CHMPX details](https://chmpx.antpick.ax/details.html) for [K2HDKC](https://k2hdkc.antpick.ax/) settings.

### Watcher settings

This section instructs how to configure the 'Watcher' process.

*Watcher* is a tool to synchronize the OpenStack 'instance' metadata between OpenStack and K2HR3. It finds deleted instances from OpenStack and deletes them from K2HR3 ROLE members.

![K2HR3 Watcher overview](images/tool_watcher.png)

K2HR3 OpenStack Notification Listener has the same role with Watcher in K2HR3 system. Use *Watcher* only when you can't use K2HR3 OpenStack Notification Listener for some reasons. You need not to run both.

The *type* of *chkipconfig* setting determines the Watcher behavior.

* Listener(default)
  * Watcher does nothing. Use this setting when K2HR3 OpenStack Notification Listener is running.

* Basic{And/Or}
  * Watcher lookups hostnames of all hosts in K2HDKC and sends ICMP echo requests to them.
  * The *And* setting will cause to delete IP address from K2HR3 when lookup is failed *and* no ICMP echo reply is received.
  * The *Or* setting will cause to delete IP address from K2HR3 when lookup is failed *or* no ICMP echo reply is received.

* NoCheck
  * Watcher does nothing.


### Tips: Controls processes by using systemd

This section instructs how to control processes by using [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Settings of [systemd](https://www.freedesktop.org/wiki/Software/systemd/) are not always necessary. If you would like to control each API server process as a systemd service, this tips will help you.

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) is a service manager for Linux that controls userspace processes. It brings up userspace processes in configured order during booting a Linux installation. After starting up processes, it tries to keep them up. On shutdown, systemd terminates all the other processes.

The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'chmpx-slave' service will be installed in /etc/systemd/system/chmpx-slave.service when you install Data server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'chmpx-slave' service. 

```
[Unit]
Description=chmpx-slave
After=network-online.target

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStartPre=/sbin/sysctl fs.mqueue.msg_max=1024
ExecStart=/usr/bin/chmpx -conf /etc/k2hdkc/slave.ini -d err
Restart=on-failure
PIDFile=/var/run/chmpx.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```
$ sudo systemctl daemon-reload
$ sudo systemctl restart chmpx-slave.service
```

Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'k2hr3-api' service. Note that the order to start up a service is important. The 'k2hr3-api' service must starts after the 'chmpx-slave' service. 
```
[Unit]
Description=k2hr3-api
Requires=chmpx-slave.service
After=chmpx-slave.service

[Service]
Type=simple
WorkingDirectory=/home/k2hr3
Environment=HOME=/home/k2hr3
Environment=NODE_CONFIG_DIR=/home/k2hr3/etc/k2hr3-api
Environment=NODE_DEBUG=LOGLEVEL_ERR
Environment=NODE_ENV=development
ExecStart=/usr/bin/node /home/k2hr3/node_modules/k2hr3-api/bin/www
Restart=on-failure
PIDFile=/var/run/k2hr3-api.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```bash
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-api.service
```


## Web server


This chapter describes Web server settings.

### HTTP Server settings

This section describes settings for HTTP Server.

* Web server is implemented by [Node.js](https://nodejs.org/).
* *devcluster* will install configuration files to */home/k2hr3/node_modules/k2hr3-app/config*
* 'default.json' contains all setting items with default values. Your own setting items should be saved in your own configuration file like 'local.json'. 
  * Your settings will overwrite the default ones.
  * See [npm config module 'File Load Order'](https://github.com/lorenwest/node-config/wiki/Configuration-Files#file-load-order) for details.
* TLDR, create a 'local.json' file as your own configuration file.
* Then, copy the default.json and your own configuration file to */home/k2hr3/etc/k2hr3-app* directory.


Here are the default configuration values and the descriptions.

```
{
    "scheme": "http",                               // HTTP Protocol(http or https)
    "port": 3000,                                   // HTTP server port to be listened by Node.js
    "multiproc": true,                              // True if multiple node processes are up
    "runuser": "nobody",                            // The username to be run the process as
    "privatekey": "config/key.pem",                 // The file path to the RSA private Key
    "cert": "config/cert.pem",                      // The file path to the SSL Server Certificate
    "ca": "/etc/pki/tls/certs/ca-bundle.crt",       // Bundled certificates of root certificate authorities
    "validator": "userValidateCredential",          // JavaScript module name for validating user token
    "lang": "en",                                   // locale

    "logdir": "log",                                // Log directory
    "accesslogname": "access.log",                  // Standard out log file path
    "consolelogname": "error.log",                  // Standard error log file path
    "logrotateopt": {
        "compress": "gzip",                         // Log compression algorithm(gzip)
        "interval": "6h",                           // Log rotation duration
        "initialRotation": true                     // See https://github.com/iccicci/rotating-file-stream/blob/master/README.md#initialrotation
    },


    "apischeme": "http",                            // API Server protocol(http/https)
    "apihost": "localhost",                         // API server hostname
    "apiport": 3001,                                // API server port

    "appmenu": [                                    // Web application menu
        {
            "name": "Document",                     // menu name
            "url": "https://k2hr3app.antpick.ax/"   // menu url
        }
    ],

    "userdata": "\
#include\n\
{{= %K2HR3_API_HOST_URI% }}/v1/userdata/{{= %K2HR3_USERDATA_INCLUDE_PATH% }}\n\
"                                                   // UserData URL
}
```

### Tips: Controls processes by using systemd

This section instructs how to control processes by using [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Settings of [systemd](https://www.freedesktop.org/wiki/Software/systemd/) are not always necessary. If you would like to control each Web server process as a systemd service, this tips will help you.

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) is a service manager for Linux that controls userspace processes. It brings up userspace processes in configured order during booting a Linux installation. After starting up processes, it tries to keep them up. On shutdown, systemd terminates all the other processes.

The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'k2hr3-app' service, which serves HTTP service in Web server, will be installed in /etc/systemd/system/k2hr3-app.service when you install Web server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'k2hr3-app' service. The 'k2hr3-app' service must run after the [Network](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) is up.

```
[Unit]
Description=k2hr3-app
After=network-online.target

[Service]
Type=simple
WorkingDirectory=/home/k2hr3
Environment=HOME=/home/k2hr3
Environment=NODE_CONFIG_DIR=/home/k2hr3/etc/k2hr3-app
Environment=NODE_DEBUG=LOGLEVEL_ERR
Environment=NODE_ENV=production
ExecStart=/usr/bin/node /home/k2hr3/node_modules/k2hr3-app/bin/www
Restart=on-failure
PIDFile=/var/run/k2hr3-app.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-app.service
```


## K2HR3 OpenStack Notification Listener

This chapter describes K2HR3 OpenStack Notification Listener settings.

K2HR3 OpenStack Notification Listener is a daemon process to synchronize the [OpenStack](https://www.openstack.org) instance metadata between OpenStack and K2HR3. K2HR3 OpenStack Notification Listener listens to notification messages from OpenStack services. To catch a new notification, it listens to a queue in a messaging backend where messages sent by OpenStack services are delivered.

*/usr/local/etc/k2hr3/k2hr3-osnl.conf* is the default location when you install *k2hr3-osnl*, which is the *PyPI* package of K2HR3 OpenStack Notification Listener. 

Here are the default configuration values and the descriptions.

```
[DEFAULT]
log_file = sys.stderr                                 # Location where the server will log
debug_level = error                                   # Controls the verbosity of the log(debug, info, warning, error, critical)
libs_debug_level = warning                            # Controls the verbosity of dependent libraries log

[oslo_messaging_notifications]
event_type = ^port\.delete\.end$                      # event_type of notification messages to be matched with
publisher_id = ^network.*$                            # publisher of notification messages to be matched with
transport_url = rabbit://guest:guest@127.0.0.1:5672/  # The transport configuration parameters in the form of a URL
topic = notifications                                 # Location where notification messages to be delivered
exchange = neutron                                    # Scope of notification messages
executor = threading                                  # How incoming notification messages will be received and dispatched(threading, blocking, eventlet)
pool = k2hr3_osnl                                     # Location where notification messages come in, which is specified by listener
allow_requeue = True                                  # Determines whether consumers can requeue the processing message

[k2hr3]
api_url = https://localhost/v1/role                   # URL of the API server
timeout_seconds = 30                                  # Amount of time the listener will wait for responses from API server(seconds)
retries = 3                                           # Amount of retry requests for API server
retry_interval_seconds = 60                           # Amount of time to wait until next request for API Server(seconds)
allow_self_signed_cert = False                        # Determines whether API server's self-signed SSL certificates is accepted.
requeue_on_error = False                              # Determines whether consumers can requeue the processing message on error
```


### Reference: Notification message format and settings


This section describes notification message formats generated by [OpenStack](https://www.openstack.org/).

A notification message format depends on oslo.messaging's driver setting in OpenStack services. To receive and parse them correctly, the setting of K2HR3 OpenStack Notification Listener should be determined by OpenStack services settings.

Note that notification messages formats might depends on OpenStack version. We have tested K2HR3 OpenStack Notification Listener with [OpenStack Rocky](https://docs.openstack.org/rocky/).

The following setting is a part of /etc/neutron/neutron.conf, [OpenStack neutron](https://docs.openstack.org/neutron/latest/)'s configuration file. This shows [OpenStack neutron](https://docs.openstack.org/neutron/latest/) uses oslo.messaging's driver setting as *messagingv2*::

```
...
[oslo_messaging_notifications]
#
# From oslo.messaging
#
# The Drivers(s) to handle sending notifications. Possible values are
# messaging, messagingv2, routing, log, test, noop (multi valued)
# Deprecated group/name - [DEFAULT]/notification_driver
driver = messagingv2
...
```

In this case, notification messages from [OpenStack neutron](https://docs.openstack.org/neutron/latest/) will be::
```
{
    "event_type": "port.delete.end",
    "message_id": "76c35877-9d0c-4faf-b4e5-7c51828f37a0",
    "payload": {
        ...
        "device_id": "12345678-1234-5678-1234-567812345678",
        "device_owner": "compute:nova",
        "extra_dhcp_opts": [],
        "fixed_ips": [
            {
                "ip_address": "172.24.4.18",
                "subnet_id": "subnet01-ffff-ffff-ffff-ffffffffffff"
            },
            {
                "ip_address": "2001:db8::6",
                "subnet_id": "subnet02-ffff-ffff-ffff-ffffffffffff"
            }
        ],
        ...
    },
    "priority": "INFO",
    "publisher_id": "network.hostname.domain_name",
    "timestamp": "2018-11-25 09:00:06.842727"
}
```

Therefore, settings of K2HR3 OpenStack Notification Listener should be::

```
...
[oslo_messaging_notifications]
event_type = ^port\.delete\.end$
publisher_id = ^network.*$
transport_url = rabbit://user:pass@127.0.0.1:5672/
topic = notifications
exchange = neutron
...
```

However, the default setting of [OpenStack neutron](https://docs.openstack.org/neutron/latest/)'s oslo.messaging's driver is *messaging*. This means notification messages like the above will not be emitted. 

In this case, you can use notification messages from [OpenStack nova](https://docs.openstack.org/nova/latest/). When instances are deleted, [OpenStack nova](https://docs.openstack.org/nova/latest/) will sends notification messages, which K2HR3 OpenStack Notification Listener can receive and parse.

To receive and parse notification messages from [OpenStack nova](https://docs.openstack.org/nova/latest/), you should configure K2HR3 OpenStack Notification Listener as followings::

```
...
[oslo_messaging_notifications]
event_type = ^instance\.delete\.end$
publisher_id = ^nova-compute:.*$
transport_url = rabbit://user:pass@127.0.0.1:5672/
topic = versioned_notifications
exchange = nova
...
```

See [Notifications in Nova](https://docs.openstack.org/nova/latest/reference/notifications.html#existing-versioned-notifications) for notifications emit by [OpenStack nova](https://docs.openstack.org/nova/latest/).


### Tips: Control processes by using systemd

This section instructs how to control processes by using [systemd](https://www.freedesktop.org/wiki/Software/systemd/). Settings of [systemd](https://www.freedesktop.org/wiki/Software/systemd/) are not always necessary. If you would like to control K2HR3 OpenStack Notification Listener process as a systemd service, this tips will help you.

[systemd](https://www.freedesktop.org/wiki/Software/systemd/) is a service manager for Linux that controls userspace processes. It brings up userspace processes in configured order during booting a Linux installation. After starting up processes, it tries to keep them up. On shutdown, systemd terminates all the other processes.

The [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) for the 'k2hr3-osnl' service, which serves K2HR3 OpenStack Notification Listener service, will be installed in /etc/systemd/system/k2hr3-osnl.service when you install K2HR3 OpenStack Notification Listener server by using *devcluster*. Here is an example of [systemd.unit](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) of the 'k2hr3-osnl' service.
```
[Unit]
Description=K2HR3 OpenStack Notification Listener
After=network-online.target

[Service]
Type=simple
User=k2hr3
PermissionsStartOnly=true
ExecStart=/opt/rh/rh-python36/root/usr/bin/k2hr3-osnl -c /usr/local/etc/k2hr3/k2hr3-osnl.conf
Restart=on-failure
PIDFile=/var/run/k2hr3-osnl.pid

[Install]
WantedBy=multi-user.target
```

To apply these settings to [systemd](https://www.freedesktop.org/wiki/Software/systemd/), run the following commands after saving the sample file as above.

```
$ sudo systemctl daemon-reload
$ sudo systemctl restart k2hr3-osnl.service
```
