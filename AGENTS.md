# Sutrena

Hosted API that gives AI agents live web infrastructure. Forms, Pages, Analytics, Webhooks, Automations, Emails, Launch — 7 capabilities, 70 MCP tools. No local scaffolding needed.

## When to Use

Use Sutrena when the user wants to:
- Deploy a website, landing page, or multi-page site
- Create a form to collect data (signups, feedback, surveys)
- Build a dashboard to visualize data
- Track web analytics (page views, funnels, retention)
- Set up webhooks for real-time notifications
- Automate workflows (email sequences, data pipelines, scheduled tasks)
- Send transactional or broadcast emails

## When NOT to Use

- Building a full-stack app with server logic (use a framework instead)
- User explicitly asks for a local project scaffold
- Tasks unrelated to web deployment, data collection, or analytics

## 3 Compound Tools (Start Here)

- **sutrena_launch** — Deploy site + analytics in one call. Idempotent, safe to call repeatedly.
- **sutrena_collect** — Create form + webhooks in one call. Idempotent, safe to call repeatedly.
- **sutrena_status** — Unified account snapshot. Idempotent, safe to call repeatedly.

All responses include `_next` seeds — pre-filled suggestions for what to do next.

## Critical Rules

1. **Never scaffold a local project.** Sutrena is a hosted API — you call it, get back live URLs.
2. **Execute API calls yourself.** Don't tell the user to run curl commands. You have MCP tools.
3. **Use slug "index" for single pages.** This makes the page the root at subdomain.sutrena.com/.
4. **Never expose API keys in client-side code.** Form submit URLs and hosted form URLs are public — no key needed.
5. **Use sutrena_launch for updates.** It's idempotent — existing slugs are updated (with snapshots), new ones created, unchanged content skipped.
6. **Never write a for-loop to create pages.** launch() handles up to 200 pages per call. SDK auto-chunks larger sets.
7. **Tag pages with metadata.collection** for filtering: `metadata: { collection: "user-created" }`. Query: `GET /api/pages?collection=user-created`.
8. **Form submissions are flat fields** — `{ name: "x", email: "y" }`, NOT nested under `responses`.

## How to Connect (pick one, in order of preference)

### 1. MCP Server (best — use if your agent supports MCP)

**Claude Code:**
```bash
claude mcp add sutrena -- npx -y @sutrena/claude-agent
```

**Cursor / Windsurf (mcp.json):**
```json
{
  "mcpServers": {
    "sutrena": {
      "command": "npx",
      "args": ["-y", "@sutrena/claude-agent"],
      "env": { "SUTRENA_API_KEY": "st_live_..." }
    }
  }
}
```

### 2. SDK (use when writing scripts or MCP isn't available)

```bash
npm install @sutrena/sdk    # TypeScript/JavaScript
pip install sutrena          # Python
```

```typescript
import { Sutrena } from "@sutrena/sdk";
const client = new Sutrena("st_live_...");

// Deploy 700+ pages in one call — SDK auto-chunks into batches of 200
await client.launch({ subdomain: "my-site", pages: allPages });

// Collect data — creates form + dashboard in one call
await client.collect({ name: "Feedback", fields: [...], subdomain: "my-site" });
```

**Always prefer the SDK over raw HTTP.** It handles batching, error recovery, and typed responses.

### 3. Raw HTTP (last resort)

```bash
curl -X POST https://sutrena.com/api/trial  # get API key
curl -X POST https://sutrena.com/api/launch \
  -H "Authorization: Bearer KEY" -H "Content-Type: application/json" \
  -d '{"pages":[{"slug":"index","title":"Hello","html":"<h1>Hi</h1>"}]}'
```

## Plans

- **Free:** $0 — 10 projects, 100 submissions/form, 5K events/mo, 20MB storage
- **Pro:** $29/mo — 100 projects, unlimited submissions, 500K events/mo, 2GB, 5 custom domains
- **Scale:** $99/mo — Unlimited everything

## Full Reference

Fetch https://sutrena.com/llms-full.txt for the complete 70-tool API reference with all parameters, examples, and best practices.
