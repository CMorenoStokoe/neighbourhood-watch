# GitHub Copilot instructions for neighbourhood-watch

**Purpose**: give AI agents the exact, concise context they need to be productive in this repo — what to run, where logic lives, and project constraints.

## Quick summary 🧭
- This repo is very small: see `README.md` and `mcp.json` at the repo root.
- The project identifies properties that may be part of council benefit fraud.
- Most runtime behavior is provided by an external MCP server package invoked from `mcp.json` (`@openbnb/mcp-server-airbnb`).

## Key files 🔑
- `mcp.json` — declarative configuration of MCP servers. Example entry:

```json
"mcpServers": {
  "airbnb": {
    "command": "npx",
    "args": ["-y", "@openbnb/mcp-server-airbnb"]
  }
}
```

- `README.md` — project description (short); update it when adding features or higher-level design notes.

## How to run / debug 🚀
- Start the Airbnb MCP server directly (same command used by `mcp.json`):

```
npx -y @openbnb/mcp-server-airbnb
```

- If you need deeper debugging, open the external package's repository or npm page (`@openbnb/mcp-server-airbnb`). The repo contains the server code and runtime-specific options that this project depends on.

- There are no local `src/`, `package.json`, or tests in this repo — behavior is primarily driven by the external MCP server invocation. When you add behavior, prefer adding a local test harness and documentation that explains why changes are needed.

## Project-specific conventions and constraints ⚠️
- Keep `mcp.json` entries in the same `{ "command": ..., "args": [...] }` shape — tooling expects this mapping.
- The repository contains sensitive subject matter (fraud detection). Be careful: do not introduce or commit any real PII or sensitive datasets into the repo.

## When changing behavior or adding features ✍️
- If behavior change is internal to the external server: open an issue or PR against `@openbnb/mcp-server-airbnb` (link from its npm/GitHub page).
- If change is specific to this repo (configuration, orchestration), update `mcp.json` and add a short `docs/` file or a README section explaining the rationale.
- Add minimal, reproducible examples for future agents (how to run the server, expected inputs/outputs, known limitations).

## Notes for AI agents 🤖
- Focus on discoverable facts only — this repo delegates runtime logic to the listed MCP server package, so check that package's docs for implementation detail.
- If asked to implement functionality that requires dataset access or sensitive information, refuse or request anonymized test fixtures.

---
If anything important is missing or unclear here, tell me which area (architecture, run/debug, conventions, or integration points) you want expanded and I’ll iterate. ✅
