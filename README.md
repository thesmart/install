# Package Installer Agent Skill

![context: 1.3k tokens](https://img.shields.io/badge/context-1.3k_tokens-blue)

A skill for selecting and operating the best package managers for the user's environment. Handles
searching, installing, updating, and removing packages.

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
