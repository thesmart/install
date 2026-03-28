# Package Manager Reference

Command-line reference for installing, uninstalling, searching, and listing packages across
supported package managers. Use this to construct the correct command for a given package manager.

## Match Fields

Each entry uses these fields to identify when a package manager applies:

- **os** — one of: `Darwin`, `Linux`, `FreeBSD`, `Windows_NT`
- **distro** — e.g. `ubuntu`, `debian`, `fedora`, `alpine`, `arch`, `nixos`
- **distro_like** — e.g. `debian`, `ubuntu`, `rhel`, `fedora`, `arch`
- **cmd_exists** — binary name to check on `$PATH`

---

## Linux Package Managers

### dnf

RPM-based package manager for Red Hat family distributions.

| Field       | Match                                       |
| ----------- | ------------------------------------------- |
| os          | `Linux`                                     |
| distro      | `fedora`, `centos`, `rhel`, `rocky`, `alma` |
| distro_like | `fedora`, `rhel`                            |
| cmd_exists  | `dnf`                                       |

System-wide only (requires `sudo`).

```sh
sudo dnf install <pkg>           # install
sudo dnf install <pkg>-<version> # specific version
sudo dnf remove <pkg>            # uninstall
dnf list installed               # list installed
dnf search <query>               # search
```

### apt

Debian package manager for Debian family distributions.

| Field       | Match                                                                 |
| ----------- | --------------------------------------------------------------------- |
| os          | `Linux`                                                               |
| distro      | `debian`, `ubuntu`, `linuxmint`, `pop`, `elementary`, `zorin`, `kali` |
| distro_like | `debian`, `ubuntu`                                                    |
| cmd_exists  | `apt`                                                                 |

System-wide only (requires `sudo`).

```sh
sudo apt install -y <pkg>             # install
sudo apt install -y <pkg>=<version>   # specific version
sudo apt remove -y <pkg>              # uninstall
apt list --installed                   # list installed
apt search <query>                     # search
```

### apk

Alpine Package Keeper for Alpine Linux and musl-based systems.

| Field      | Match    |
| ---------- | -------- |
| os         | `Linux`  |
| distro     | `alpine` |
| cmd_exists | `apk`    |

System-wide only (requires `sudo` outside containers).

```sh
apk add <pkg>                   # install
apk add <pkg>=<version>         # specific version
apk del <pkg>                   # uninstall
apk list --installed            # list installed
apk search <query>              # search
```

### pacman

Arch Linux package manager.

| Field       | Match                                      |
| ----------- | ------------------------------------------ |
| os          | `Linux`                                    |
| distro      | `arch`, `manjaro`, `endeavouros`, `garuda` |
| distro_like | `arch`                                     |
| cmd_exists  | `pacman`                                   |

System-wide only (requires `sudo`).

```sh
sudo pacman -S --noconfirm <pkg>          # install
sudo pacman -S --noconfirm <pkg>=<ver>    # specific version
sudo pacman -R --noconfirm <pkg>          # uninstall
pacman -Q                                 # list installed
pacman -Ss <query>                        # search
```

### snap

Snapcraft package manager, available on many Linux distributions.

| Field      | Match   |
| ---------- | ------- |
| os         | `Linux` |
| cmd_exists | `snap`  |

System-wide only (requires `sudo`).

```sh
sudo snap install <pkg>                       # install
sudo snap install <pkg> --channel=<ver>/stable # specific version
sudo snap remove <pkg>                        # uninstall
snap list                                      # list installed
snap find <query>                              # search
```

### nix

Nix package manager. Cross-platform but primarily Linux and macOS.

| Field      | Match             |
| ---------- | ----------------- |
| os         | `Linux`, `Darwin` |
| distro     | `nixos`           |
| cmd_exists | `nix-env`         |

User-level by default (`~/.nix-profile`). System-wide via `nixos-rebuild` on NixOS.

```sh
nix-env -iA nixpkgs.<pkg>       # install (user)
nix-env -iA nixpkgs.<pkg>-<ver> # specific version
nix-env -e <pkg>                 # uninstall
nix-env -q --installed           # list installed
nix search nixpkgs <query>       # search
```

### pacstall

AUR-like package manager for Debian/Ubuntu systems.

| Field       | Match              |
| ----------- | ------------------ |
| os          | `Linux`            |
| distro      | `debian`, `ubuntu` |
| distro_like | `debian`, `ubuntu` |
| cmd_exists  | `pacstall`         |

System-wide only (requires `sudo`).

```sh
sudo pacstall -I <pkg>           # install
sudo pacstall -R <pkg>           # uninstall
pacstall -L                      # list installed
pacstall -S <query>              # search
```

---

## macOS Package Managers

### brew

Homebrew. The dominant macOS package manager; also available on Linux.

| Field      | Match             |
| ---------- | ----------------- |
| os         | `Darwin`, `Linux` |
| cmd_exists | `brew`            |

User-level by default (installs to Homebrew prefix, no `sudo`).

```sh
brew install <pkg>               # install
brew install <pkg>@<version>     # specific version
brew uninstall <pkg>             # uninstall
brew list                        # list installed
brew search <query>              # search
```

### port

MacPorts. macOS only.

| Field      | Match    |
| ---------- | -------- |
| os         | `Darwin` |
| cmd_exists | `port`   |

System-wide only (requires `sudo`).

```sh
sudo port install <pkg>          # install
sudo port install <pkg> @<version> # specific version
sudo port uninstall <pkg>        # uninstall
port installed                   # list installed
port search <query>              # search
```

---

## Windows Package Managers

### winget

Windows Package Manager (built into Windows 10+).

| Field      | Match        |
| ---------- | ------------ |
| os         | `Windows_NT` |
| cmd_exists | `winget`     |

User-level by default. Use `--scope machine` for system-wide (requires admin).

```sh
winget install <pkg>                 # install (user)
winget install <pkg> --scope machine # install (system)
winget install <pkg> --version <ver> # specific version
winget uninstall <pkg>               # uninstall
winget list                          # list installed
winget search <query>                # search
```

### choco

Chocolatey package manager for Windows.

| Field      | Match        |
| ---------- | ------------ |
| os         | `Windows_NT` |
| cmd_exists | `choco`      |

System-wide by default (requires admin shell).

```sh
choco install <pkg> -y               # install
choco install <pkg> --version <ver> -y # specific version
choco uninstall <pkg> -y             # uninstall
choco list                           # list installed
choco search <query>                 # search
```

### scoop

Scoop package manager for Windows (user-level installs).

| Field      | Match        |
| ---------- | ------------ |
| os         | `Windows_NT` |
| cmd_exists | `scoop`      |

User-level by default. Use `sudo scoop install -g <pkg>` for system-wide (requires admin).

```sh
scoop install <pkg>              # install (user)
scoop install <pkg>@<version>    # specific version
scoop uninstall <pkg>            # uninstall
scoop list                       # list installed
scoop search <query>             # search
```

---

## Cross-Platform Package Managers

### npm

Node.js package manager. Works anywhere Node.js is installed.

| Field      | Match                                      |
| ---------- | ------------------------------------------ |
| os         | `Linux`, `Darwin`, `FreeBSD`, `Windows_NT` |
| cmd_exists | `npm`                                      |

User-level when installed via nvm/fnm. System-wide if Node was installed via OS package manager (may need `sudo`).

```sh
npm install -g <pkg>             # install
npm install -g <pkg>@<version>   # specific version
npm uninstall -g <pkg>           # uninstall
npm ls -g                        # list installed
npm search <query>               # search
```

### pip

Python package manager. Works anywhere Python is installed.

| Field      | Match                                      |
| ---------- | ------------------------------------------ |
| os         | `Linux`, `Darwin`, `FreeBSD`, `Windows_NT` |
| cmd_exists | `pip3` or `pip`                            |

User-level with `--user`. System-wide without it (may need `sudo`). Prefer `--user` or a virtualenv.

```sh
pip install --user <pkg>         # install (user)
pip install <pkg>                # install (system, may need sudo)
pip install <pkg>==<version>     # specific version
pip uninstall -y <pkg>           # uninstall
pip list                         # list installed
pip index versions <pkg>         # search versions
```

### mise

Cross-platform polyglot tool version manager.

| Field      | Match                                      |
| ---------- | ------------------------------------------ |
| os         | `Linux`, `Darwin`, `FreeBSD`, `Windows_NT` |
| cmd_exists | `mise`                                     |

User-level by default (`~/.local/share/mise`).

```sh
mise use -g <pkg>                # install
mise install <pkg>@<version>     # specific version
mise uninstall <pkg>@<version>   # uninstall
mise ls                          # list installed
mise ls-remote <pkg>             # search versions
```

### go

Go module installer. Installs Go-based CLI tools to `$GOPATH/bin` (or `$GOBIN`).

| Field      | Match                                      |
| ---------- | ------------------------------------------ |
| os         | `Linux`, `Darwin`, `FreeBSD`, `Windows_NT` |
| cmd_exists | `go`                                       |

User-level by default (`$GOPATH/bin` or `$GOBIN`).

```sh
go install <module>@latest           # install latest
go install <module>@v<version>       # specific version
rm "$(which <binary>)"               # uninstall (manual)
ls "$(go env GOPATH)/bin"            # list installed
go search <query>                    # search (Go 1.24+)
```

### cargo

Rust package installer. Compiles and installs binaries from crates.io to `$CARGO_HOME/bin`.

| Field      | Match                                      |
| ---------- | ------------------------------------------ |
| os         | `Linux`, `Darwin`, `FreeBSD`, `Windows_NT` |
| cmd_exists | `cargo`                                    |

User-level by default (`$CARGO_HOME/bin`).

```sh
cargo install <crate>                # install latest
cargo install <crate> --version <ver> # specific version
cargo uninstall <crate>              # uninstall
cargo install --list                 # list installed
cargo search <query>                 # search
```

### pkgx

Cross-platform package runner (macOS, Linux).

| Field      | Match             |
| ---------- | ----------------- |
| os         | `Linux`, `Darwin` |
| cmd_exists | `pkgx`            |

User-level by default (`~/.pkgx`).

```sh
pkgx install <pkg>              # install
pkgx uninstall <pkg>            # uninstall
pkgx list                       # list installed
pkgx search <query>             # search
```

---

## FreeBSD Package Manager

### pkg

FreeBSD binary package manager.

| Field      | Match     |
| ---------- | --------- |
| os         | `FreeBSD` |
| cmd_exists | `pkg`     |

System-wide only (requires `sudo` or root).

```sh
sudo pkg install -y <pkg>             # install
sudo pkg install -y <pkg>-<version>   # specific version
sudo pkg delete -y <pkg>              # uninstall
pkg info                               # list installed
pkg search <query>                     # search
```

---

## Package Manager Selection

When multiple package managers are available, **ask the user** which one they want to use. Present
the detected options and let them choose. Do not assume a default.

The user may prefer `npm` over `apt`, or `mise` over `brew`, depending on their workflow.
