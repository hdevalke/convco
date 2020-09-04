---
layout: page
title: convco-commit
permalink: /commit/
---

Interactive cli to create a conventional commit.
A wizard will guide you to create a conventional commit.

## Example

```sh
convco commit --feat -- -p --edit
```

## Usage

```plain
convco-commit 0.3.1
Helps to make conventional commits

USAGE:
    convco commit [FLAGS] [OPTIONS] [-- <extra-args>...]

FLAGS:
        --breaking    Introduces a breaking change
        --build       Changes that affect the build system or external dependencies
        --chore       Other changes that don't modify src or test files
        --ci          Changes to CI configuration files and scripts
        --docs        Documentation only changes
        --feat        A new feature
        --fix         A bug fix
    -h, --help        Prints help information
        --perf        A code change that improves performance
        --refactor    A code change that neither fixes a bug nor adds a feature
        --style       Changes that do not affect the meaning of the code (e.g. formatting)
        --test        Adding missing tests or correcting existing tests
    -V, --version     Prints version information

OPTIONS:
    -c, --config <config>    
    -C <path>                Run as if convco was started in <path> instead of the current working directory

ARGS:
    <extra-args>...    Extra arguments passed to the git command
```
