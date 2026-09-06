---
summary: "Anthropic models, Claude CLI, and native Claude session catalog."
read_when:
  - You are installing, configuring, or auditing the anthropic plugin
title: "Anthropic plugin reference"
---

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

Anthropic models, Claude CLI, and native Claude session catalog.

## Distribution

- Package: `@openclaw/anthropic-provider`
- Install route: included in OpenClaw

## Surface

- Providers: `anthropic`
- Contracts: `mediaUnderstandingProviders`, `usageProviders`

<!-- openclaw-plugin-reference:manual-start -->

## Native session catalog

The plugin discovers Claude CLI and Claude Desktop sessions on the Gateway and
on paired nodes. A paired node advertises these node commands:

- `anthropic.claude.sessions.list.v1` lists the native sessions on that host.
- `anthropic.claude.sessions.read.v1` reads one native session transcript.
- `anthropic.claude.terminal.resume.v1` opens `claude --resume <session-id>` in
  the operator terminal on the owning host.

OpenClaw enables the catalog by default. Set
`plugins.entries.anthropic.config.sessionCatalog.enabled: false` to turn off the
operator catalog and the paired-node catalog commands. That setting leaves
Anthropic models and the Claude CLI backend in place.

<!-- openclaw-plugin-reference:manual-end -->

## Related docs

- [anthropic](/providers/anthropic)
