# Known issues

To see all current issues, go to <https://github.com/actions-oss/act-cli/issues>

- [`MODULE_NOT_FOUND`](./module_not_found.md)

## Manual cleanup

Applies to linux and macOS.

Resource leakage of docker images and container

### Remove all containers managed by act

```sh
docker ps -a --format '{{ if eq (truncate .Names 4) "act-" }}
{{ .ID }}
{{end}}' | xargs docker rm -f
```

### Remove all volumes managed by act

```sh
docker volume ls --format '{{ if eq (truncate .Name 4) "act-" }}
{{ .Name }}
{{ end }}' | xargs docker volume rm -f
```

### Remove all images managed by act

```sh
docker images --format '{{ if eq (truncate .Repository 4) "act-" }}
{{ .ID }}
{{ end }}' | xargs docker rmi -f
```
