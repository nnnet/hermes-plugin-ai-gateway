# ai-gateway

Hermes model-provider plugin for **Vercel AI Gateway** — routes requests
to multiple LLM backends through Vercel's gateway service with
attribution headers and reasoning config passthrough.

## What it does

Subclasses `ProviderProfile` and forwards requests via the Vercel AI
Gateway endpoint. Adds:

- Attribution headers (gateway-required)
- Full reasoning config passthrough for thinking-capable models

## Configuration

In `~/.hermes/config.yaml`:

```yaml
providers:
  ai-gateway-provider:
    name: AI Gateway
    base_url: https://<your-gateway-host>/v1
    api_key: ${AI_GATEWAY_KEY}
    api_mode: anthropic_messages
    default_model: claude-haiku-4-5
    models:
      - claude-haiku-4-5
      - claude-sonnet-4-6
```

Pick this provider in `model.provider:` or in `fallback_providers[]`.

## Mounting

External plugin: pulled by
[`nnnet/AiManager:infra/hermes/scripts/sync-external-plugins.sh`](https://github.com/nnnet/AiManager/blob/prod/infra/hermes/scripts/sync-external-plugins.sh)
into `sources/hermes-external-plugins/ai-gateway/`, then bind-mounted at
`/opt/data/plugins/model-providers/ai-gateway/`.

## License

MIT — see LICENSE.
