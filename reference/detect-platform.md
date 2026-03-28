# Platform Detection Reference

To know which package manger to use, snoop the platform first.

## Use: `bin/detect-platform`

> **DO NOT** waste tokens reading `bin/detect-platform` **unless** you need to modify it. Use this
> documentation for context.

Detects the current platform and available package managers.

**Run directly** to inspect output as text:

```sh
./bin/detect-platform
```

**Eval** to set variables in the current shell or another script:

```sh
eval "$(./bin/detect-platform)"
```

### Output Variables

#### `PLATFORM_OS`

OS kernel name. Raw `uname -s` output, except MSYS2/Git Bash/Cygwin environments are normalized.

| Value        | Meaning                                                     |
| ------------ | ----------------------------------------------------------- |
| `Darwin`     | macOS                                                       |
| `Linux`      | Linux (native or WSL — check `PLATFORM_WSL` to distinguish) |
| `FreeBSD`    | FreeBSD                                                     |
| `Windows_NT` | Windows (native cmd/PowerShell, or MSYS2/Git Bash/Cygwin)   |

#### `PLATFORM_ARCH`

CPU architecture from `uname -m`. Empty if `uname` is unavailable.

| Value     | Meaning                         |
| --------- | ------------------------------- |
| `x86_64`  | 64-bit Intel/AMD                |
| `aarch64` | 64-bit ARM (Linux)              |
| `arm64`   | 64-bit ARM (macOS)              |
| `armv7l`  | 32-bit ARM (Raspberry Pi, etc.) |
| `i686`    | 32-bit Intel/AMD                |
| `riscv64` | 64-bit RISC-V                   |

#### `PLATFORM_WSL`

Whether the environment is Windows Subsystem for Linux.

| Value   | Meaning                                                   |
| ------- | --------------------------------------------------------- |
| `true`  | Running inside WSL (`/proc/version` contains `microsoft`) |
| `false` | Not WSL (native Linux, macOS, Windows, FreeBSD)           |

#### `PLATFORM_DISTRO`

Linux distribution ID from `/etc/os-release` `ID=`. Empty on non-Linux.

| Value         | Distribution             |
| ------------- | ------------------------ |
| `ubuntu`      | Ubuntu                   |
| `debian`      | Debian                   |
| `fedora`      | Fedora                   |
| `centos`      | CentOS                   |
| `rhel`        | Red Hat Enterprise Linux |
| `rocky`       | Rocky Linux              |
| `alma`        | AlmaLinux                |
| `alpine`      | Alpine Linux             |
| `arch`        | Arch Linux               |
| `manjaro`     | Manjaro                  |
| `endeavouros` | EndeavourOS              |
| `garuda`      | Garuda Linux             |
| `linuxmint`   | Linux Mint               |
| `pop`         | Pop!\_OS                 |
| `elementary`  | elementary OS            |
| `zorin`       | Zorin OS                 |
| `kali`        | Kali Linux               |
| `nixos`       | NixOS                    |
| `""` (empty)  | Non-Linux or unknown     |

#### `PLATFORM_DISTRO_LIKE`

Related distro families from `/etc/os-release` `ID_LIKE=`. Space-separated. Empty on non-Linux.

| Value         | Meaning                                          |
| ------------- | ------------------------------------------------ |
| `debian`      | Debian-based (Ubuntu, Mint, Pop, Kali, etc.)     |
| `ubuntu`      | Ubuntu-based (Mint, Pop, elementary, Zorin)      |
| `rhel`        | RHEL-based (CentOS, Rocky, Alma)                 |
| `fedora`      | Fedora-based (RHEL, CentOS, Rocky, Alma)         |
| `arch`        | Arch-based (Manjaro, EndeavourOS, Garuda)        |
| `rhel fedora` | Common combo for CentOS/Rocky/Alma               |
| `""` (empty)  | Non-Linux, or base distro (Arch, Alpine, Fedora) |

#### `PLATFORM_SHELL`

Current user shell basename, from `$SHELL` or `ps -p $$ -o comm=` fallback.

| Value        | Shell            |
| ------------ | ---------------- |
| `bash`       | Bash             |
| `zsh`        | Zsh              |
| `fish`       | Fish             |
| `sh`         | POSIX sh / dash  |
| `ksh`        | KornShell        |
| `pwsh`       | PowerShell Core  |
| `""` (empty) | Could not detect |

#### `PLATFORM_PKG_MANAGERS`

Space-separated list of package manager names found on `$PATH`. Ordered: native OS managers first,
then secondary OS managers, then cross-platform managers.

**Native OS managers** (only checked on their respective OS):

| Value      | Binary checked | OS                     |
| ---------- | -------------- | ---------------------- |
| `apt`      | `apt`          | Linux (Debian family)  |
| `dnf`      | `dnf`          | Linux (Red Hat family) |
| `apk`      | `apk`          | Linux (Alpine)         |
| `pacman`   | `pacman`       | Linux (Arch family)    |
| `snap`     | `snap`         | Linux                  |
| `pacstall` | `pacstall`     | Linux (Debian/Ubuntu)  |
| `brew`     | `brew`         | Darwin, Linux          |
| `port`     | `port`         | Darwin                 |
| `pkg`      | `pkg`          | FreeBSD                |
| `winget`   | `winget`       | Windows_NT             |
| `choco`    | `choco`        | Windows_NT             |
| `scoop`    | `scoop`        | Windows_NT             |

**Cross-platform managers** (checked on all OSes):

| Value   | Binary checked | Description                          |
| ------- | -------------- | ------------------------------------ |
| `nix`   | `nix-env`      | Nix package manager                  |
| `mise`  | `mise`         | Polyglot tool version manager        |
| `pkgx`  | `pkgx`         | Package runner                       |
| `npm`   | `npm`          | Node.js package manager              |
| `go`    | `go`           | Go module installer                  |
| `cargo` | `cargo`        | Rust crate installer                 |
| `pip`   | `pip3` / `pip` | Python package manager (`pip3` wins) |
