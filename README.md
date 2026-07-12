# NightSquawk MCP Servers

Open-source [Model Context Protocol](https://modelcontextprotocol.io) servers by [NightSquawk Tech](https://nightsquawk.tech), an MSP/MSSP. We build these to run our own operations, then publish them.

## Index

| Server | Connects to | What you can do |
|---|---|---|
| [proxmox-mcp-server](https://github.com/NightSquawk/proxmox-mcp-server) | Proxmox VE + Proxmox Datacenter Manager | Query and manage nodes, VMs, containers, storage, and cluster config across the full PVE and PDM APIs (675+ endpoints). Writes are env-gated. |
| [tacticalrmm-mcp-server](https://github.com/NightSquawk/tacticalrmm-mcp-server) | TacticalRMM | Read agents, checks, alerts, tasks, software, updates, and audit logs from a self-hosted TacticalRMM instance. |
| [kimai-mcp-server](https://github.com/NightSquawk/kimai-mcp-server) | Kimai | Browse customers, projects, activities, and timesheets; create and manage time entries with confirmation-guarded writes. |
| [gohighlevel-mcp-server](https://github.com/NightSquawk/gohighlevel-mcp-server) | GoHighLevel CRM | Full custom-field CRUD, contacts (including delete), opportunities, tags, conversations, and calendars. Fills the gaps the official GHL MCP leaves open. |
| [invoiceninja-mcp-server](https://github.com/NightSquawk/invoiceninja-mcp-server) | Invoice Ninja v5 | Reach the entire v5 API (379 endpoints): clients, invoices, quotes, payments, reports. Mutations require explicit authorization and are backed up before execution. |
| [appfolio-mcp-server](https://github.com/NightSquawk/appfolio-mcp-server) | AppFolio Property Manager | Run any of 137 reports and query the Database API (156 endpoints) for properties, tenants, leases, and accounting data. |

More servers are on the way; watch this repo for updates.

## Quick start

Each server runs over stdio via npx and works with any MCP client (Claude Desktop, Claude Code, Cursor, etc.). The general shape:

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

Every repo's README documents its required environment variables and setup.

## Design notes

Several servers use a catalog design: instead of registering dozens of tools, they expose three (`list_endpoints`, `describe_endpoint`, `call_endpoint`) over a generated JSON catalog of the target API. The model discovers operations on demand, which keeps the standing context cost per server tiny when many MCP servers are loaded at once. Write operations are always gated behind explicit confirmation.

Shared plumbing lives in [`@nightsquawktech/mcp-core`](https://github.com/NightSquawk/mcp-core).

## License

Everything here is licensed under the GNU AGPL v3.0. Free for personal and open-source use.

Organizations that cannot comply with the AGPL can purchase a commercial license, and hosted/managed versions are available. See any repo's COMMERCIAL.md or contact hello@nightsquawk.tech.
