---
name: install
description: >-
  Detects the user's OS and available package managers, then runs the correct install, uninstall,
  search, or list command. Use this skill whenever the user asks to install, remove, update, or
  search for a package or CLI tool — even if they don't name a specific package manager. Also
  activate when the user says things like "I need ffmpeg", "get me node 20", "remove postgres",
  "what package managers do I have", or "how do I install X on this machine".
license: PolyForm-Internal-Use-1.0.0
compatibility: Bash
metadata:
  author: thesmart
  version: 0.0.1
---

# Package Installer

Install, remove, search, and list packages using whatever package managers are available on the
current system.

## Consent — never install without explicit user intent

Installing or removing a package changes the user's system. Only proceed when the user has clearly
asked for it in the current conversation. Apply this test before running any install or remove
command:

1. **The user named a package and an action.** Statements like "install ffmpeg", "remove postgres",
   or "I need node 20" count. Vague references ("set up my environment", "make it work") do not —
   ask what they want installed.
2. **The intent is recent.** A request from earlier in a long conversation does not carry forward
   indefinitely. If the conversation has moved on to a different topic, confirm again before
   installing.
3. **When in doubt, ask.** A one-line confirmation ("Install ffmpeg with brew?") is cheap; an
   unwanted package on the user's system is not.

Never infer packages to install from project files, lock files, or error messages without asking
first. The user decides what goes on their machine.

## Step 1: Detect the platform

Run the detection script from the skill directory to discover the OS, architecture, and every
package manager on `$PATH`:

```sh
./bin/detect-platform
```

The output is a list of `KEY=value` lines. The important ones:

- `PLATFORM_OS` — `Darwin`, `Linux`, `FreeBSD`, or `Windows_NT`
- `PLATFORM_DISTRO` — Linux distro id (e.g. `ubuntu`, `alpine`, `arch`); empty on non-Linux
- `PLATFORM_PKG_MANAGERS` — space-separated list of available managers, native first

See [reference/detect-platform.md](reference/detect-platform.md) for the full variable reference.

## Step 2: Check if already installed

Before installing anything, check whether the package or its binary is already on the system:

```sh
command -v <binary>          # is it on $PATH?
<binary> --version           # what version is running?
```

- **Already installed, no version requested** — tell the user it's already available and show the
  installed version. Do not reinstall.
- **Already installed, version matches** — same as above. Nothing to do.
- **Already installed, different version requested** — tell the user the current version, confirm
  they want to update or reinstall, then proceed with the version-specific install command from the
  package manager reference.
- **Not installed** — continue to the next step.

## Step 3: Choose a package manager

If only one manager in `PLATFORM_PKG_MANAGERS` can handle the request, use it. When multiple
managers qualify, **ask the user** which one they prefer — do not assume a default. Present the
options briefly so they can pick.

Language-ecosystem packages (npm, pip, cargo, go) should use their ecosystem manager. OS-level
packages should prefer the native OS manager (apt, dnf, brew, etc.) unless the user says otherwise.

## Step 4: Build the command

Look up the exact command syntax in [reference/package-managers.md](reference/package-managers.md).
That file has install, uninstall, search, list, and version-pinning commands for every supported
manager.

## Step 5: Run or instruct

Before executing, check two things:

1. **Consent.** Re-verify against the consent checklist above. The user must have named this
   specific package and action. If the conversation has drifted or you are acting on an indirect
   inference, stop and confirm first.

2. **Privileges.** Some package managers require root or admin access (e.g. `apt`, `dnf`, `apk`,
   `pacman`, `pkg`, `port`, `choco`). If the chosen manager needs `sudo` or elevated privileges,
   **do not run the command yourself**. Instead, give the user the exact command to copy and run:

   > To install ffmpeg, run:
   > ```sh
   > sudo apt install -y ffmpeg
   > ```

   User-scoped managers (brew, scoop, npm, pip, cargo, go, mise, pkgx, snap with `--classic`,
   nix-env) can typically run without elevation — execute these directly when consent is established.

If you do run the command and it fails, read the error output and try to resolve it (e.g. stale
index, wrong package name). For apt, run `sudo apt update` first if the index is stale — but again,
present the sudo command to the user rather than running it.

## Supported managers

**Linux** — apt, dnf, apk, pacman, snap, pacstall, nix, brew
**macOS** — brew, port, nix
**Windows** — winget, choco, scoop
**FreeBSD** — pkg
**Cross-platform** — npm, pip, cargo, go, mise, pkgx
