---
layout: contents
language: en-us
title: CLI token
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_tokenja.html
lang_opp_word: To Japanese
prev_url: cli_version.html
prev_string: CLI version
top_url: cli.html
top_string: Command Line Interface
next_url: cli_list.html
next_string: CLI list
---

# Token Subcommand
Describes the **token** subcommand of the K2HR3 Command Line Interface(CLI).

The **token** subcommand is a function that provides [TOKEN API](api_token.html) as a Command Line Interface(CLI).
For more information on the API, see [TOKEN API](api_token.html).

## Show
Displays the token information specified in the option or the token set in the configuration file.

### Format(1)
```
k2hr3 token show utoken [--unscopedtoken(-utoken) unscoped token]
```
Displays the information of the Unscoped token of K2HR3 specified as an option or the Unscoped token set in the configuration file.
If you use the value in the configuration file, do not optionally specify the token.

### Format(2)
```
k2hr3 token show token [--scopedtoken(-token) scoped token]
```
Displays the information of the Scoped token of K2HR3 specified as an option or the Scoped token set in the configuration file.
If you use the value in the configuration file, do not optionally specify the token.

## Create
Generate an Unscoped or Scoped token for K2HR3.

### Format(1)
```
k2hr3 token create utoken_cred [--user(-u) user name] [--passphrase(-p) passphrase]
```
Generate a K2HR3 Unscoped token using user credentials(username, passphrase).
If the user name and passphrase are omitted, the user name and passphrase set in the configuration file will be used.
If those values ​​are not set in the configuration file, and the `--interactive(-i)` option is specified, you will be prompted interactively.

### Format(2)
```
k2hr3 token create utoken_optoken [--openstacktoken(-optoken) openstack token]
```
Use OpenStack tokens(Unscoped or Scoped) to generate K2HR3 Unscoped tokens.
If the OpenStack token(Unscoped or Scoped) is omitted, the OpenStack token(Unscoped or Scoped) set in the configuration file will be used.
If the value is not set in the configuration file, and the `--interactive(-i)` option is specified, you will be prompted interactively.

### Format(3)
```
k2hr3 token create token_cred [--user(-u) user name] [--passphrase(-p) passphrase] [--tenant(-t) tenant]
```
Generate a K2HR3 Scoped token using user credentials (username, passphrase) and tenant name.
If the user name, passphrase, and tenant name are omitted, the user name, passphrase, and tenant name set in the configuration file will be used.
If those values ​​are not set in the configuration file, and the `--interactive(-i)` option is specified, you will be prompted interactively.

### Format(4)
```
k2hr3 token create token_utoken [--unscopedtoken(-utoken) unscoped token] [--tenant(-t) tenant]
```
Generate a K2HR3 Scoped token using the K2HR3 Unscoped token and tenant name.
If the K2HR3 Unscoped token and tenant name are omitted, the K2HR3 Unscoped token and tenant name set in the configuration file will be used.
If those values ​​are not set in the configuration file, and the `--interactive(-i)` option is specified, you will be prompted interactively.

### Format(5)
```
k2hr3 token create token_optoken [--openstacktoken(-optoken) openstack token] [--tenant(-t) tenant]
```
Generate a K2HR3 Scoped token using the OpenStack token(Unscoped or Scoped) and the tenant name.
If the OpenStack token(Unscoped or Scoped) and tenant name are omitted, the OpenStack token(Unscoped or Scoped) and tenant name set in the configuration file will be used.
If those values ​​are not set in the configuration file, and the `--interactive(-i)` option is specified, you will be prompted interactively.

## Check
Check the Unscoped or Scoped token of K2HR3.

### Format(1)
```
k2hr3 token check [--unscopedtoken(-utoken) unscoped token]
k2hr3 token check [--scopedtoken(-token) scoped token]
```
Validate the specified K2HR3 Unscoped or Scoped token.
If you omit the token option, the Scoped token set in the configuration file is checked.

## Options
You can specify the following options:
- -\-help(-h)
- -\-config(-c) [file]
- -\-interactive(-i)
- -\-saveconfig(-s)
- -\-savepassphrase(-sp)
