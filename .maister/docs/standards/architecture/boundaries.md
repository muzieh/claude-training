# Architecture: System Boundaries

### No backend, no network calls, no telemetry
The app must not make API calls, contact a server, or send analytics. All state is client-side in `localStorage`. There is no backend to add features to.

### Companion to Claude Desktop, not a replacement
The app is a separate browser window opened alongside Claude Desktop. There is no integration, automation, or proxying — the learner reads instructions in one window and executes them in Claude Desktop in the other. Do not add Claude API calls, MCP server hooks, or any cross-window automation.

### Works offline after first load
Once `index.html` and the Tailwind CDN script are cached, the page must work offline. Any new dependency must preserve this property.

**Why this matters**: These boundaries define what the project *is*. Crossing any of them turns a learning aid into a different product.
