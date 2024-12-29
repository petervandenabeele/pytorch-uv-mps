# Installing PyTorch with uv

Ref. <https://docs.astral.sh/uv/guides/integration/pytorch/#installing-pytorch>.

On Mac OS X with M1 chip.

## Brew - Xcode

Brew install of uv.

```zsh
brew update && brew upgrade && brew install uv && brew doctor && echo "SUCCESS :-)"
```

Make sure Xcode is installed.

```zsh
xcode-select --install
xcode-select --version  # xcode-select version 2409.
```

## Python with uv

Install python 3.12 with uv (very fast !) and pin it:

```zsh
uv python install 3.12.8
# Installed Python 3.12.8 in 2.14s
#  + cpython-3.12.8-macos-aarch64-none
uv python pin
```

Check where it is installed ("stay curious!"):

```zsh
uv python list | grep 'uv' | grep '3\.12\.8'
# cpython-3.12.8-macos-aarch64-none                 /Users/peter_v/.local/share/uv/python/cpython-3.12.8-macos-aarch64-none/bin/python3.12
```

Initialize `uv` with default config:

```zsh
uv init --python 3.12.8
# => Initialized project `pytorch-uv-mps`
```

This yields a default, basic pyproject.toml:

```zsh
cat pyproject.toml
```

```toml
[project]
name = "pytorch-uv-mps"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12.8"
dependencies = []
```
