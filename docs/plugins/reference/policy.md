---
summary: "Adds policy-backed doctor checks for workspace conformance."
read_when:
  - You are installing, configuring, or auditing the policy plugin
title: "Policy plugin reference"
---

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

Adds policy-backed doctor checks for workspace conformance.

## Distribution

- Package: `@openclaw/policy`
- Install route: included in OpenClaw

## Surface

- CLI commands: `openclaw policy`

<!-- openclaw-plugin-reference:manual-start -->

## Behavior

The Policy plugin contributes doctor health checks for policy-managed OpenClaw
settings and governed workspace declarations. Policy covers these areas:

- Channel conformance
- Governed tool metadata
- MCP server posture
- Model-provider posture
- Private-network access posture
- Gateway exposure posture
- Agent workspace and tool posture
- Configured global and per-agent tool posture
- Configured sandbox runtime posture
- Ingress and channel access posture
- Data-handling posture
- OpenClaw config secret provider and auth profile posture

Policy stores authored requirements in `policy.jsonc`, observes existing
OpenClaw settings and workspace declarations as evidence, and reports drift
through `openclaw policy check` and `openclaw doctor --lint`. A clean policy
check emits policy, evidence, findings, and attestation hashes that operators
can record for audit.

### Scopes

`openclaw policy check`, `watch`, and workspace-relative `compare` accept
`--agent <id>`. Explicit multi-agent fleets must select the workspace owner.
The plugin does not infer one from roster order.

Named policy scopes under `scopes.<scopeName>` can add stricter normal policy
sections for the selector they list.

- `agentIds` supports `tools`, `agents.workspace`, `sandbox`,
  `dataHandling.memory`, and `execApprovals`.
- `channelIds` supports `ingress.channels`.

Policy checks runtime agent ids that `agents.entries.*` does not list against
inherited global and default posture. Those ids never pass silently with no
evidence. Every scope present in `policy.jsonc` must be valid and enforceable
for its selector. Overlay rules are additional claims, so they do not weaken
top-level policy. One overlay rule can produce its own finding when the same
observed config violates both scopes.

### Compare

`openclaw policy compare --baseline <file>` compares one policy file to another
policy file. It is config-level conformance only. It uses policy rule metadata
to check that the checked policy is not missing or weaker than the authored
baseline. It does not inspect runtime state, credentials, or secret values.

### Posture rules

Tool posture rules can require approved profiles, workspace-only filesystem
tools, bounded exec security/ask/host settings, disabled elevated mode, exact
`alsoAllow` entries, and required tool deny entries. The evidence records
additive `alsoAllow` entries because they can widen effective tool posture.
These checks observe config conformance only. They do not read runtime approval
state or add runtime enforcement.

Sandbox posture rules can require approved sandbox modes/backends, deny host
container networking, deny container namespace joins, require read-only container
mounts, deny container runtime socket mounts and unconfined container profiles,
and require sandbox browser CDP source ranges.
These checks observe config conformance only. They do not read runtime approval
state, inspect live containers, or add runtime enforcement.

Data-handling rules can require sensitive logging redaction, deny telemetry
content capture, require session retention maintenance, and deny session
transcript memory indexing. These checks observe config conformance only. They
do not inspect raw logs, telemetry exports, transcripts, memory files, secrets,
or personal data.

<!-- openclaw-plugin-reference:manual-end -->

## Related docs

- [policy](/cli/policy)
