# Installing PyTorch with uv

Ref. <https://docs.astral.sh/uv/guides/integration/pytorch/#installing-pytorch>.

On Mac OS X with M1 chip.

## Brew - Xcode

Brew install of uv.

```zsh
brew update && brew upgrade && brew install uv && brew doctor && echo SUCCESS
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

## uv init with some dev tools

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

Add flake8 and black

```zsh
uv add flake8 black --dev
```

Now we can run flake8 and black on the `/code` dir
(besides running automatically in the IDE).

```zsh
uv run black code && uv run flake8 code && echo SUCCESS
```

## Add torch and torchvision for different platform

For now (since only doing this for Mac ARM architecture), I am forcing `cpu` versions
for all architectures. Turns out that on Mac, the `+cpu` extension on the package name
is not needed when downloading wheels (presumable because there are no other extensions?).
On other architectures, a `+cpu` is added to the name (but not tested here).

Edit the `pyproject.toml` to add these blocks:

```toml
[tool.uv.sources]
torch = [
  { index = "pytorch-cpu" },
]
torchvision = [
  { index = "pytorch-cpu" },
]

[[tool.uv.index]]
name = "pytorch-cpu"
url = "https://download.pytorch.org/whl/cpu"
explicit = true
```

Then add torch and torchvision:

```zsh
uv add torch torchvision
```

This will update the `pyproject.toml` file and the `uv.lock` file.

## Add notebook and main huggingface and StabilityAI related pakcages

Additional packages in pyproject.toml:
```
    "ipykernel>=6.29.5",
    "ipywidgets>=8.1.5",
    "diffusers>=0.32.1",
    "transformers>=4.47.1",
    "accelerate>=1.2.1",
    "huggingface-hub[cli]>=0.27.0",
    "protobuf>=5.29.2",
    "sentencepiece>=0.2.0",
```
