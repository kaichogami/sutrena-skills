# sutrena-skills

Agent skills for [Sutrena](https://sutrena.com) — the hosted API that gives AI agents live web infrastructure.

## Install

**Claude Code:**
```bash
# Install the skill (one-time)
npx skills add kaichogami/sutrena-skills -g

# Add MCP server for tool access
claude mcp add sutrena -- npx -y @sutrena/claude-agent
```

**Cursor:**
```bash
npx skills add kaichogami/sutrena-skills -g
```
Then add to `.cursor/mcp.json`:
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

**GitHub Copilot:**
Copy `AGENTS.md` to your repo root, or point Copilot to:
```
https://sutrena.com/api/agent/skill
```

**Windsurf:**
Same as Cursor — add the MCP config to `.windsurf/mcp.json`.

## What's Included

| File | Purpose |
|------|---------|
| `skills/sutrena/SKILL.md` | Thin skill for skills.sh-compatible tools |
| `AGENTS.md` | Universal agent context (GitHub Copilot, etc.) |
| `.cursor/rules/sutrena.mdc` | Cursor rules (alwaysApply) |
| `.github/copilot-instructions.md` | GitHub Copilot instructions |

## Full Reference

For the complete API reference with all 65 tools, parameters, and examples:
- `https://sutrena.com/llms-full.txt`
- `https://sutrena.com/llms.txt` (summary)

## License

Apache-2.0
