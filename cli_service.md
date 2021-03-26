---
layout: contents
language: en-us
title: CLI service
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_serviceja.html
lang_opp_word: To Japanese
prev_url: cli_resource.html
prev_string: CLI resource
top_url: cli.html
top_string: Command Line Interface
next_url: cli_acr.html
next_string: CLI acr
---

# Service Subcommand
Describes the **service** subcommand of the K2HR3 Command Line Interface(CLI).

The **service** subcommand is a function that provides [SERVICE API](api_service.html) as a Command Line Interface(CLI).
For more information on the API, see [SERVICE API](api_service.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Show
Displays SERVICE information.

### Format(1)
```
k2hr3 service show [service name | yrn path]
```
Displays information about the specified SERVICE.

## Create
Generate a SERVICE.

### Format(1)
```
k2hr3 service create [service name | yrn path] [--verify verify url]
```
Generate a SERVICE with accompanying information.

## Delete
Delete the SERVICE.

### Format(1)
```
k2hr3 service delete [service name | yrn path]
```
Deletes the specified SERVICE.

## Update Verify URL
Update the Verify URL for the SERVICE.

### Format(1)
```
k2hr3 service verify [service name | yrn path] [verify url]
```
Updates the Verify URL for the specified SERVICE.

## Tenant Member
Operate the tenant member(MEMBER) of the SERVICE.

### Format(1)
```
k2hr3 service tenant add [service name | yrn path] [member tenant] [--clear_tenant]
```
Adds a tenant member(MEMBER) for the specified SERVICE.
If `--clear_tenant` is specified, the existing tenant member(MEMBER) will be deleted.

### Format(2)
```
k2hr3 service tenant delete [service name | yrn path] [member tenant]
```
Deletes the tenant member(MEMBER) of the specified SERVICE.

### Format(3)
```
k2hr3 service tenant check [service name | yrn path] [member tenant]
```
Check if you are a tenant member(MEMBER) of the specified SERVICE.

## Tenant Member's Service
Operate the SERVICE on the tenant member(MEMBER) side of the SERVICE.

### Format(1)
```
k2hr3 service member clear [service name | yrn path] [member tenant]
```
Deletes the SERVICE on the tenant member(MEMBER) side of the specified SERVICE.
When executing this command, specify the Scoped token of K2HR3 on the tenant member(MEMBER) side.

## Options
You can specify the following options:
- -\-help(-h)
- -\-verify [string or verify url]
- -\-clear_tenant
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
