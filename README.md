# Browser Power for Kiro

A [Kiro](https://kiro.dev) power that provides browser automation capabilities via Playwright MCP.

Navigate pages, click elements, fill forms, take screenshots, and monitor network requests and console messages — all from within the Kiro agent.

## Quick Start

1. Clone this repo
2. In Kiro, open Command Palette → "Powers" → "Add power from Local Path"
3. Select the cloned directory

Or manually copy `POWER.md` and `mcp.json` to `.kiro/powers/browser/` in your workspace.

## What's Included

| File | Purpose |
|------|---------|
| `POWER.md` | Power metadata, keywords, and usage instructions |
| `mcp.json` | MCP server configuration (Playwright + Chrome DevTools) |

## MCP Servers

- **Playwright** (enabled) — Full browser automation via `@playwright/mcp`
- **Chrome DevTools** (disabled) — Alternative via `chrome-devtools-mcp`, enable in `mcp.json` if preferred

## Prerequisites

- [Node.js](https://nodejs.org/) (for `npx`)
- Playwright browsers will be installed automatically on first use

## License

MIT
