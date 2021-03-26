---
layout: contents
language: en-us
title: CLI userdata
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_userdataja.html
lang_opp_word: To Japanese
prev_url: cli_acr.html
prev_string: CLI acr
top_url: cli.html
top_string: Command Line Interface
next_url: cli_extdata.html
next_string: CLI extdata
---

# USERDATA Subcommand
Describes the **userdata** subcommand of the K2HR3 Command Line Interface(CLI).

The **userdata** subcommand is a feature that provides the [USERDATA API](api_userdata.html) as a Command Line Interface(CLI).
For more information on the API, see [USERDATA API](api_userdata.html).

This command requires a K2HR3 Scoped token. Specify the Scoped token of K2HR3 in the option or configuration file, or specify the `--interactive(-i)` option.

## Get
Gets and displays the UserDataScript for OpenStack.

### Format(1)
```
k2hr3 userdata [registerpath] [--output file path]
```
Get the contents of UserDataScript for OpenStack by specifying the **registrepath** that will be obtained when the role token is generated.
For information on working with role tokens, see [Role Subcommand](cli_role.html).

## Options
You can specify the following options:
- -\-help(-h)
- -\-output [file path]
- -\-scopedtoken(-token) [scoped token]
- -\-config(-c) [file]
- -\-interactive(-i)
