---
layout: contents
language: en-us
title: CLI list
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_listja.html
lang_opp_word: To Japanese
prev_url: cli_token.html
prev_string: CLI token
top_url: cli.html
top_string: Command Line Interface
next_url: cli_role.html
next_string: CLI role
---

# List Subcommand
Describes the **list** subcommand of the K2HR3 Command Line Interface(CLI).

The **list** subcommand is a feature that provides the [LIST API](api_list.html) as a Command Line Interface(CLI).
For more information on the API, see [LIST API](api_list.html).

## List
Displays a list of SERVICEs, ROLEs, POLICIes or RESOURCEs.
This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

### Format(1)
```
k2hr3 list service [service name]
```
The information below the specified service name is displayed.

### Format(2)
```
k2hr3 list role [yrn path] [service name]
```
Displays the following information for the specified ROLE.
If a service name is specified, the information of the specified ROLE under the SERVICE is displayed.

### Format(3)
```
k2hr3 list policy [yrn path] [service name]
```
Displays the following information for specified POLICY-RULE.
If a service name is specified, the information of the specified POLICY-RULE under the SERVICE is displayed.

### Format(4)
```
k2hr3 list ressource [yrn path] [service name]
```
Displays the following information for specified RESOURCE.
If a service name is specified, the information of the specified RESORUCE under the SERVICE is displayed.

## Options
You can specify the following options:
- -\-help(-h)
- -\-expand
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
