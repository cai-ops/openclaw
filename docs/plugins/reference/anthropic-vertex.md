---
summary: "OpenClaw Anthropic Vertex provider plugin for Claude models on Google Vertex AI."
read_when:
  - You are installing, configuring, or auditing the anthropic-vertex plugin
title: "Anthropic Vertex plugin reference"
---

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

OpenClaw Anthropic Vertex provider plugin for Claude models on Google Vertex AI.

## Distribution

- Package: `@openclaw/anthropic-vertex-provider`
- Install route: npm or ClawHub

## Surface

- Providers: `anthropic-vertex`

<!-- openclaw-plugin-reference:manual-start -->

## Configure

The plugin reads Google Application Default Credentials from the Gateway
process environment. Set these variables on the Gateway host:

- `GOOGLE_APPLICATION_CREDENTIALS`: path to the credentials JSON file. Without
  it the plugin reads `~/.config/gcloud/application_default_credentials.json`.
  On Windows it reads `%APPDATA%\gcloud\application_default_credentials.json`.
- `ANTHROPIC_VERTEX_PROJECT_ID`: the Google Cloud project id. The plugin also
  accepts `GOOGLE_CLOUD_PROJECT` or `GOOGLE_CLOUD_PROJECT_ID`. Without any of
  them it uses the `project_id` field in the credentials file.
- `GOOGLE_CLOUD_LOCATION`: the Vertex region. The plugin also accepts
  `CLOUD_ML_REGION`. The default region is `global`.
- `ANTHROPIC_VERTEX_USE_GCP_METADATA=1`: read credentials from the GCP metadata
  server instead of a credentials file.

A `baseUrl` on the model entry overrides the region variables. See
[Model providers](/concepts/model-providers) for the model entry schema.

## Claude Fable 5

Use `anthropic-vertex/claude-fable-5` where the model is available in your Google Cloud region.
Fable 5 always uses adaptive thinking and defaults to `high` effort. `/think off` and
`/think minimal` use `low` effort because the model does not support disabling thinking.

The bundled Vertex catalog has no `claude-fable-5-1` entry. The bare `fable`
alias described in [Anthropic](/providers/anthropic) resolves inside the
Anthropic provider, so name the Vertex model ref in full.

## Claude Sonnet 5

Use `anthropic-vertex/claude-sonnet-5` with Vertex's `global`, `us`, or `eu`
endpoint. Sonnet 5 defaults to adaptive thinking at `high` effort and supports
`/think off` or the native `/think xhigh|max` levels. OpenClaw publishes its
1,000,000-token context window and 128,000-token output limit automatically.

Catalog pricing follows [Google's current Vertex pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#anthropics-claude-models):
`$2/$10` per million input/output tokens for `global`, or `$2.20/$11` for
the `us` and `eu` multi-region endpoints. Cache hits and 5-minute cache writes
cost `$0.20/$2.50` globally or `$0.22/$2.75` in either multi-region endpoint,
per million tokens. These USD rates apply at both 200K input tokens or less
and above 200K input tokens.

<!-- openclaw-plugin-reference:manual-end -->
