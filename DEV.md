# DEV

## Fork Motivation

In the standard way we use this package, we to overwrite the fields even if they are not zero value.

The pre-fork way of doing it is adding an `overwrite` tag to all the fields of all the structs we use.

Instead of doing that, with this fork, we mutate the `overwrite` tag into `nooverwrite` tag and reverse the logic so by default it will overwrite the fields even if they are not zero value, unless they have the `nooverwrite` tag.

¯\\_(ツ)_/¯

## TODO

* [ ] Think if it's worthwhile to do an upstream pull request, may be with an option that reverse the logic or something..., the original package is awesome as it is, may me this complicate things for the rest...

## Chore

In the local clone, after pulling commits and tags from upstream and reapplying the fork changes and testing, we need to apply a tag that is `semver` superior but also that is not going to have conflicts with any future upstream tag.

Use tags with the following structure:

```text
AAA = 3 digit 0 padded UPSTREAM_MAYOR

BBB = 3 digit 0 padded UPSTREAM_MINOR

CCC = 3 digit 0 padded UPSTREAM_PATCH

DDD = 3 digit 0 padded incremental counter starting in 1

FORK_TAG = 1<AAA><BBB><CCC><DDD>

v<UPSTREAM_MAYOR>.<UPSTREAM_MINOR>.<FORK_TAG>

v<UPSTREAM_MAYOR>.<UPSTREAM_MINOR>.<FORK_TAG>-pre

v<UPSTREAM_MAYOR>.<UPSTREAM_MINOR>.<FORK_TAG>+build

v<UPSTREAM_MAYOR>.<UPSTREAM_MINOR>.<FORK_TAG>-pre+build
```

For example:

| upstream | fork              | issue |
| -------- | ----------------- | ----- |
| 2.3.1    |                   |       |
|          | 2.3.1002003001001 | ok    |
| 2.3.2    |                   |       |
|          | 2.3.1002003002001 | ok    |
|          | 2.3.1002003002002 | ok    |
|          | 2.3.1002003002003 | ok    |
| 2.4.1    |                   |       |
|          | 2.3.1002004001001 | ok    |
| 3.3.1    |                   |       |
|          | 2.3.1003003001001 | ok    |

Invalid options:

| upstream | fork      | issue                                                 |
| -------- | --------- | ----------------------------------------------------- |
| 2.3.1    |           |                                                       |
|          | 2.3.2     | future conflict with upstream tag                     |
|          | 2.4.1     | worst future conflict with upstream tag               |
|          | 3.3.1     | even worst future conflict with upstream tag          |
|          | 2.3.1-001 | is a semver pre-release so it's not picked for update |
|          | 2.3.1+001 | the build meta tag it's not picked for update         |
| 2.3.2    |           |                                                       |
| 2.4.1    |           |                                                       |
| 3.3.1    |           |                                                       |
