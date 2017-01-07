+++
author = ""
categories = ["command-of-the-day", "linux"]
date = "2017-01-02T23:43:22-08:00"
description = ""
draft = true
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Command of the Day 1: compgen"
type = "post"

+++
### Simple explanation

Show all available commands, aliases and functions

### whatis

compgen [builtins] (1) - bash built-in commands, see bash(1)

### help

`compgen: usage: compgen [-abcdefgjksuv] [-o option]  [-A action] [-G globpat] [-W wordlist]  [-F function] [-C command] [-X filterpat] [-P prefix] [-S suffix] [word]​`

### man

man 1 bash

# Usage

How are we going to create a list of commands for ‘Command of the Day’? Compgen!

compgen

*   -a: List of user aliases
*   -b: List of built-in shell commands
*   -c: List of all commands you can run
*   -e: List of shell variables
*   -k: List of built-in shell keywords
*   -A function: List of available bash functions

# Tip

Create an alias for compgen to show all functions: alias compgen=‘compgen -abckA function’. This will print in list format including all aliases, built-ins, commands and functions available

# References

*   [https://www.cyberciti.biz/open-source/command-line-hacks/compgen-linux-command/](https://www.cyberciti.biz/open-source/command-line-hacks/compgen-linux-command/)
*   [http://unix.stackexchange.com/questions/151118/understand-compgen-builtin-command](http://unix.stackexchange.com/questions/151118/understand-compgen-builtin-command)