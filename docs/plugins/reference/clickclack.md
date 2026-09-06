---
summary: "OpenClaw ClickClack channel plugin."
read_when:
  - You are installing, configuring, or auditing the clickclack plugin
title: "Clickclack plugin reference"
---

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

OpenClaw ClickClack channel plugin.

## Distribution

- Package: `@openclaw/clickclack`
- Install route: npm or ClawHub: `clawhub:@openclaw/clickclack`

## Surface

- Channels: `clickclack`
- Contracts: `tools`

<!-- openclaw-plugin-reference:manual-start -->

The plugin can optionally create a lifecycle-synchronized ClickClack channel
for each OpenClaw session. A managed discussion channel runs a side session
under the same agent id as the attached main session. The side agent observes
the main session with `sessions_history` and `session_status`. It uses
`sessions_send` only when people in the discussion ask it to relay or steer the
main session.

The attached main session receives a `discussion` tool. That tool reads the
latest messages and recent thread replies. It has no write or lifecycle side
effects. See
[ClickClack session discussions](/channels/clickclack#session-discussions)
for configuration and session-tool visibility requirements.

<!-- openclaw-plugin-reference:manual-end -->

## Related docs

- [clickclack](/channels/clickclack)
