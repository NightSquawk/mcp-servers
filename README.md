# NightSquawk MCP Servers

Open-source [Model Context Protocol](https://modelcontextprotocol.io) servers by [NightSquawk Tech](https://nightsquawk.tech), an MSP/MSSP. We build these to run our own operations, then publish them.

## Servers

| Server | Connects to | Style |
|---|---|---|
| [proxmox-mcp-server](https://github.com/NightSquawk/proxmox-mcp-server) | Proxmox VE + Proxmox Datacenter Manager | Catalog |
| [appfolio-mcp-server](https://github.com/NightSquawk/appfolio-mcp-server) | AppFolio Property Manager (Reports + Database APIs) | Catalog |
| [invoiceninja-mcp-server](https://github.com/NightSquawk/invoiceninja-mcp-server) | Invoice Ninja v5 | Catalog |
| [everything-mcp-server](https://github.com/NightSquawk/everything-mcp-server) | Everything (voidtools) local file search | Catalog |
| [tacticalrmm-mcp-server](https://github.com/NightSquawk/tacticalrmm-mcp-server) | TacticalRMM | Curated tools |
| [kimai-mcp-server](https://github.com/NightSquawk/kimai-mcp-server) | Kimai time tracking | Curated tools |
| [gohighlevel-mcp-server](https://github.com/NightSquawk/gohighlevel-mcp-server) | GoHighLevel CRM | Curated tools |

Shared runtime: [mcp-core](https://github.com/NightSquawk/mcp-core) (`@nightsquawktech/mcp-core`).

## Two styles

**Catalog** servers expose three generic tools (`list_endpoints`, `describe_endpoint`, `call_endpoint`) over a generated JSON catalog of the target API. The model discovers operations on demand instead of carrying every tool definition in context. This keeps the standing context cost per server tiny (3 tool definitions instead of dozens), which matters when many MCP servers are loaded at once. Write operations are gated and require explicit confirmation.

**Curated** servers register one hand-written tool per operation, with tuned descriptions and response shaping. The curated servers are planned to be rewritten in the catalog style.

## Using a server

Each repo has its own README with setup details. The general shape, for any MCP client (Claude Desktop, Claude Code, Cursor, etc.):

```json
{
  "mcpServers": {
    "proxmox": {
      "command": "npx",
      "args": ["-y", "@nightsquawktech/proxmox-mcp-server"],
      "env": {
        "...": "see the server's README for required variables"
      }
    }
  }
}
```

## License

All servers and mcp-core are licensed under the GNU AGPL v3.0. Free for personal and open-source use.

Organizations that cannot comply with the AGPL can purchase a commercial license, and hosted/managed versions are available. See any repo's COMMERCIAL.md or contact hello@nightsquawk.tech.
