---
layout: contents
language: en-us
title: CLI policy
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_policyja.html
lang_opp_word: To Japanese
prev_url: cli_role.html
prev_string: CLI role
top_url: cli.html
top_string: Command Line Interface
next_url: cli_resource.html
next_string: CLI resource
---

# Policy Subcommand
Describes the **policy** subcommand of the K2HR3 Command Line Interface(CLI).

The **policy** subcommand is a feature that provides the [POLICY API](api_policy.html) as a Command Line Interface(CLI).
For more information on the API, see [POLICY API](api_policy.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Show
Displays POLICY-RULE information.

### Format(1)
```
k2hr3 policy show [policy name | yrn path]
```
Displays information on the specified POLICY-RULE.

## Create
Generate a POLICY-RULE.

### Format(1)
```
k2hr3 policy create [policy name | yrn path] [--effect effect type] [--action action type] [--resource resource yrn path] [--alias policy yrn path]
```
Create a POLICY-RULE with accompanying information.

## Delete
Delete the POLICY-RULE.

### Format(1)
```
k2hr3 policy delete [policy name | yrn path]
```
Deletes the specified POLICY-RULE.

## Options
You can specify the following options:
- -\-help(-h)
- -\-effect [allow or deny]
- -\-action [yrn:yahoo::::action:read or yrn:yahoo::::action:write]
- -\-resource [resouces]
- -\-alias [aliases]
- -\-service [service name]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
