# NightSquawk MCP Server README & Metadata Standard

This standard applies to every repo in the NightSquawk MCP family (`mcp-core`, all `*-mcp-server` repos, and this index repo). It defines the branch model, repo/npm metadata, README structure, and voice rules. The copy-paste skeleton lives in [README-TEMPLATE.md](README-TEMPLATE.md).

**Who we are optimizing for:** someone searching "\<product\> mcp server", "\<product\> claude integration", or "cursor \<product\> mcp" who wants a working config in under a minute, plus the MSP/vendor evaluating whether this is safe to point at production systems.

## 1. Branch model

| Branch | Role |
|---|---|
| `v1.0.0` | Default branch. Stable, published state. Only receives merges from `develop`. |
| `develop` | All work lands here first: features, docs, README changes, everything. |

Flow: commit to `develop`, then merge/push `develop` into `v1.0.0` when releasing. Never commit directly to `v1.0.0` except CI/infra hotfixes. npm publishing triggers on `v*` git tags, which is unaffected by branch names.

## 2. GitHub repo metadata

- **Description** (shows in Google and GitHub search results, keep under ~160 chars):
  `<Product> MCP server for Claude, Cursor, and AI agents: <one concrete capability clause with a number>.`
  Example: `Proxmox MCP server for Claude, Cursor, and AI agents: all 993 PVE + PDM API endpoints behind 6 catalog-backed tools, writes env-gated.`
- **Topics** (10-12 max). Base set on every repo:
  `mcp`, `mcp-server`, `model-context-protocol`, `ai`, `claude`, `typescript`
  Plus 3-6 product/domain tags, e.g. `proxmox`, `proxmox-ve`, `virtualization`, `homelab` or `kimai`, `time-tracking`, `msp`.
- **Website field:** `https://nightsquawk.tech`
- **Social preview image:** 1280x640 branded card per repo (product logo + "MCP Server" + NightSquawk mark). Pending a design pass; track as a follow-up.

## 3. npm metadata (package.json)

- `description`: identical to the GitHub description.
- `keywords`: **required**, 8-15 entries. Base set:
  `mcp`, `mcp-server`, `model-context-protocol`, `modelcontextprotocol`, `claude`, `cursor`, `ai-agent`, `llm`
  plus product terms (`proxmox`, `proxmox-ve`, `pve`, ...). npm search and Google both index these.
- `homepage`, `repository`, `bugs` fields must all be set and point at the GitHub repo.
- The README ships in the npm package. npmjs.com renders it as a second SEO surface, so relative links must be absolute GitHub URLs or they break on npm.

## 4. README structure

Sections in this exact order. Skip a section only if it genuinely does not apply.

1. **H1:** `# <Product> MCP Server`. Exact-match keyword, nothing clever.
2. **Badge row:** npm version, npm downloads, OpenSSF Scorecard, license (AGPL-3.0), Node version. One line, immediately under the H1.
3. **Install button row:** one-click install badges, immediately under the badge row.
   - **Add to Cursor** (official deeplink): `[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=<key>&config=<base64>)` where `<base64>` is the base64-encoded server config JSON (`{"command":"npx","args":["-y","@nightsquawktech/<repo>"],"env":{...}}`).
   - **Install in VS Code** (shields badge): link target `https://insiders.vscode.dev/redirect/mcp/install?name=<key>&config=<urlencoded-json>`.
   - **Download for Claude Desktop** (shields badge): links to the `.mcpb` Desktop Extension asset on the repo's `mcpb-v<version>` GitHub release. Download + double-click = installed; Claude Desktop prompts for the env vars via the `user_config` UI. Badge: `[![Download for Claude Desktop](https://img.shields.io/badge/Claude_Desktop-Download_.mcpb-D97757?style=flat-square)](https://github.com/NightSquawk/<repo>/releases/download/mcpb-v<version>/<name>-<version>.mcpb)`. Each repo carries `manifest.json` + `scripts/build-mcpb.mjs` (pilot: tacticalrmm-mcp-server); release tags use the `mcpb-v` prefix so they never trigger the `v*` npm publish workflow.
   - There is no one-click web button for Claude Code: it installs via the `claude mcp add` one-liner in Quick start.
4. **Lede paragraph.** This is the SEO payload and the pitch. 2-3 sentences that must contain, within the first ~50 words: the phrase "MCP (Model Context Protocol) server", the product name and what it connects to, "Claude Desktop, Claude Code, Cursor, and any MCP client", and the headline number (endpoint count, tool count, report count).
5. **Feature snapshot.** 4-6 bullets or a small table. Every claim quantified: "993 endpoints", "137 reports", not "comprehensive coverage".
6. **`## Quick start`.** Copy-paste config within the first screenful. The JSON block must list **every env var the server reads**, each with its recommended value (real default, sane example, or `false` for gates), so a user deletes what they do not need instead of hunting for what is missing. Client-specific subheadings, because each is a long-tail search phrase:
   - `### Claude Code`: the `claude mcp add` one-liner first, then the `.mcp.json` block
   - `### Claude Desktop` (`claude_desktop_config.json`)
   - `### Cursor`: the Add to Cursor button again, plus `.cursor/mcp.json`
   The JSON is identical except for file location; say so once instead of repeating prose.
7. **`## Tools`.** Table: tool name, what it does. For catalog-backed servers, explain the list/describe/call triple in one paragraph and link to `mcp-core`.
8. **`## Configuration`.** Env var table: name, required?, default, purpose. This is the reference the Quick start values come from; keep the two in sync.
9. **`## Security & write safety`.** Read-only by default, how the write gate works, `confirm: true` on destructive calls, what credentials are needed and the least-privilege setup. This section closes the deal with the MSP/sysadmin evaluator; never bury it.
10. **`## API coverage`.** Every single endpoint/report/operation the server covers, no sampling. Structure: a summary table of counts by category up top, then one collapsible `<details>` block per category containing a `Method | Path | Operation ID` table (or `Report | ID` for report catalogs). This section is **generated from the catalog by a script**, never hand-maintained; regenerate whenever the catalog changes. Besides being the honest coverage claim, every path string is a long-tail keyword.
11. **`## Contributing`.** One line: contributions and issues are welcome; open an issue first before submitting a PR.
12. **`## License`.** AGPL-3.0, free for personal and open-source use; commercial licensing and hosted versions available, contact `hello@nightsquawk.tech`, link COMMERCIAL.md. Include a **Copyright** subsection: for copyright concerns or takedown requests, contact `hello@nightsquawk.tech`.
13. **Footer line:** `Built and production-used by [NightSquawk Tech](https://nightsquawk.tech), an MSP/MSSP. We run these servers against our own infrastructure before publishing them.`

## 5. Voice rules

- **No em dashes.** Use a colon, comma, or hyphen instead.
- Numbers over adjectives. If a claim has no number, either find the number or cut the claim.
- Banned words: revolutionary, blazing, powerful, seamless, supercharge, unleash, game-changing.
- Second person for setup instructions ("Add this to your config"), plain present tense for behavior ("Reads execute by default").
- Bold sparingly: reserve it for the facts a skimmer must not miss (write gate, endpoint count).
- Code and env var names always in backticks.

## 6. Index repo (mcp-servers)

The index README keeps one table row per server: name, what it connects to, what you can do (quantified). Update the row in the same PR that changes a server's headline capability. The index repo follows this same branch model.

## 7. Release checklist

Before merging `develop` into `v1.0.0`:

- [ ] README follows section order above; lede contains all four SEO elements
- [ ] Quick start JSON lists every env var with a recommended value, in sync with the Configuration table
- [ ] API coverage section regenerated from the catalog (counts match the lede and feature snapshot)
- [ ] Install buttons resolve: Cursor base64 config and VS Code URL reflect the current env vars
- [ ] GitHub description + topics match section 2
- [ ] `package.json` keywords + description match section 3
- [ ] Links are absolute (npm README surface)
- [ ] Index repo row updated if capabilities changed
- [ ] No em dashes, no banned words
