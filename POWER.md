---
name: "browser"
displayName: "Browser"
description: "Browser automation. Navigate pages, click elements, fill forms, take screenshots, monitor network requests and console messages."
keywords: ["browser", "navigate", "click", "screenshot", "form", "web", "ui", "page", "tab", "snapshot", "dom", "network", "console"]
---

# Browser

Browser automation power for [Kiro](https://kiro.dev). Provides tools for navigating web pages, interacting with UI elements, taking screenshots, and monitoring network/console activity via Playwright MCP.

## Installation

1. Open Kiro IDE
2. Open the Powers panel (Command Palette → "Powers")
3. Click "Add power from Local Path"
4. Select the cloned directory

Or copy the `POWER.md` and `mcp.json` files into your workspace at `.kiro/powers/browser/`.

## When to Use Browser

Use browser tools when:
- Web search returns insufficient or outdated information
- You need to interact with a web application (forms, buttons, navigation)
- Verifying UI behavior or testing web interfaces
- Fetching content from URLs that web search cannot access

## Session Management

Keep browser open after completing tasks:
- Closing may trigger permission dialogs that block autonomous execution
- User may have other tabs open that would be lost
- Reopening is slower than reusing an existing session

Reuse existing tabs when possible:
- Check for tabs already open on the relevant topic
- Only open new tabs when no related tab exists
- This preserves user context and reduces resource usage

## Best Practices

| Do | Don't |
|----|-------|
| Use `browser_snapshot` for element interaction | Use screenshots for actions |
| Wait for page loads before interacting | Click elements before page is ready |
| Use specific element refs from snapshots | Guess at element selectors |
| Handle dialogs explicitly | Ignore unexpected dialogs |

## JS-Rendered Sites (Use Browser Instead of webFetch)

Many documentation sites render content via JavaScript. The `webFetch` tool only retrieves raw HTML, which returns empty or skeleton content for JS-rendered sites.

When `webFetch` returns empty/skeleton content:
1. Open the URL in the browser (`browser_navigate`)
2. Use `browser_snapshot` to read the rendered page content
3. The browser executes JavaScript and renders the full page

Workflow for documentation lookup:
1. Try `web_search` first to find the right URL
2. If `webFetch` returns skeleton content, switch to browser
3. Navigate to the URL and snapshot the page
4. Extract the information from the snapshot

## Error Recovery

If browser interaction fails:
1. Take a snapshot to understand current page state
2. Check for dialogs, overlays, or loading states
3. Retry with appropriate waits if needed
4. Report the issue if it persists after 2 attempts

## MCP Servers

This power bundles two MCP servers (configured in `mcp.json`):

- **playwright** — Primary browser automation via `@playwright/mcp`. Uses a persistent user data directory (`.playwright-data`) for session reuse. The `browser_close` tool is disabled by default to prevent accidental session loss.
- **chrome-devtools** — Alternative browser automation via `chrome-devtools-mcp`. Disabled by default; enable it in `mcp.json` if you prefer DevTools Protocol over Playwright.

## License

MIT
