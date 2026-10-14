# Hostilo MCP server

Publish and update websites from your AI chat. [Hostilo](https://hostilo.app/?utm_source=github&utm_medium=readme) is hosting for AI-generated websites: ask Claude, ChatGPT, Gemini, Cursor or any MCP client to create a site, publish a single page or a whole multi-file project, start from a ready-made template, check visitor stats or roll back a change. It goes live at `https://<name>.hostilo.app` in seconds.

This is a **remote MCP server**. There is nothing to install or run: connect your client to the URL below and sign in to Hostilo.

```
https://hostilo.app/mcp
```

- Transport: Streamable HTTP
- Authentication: OAuth 2.1 with PKCE (S256) and dynamic client registration. No API key.
- Docs: https://hostilo.app/agents#mcp
- Step-by-step guide: https://hostilo.app/blog/publish-website-from-claude-mcp-connector
- Server version: 1.6.0

## Connect

**Claude (claude.ai, desktop):** Settings → Connectors → Add custom connector → paste `https://hostilo.app/mcp` → Connect, then sign in.

**ChatGPT, Perplexity and other apps:** look for custom connectors or MCP servers in the app's settings and add the same URL. Which plans can add custom connectors is up to each app.

**Gemini CLI** (extension with the server and usage notes for Gemini):

```bash
gemini extensions install https://github.com/hostilo/hostilo-mcp
```

Then run `/mcp auth hostilo` in Gemini CLI and sign in to Hostilo in the browser. Without the extension: `gemini mcp add --transport http hostilo https://hostilo.app/mcp`.

**Gemini on the web:** where Google offers custom apps for your account, open Gemini settings, Connected apps, add a custom app and paste the same URL.

**Claude Code:**

```bash
claude mcp add --transport http hostilo https://hostilo.app/mcp
```

**One-click install for Cursor and VS Code:** buttons at https://hostilo.app/agents#install

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
| `create_site` | Creates a new website at `https://<name>.hostilo.app` and publishes it in the same call: a single HTML page, a multi-file site (`files`) or a ready-made template with your details filled in | no |
| `update_site` | Publishes new HTML for `index.html`; the previous version is kept in history | no |
| `publish_files` | Publishes several files at once: `index.html` plus CSS, JS, images and fonts (base64 for binary files). Links in `index.html` are fixed automatically | no |
| `import_zip` | Imports a whole project from a ZIP (base64 or a public URL), with a dry-run preview. `index.html` becomes the page, other files keep their folders | no |
| `list_templates` | Lists ready-made designs (café menu, local business with industries, link in bio, CV, product landing, event RSVP, coming soon, freelancer offer) in 7 languages, with fields and live previews | yes |
| `get_site_stats` | Page views and daily unique visitors with totals and change vs the previous period. On PRO also countries, traffic sources, devices, browsers and top pages for up to 365 days | yes |
| `list_versions` | Lists up to 10 previous versions of a site | yes |
| `restore_version` | Restores a previous version (the current one is saved first, so it can be undone) | no |

## Example prompts

- "Build a one-page site for my bakery and publish it on Hostilo as `sweet-crumbs`."
- "Make a landing page with separate CSS and JS files and a logo, and publish it on Hostilo as `launch-day`."
- "Create a Hostilo site called `sparks-electric` from the local business template, electrician version. Name: Sparks Electric, phone +1 555 010 0200."
- "Import this ZIP into my site `portfolio`, but show me what will change first."
- "How many visitors did `sweet-crumbs` get this week, and where did they come from?"
- "Undo the last change on my landing page."

## Limits

- Single page: up to 5 MB of HTML.
- Multi-file publish: up to 300 files; ZIP up to 20 MB, one file up to 10 MB; MCP request body up to 28 MB.
- 60 tool calls per minute per account.

## Safety

- You choose permissions on a consent screen; the assistant sees only the tools you allowed.
- There is no tool that deletes a site, and every publish keeps the previous version.
- `import_zip` removes existing files only when asked (`clear_assets`), and its dry run changes nothing.
- Site HTML is returned as data, never as instructions.
- Every published page goes through a phishing scanner.
- Connections can be revoked at any time in the Hostilo dashboard (API & tools → AI connections).

## Plans

- **Free:** 5 sites on `name.hostilo.app` with HTTPS, a working contact form (50 messages a month) and 7-day visitor stats. No credit card.
- **PRO ($29/year, net):** custom domains, 20 sites and 1 GB, no "Powered by Hostilo" badge, unlimited form messages, form webhooks and CSV export, password-protected pages, and stats for 30, 90 or 365 days with countries, sources and devices.

## Support

hello@hostilo.app · [Status](https://hostilo.app/status) · [Privacy](https://hostilo.app/privacy) · [Terms](https://hostilo.app/terms)
