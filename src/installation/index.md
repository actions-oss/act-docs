# Installation

## Necessary prerequisites for running `act`

`act` depends on `docker` (exactly Docker Engine API) to run workflows in containers. As long you don't require container isolation, you can run selected (e.g. windows or macOS) jobs directly on your System see [Runners](../usage/runners.md). In the latter case you don't need to have docker installed or running.

If you are using macOS, please be sure to follow the steps outlined in [Docker Docs for how to install Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/).

If you are using Windows, please follow steps for [installing Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/).

If you are using Linux, you will need to [install Docker Engine](https://docs.docker.com/engine/install/).

To use `act` with remote Docker Engine API compatible host, see [Custom container engine](./../usage/custom_engine.md)
`act` is currently not supported with `podman` or other container backends (it might work, but it's not guaranteed).
Please see [#303](https://github.com/nektos/act/issues/303) for updates.

## Pre-built artifacts

### Manual download of prebuilt executable

Prebuilt executables for multiple platforms are available via [latest release](https://github.com/actions-oss/act-cli/releases/latest) page.
You can unpack and run them in terminal specifying full path or add them to one of the paths included in `PATH` environment variable.

- [macOS 64-bit (Apple Silicon)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Darwin_arm64.tar.gz)
- [macOS 64-bit (Intel)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Darwin_x86_64.tar.gz)
- [Linux 64-bit (arm64/aarch64)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Linux_arm64.tar.gz)
- [Linux 32-bit (armv6)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Linux_armv6.tar.gz)
- [Linux 32-bit (armv7)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Linux_armv7.tar.gz)
- [Linux 32-bit (i386/x86)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Linux_i386.tar.gz)
- [Linux 64-bit (amd64/x86_64)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Linux_x86_64.tar.gz)
- [Windows 64-bit (arm64/aarch64)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Windows_arm64.zip)
- [Windows 32-bit (armv7)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Windows_armv7.zip)
- [Windows 32-bit (i386/x86)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Windows_i386.zip)
- [Windows 64-bit (amd64/x86_64)](https://github.com/actions-oss/act-cli/releases/latest/download/act-cli_Windows_x86_64.zip)

### Build from source

Requires Go toolchain 1.23+

```shell
git clone https://github.com/actions-oss/act-cli.git
cd act/
make build
# OR
go build -ldflags "-X main.version=$(git describe --tags --dirty --always | sed -e 's/^v//')" -o dist/local/act main.go
```

## Installation via software package manager

`act` is available in below package repositories

- [GitHub CLI](./gh.md) (`Linux`, `macOS`, `Windows`, `FreeBSD`)
