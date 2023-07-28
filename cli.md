---
layout: contents
language: en-us
title: Command Line Interface
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: clija.html
lang_opp_word: To Japanese
prev_url: usage_template.html
prev_string: Template Engine
top_url: usage.html
top_string: Usage
next_url: helm_chart.html
next_string: Helm Chart
---

# Command Line Interface (CLI)
The K2HR3 Command Line Interface(CLI) provides an interface that allows you to operate the [REST API](api.html) provided by K2HR3 from the command line.  
It provides the same function as [K2HR3 Web Application](usage_app.html) for manipulating the data of the K2HR3 system as a **Command Line Interface**.  

## Overview
To use the K2HR3 command line interface(CLI), you can install it as a package or extract the source code.  
The K2HR3 Command Line Interface(CLI) uses the [K2HR3 REST API](api.html), so it can run on hosts that can connect to the **REST API server**.  

### How to use
The K2HR3 Command Line Interface(CLI) is provided as a single command(`k2hr3`).  
You can check the help by specifying the `--help(-h)` option to see the usage details.  
```
$ k2hr3 --help
$ k2hr3 <sub command> --help
```

### Install package
Describes how to install the K2HR3 command line interface(CLI) as a package.  

The K2HR3 Command Line Interface(CLI) distributes packages at [packagecloid.io](https://packagecloud.io/app/antpickax/stable/search?q=k2hr3-cli).  
The K2HR3 Command Line Interface(CLI) is available in environments where **Bourne Shell**(`/bin/sh`) and `curl` can work.  
You can install it by following the steps below.  

#### Set package repository
Please set the repository of [packagecloid.io](https://packagecloud.io/antpickax/stable) before installation.  
Register the repository by referring to [here](https://packagecloud.io/antpickax/stable/install).  
```
# curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.deb.sh | sudo bash
 or
# curl -s https://packagecloud.io/install/repositories/antpickax/stable/script.rpm.sh | sudo bash
```

### Extract the source code
If you want to use the OS for which the package is not provided, or if you want to use it without installing the package, you can download the source code directly from the [github.com repository](https://github.com/yahoojapan/k2hr3_cli) and use it.  
For more information on how to use github.com and git commands, please refer to the documentation.  

To expand and use the source code, you need to set the following environment variables.  
```
$ export K2HR3CLI_LIBEXEC_DIR <k2hr3_cli repository top dir>/src/libexec
```
The K2HR3 Command Line Interface(CLI) program(`k2hr3`) is located in `<k2hr3_cli repository top dir>/src/k2hr3`, so execute this file.  

## Details
Describes how to use the K2HR3 Command Line Interface(CLI).

### Common
The K2HR3 Command Line Interface(CLI) command format is shown below.  
```
$ k2hr3 --help(-h)
 or
$ k2hr3 <sub command> <options...>
```
Subcommand(**<sub command>**) corresponds to each [K2HR3 REST API](api.html).(See below)  

#### Display help
How to use the K2HR3 Command Line Interface(CLI) can be found in the help as follows.  
```
$ k2hr3 --help(-h)
```
As mentioned above, displaying help without Subcommand(**<sub command>**) will display an overview of the K2HR3 Command Line Interface(CLI).  

To get help for each Subcommand, do the following:  
```
$ k2hr3 <sub command> --help(-h)
```
The usage of each Subcommand(**<sub command>**) is displayed.  

#### Options
The K2HR3 Command Line Interface (CLI) has options.  
See [here](cli_options.html) for a description of each option.  
The options that can be specified differ depending on Subcommand, so refer to the explanation of each Subcommand.  

### Subcommands
This section describes the K2HR3 Command Line Interface(CLI) subcommands.

#### [version](cli_version.html)
Displays the version of the K2HR3 Command Line Interface(CLI).

#### [config](cli_config.html)
K2HR3 Command Line Interface(CLI) configuration related subcommands.  
The K2HR3 command line interface(CLI) allows you to keep the values specified by some options in the configuration file.  
This allows you to use the values saved in your configuration without specifying these options when running commands in succession.  

#### [token](cli_token.html)
This is a subcommand for manipulating the tokens required to use the [K2HR3 REST API](api.html).
This is the subcommand corresponding to [TOKEN API](api_token.html).

#### [list](cli_list.html)
This is a subcommand corresponding to [LIST API](api_list.html).  
A subcommand that displays the path list for K2HR3 ROLE, POLICY RULE, and RESOURCE.  

#### [role](cli_role.html)
This is a subcommand corresponding to [ROLE API](api_role.html).  
This is a subcommand that operates the ROLE of K2HR3.  

#### [policy](cli_policy.html)
This is a subcommand corresponding to [POLICY API](api_policy.html).  
This is a subcommand that operates the POLICY RULE of K2HR3.  

#### [resource](cli_resource.html)
This is a subcommand corresponding to [RESOURCE API](api_resource.html).  
This is a subcommand that operates the RESOURCE of K2HR3.  

#### [service](cli_service.html)
This is a subcommand corresponding to [SERVICE API](api_service.html).  
This is a subcommand that operates the SERVICE of K2HR3.  

#### [tenant](cli_tenant.html)
This is a subcommand corresponding to [TENANT API](api_service.html).  
This is a subcommand that operates the LOCAL TENANT of K2HR3.  

#### [acr](cli_acr.html)
This is a subcommand corresponding to [ACR (ACCESS CROSS ROLE) API](api_acr.html).  
This is a subcommand to operate ACR(ACCESS CROSS ROLE) used by the +SERVICE function of K2HR3.  

#### [userdata](cli_userdata.html)
This is a subcommand corresponding to [USERDATA API](api_userdata.html).  
This is a subcommand that operates the USER DATA SCRIPT of K2HR3.  

#### [extdata](cli_extdata.html)
This is a subcommand corresponding to [EXTDATA API](api_extdata.html).  
This is a subcommand that operates the EXT(RA) DATA SCRIPT of K2HR3.  
