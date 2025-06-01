# Introduction

<div class="warning">

This is a derivative of [nektos/act](https://github.com/nektos/act)
between version v0.2.71 from January 2025 and v0.2.72 February 2025

</div>

- Support for macOS VMs using tart `-P tart://`
- `--use-new-action-cache` has been removed, the default clone mode of nektos/act has been removed
- CI tests are run in 6min compared to 17min on nektos/act
- Flags `--pull=false` and `--rebuild=false` are inverted to `--no-poll` and `--no-rebuild`
