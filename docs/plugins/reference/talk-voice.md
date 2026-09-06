---
summary: "Manage Talk voice selection (list/set)."
read_when:
  - You are installing, configuring, or auditing the talk-voice plugin
title: "Talk Voice plugin reference"
---

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

Manage Talk voice selection (list/set).

## Distribution

- Package: `openclaw`
- Install route: included in OpenClaw

## Surface

- Slash commands: `/voice`

<!-- openclaw-plugin-reference:manual-start -->

## Configure a Talk voice from chat

Set `talk.provider` and configure the matching `talk.providers.<provider>`
entry before you use the command. The active provider must support voice
listing. [Talk](/nodes/talk) documents both config keys.

- `/voice status` shows the active provider and the selected provider-scoped
  voice ID.
- `/voice list [limit]` lists voices from the active provider. The default
  limit is 12. The maximum limit is 50.
- `/voice set <voiceId|name>` resolves a voice by exact ID, exact name, or
  partial name. It then saves the voice to
  `talk.providers.<activeProvider>.voiceId`.

Discord registers the native command as `/talkvoice`. That command takes the
same subcommands and arguments. Status and list are read-only. Setting a voice
requires the message-channel owner or a Gateway client with `operator.admin`.

The command reports failures visibly in chat. Missing Talk configuration names
the required keys. Provider lookup errors include the provider error. Unknown
voices suggest listing the available voices. Unauthorized writes state the
required permission.

## Related docs

- [Talk](/nodes/talk)

<!-- openclaw-plugin-reference:manual-end -->
