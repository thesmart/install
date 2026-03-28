# Reference files

## Keeping `bin/detect-platform` in sync

Whenever a package manager is added, removed, or renamed in
[package-managers.md](./package-managers.md), update `bin/detect-platform` to match:

- Added a new package manager? Add a `_has_cmd <binary> && _add_pm <name>` line in the appropriate
  section (OS-specific `case` branch for native managers, or the cross-platform block after the
  `case`).
- Removed a package manager? Remove its `_has_cmd` line.
- Renamed the `cmd_exists` binary? Update the corresponding `_has_cmd` argument.
