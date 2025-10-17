# cf_ai_OwenChen

This repository contains a Cloudflare Agents-based AI application scaffolded from the official starter and customized to use Workers AI (Llama 3.3) with stateful coordination via Durable Objects, a chat UI, and simple memory + scheduling tools.

## Components

- **LLM**: Workers AI model `@cf/meta/llama-3.3-70b-instruct-fp8` (configurable via `WORKERS_AI_MODEL`)
- **Workflow/coordination**: Cloudflare Agents on Durable Objects (`Chat` DO), scheduling via built-in `this.schedule`
- **User input**: React chat UI (Vite), streaming responses
- **Memory/state**: Durable Object-backed agent with persisted messages; tools `rememberNote` and `recallMemories`

## Quick start (local)

```bash
cd agents-starter
npm install
npm run start
```

The UI will check the Workers AI binding automatically. Ensure `wrangler.jsonc` has:

```jsonc
{
  "ai": { "binding": "AI", "remote": true },
  "durable_objects": { "bindings": [{ "name": "Chat", "class_name": "Chat" }] },
  "migrations": [{ "tag": "v1", "new_sqlite_classes": ["Chat"] }]
}
```

## Deploy

```bash
cd agents-starter
npm run deploy
```

## Try it

- Chat normally and ask it to schedule something (e.g., "remind me in 30 seconds to stretch").
- Save memory: "remember this: my favorite color is teal"; then "recall memories".

## Repository requirements

- Name: prefixed with `cf_ai_` (this repo is `cf_ai_OwenChen`)
- Includes this `README.md` and clear instructions

## References

- Cloudflare Agents docs: [`https://developers.cloudflare.com/agents/`](https://developers.cloudflare.com/agents/)
- Cloudflare Agents Starter: [`https://github.com/cloudflare/agents-starter`](https://github.com/cloudflare/agents-starter)
