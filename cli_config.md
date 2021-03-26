---
layout: contents
language: en-us
title: CLI config
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: cli_configja.html
lang_opp_word: To Japanese
prev_url: cli_options.html
prev_string: CLI options
top_url: cli.html
top_string: Command Line Interface
next_url: cli_version.html
next_string: CLI version
---

# Config Subcommand
Describes the **config** subcommand of the K2HR3 Command Line Interface(CLI).

The **config** subcommand is a function to display and operate the contents of the K2HR3 Command Line Interface(CLI) configuration(file).

## Show
Displays the contents of the K2HR3 Command Line Interface(CLI) configuration(file).

### Format(1)
```
k2hr3 config show
```
Displays a list of variables that can be set in the K2HR3 Command Line Interface(CLI) configuration(file).

### Format(2)
```
k2hr3 config show all
```
Displays the variables and their values ​​set in the K2HR3 Command Line Interface(CLI) configuration(file).

### Format(3)
`` ```
k2hr3 config show [variable name]
`` ```
Displays the specified variable and its value set in the K2HR3 Command Line Interface(CLI) configuration(file).

## Set
Set values ​​for variables in the K2HR3 command line interface(CLI) configuration(file).

### Format(1)
`` ```
k2hr3 config set [variable name] [value]
`` ```
Sets a value to the specified variable in the K2HR3 Command Line Interface(CLI) configuration(file).

## Clear
Clears the value of a variable in the K2HR3 Command Line Interface(CLI) configuration(file).

### Format(1)
`` ```
k2hr3 config clear [variable name]
`` ```
Clears(unset) the value of the specified variable in the K2HR3 Command Line Interface(CLI) configuration(file).

## Options
You can specify the following options:
- -\-help(-h)
- -\-config(-c) [file]
