# Install EWCCLI

Use this reference for installing `ewccli` and checking the local `ewc` command.

## Requirements

- Python 3.10 through 3.14.
- `git` for custom Hub item deployment from repositories.
- Network access for package installation and EWC Community Hub catalogue download.

Pin the release this skill covers: `ewccli==0.10.0`. Every command and flag in these references was verified against it, and a newer release may register, rename, or remove `ewc` commands. Move to a newer version only after re-checking `ewc --help` and the upstream changelog at https://github.com/ewcloud/ewccli.

## Locate The CLI First

Find the command on `PATH` before proposing any install: `command -v ewc` on Linux and macOS, `where ewc` on Windows. Never assume a project `.venv`, a personal virtualenv directory, or any other path; the user says where their environment is. If the command is missing, install it into one of the standard user-tool locations below, or into a virtual environment at a path the user names (`<venv>`).

| Method | Executable lands in | Environment lives in |
| --- | --- | --- |
| `uv tool install` | `~/.local/bin` (Linux, macOS); `%USERPROFILE%\.local\bin` (Windows) | `~/.local/share/uv/tools`; `%APPDATA%\uv\tools` |
| `pipx install` | `~/.local/bin`; `%USERPROFILE%\.local\bin` | `~/.local/pipx/venvs`; `%USERPROFILE%\pipx\venvs` |
| Virtual environment | `<venv>/bin` (`<venv>\Scripts` on Windows) | `<venv>`, a path the user chooses |

If the executable directory is not on `PATH`, `uv tool update-shell` or adding it to the shell startup file fixes that; say which file only after asking which shell the user runs.

## Installation Choices

As a user tool (Python 3.10 or newer):

```bash
uv tool install --python 3.12 'ewccli==0.10.0'
ewc --help
ewc version
```

Into a virtual environment at a path the user names:

```bash
python3 -m venv <venv>
<venv>/bin/python -m pip install 'ewccli==0.10.0'
<venv>/bin/ewc --help
```

For an existing Python environment:

```bash
python -m pip install 'ewccli==0.10.0'
ewc --help
ewc version
```

## PATH Warning

If pip or uv prints that `ewc` was installed in a directory not on `PATH`, that directory is `~/.local/bin` on Linux and macOS and `%USERPROFILE%\.local\bin` or the Python `Scripts` directory on Windows. Ask which shell the user runs, then add the directory to that shell's startup file, or run `uv tool update-shell` for uv installs.

## Container Option

For container-based isolation, point the user to the upstream repository README: https://github.com/ewcloud/ewccli.

## Credential-Free Verification

These checks do not require European Weather Cloud credentials:

```bash
ewc --help
ewc version
ewc login --help
ewc hub --help
ewc infra --help
python -c "import ewccli; print(ewccli.__file__)"
```

Do not run `ewc login`, `ewc hub deploy`, or `ewc infra create/delete` as a basic install check.
