# {{PRODUCT}} MCP Server

<!-- Copy everything below the divider into the server repo's README.md and replace {{PLACEHOLDERS}}. Rules and section rationale: README-STANDARD.md -->
<!-- {{CURSOR_B64}} = base64 of {"command":"npx","args":["-y","@nightsquawktech/{{REPO}}"],"env":{...all vars...}} -->
<!-- {{VSCODE_URLENC}} / {{VSCODE_JSON}} = URL-encoded / inline version of the same JSON (VS Code json includes "name") -->

---

# {{PRODUCT}} MCP Server

[![npm version](https://img.shields.io/npm/v/@nightsquawktech/{{REPO}})](https://www.npmjs.com/package/@nightsquawktech/{{REPO}})
[![npm downloads](https://img.shields.io/npm/dm/@nightsquawktech/{{REPO}})](https://www.npmjs.com/package/@nightsquawktech/{{REPO}})
[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/NightSquawk/{{REPO}}/badge)](https://scorecard.dev/viewer/?uri=github.com/NightSquawk/{{REPO}})
[![License: AGPL-3.0](https://img.shields.io/badge/license-AGPL--3.0-blue)](https://github.com/NightSquawk/{{REPO}}/blob/v1.0.0/LICENSE)
[![Node](https://img.shields.io/node/v/@nightsquawktech/{{REPO}})](https://nodejs.org)

An MCP (Model Context Protocol) server for **{{PRODUCT}}**, connecting {{WHAT_IT_CONNECTS_TO}} to AI tools.

## Quick start

### Claude

[![Download for Claude Desktop](https://img.shields.io/badge/Claude_Desktop-Download_.mcpb-D97757?style=flat-square)](https://github.com/NightSquawk/{{REPO}}/releases/download/mcpb-v{{VERSION}}/{{REPO}}-{{VERSION}}.mcpb)

**bash (macOS/Linux):**

```bash
{{ENV_VAR_1}}="{{RECOMMENDED_VALUE}}"
{{ENV_VAR_2}}="{{RECOMMENDED_VALUE}}"

claude mcp add {{SERVER_KEY}} \
  --env {{ENV_VAR_1}}="${{ENV_VAR_1}}" \
  --env {{ENV_VAR_2}}="${{ENV_VAR_2}}" \
  -- npx -y @nightsquawktech/{{REPO}}
```

**PowerShell (Windows):**

```powershell
${{ENV_VAR_1}} = "{{RECOMMENDED_VALUE}}"
${{ENV_VAR_2}} = "{{RECOMMENDED_VALUE}}"

claude mcp add {{SERVER_KEY}} `
  --env "{{ENV_VAR_1}}=${{ENV_VAR_1}}" `
  --env "{{ENV_VAR_2}}=${{ENV_VAR_2}}" `
  -- npx -y @nightsquawktech/{{REPO}}
```

### Cursor

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name={{SERVER_KEY}}&config={{CURSOR_B64}})

Or put the [mcp.json](#mcpjson) block in `.cursor/mcp.json`, then verify with:

```bash
agent mcp list
```

(The Cursor CLI manages configured servers but has no `mcp add`; install is via the button or `mcp.json`.)

### VS Code

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name={{SERVER_KEY}}&config={{VSCODE_URLENC}})

**bash (macOS/Linux):**

```bash
{{ENV_VAR_1}}="{{RECOMMENDED_VALUE}}"
{{ENV_VAR_2}}="{{RECOMMENDED_VALUE}}"

code --add-mcp '{"name":"{{SERVER_KEY}}","command":"npx","args":["-y","@nightsquawktech/{{REPO}}"],"env":{"{{ENV_VAR_1}}":"'"${{ENV_VAR_1}}"'","{{ENV_VAR_2}}":"'"${{ENV_VAR_2}}"'"}}'
```

**PowerShell (Windows):**

```powershell
${{ENV_VAR_1}} = "{{RECOMMENDED_VALUE}}"
${{ENV_VAR_2}} = "{{RECOMMENDED_VALUE}}"

$config = @{
  name = "{{SERVER_KEY}}"
  command = "npx"
  args = @("-y", "@nightsquawktech/{{REPO}}")
  env = @{
    {{ENV_VAR_1}} = ${{ENV_VAR_1}}
    {{ENV_VAR_2}} = ${{ENV_VAR_2}}
  }
} | ConvertTo-Json -Compress

code --add-mcp $config
```

### Codex

**bash (macOS/Linux):**

```bash
{{ENV_VAR_1}}="{{RECOMMENDED_VALUE}}"
{{ENV_VAR_2}}="{{RECOMMENDED_VALUE}}"

codex mcp add {{SERVER_KEY}} \
  --env {{ENV_VAR_1}}="${{ENV_VAR_1}}" \
  --env {{ENV_VAR_2}}="${{ENV_VAR_2}}" \
  -- npx -y @nightsquawktech/{{REPO}}
```

**PowerShell (Windows):**

```powershell
${{ENV_VAR_1}} = "{{RECOMMENDED_VALUE}}"
${{ENV_VAR_2}} = "{{RECOMMENDED_VALUE}}"

codex mcp add {{SERVER_KEY}} `
  --env "{{ENV_VAR_1}}=${{ENV_VAR_1}}" `
  --env "{{ENV_VAR_2}}=${{ENV_VAR_2}}" `
  -- npx -y @nightsquawktech/{{REPO}}
```

Or add it to `~/.codex/config.toml` under `[mcp_servers.{{SERVER_KEY}}]`.

### mcp.json

Every environment variable the server reads, with recommended values:

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

File locations: `.mcp.json` in your project root (Claude Code), `claude_desktop_config.json` (Claude Desktop), `.cursor/mcp.json` (Cursor).

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

> [!IMPORTANT]
> The write gate is a guardrail, not a security boundary. The env vars in your MCP config are real credentials, and an AI agent with shell access can bypass the MCP tools and call the {{PRODUCT}} API directly with them. If you need hard read-only, enforce it at the source: scope the API key or token itself to read-only permissions.

## Tools

<!-- Catalog-backed servers: add one paragraph here explaining discover/describe/call and link mcp-core. -->

```
{{TOOL_1}}                {{WHAT_IT_DOES}}
{{TOOL_2}}                {{WHAT_IT_DOES}}
{{TOOL_3}}                {{WHAT_IT_DOES}}
{{TOOL_4}}                {{WHAT_IT_DOES}}
```

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
