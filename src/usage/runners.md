# Runners

GitHub Actions offers managed [virtual environments](https://help.github.com/en/actions/reference/virtual-environments-for-github-hosted-runners) for running workflows.
In order for `act` to run your workflows locally, it must run a container for the runner defined in your workflow file. Here are the images that `act` uses for each runner type and size:

| GitHub Runner   | Micro Docker Image               | Medium Docker Image                               | Large Docker Image                                 |
| --------------- | -------------------------------- | ------------------------------------------------- | -------------------------------------------------- |
| `ubuntu-latest` | [`node:16-buster-slim`][micro]   | [`catthehacker/ubuntu:act-latest`][docker_images] | [`catthehacker/ubuntu:full-latest`][docker_images] |
| `ubuntu-22.04`  | [`node:16-bullseye-slim`][micro] | [`catthehacker/ubuntu:act-22.04`][docker_images]  | [`catthehacker/ubuntu:full-22.04`][docker_images]  |
| `ubuntu-20.04`  | [`node:16-buster-slim`][micro]   | [`catthehacker/ubuntu:act-20.04`][docker_images]  | [`catthehacker/ubuntu:full-20.04`][docker_images]  |
| `ubuntu-18.04`  | [`node:16-buster-slim`][micro]   | [`catthehacker/ubuntu:act-18.04`][docker_images]  | [`catthehacker/ubuntu:full-18.04`][docker_images]  |

[micro]: https://hub.docker.com/_/buildpack-deps
[docker_images]: https://github.com/catthehacker/docker_images

If you want to run Windows and macOS based platforms and you are running act within that specfic environment you can opt out of docker and run them directly on your host system.

Here are some examples
```sh
act -P ubuntu-latest=-self-hosted
act -P windows-latest=-self-hosted
act -P macos-latest=-self-hosted
```

## Default runners are intentionally incomplete

These default images do **not** contain **all** the tools that GitHub Actions offers by default in their runners.
Many things can work improperly or not at all while running those image.
Additionally, some software might still not work even if installed properly, since GitHub Actions are running in fully virtualized machines while `act` is using Docker containers (e.g. Docker does not support running `systemd`).
In case of any problems [please create issue](https://github.com/actions-oss/act-cli/issues/new/choose) in respective repository and issues with any image from user `catthehacker` in [`catthehacker/docker_images`](https://github.com/catthehacker/docker_images))

## Alternative runner images

- [`catthehacker/ubuntu:full-*`](https://github.com/catthehacker/docker_images/pkgs/container/ubuntu) - filesystem dump of the Runners provided by GitHub, see [`ChristopherHX/runner-image-blobs`](https://github.com/ChristopherHX/runner-image-blobs) or [`catthehacker/docker_images`](https://github.com/catthehacker/docker_images) for more information

### Use an alternative runner image

To use a different image for the runner, use the `-P` option.

```sh
act -P <platform>=<docker-image>
```

If your workflow uses `ubuntu-18.04`, consider below line as an example for changing Docker image used to run that workflow:

```sh
act -P ubuntu-18.04=nektos/act-environments-ubuntu:18.04
```

If you use multiple platforms in your workflow, you have to specify them to change which image is used.
For example, if your workflow uses `ubuntu-18.04`, `ubuntu-16.04` and `ubuntu-latest`, specify all platforms like below

```sh
act -P ubuntu-18.04=nektos/act-environments-ubuntu:18.04 -P ubuntu-latest=ubuntu:latest -P ubuntu-16.04=node:16-buster-slim
```

### Using local runner images

The `--pull` flag is set to true by default due to a breaking on older default docker images. This would pull the docker image everytime act is executed.

Set `--pull` to false if a local docker image is needed
```sh
  act --pull=false
```

Alternatively turn on offline mode

```sh
  act --action-offline-mode
```
