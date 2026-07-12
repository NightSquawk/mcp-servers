# {{PRODUCT}} MCP Server

<!-- Copy everything below the divider into the server repo's README.md and replace {{PLACEHOLDERS}}. Rules and section rationale: README-STANDARD.md -->

---

# {{PRODUCT}} MCP Server

[![npm version](https://img.shields.io/npm/v/@nightsquawktech/{{REPO}})](https://www.npmjs.com/package/@nightsquawktech/{{REPO}})
[![npm downloads](https://img.shields.io/npm/dm/@nightsquawktech/{{REPO}})](https://www.npmjs.com/package/@nightsquawktech/{{REPO}})
[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/NightSquawk/{{REPO}}/badge)](https://scorecard.dev/viewer/?uri=github.com/NightSquawk/{{REPO}})
[![License: AGPL-3.0](https://img.shields.io/badge/license-AGPL--3.0-blue)](https://github.com/NightSquawk/{{REPO}}/blob/v1.0.0/LICENSE)
[![Node](https://img.shields.io/node/v/@nightsquawktech/{{REPO}})](https://nodejs.org)

An MCP (Model Context Protocol) server for **{{PRODUCT}}**, connecting {{WHAT_IT_CONNECTS_TO}} to Claude Desktop, Claude Code, Cursor, and any MCP client. {{HEADLINE_NUMBER_SENTENCE, e.g. "Covers all 993 API endpoints behind 6 catalog-backed tools."}} {{DIFFERENTIATOR_SENTENCE, e.g. "Reads execute by default; writes are blocked unless explicitly enabled."}}

- {{QUANTIFIED_FEATURE_1}}
- {{QUANTIFIED_FEATURE_2}}
- {{QUANTIFIED_FEATURE_3}}
- **Read-only by default**: writes require {{WRITE_GATE_ENV}} plus per-call confirmation
- Runs over stdio via `npx`, no install step

## Quick start

Add the block below to your MCP client config. The JSON is identical for every client; only the file location differs.

### Claude Code

`.mcp.json` in your project root:

```json
{
  "mcpServers": {
    "{{SERVER_KEY}}": {
      "command": "npx",
      "args": ["-y", "@nightsquawktech/{{REPO}}"],
      "env": {
        "{{ENV_VAR_1}}": "{{EXAMPLE_VALUE}}",
        "{{ENV_VAR_2}}": "{{EXAMPLE_VALUE}}"
      }
    }
  }
}
```

### Claude Desktop

Same block in `claude_desktop_config.json` (Settings > Developer > Edit Config).

### Cursor

Same block in `.cursor/mcp.json`.

## Tools

| Tool | Purpose |
|---|---|
| `{{TOOL_1}}` | {{WHAT_IT_DOES}} |
| `{{TOOL_2}}` | {{WHAT_IT_DOES}} |
| `{{TOOL_3}}` | {{WHAT_IT_DOES}} |

<!-- Catalog-backed servers: add one paragraph explaining discover/describe/call and link mcp-core. -->

## Configuration

| Variable | Required | Default | Purpose |
|---|---|---|---|
| `{{ENV_VAR_1}}` | yes | | {{PURPOSE}} |
| `{{ENV_VAR_2}}` | yes | | {{PURPOSE}} |
| `{{WRITE_GATE_ENV}}` | no | `false` | Enables write operations |

## Security & write safety

{{PRODUCT}} credentials: {{LEAST_PRIVILEGE_SETUP, e.g. "create a dedicated API token with read scope; see below"}}.

- All write operations are **disabled by default**. Set `{{WRITE_GATE_ENV}}=true` to enable them.
- Destructive operations additionally require `confirm: true` on the individual call.
- {{ANY_OTHER_GUARDRAIL, e.g. backups before mutation, rate limits}}

## How it works

{{ARCHITECTURE_PARAGRAPH: catalog generation, schema source, determinism. 3-6 sentences, link out for depth.}}

Shared runtime: [`@nightsquawktech/mcp-core`](https://github.com/NightSquawk/mcp-core).

## Example prompts

- "{{REALISTIC_PROMPT_1}}"
- "{{REALISTIC_PROMPT_2}}"
- "{{REALISTIC_PROMPT_3}}"

## Development

```bash
git clone https://github.com/NightSquawk/{{REPO}}.git
cd {{REPO}}
npm install
npm run build
```

{{CATALOG_REGEN_INSTRUCTIONS_IF_APPLICABLE}}

Branches: `v1.0.0` is the stable default branch; all work lands on `develop` first. PRs target `develop`.

## Related servers

Part of the [NightSquawk MCP server family](https://github.com/NightSquawk/mcp-servers): [{{SIBLING_1}}](https://github.com/NightSquawk/{{SIBLING_1}}), [{{SIBLING_2}}](https://github.com/NightSquawk/{{SIBLING_2}}), and more.

## License

AGPL-3.0: free for personal and open-source use. Organizations that cannot comply with the AGPL can purchase a commercial license, and hosted/managed versions are available. See [COMMERCIAL.md](https://github.com/NightSquawk/{{REPO}}/blob/v1.0.0/COMMERCIAL.md) or contact hello@nightsquawk.tech.

---

Built and production-used by [NightSquawk Tech](https://nightsquawk.tech), an MSP/MSSP. We run these servers against our own infrastructure before publishing them.
