---
layout: contents
language: en
title: Tools
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: toolsja.html
lang_opp_word: To Japanese
prev_url: environments.html
prev_string: Environments/Settings
top_url: index.html
top_string: TOP
next_url: 
next_string: 
---

# Tools and Utilities

This page provides information about tools and utilities for K2HR3.

## Tools and utilities provided by K2HR3

This chapter instructs tools and utilities provided by the K2HR3 system.

### Watcher

This section instructs how to use *Watcher*.

*Watcher* is a tool to synchronize the OpenStack 'instance' metadata between OpenStack and K2HR3. It finds deleted instances from OpenStack and deletes them from K2HR3 ROLE members.

![K2HR3 Watcher overview](images/tool_watcher.png)

K2HR3 OpenStack Notification Listener has the same role in K2HR3 system. Use *Watcher* only when you can't use  K2HR3 OpenStack Notification Listener for some reasons. You need not to run both.


Here is the *Watcher* usage::

```
$ git clone https://github.com/yahoojapan/k2hr3_api.git && cd k2hr3_api
$ ./bin/run.sh -h
Usage:   run.sh [--production(default) | --development]
            [--stop]
            [--background(-bg) | --foreground(-fg)]
            [--debug(-d) | --debug-nobrk(-dnobrk)]
            [--debuglevel DBG/MSG/WARN/ERR/(custom debug level)]
            [--watcher [--oneshot]]

Option:  --production           : Set 'production' to NODE_ENV environment
                                  (This option is default and exclusive with
                                  the '--development' option)
         --development          : Set 'development' to NODE_ENV environment
                                  (exclusive with the '--production' option)
         --stop                 : Stop www or watcher nodejs process
         --debug(-d)            : Run with nodejs inspector option
         --debug-nobrk(-dnobrk) : Run with nodejs inspector option
                                  (no break at start)
         --debuglevel           : Specify the level of debug output.
                                  (DBG/MSG/WARN/ERR/custom debug level)
         --watcher              : Run IP watcher process as daemon
         --oneshot              : Run watcher process only once
```

* --watcher
  * Runs as a daemon.
  
* -os or --oneshot
  * Runs once and exits.

The API server npm package(k2hr3-api) will contain the *Watcher* program. The default path is */home/k2hr3/node_modules/k2hr3-api/bin/run.sh*

### devcluster

This section instructs how to use *devcluster*.

*devcluster* is a tool to install all K2HR3 subsystems in a Linux host for development and test purpose.

```bash
$ git clone https://github.com/yahoojapan/k2hr3_utils.git && cd k2hr3_utils/devcluster
$ sh cluster.sh -h
usage : cluster.sh [-d] [-f file] [-o file] [-p file] [-h] [-t url] [-v]
    -d        print debug messages
    -i file   k2hr3-api package file path(or URL)
    -o file   k2hr3-osnl package file path(or URL)
    -p file   k2hr3-app package file path(or URL)
    -h        display this message and exit
    -s url    OpenStack Identity Service Endpoint(Default: 'http://127.0.0.1/identity')
    -t url    TransportURL(Default: 'rabbit://guest:guest@127.0.0.1:5672/')
    -v        display version and exit
```

* -d
  * Runs in debug mode
  
* -i
  * k2hr3-api npm package file path(or URL)
  * For development use only
  
* -o
  * k2hr3-osnl PyPI package file path(or URL)
  * For development use only
  
* -p
  * k2hr3-app npm package file path(or URL)
  * For development use only
  
* -h
  * Shows this text
  
* -s
  * OpenStack Identity service API endpoint URL
  
* -t
  * The messaging backend transport configuration parameters in the form of a URL
  * See the [oslo.messaging's Transport](https://docs.openstack.org/oslo.messaging/latest/reference/transport.html#oslo_messaging.TransportURL) for details. 
  
* -v
  * Shows the script version
  

## Other tools

This chapter introduces useful tools in k2hr3 subsystem packages.

### k2hdkclinetool

[K2HDKC](https://k2hdkc.antpick.ax/) is a NoSQL database used in k2hr3. k2hdkclinetool is a tool to provides all kinds of operations to data on a [K2HDKC](https://k2hdkc.antpick.ax/) cluster.

See [k2hdkc tools](https://k2hdkc.antpick.ax/k2hdkclinetool.html) tools for details.

### chmpxlinetool

[CHMPX](https://chmpx.antpick.ax/) is a software for clustering multiple hosts over networking. chmpxlinetool is a tool to control chmpx processes interactively.

See [chmpx tools](https://chmpx.antpick.ax/tools.html) for details.

### chmpxstatus

[CHMPX](https://chmpx.antpick.ax/) is a software for clustering multiple hosts over networking. chmpxstatus is a tool to display the status of hosts in a cluster.

See [chmpx tools](https://chmpx.antpick.ax/tools.html) for details.

### k2hlinetool

[K2HASH](https://k2hash.antpick.ax/) is a library for KVS. k2hlinetool is a tool to provides all kinds of operations to data in a [K2HASH](https://k2hash.antpick.ax/) database file.

See [k2hash tools](https://k2hash.antpick.ax/tools.html) for details.


