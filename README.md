# research

This repository is sandbox for ml experiments.

## Usage

Anyway copy template directory.

```bash
# If you create sandbox for recommendation project.
$cp -r ./template recommendation
```

Build docker images for each directory

```shell
$cd recommendation
$make build

# If you run container
$make run

# If you in running container
$make exec
root@f70caead665f:/workspace

# If you want to use jupyterlab in container
root@f70caead665f:/workspace# make jupyterlab
```
