---
layout: contents
language: en-us
title: CLI tenant
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_tenantja.html
lang_opp_word: To Japanese
prev_url: cli_service.html
prev_string: CLI service
top_url: cli.html
top_string: Command Line Interface
next_url: cli_acr.html
next_string: CLI acr
---

# Tenant Subcommand
Describes the **tenant** subcommand of the K2HR3 Command Line Interface(CLI).

The **tenant** subcommand is a feature that provides the [TENANT API](api_tenant.html) as a Command Line Interface(CLI).
For more information on the API, see [TENANT API](api_tenant.html).

This command requires a K2HR3 Unscoped token. Specify the Unscoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Show
Displays LOCAL TENANT information.

### Format(1)
```
k2hr3 tenant show [--expand]
```
Displays lists the names(or all information including name) of LOCAL TENANT associated with the user.

### Format(2)
```
k2hr3 tenant show <tenant name>
```
Displays information for the specified LOCAL TENANT.

## Create
Create a new LOCAL TENANT.

### Format(1)
```
k2hr3 tenant create <tenant name> [--display <display name>] [--description <description>] [--users '["user","user",...]']
```
Create a new LOCAL TENANT with accompanying information.  
Specify the `tenant name` with the `local@` prefix.(If this is omitted, it will be granted automatically.)

## Update
Update all information of LOCAL TENANT.

### Format(1)
```
k2hr3 tenant update <tenant name> --tenantid <tenant id> [--display <display name>] [--description <description>] [--users '["user","user",...]']
```
Update all information of LOCAL TENANT.  
Specify the `tenant name` with the `local@` prefix.  
The `tenant id` must be a valid value.  

## Delete
Delete the LOCAL TENANT.

### Format(1)
```
k2hr3 tenant delete <tenant name> --tenantid <tenant id>
```
Deletes the specified LOCAL TENANT.  
The `tenant id` must be a valid value.  

## Options
You can specify the following options:
- -\-help(-h)
- -\-tenantid [tenant name]
- -\-display [display name for tenant]
- -\-description [description of tenant]
- -\-users [user name array as JSON string]
- -\-expand
