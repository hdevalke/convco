---
layout: page
title: configuration
permalink: /configuration/
---

Configuration is based on the [conventional changelog config spec][1].

The configuration must be specified in a `.versionrc` file in the root of the repository.
YAML of JSON can be used to declare the configuration.
`host`, `owner` and `repository` will not be looked up from `package.json` as `convco` is build tool agnostic.

Additionally `scopeRegex` and `template` can be specified to restrict scopes or use a different template directory.

Most configuration is used with `convco-changelog`, but `scopeRegex` is used in the other commands.

## Configuration

{% raw %}
| config key                   | description                              | default value                              |
| ---------------------------- | ---------------------------------------- | -------------------------------------------|
| `header`                     | the header of the changelog              | `"# Changelog\n\n"`                        |
| `types`                      | show/hide/group commit types             | see [default configuration](#default-configuration)                              |
| `preMajor`                   | automatically set by `convco`            | `true` if version `<1.0.0` else `false`    |
| `commitUrlFormat`            | a URL to a specific commit hash          | `"{{host}}/{{owner}}/{{repository}}/commit/{{hash}}"`                            |
| `compareUrlFormat`           | a URL to compare two git shas            | `"{{host}}/{{owner}}/{{repository}}/compare/{{previousTag}}...{{currentTag}}"`   |
| `issueUrlFormat`             | a URL to the issue                       | `"{{host}}/{{owner}}/{{repository}}/issues/{{id}}"`                              |
| `userUrlFormat`              | a URL to the user's profile              | `"{{host}}/{{user}}"`                      |
| `releaseCommitMessageFormat` | not used                                 | `"chore(release): {{currentTag}}`          |
| `issuePrefixes`              | used to detect issues in the commit body | `[ "#" ]`                                  |
| `host`                       | the host to be used in `commitUrlFormat`, `compareUrlFormat`, `issueUrlFormat` | extracted from `git remote get-url origin` |
| `owner`                      | the repository owner                     | extracted from `git remote get-url origin` |
| `repository`                 | the repository url                       | extracted from `git remote get-url origin` |
| `template`                   | template directory path                  | empty, the build in [template][2] is used  |
| `scopeRegex`                 | limit valid scopes                       | `"[[:alnum:]]+(?:[-_/][[:alnum:]]+)*"`     |
{% endraw %}

### URL formats

The commit, compare, issue and user url format can

### Default configuration

{% raw %}

```yaml
# .versionrc
---
header: "# Changelog\n\n"
types:
  - type: feat
    section: Features
    hidden: false
  - type: fix
    section: Fixes
    hidden: false
  - type: build
    section: Other
    hidden: true
  - type: chore
    section: Other
    hidden: true
  - type: ci
    section: Other
    hidden: true
  - type: docs
    section: Documentation
    hidden: true
  - type: style
    section: Other
    hidden: true
  - type: refactor
    section: Other
    hidden: true
  - type: perf
    section: Other
    hidden: true
  - type: test
    section: Other
    hidden: true
preMajor: false
commitUrlFormat: "{{host}}/{{owner}}/{{repository}}/commit/{{hash}}"
compareUrlFormat: "{{host}}/{{owner}}/{{repository}}/compare/{{previousTag}}...{{currentTag}}"
issueUrlFormat: "{{host}}/{{owner}}/{{repository}}/issues/{{id}}"
userUrlFormat: "{{host}}/{{user}}"
releaseCommitMessageFormat: "chore(release): {{currentTag}}"
issuePrefixes:
  - "#"
host: ~
owner: ~
repository: ~
template: ~
scopeRegex: "[[:alnum:]]+(?:[-_/][[:alnum:]]+)*"
```

{% endraw %}

[1]: https://github.com/conventional-changelog/conventional-changelog-config-spec/blob/master/versions/2.1.0/README.md
[2]: https://github.com/hdevalke/convco/tree/master/src/conventional/changelog