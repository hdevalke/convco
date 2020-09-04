---
layout: page
title: convco-check
permalink: /check/
---

Check all commits or range for errors against the convention.

## Examples

```sh
convco check
```

Output:

```plain
FAIL   123ab45   first line doesn't match `<type>[optional scope]: <description>`   lorem ipsum

1/13 failed
```

This could be used in a git pre-push or pre-receive hook to enforce conventional commits.

```sh
#!/usr/bin/env sh
# put this file in: .git/hooks/pre-push
z40=0000000000000000000000000000000000000000
while read _ local_sha _ remote_sha; do
  if [ "$local_sha" != $z40 ]; then
    if [ "$remote_sha" = $z40 ]; then
      # New branch, examine all commits
      range="$local_sha"
    else
      # Update to existing branch, examine new commits
      range="$remote_sha..$local_sha"
    fi

    # Check for WIP commit
    if ! convco check "$range"; then
      exit 1
    fi
  fi
done
```

```sh
#!/usr/bin/env sh
# put this file in: .git/hooks/pre-receive
z40=0000000000000000000000000000000000000000
while read old_sha new_sha _; do
  if [ "$new_sha" != $z40 ]; then
    if [ "$old_sha" = $z40 ]; then
      # New branch, examine all commits
      range="$new_sha"
    else
      # Update to existing branch, examine new commits
      range="$old_sha..$new_sha"
    fi

    # Check for WIP commit
    if ! convco check "$range"; then
      exit 1
    fi
  fi
done
```

## Usage

```plain
convco-check 0.3.1
Verifies if all commits are conventional

USAGE:
    convco check [OPTIONS] [rev]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -c, --config <config>    
    -C <path>                Run as if convco was started in <path> instead of the current working directory

ARGS:
    <rev>     [default: HEAD]
```
