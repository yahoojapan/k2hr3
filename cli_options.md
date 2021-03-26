---
layout: contents
language: en-us
title: CLI options
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_optionsja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: cli.html
top_string: Command Line Interface
next_url: cli_config.html
next_string: CLI config
---

# Options for Command Line Interface(CLI)
Describes K2HR3 command line interface (CLI) options.  
Use these options according to Subcommand.  
See the description of each Subcommand and which options are available.  

## Common Options
The following options are common to Subcommand.   

### -\-help(-h)
Display help for K2HR3 Command Line Interface(CLI).  
If Subcommand is not specified, the option description and the description of each Subcommand are displayed.  
When accompanied by Subcommand, the description of the specified Subcommand is displayed.  

### -\-version(-v)
Displays the version of the K2HR3 Command Line Interface(CLI).  

### -\-config(-c) [file path]
This option specifies the configuration file to load when the K2HR3 command line interface(CLI) starts.  
You can check and change the keywords described in the configuration file with [CLI config](cli_config.html).  
If this option is not specified, the configuration files will be detected and loaded in the following order:  
- ${HOME}/.antpickax/k2hr3.config
- /etc/antpickax/k2hr3.config

### -\-interactive(-i)
If this option is specified, you will be prompted interactively if there are any unspecified options or parameters.  
And this option cannot be specified with `--nointeractive(-ni)`.

### -\-nointeractive(-ni)
If it finds an unspecified required option, it will make an error.  
This is the default behavior.  
And this option cannot be specified with `--interactive(-i)`.  

### -\-messagelevel(-m) [level]
This option specifies the output level of the message.  
The following values can be specified for the optional parameters.  
- silent, slt, 0  
output nothing.
- error, err, 1  
output only error level message.
- warning, warn, wan, 2  
output only error and warning level message.
- information, info, inf, 3  
output only error, warning and information level message.
- debug, dbg, 4  
output only error, warning, information and debug level message.

### -\-curldebug(-cd)
Specifies the verbose option when executing the curl command.  
If this option is specified, detailed information will be printed to standard error.  

### -\-curlbody(-cb)
Shows the response body after executing the curl command.  
If you specify this option, we recommend that you also specify `-\-curldebug(-cd)`.

### -\-nodate(-nd)
The date and time are not displayed in the output message.  
By default, the date and time are displayed.  

### -\-nocolor(-nc)
Does not color the output message.  
By default, it is colored.

### -\-json(-j)
The json output of the command result is formatted and displayed in an easy-to-understand manner.  

### -\-apiuri(-a) [k2hr3 rest api uri]
Specifies the URI to the K2HR3 REST API.(ex. https://127.0.0.1:3000)  

## Authentication options
Most Subcommand communicate with the K2HR3 REST API server, which requires a token.  
These options are related to this authentication.  
If you need a token and the token is not stored in the configuration file, you need to specify these options.  

### -\-user(-u) [user name]
Specifies the K2HR3 user name for credential authentication.  

### -\-passphrase(-p) [passphrase]
Specify the K2HR3 passphrase for credential authentication.  
If you use this option, the passphrase may remain in the command history.  
We recommend that you specify `--interactive(-i)` and enter the passphrase interactively without using this option.  

### -\-tenant(-t) [tenant name]
Specify the tenant(project) to get the Scoped Token.  

### -\-unscopedtoken(-utoken) [token]
Specify the Unscoped Token, for example, to get the Scoped Token.  

### -\-scopedtoken(-token) [token]
Specify the Scoped Token required to call various APIs.  

### -\-openstacktoken(-optoken) [token]
Specify the Token(Unscoped or Scoped) issued by the OpenStack system to obtain the Unscoped and Scoped Token.  

### -\-saveconfig(-s)
This option can be specified in the command that performs the process of generating a token for K2HR3.  
If this option is specified, the elements(user name, tenant name, K2HR3 REST API URI, Unscoped token, OpenStack token, etc.) used to generate the (Scoped or Unscoped) token will be saved in the configuration file.  
You can check the saved elements using the [CLI config](cli_config.html) command.  

### -\-savepassphrase(-sp)
process of generating a token for K2HR3.  
If a passphrase is specified to generate the K2HR3 token(Scoped or Unscoped), the passphrase is saved in the configuration file.  
However, you should avoid storing passphrases in configuration files whenever possible.  

## Other Options
The following options are options that can be specified by Subcommand.  
Check the description of each Subcommand to see if it can be specified.  

### -\-expand
This option grants the `expand=true` parameter to the target API.  
As a result, you will receive the expanded response data.  
For the contents of the response data, check the explanation of each Subcommand.  

### -\-policies [policies]
Specifies the POLICY YRN paths.  
If you specify multiple POLICY, pass the parameters as an array in JSON format.  

### -\-alias [alias]
Specifies the ALIAS YRN path.  

### -\-host [hostname or IP address]
Specifies the hostname(or IP address).  

### -\-port [port number]
Specifies the port number.  

### -\-cuk [cuk]
Specifies the CUK string.  

### -\-extra [data]
Specifies the Extra data.  

### -\-tag [tag]
Specifies the tag.  

### -\-expire [value]
Specifies the expire seconds.

### -\-type [type]
Specifies the resource type(`string`, `object`, `null` or `undefined`) of the RESOURCE.  

### -\-data [value]
Specify the data of the RESOURCE.  
If the resource type is `string`, specify a string literal.  
If the resource type is `object`, the data specifies a JSON object.  

### -\-datafile [file path]
Data can be specified in a file if the resource type is `string`.  
If the data contains unescaped characters such as line breaks, you can specify it in the file.  

### -\-keys [data]
Specifies the key and value that is an element of the `keys` of the RESOURCE.  
You can specify multiple key and value as a JSON object.  

### -\-service [service name]
Specifies the SERVICE name.  

### -\-keynames [keynames]
Specifies the key name in the RESOURCE.  

### -\-aliases [aliases]
Specifies the ALIAS YRN path.  
If you specify multiple ALIAS, pass the parameters as an array in JSON format.  

### -\-effect [allow or deny]
Specifies the POLICY's EFFECT as `allow` or` deny`.  

### -\-action [type]
Specifies the POLICY's ACTION.  
Specify either or both of `yrn:yahoo::::action:read` and `yrn:yahoo::::action:write`.  
If you specify more than one, pass it as a JSON array.  

### -\-clear_tenant
Specify this to delete an existing tenant from the MEMBER of the SERVICE.  

### -\-verify [url or string]
In the `service` subcommand, specify a URL to define a dynamic resource or string literal or Boolean literal.  

### -\-cip [IP address]
An IP address, which is owned by a service member and the other end IP address of the service owner(a peer IP).  

### -\-cport [port number]
An port number, which is used to determine the K2HR3 ROLE name of the IP address.  

### -\-crole [role name]
Specify a K2HR3 ROLE name.  
If a service member host is a member of multiple K2HR3 ROLE, the service member should pass the K2HR3 ROLE name it want to be authorized.  

### -\-ccuk [cuk]
This parameter is reserved for future use.  
Setting this currently has no effect.  

### -\-sport [port number]
A port number of the SERVICE OWNER host.  
The IP address of the SERVICE OWNER host is not required.  

### -\-srole [role name]
A role name assigned to SERVICE OWNER host.  

### -\-scuk [cuk]
This parameter is reserved for future use.  

### -\-output [file path]
Specify the file path to output the command result.  
Specify this option for the K2HR3 REST API, which returns a file.  
