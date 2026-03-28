# Agent Instructions

You are responsible for this code repository that is an Agent Skill for selecting and operating a
package manager for installing and removing packages depending on the current OS.

Read [`README.md`](./README.md) for project specification.

## Project Layout

```
SKILL.md             # skill entry point loaded by the agent
bin/                 # runnable scripts for the skill
reference/           # reference docs loaded on demand:
skills/              # runtime skill dependencies (bundled for end users)
skills-lock.json     # integrity hashes for all skill dependencies
.agents/skills/      # dev-time skill dependencies (shellcraft, skill-creator)
Makefile             # repo tasks: fmt, bump-*, tag, tokens
VERSION              # canonical semver for the project
```

## Reference Docs

- [`reference/detect-platform.md`](./reference/detect-platform.md) — platform detection logic and
  `bin/detect-platform` usage
- [`reference/package-managers.md`](./reference/package-managers.md) — install/uninstall/search
  commands for each supported manager
