# UV Guide

## Installation and update

1. Linux
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh

# update
uv self update
```

2. Windows
```ps
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# update
uv self update
```

## Uninstall uv

1. Clean up stored data (optional):
```bash
uv cache clean
rm -r "$(uv python dir)"
rm -r "$(uv tool dir)"
```

2. Remove the uv and uvx binaries
```bash
rm ~/.local/bin/uv ~/.local/bin/uvx
```

## Projects
uv manages project dependencies and environments, with support for lockfiles, workspaces, and more, similar to rye or poetry
```bash
# initialize a project named example
uv init example

cd example

# create virtual environment if nor available and add dependency ruff
uv add ruff

# remove a dependency from the project
uv remove ruff

# run a command in the project environment.
uv run ruff check

# create a lockfile for the project's dependencies.
uv lock

# sync the project's dependencies with the environment
uv sync

# view the dependency tree for the project
uv tree

# build the project into distribution archives
uv build

# publish the project to a package index
uv publish

```

## Scripts
uv manages dependencies and environments for single-file scripts
```bash
# create a new script and add inline metadata declaring its dependencies
echo 'import requests; print(requests.get("https://astral.sh"))' > example.py

# add a dependency to a script
uv add --script example.py requests

# run the script in an isolated virtual environment
uv run example.py

# remove a dependency from a script
uv remove --script example.py requests
```

## Tools
uv executes and installs command-line tools provided by Python packages, similar to pipx

```bash
# run a tool in an ephemeral environment using uvx (an alias for uv tool run)
# uvx / uv tool run
uvx pycowsay 'hello world!'

# install tool ruff
uv tool install ruff
ruff --version

# uninstall a tool
uv tool uninstall ruff

# list installed tools
uv tool list

# update the shell to include tool executables
uv tool update-shell

```

## Python Versions
uv installs Python and allows quickly switching between versions.

```bash
# install multiple Python versions
uv python install 3.10 3.11 3.12

# View available Python versions.
uv python list

# Find an installed Python version.
uv python find 3.11

# download Python versions as needed
uv venv --python 3.12.0

# run python version
uv run --python pypy@3.8 -- python

# use a specific Python version in the current directory/project
uv python pin 3.11

# Uninstall a Python version.
uv python uninstall 3.11

```

## The pip interface
uv provides a drop-in replacement for common pip, pip-tools, and virtualenv commands

```bash

# create a virtual environment
uv venv

# install packages into the current environment
uv pip install

# show details about an installed package
uv pip show

# list installed packages
uv pip list

# list installed packages and their versions
uv pip freeze

# compile requirements into a platform-independent requirements file
uv pip compile docs/requirements.in \
   --universal \
   --output-file docs/requirements.txt



# install the locked requirements
uv pip sync docs/requirements.txt


```
## Reference
1. [uv docs](https://docs.astral.sh/uv/)
2. [uv installation guide](https://docs.astral.sh/uv/getting-started/installation/#docker)
