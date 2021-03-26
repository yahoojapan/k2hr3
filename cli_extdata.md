---
layout: contents
language: en-us
title: CLI extdata
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_extdataja.html
lang_opp_word: To Japanese
prev_url: cli_userdata.html
prev_string: CLI userdata
top_url: cli.html
top_string: Command Line Interface
next_url: 
next_string: 
---

# EXTDATA Subcommand
Describes the **extdata** subcommand of the K2HR3 Command Line Interface(CLI).

The **exitdata** subcommand is a feature that provides the [EXTDATA API](api_extdata.html) as a Command Line Interface(CLI).
For more information on the API, see [EXTDATA API](api_extdata.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Get
Gets and displays the user-defined EXTRA DATA SCRIPT.

### Format(1)
```
k2hr3 extdata [extdata name] [registerpath] [user agent] [--output file path]
```
Gets the contents of the user-defined EXTRA DATA SCRIPT by specifying the **registrepath** that will be retrieved when the role token is generated.
For information on working with role tokens, see [Role Subcommand](cli_role.html).

## Options
You can specify the following options:
- -\-help(-h)
- -\-output [file path]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
