---
layout: contents
language: en-us
title: CLI role
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_roleja.html
lang_opp_word: To Japanese
prev_url: cli_list.html
prev_string: CLI list
top_url: cli.html
top_string: Command Line Interface
next_url: cli_policy.html
next_string: CLI policy
---

# Role Subcommand
Describes the **role** subcommand of the K2HR3 Command Line Interface(CLI).

The **role** subcommand is a feature that provides the [ROLE API](api_role.html) as a Command Line Interface(CLI).
For more information on the API, see [ROLE API](api_role.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Show
Displays information about the ROLE.

### Format(1)
```
k2hr3 role show [role name | yrn path]
```
Displays information for the specified ROLE.

## Create
Create a ROLE.

### Format(1)
```
k2hr3 role create [role name | yrn path] [--policies policy path] [--alias role path]
```
Generates the specified ROLE.

## Delete
Delete the ROLE.

### Format(1)
```
k2hr3 role delete [role name | yrn path]
```
Deletes the specified ROLE.

## Host
Operate(add/delete) the HOST member of the ROLE.

### Format(1)
```
k2hr3 role host add [role name | yrn path] [--host hostname or ip address] [--port port number] [--cuk custom unique key] [--extra extra information] [--tag tag name]
```
Registers the specified HOST as a member with the accompanying information in the specified ROLE.

### Format(2)
```
k2hr3 role host delete [role name | yrn path] [--host hostname or ip address] [--port port number] [--cuk custom unique key]
```
Removes the specified HOST from the members of the specified ROLE.

## Role Token
Operates a role token.

### Format(1)
```
k2hr3 role token show [role name | yrn path]
```
Displays a list of role tokens for the specified ROLE.

### Format(2)
```
k2hr3 role token create [role name | yrn path] [--expire seconds]
```
Generates a role token for the specified ROLE.

### Format(3)
```
k2hr3 role token delete [role token]
```
Deletes(clears) the specified role token.

### Format(4)
```
k2hr3 role token check [role name | yrn path] [role token]
```
Checks if the specified role token is valid.

## Options
You can specify the following options:
- -\-help(-h)
- -\-policies [policies]
- -\-alias [aliases]
- -\-host [hostanme or IP address]
- -\-port [port number]
- -\-cuk [cuk string]
- -\-extra [extra data]
- -\-tag [tag]
- -\-expire [seconds]
- -\-expand
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
