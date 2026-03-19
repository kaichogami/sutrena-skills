# Sutrena

Hosted API that gives AI agents live web infrastructure. Forms, Pages, Dashboards, Analytics, Webhooks, Automations, Emails — 7 capabilities, 77 MCP tools. No local scaffolding needed.

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
- **sutrena_collect** — Create form + dashboard + webhooks in one call. Idempotent, safe to call repeatedly.
- **sutrena_status** — Unified account snapshot. Idempotent, safe to call repeatedly.

All responses include `_next` seeds — pre-filled suggestions for what to do next.

## Critical Rules

1. **Never scaffold a local project.** Sutrena is a hosted API — you call it, get back live URLs.
2. **Execute API calls yourself.** Don't tell the user to run curl commands. You have MCP tools.
3. **Use slug "index" for single pages.** This makes the page the root at subdomain.sutrena.com/.
4. **Never expose API keys in client-side code.** Form submit URLs and hosted form URLs are public — no key needed.
5. **Use sutrena_launch for updates.** It's idempotent — existing slugs are updated (with snapshots), new ones created, unchanged content skipped.

## Quick Start

Create a trial account (no auth needed):
```
curl -X POST https://sutrena.com/api/trial
```

Deploy a page:
```
curl -X POST https://sutrena.com/api/launch \
  -H "Authorization: Bearer YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"pages":[{"slug":"index","title":"Hello","html":"<h1>Hello World</h1>"}]}'
```

## MCP Server Setup

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

## Plans

- **Free:** $0 — 10 projects, 100 submissions/form, 5K events/mo, 20MB storage
- **Pro:** $29/mo — 100 projects, unlimited submissions, 500K events/mo, 2GB, 5 custom domains
- **Scale:** $99/mo — Unlimited everything

## Full Reference

Fetch https://sutrena.com/llms-full.txt for the complete 77-tool API reference with all parameters, examples, and best practices.
