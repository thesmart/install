# Package Installer Agent Skill

![context: 1.3k tokens](https://img.shields.io/badge/context-1.3k_tokens-blue)

A skill for selecting and operating the best package managers for the user's environment. Handles
searching, installing, updating, and removing packages.

## Features

- Automatic platform detection (OS, distro, arch, WSL, shell)
- Discovers available package managers on the system
- Install, uninstall, search, list, and version-pin packages
- User-level vs system-level scope awareness

## Supported Package Managers

| Manager  | Platforms                       |
| -------- | ------------------------------- |
| apt      | Debian, Ubuntu, Mint, Pop, Kali |
| dnf      | Fedora, RHEL, CentOS, Rocky     |
| apk      | Alpine Linux                    |
| pacman   | Arch, Manjaro, EndeavourOS      |
| snap     | Linux (most distros)            |
| nix      | Linux, macOS                    |
| pacstall | Debian, Ubuntu                  |
| brew     | macOS, Linux                    |
| port     | macOS                           |
| winget   | Windows 10+                     |
| choco    | Windows                         |
| scoop    | Windows                         |
| npm      | cross-platform                  |
| pip      | cross-platform                  |
| mise     | cross-platform                  |
| go       | cross-platform                  |
| cargo    | cross-platform                  |
| pkgx     | macOS, Linux                    |
| pkg      | FreeBSD                         |

---

## Installation

### Vercel Skills CLI

```sh
npx skills add thesmart/install
```

### Manual

Clone into your Claude Code skills directory:

```sh
git clone https://github.com/thesmart/install.git ~/.claude/skills/install
```

---

## Development Dependencies

- [Node.js / npx](https://nodejs.org/) — used for formatting (prettier)
- [yq](https://github.com/mikefarah/yq#install) — used for YAML frontmatter updates in SKILL.md

### Agent Skill Dependencies

- [shellcraft](https://github.com/thesmart/shellcraft) — portable POSIX shell script authoring
- [skill-creator](https://github.com/anthropics/skills) — skill creation, evaluation, and
  optimization

---

## License Terms

This software is licensed under the [PolyForm Internal Use License 1.0.0](./LICENSE).

Informal license summary:

- **Internal use only**: Use and modify freely within your organization.
- **No distribution**: You cannot redistribute outside your organization, no sublicensing.
- **No warranty**: Provided "as is" with no liability.
