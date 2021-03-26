---
layout: contents
language: en-us
title: CLI version
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_versionja.html
lang_opp_word: To Japanese
prev_url: cli_config.html
prev_string: CLI config
top_url: cli.html
top_string: Command Line Interface
next_url: cli_token.html
next_string: CLI token
---

# Version Subcommand
Describes the **version** subcommand of the K2HR3 Command Line Interface(CLI).

The **version** subcommand is a function provided as the Command Line Interface(CLI) of the [VERSION API](api_version.html).
For more information on the API, see [VERSION API](api_version.html).

## k2hr3 version
Display the list of [K2HR3 REST API](api.html).

### Format
```
k2hr3 version
```

## k2hr3 version [version string]
Displays a list of the specified versions of the [K2HR3 REST API](api.html).
Currently only `v1` is supported.

### Format
```
k2hr3 version v1
```

## Options
You can specify the following options:
- -\-help(-h)
- -\-json(-j)
