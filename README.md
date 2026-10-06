# Hostilo MCP server

Publish and update websites from your AI chat. [Hostilo](https://hostilo.app/?utm_source=github&utm_medium=readme) is hosting for AI-generated HTML: ask Claude, ChatGPT, Cursor or any MCP client to create a site, publish new HTML or roll back a change, and it goes live at `https://<name>.hostilo.app` in seconds.

This is a **remote MCP server**. There is nothing to install or run: connect your client to the URL below and sign in to Hostilo.

```
https://hostilo.app/mcp
```

- Transport: Streamable HTTP
- Authentication: OAuth 2.1 with PKCE (S256) and dynamic client registration. No API key.
- Docs: https://hostilo.app/agents#mcp
- Step-by-step guide: https://hostilo.app/blog/publish-website-from-claude-mcp-connector

## Connect

**Claude (claude.ai, desktop):** Settings → Connectors → Add custom connector → paste `https://hostilo.app/mcp` → Connect, then sign in.

**Claude Code:**

```bash
claude mcp add --transport http hostilo https://hostilo.app/mcp
```

**Cursor, Windsurf, VS Code and other clients (`mcp.json`):**

```json
{
  "mcpServers": {
    "hostilo": { "url": "https://hostilo.app/mcp" }
  }
}
```

## Tools

| Tool | What it does | Read-only |
|---|---|---|
| `list_sites` | Lists your websites with live URLs, custom domains and last update time (paginated) | yes |
| `get_site` | Returns the current HTML of a site (up to 1 MB) | yes |
| `create_site` | Creates a new website at `https://<name>.hostilo.app`, optionally with its HTML | no |
| `update_site` | Publishes new HTML; the previous version is kept in history | no |
| `list_versions` | Lists up to 10 previous versions of a site | yes |
| `restore_version` | Restores a previous version (the current one is saved first, so it can be undone) | no |

## Example prompts

- "Build a one-page site for my bakery and publish it on Hostilo as `sweet-crumbs`."
- "Change the headline on my portfolio site to 'Product designer in Lisbon'."
- "Undo the last change on my landing page."

## Safety

- You choose permissions on a consent screen; the assistant sees only the tools you allowed.
- There is no delete tool, and every publish keeps the previous version.
- Site HTML is returned as data, never as instructions.
- Connections can be revoked at any time in the Hostilo dashboard (API & tools → AI connections).

## Plans

Free plan with 5 sites on `name.hostilo.app` and HTTPS, no credit card. PRO ($29/year) adds custom domains and 20 sites.

## Support

hello@hostilo.app · [Privacy](https://hostilo.app/privacy) · [Terms](https://hostilo.app/terms)
