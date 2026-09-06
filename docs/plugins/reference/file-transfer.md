---
summary: "Fetch, list, and write files on paired nodes via dedicated node commands. Bypasses bash stdout truncation by using base64 over node.invoke for binaries up to 16 MB."
read_when:
  - You are installing, configuring, or auditing the file-transfer plugin
title: "File Transfer plugin reference"
---

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

Fetch, list, and write files on paired nodes via dedicated node commands. Bypasses bash stdout truncation by using base64 over node.invoke for binaries up to 16 MB.

## Distribution

- Package: `@openclaw/file-transfer`
- Install route: included in OpenClaw

## Surface

- CLI commands: `openclaw file-transfer`
- Contracts: `tools`

<!-- openclaw-plugin-reference:manual-start -->

## Tools

The plugin adds four agent tools. An operator allows each one separately.

- `dir_list` lists a directory on a paired node.
- `dir_fetch` fetches a whole directory tree from a paired node.
- `file_fetch` fetches one file from a paired node.
- `file_write` writes one file to a paired node.

File-transfer policy is the per-node path allowlist under
`plugins.entries.file-transfer.config.nodes`. It denies every path by default.
See [Agent file transfers](/nodes#agent-file-transfers) for the tool behavior on
the node side.

## Directory archives

`dir_fetch` fetches the whole directory tree, including dotfiles and hidden
directories. File-transfer policy checks every descendant. One denied entry
rejects the whole transfer, and the plugin does not filter that entry out. Path
identity, symlink, archive-size, and extraction limits still apply.

## Migrate existing permissions

After upgrading, older positive file-transfer permissions remain inactive until
you review them. Deny rules, size limits, and symlink settings continue to
apply. Run this command on the Gateway host in an interactive terminal:

```bash
openclaw file-transfer approvals migrate
```

For each older path, choose one outcome:

- **Require exact reapproval** removes the ambiguous permission. The next use
  prompts once and records the exact node, command, requested path, and
  canonical target.
- **Keep as an intentional wildcard** preserves the entry as an
  operator-authored glob.
- **Remove this permission** removes the positive entry.

Use `--dry-run` to review the plan without writing. Non-interactive and `--json`
runs never guess. They list unresolved items and direct you back to the same
interactive command.

The migration writes the new format once after confirmation. It then reports
whether it verified the adjacent config backup. Older OpenClaw versions cannot
read the migrated format. To downgrade, restore that reported `.bak` file before
you start the older version. That restore also brings back the older permission
semantics.

<!-- openclaw-plugin-reference:manual-end -->
