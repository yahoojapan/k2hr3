---
layout: contents
language: en-us
title: CLI resource
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_resourceja.html
lang_opp_word: To Japanese
prev_url: cli_policy.html
prev_string: CLI policy
top_url: cli.html
top_string: Command Line Interface
next_url: cli_service.html
next_string: CLI service
---

# Resource Subcommand
Describes the **resource** subcommand of the K2HR3 Command Line Interface(CLI).

The **resource** subcommand is a feature that provides the [RESOURCE API](api_resource.html) as a Command Line Interface(CLI).
For more information on the API, see [RESOURCE API](api_resource.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Show
Displays RESOURCE information.

### Format(1)
```
k2hr3 resource show [resource name | yrn path]
```
Displays information on the specified RESOURCE.

## Create
Generates and updates RESOURCE.

### Format(1)
```
k2hr3 resource create [resource name | yrn path] [--type type] [--data data] [--datafile filepath] [--keys key pair] [--alias role path]
```
If you specify a RESOURCE that does not exist, it will be generated with the accompanying information.
If you specify an existing RESOURCE, update its accompanying information.

## Delete
Delete the RESOURCE or the element of the RESOURCE.

### Format(1)
```
k2hr3 resource delete [resource name | yrn path] [--type type] [--keynames key names] [--aliases aliases]
```
If no option is specified, the RESOURCE is deleted.
If the option is specified, the accompanying information of the RESOURCE is deleted.

## Options
You can specify the following options:
- -\-help(-h)
- -\-type [type]
- -\-data [resource data]
- -\-datafile [resoruce data file]
- -\-keys [key value datas]
- -\-alias [aliases]
- -\-service [service name]
- -\-keynames [key names]
- -\-aliases [aliases]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
