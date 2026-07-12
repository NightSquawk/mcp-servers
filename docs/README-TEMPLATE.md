# {{PRODUCT}} MCP Server

<!-- Copy everything below the divider into the server repo's README.md and replace {{PLACEHOLDERS}}. Rules and section rationale: README-STANDARD.md -->
<!-- {{CURSOR_B64}} = base64 of {"command":"npx","args":["-y","@nightsquawktech/{{REPO}}"],"env":{...all vars...}} -->
<!-- {{VSCODE_URLENC}} = URL-encoded {"command":"npx","args":["-y","@nightsquawktech/{{REPO}}"],"env":{...all vars...}} -->

---

# {{PRODUCT}} MCP Server

[![npm version](https://img.shields.io/npm/v/@nightsquawktech/{{REPO}})](https://www.npmjs.com/package/@nightsquawktech/{{REPO}})
[![npm downloads](https://img.shields.io/npm/dm/@nightsquawktech/{{REPO}})](https://www.npmjs.com/package/@nightsquawktech/{{REPO}})
[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/NightSquawk/{{REPO}}/badge)](https://scorecard.dev/viewer/?uri=github.com/NightSquawk/{{REPO}})
[![License: AGPL-3.0](https://img.shields.io/badge/license-AGPL--3.0-blue)](https://github.com/NightSquawk/{{REPO}}/blob/v1.0.0/LICENSE)
[![Node](https://img.shields.io/node/v/@nightsquawktech/{{REPO}})](https://nodejs.org)

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name={{SERVER_KEY}}&config={{CURSOR_B64}})
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name={{SERVER_KEY}}&config={{VSCODE_URLENC}})

An MCP (Model Context Protocol) server for **{{PRODUCT}}**, connecting {{WHAT_IT_CONNECTS_TO}} to Claude Desktop, Claude Code, Cursor, and any MCP client. {{HEADLINE_NUMBER_SENTENCE, e.g. "Covers all 993 API endpoints behind 6 catalog-backed tools."}} {{DIFFERENTIATOR_SENTENCE, e.g. "Reads execute by default; writes are blocked unless explicitly enabled."}}

- {{QUANTIFIED_FEATURE_1}}
- {{QUANTIFIED_FEATURE_2}}
- {{QUANTIFIED_FEATURE_3}}
- **Read-only by default**: writes require `{{WRITE_GATE_ENV}}` plus per-call confirmation
- Runs over stdio via `npx`, no install step

## Quick start

The config below lists **every** environment variable the server reads, with recommended values. Delete the optional ones you do not need. The JSON is identical for every client; only the file location differs.

### Claude Code

```bash
claude mcp add {{SERVER_KEY}} \
  --env {{ENV_VAR_1}}={{RECOMMENDED_VALUE}} \
  --env {{ENV_VAR_2}}={{RECOMMENDED_VALUE}} \
  -- npx -y @nightsquawktech/{{REPO}}
```

Or in `.mcp.json` at your project root:

```json
{
  "mcpServers": {
    "{{SERVER_KEY}}": {
      "command": "npx",
      "args": ["-y", "@nightsquawktech/{{REPO}}"],
      "env": {
        "{{ENV_VAR_1}}": "{{RECOMMENDED_VALUE}}",
        "{{ENV_VAR_2}}": "{{RECOMMENDED_VALUE}}",
        "{{OPTIONAL_ENV_VAR_1}}": "{{RECOMMENDED_VALUE}}",
        "{{OPTIONAL_ENV_VAR_2}}": "{{RECOMMENDED_VALUE}}",
        "{{WRITE_GATE_ENV}}": "false"
      }
    }
  }
}
```

### Claude Desktop

Same JSON block in `claude_desktop_config.json` (Settings > Developer > Edit Config).

### Cursor

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name={{SERVER_KEY}}&config={{CURSOR_B64}})

Or the same JSON block in `.cursor/mcp.json`.

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
| `{{OPTIONAL_ENV_VAR_1}}` | no | `{{DEFAULT}}` | {{PURPOSE}} |
| `{{OPTIONAL_ENV_VAR_2}}` | no | `{{DEFAULT}}` | {{PURPOSE}} |
| `{{WRITE_GATE_ENV}}` | no | `false` | Enables write operations |

## Security & write safety

{{PRODUCT}} credentials: {{LEAST_PRIVILEGE_SETUP, e.g. "create a dedicated API token with read scope; see below"}}.

- All write operations are **disabled by default**. Set `{{WRITE_GATE_ENV}}=true` to enable them.
- Destructive operations additionally require `confirm: true` on the individual call.
- {{ANY_OTHER_GUARDRAIL, e.g. backups before mutation, rate limits}}

## API coverage

<!-- GENERATED SECTION: do not edit by hand. Regenerate from the catalog with scripts/generate-api-coverage.mjs whenever the catalog changes. -->

{{TOTAL_COUNT}} operations covered.

| Category | Operations |
|---|---|
| {{CATEGORY_1}} | {{COUNT}} |
| {{CATEGORY_2}} | {{COUNT}} |

<details>
<summary><strong>{{CATEGORY_1}}</strong> ({{COUNT}} operations)</summary>

| Method | Path | Operation ID |
|---|---|---|
| GET | `{{/path/one}}` | `{{operation_id}}` |
| POST | `{{/path/two}}` | `{{operation_id}}` |

</details>

<details>
<summary><strong>{{CATEGORY_2}}</strong> ({{COUNT}} operations)</summary>

| Method | Path | Operation ID |
|---|---|---|
| GET | `{{/path/three}}` | `{{operation_id}}` |

</details>

<!-- Report-catalog servers (e.g. AppFolio): use Report | ID columns instead. -->

## Contributing

Contributions and issues are welcome. Please open an issue first before submitting a PR.

## License

AGPL-3.0: free for personal and open-source use. Organizations that cannot comply with the AGPL can purchase a commercial license, and hosted/managed versions are available. See [COMMERCIAL.md](https://github.com/NightSquawk/{{REPO}}/blob/v1.0.0/COMMERCIAL.md) or contact hello@nightsquawk.tech.

### Copyright

For copyright concerns or takedown requests, contact hello@nightsquawk.tech.

---

Built and production-used by [NightSquawk Tech](https://nightsquawk.tech), an MSP/MSSP. We run these servers against our own infrastructure before publishing them.
