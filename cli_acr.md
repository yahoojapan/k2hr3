---
layout: contents
language: en-us
title: CLI acr
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_acrja.html
lang_opp_word: To Japanese
prev_url: cli_service.html
prev_string: CLI service
top_url: cli.html
top_string: Command Line Interface
next_url: cli_userdata.html
next_string: CLI userdata
---

# ACR(ACCESS CROSS ROLE) Subcommand
Describes the **acr(ACCESS CROSS ROLE)** subcommand of the K2HR3 Command Line Interface(CLI).

**acr(ACCESS CROSS ROLE)** Subcommand is a function that provides [ACR API](api_acr.html) as Command Line Interface(CLI).
For more information on the API, see [ACR API](api_acr.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Show
Displays the Scoped token information of the tenant member(MEMBER) of the SERVICE.
It also displays the RESOURCE associated with the tenant member(MEMBER) of the SERVICE.

### Format(1)
```
k2hr3 acr show tenant [service name | yrn path]
```
Displays the Scoped token information of the tenant member(MEMBER) of the specified SERVICE.
In this command, specify the Scoped token of the tenant member(MEMBER).

### Format(2)
```
k2hr3 acr show resource [service name | yrn path] [--cip client IP address] [--cport client port] [--crole client role] [--ccuk client CUK] [- -sport service port] [--srole service role] [--scuk service CUK]
```
Displays the RESOURCE associated with the tenant member(MEMBER) of the specified SERVICE.
In this command, specify the Scoped token of the tenant member(MEMBER).

## Add
Create ROLE, POLICY-RULE, and RESOURCE in the tenant member(MEMBER) of the SERVICE.

### Format(1)
```
k2hr3 acr add [service name | yrn path]
```
Create ROLE, POLICY-RULE, and RESOURCE as tenant member(MEMBER) of the specified SERVICE.
In this command, specify the Scoped token of the tenant member(MEMBER).

## Delete
Delete the ROLE, POLICY-RULE, and RESOURCE as a tenant member(MEMBER) of the SERVICE.

### Format(1)
```
k2hr3 acr delete [service name | yrn path]
```
Deletes the ROLE, POLICY-RULE, and RESOURCE as a tenant member(MEMBER) of the specified SERVICE.
In this command, specify the Scoped token of the tenant member(MEMBER).

## Options
You can specify the following options:
- -\-help(-h)
- -\-cip [IP address]
- -\-cport [port number]
- -\-crole [role name or yrn path]
- -\-ccuk [cuk]
- -\-sport [port number]
- -\-srole [role name or yrn path]
- -\-scuk [cuk]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
