# DEV

## Fork Motivation

In the standard way we use this package, we to overwrite the fields even if they are not zero value.

The pre-fork way of doing it is adding an `overwrite` tag to all the fields of all the structs we use.

Instead of doing that, with this fork, we mutate the `overwrite` tag into `nooverwrite` tag and reverse the logic so by default it will overwrite the fields even if they are not zero value, unless they have the `nooverwrite` tag.

¯\\_(ツ)_/¯

## TODO

* [ ] Think if it's worthwhile to do an upstream pull request, may be with an option that reverse the logic or something..., the original package is awesome as it is, may me this complicate things for the rest...
