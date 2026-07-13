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
3. **Lede paragraph.** One sentence: `An MCP (Model Context Protocol) server for **<Product>**, connecting <what it connects to> to AI tools.` No feature bullet list; the numbers live in Tools and API coverage.
4. **`## Quick start`.** No preamble paragraph. One `###` subsection per client, each in the same shape: install button first (when one exists), CLI command second. Then a final `### mcp.json` subsection with the plain JSON. Subsection order and contents:
   - `### Claude`: the **Download for Claude Desktop** `.mcpb` badge, then the `claude mcp add` one-liner for Claude Code. Badge: `[![Download for Claude Desktop](https://img.shields.io/badge/Claude_Desktop-Download_.mcpb-D97757?style=flat-square)](https://github.com/NightSquawk/<repo>/releases/download/mcpb-v<version>/<name>-<version>.mcpb)`. Each repo carries `manifest.json` + `scripts/build-mcpb.mjs` (pilot: tacticalrmm-mcp-server); `.mcpb` release tags use the `mcpb-v` prefix so they never trigger the `v*` npm publish workflow.
   - `### Cursor`: the official **Add to Cursor** button: `[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=<key>&config=<base64>)` where `<base64>` is the base64-encoded server config JSON (`{"command":"npx","args":["-y","@nightsquawktech/<repo>"],"env":{...}}`). Cursor's CLI (`agent mcp`) has list/login/enable/disable but **no `mcp add`** (verified against cursor.com/docs/cli/mcp): install is button or `.cursor/mcp.json`, then `agent mcp list` to verify.
   - `### VS Code`: the **Install in VS Code** shields badge linking `https://insiders.vscode.dev/redirect/mcp/install?name=<key>&config=<urlencoded-json>`, then the `code --add-mcp '<json>'` one-liner.
   - `### Codex`: CLI only, the `codex mcp add` one-liner (`~/.codex/config.toml` for manual setup).
   - `### mcp.json`: the plain JSON block, listing **every env var the server reads** with its recommended value (real default, sane example, or `false` for gates), plus one line naming where each client keeps the file.
   - **Every CLI block defines the env values as shell variables at the top**, then references them, so the user edits values once at the top instead of inside command arguments or inline JSON.
   - **Every CLI subsection ships two labeled blocks**: `**bash (macOS/Linux):**` (`VAR="value"`, `\` continuations, `"$VAR"` references) and `**PowerShell (Windows):**` (`$VAR = "value"`, backtick continuations, `"KEY=$VAR"` references; for VS Code build the JSON with a hashtable piped to `ConvertTo-Json -Compress`). bash syntax is not valid PowerShell, and the MSP audience is Windows-heavy.
   - **No LM Studio / Goose buttons**: their deeplinks use custom protocols (`lmstudio://`, `goose://`) which GitHub's markdown sanitizer strips, leaving a dead button image (verified against the GitHub render API). Only https-wrapped deeplinks work in READMEs. Claude Code and Codex have no deeplink protocol at all: CLI one-liners only.
5. **`## Configuration`.** Env var table: name, required?, default, purpose. This is the reference the Quick start values come from; keep the two in sync.
6. **`## Security & write safety`.** Read-only by default, how the write gate works, `confirm: true` on destructive calls, what credentials are needed and the least-privilege setup. This section closes the deal with the MSP/sysadmin evaluator; never bury it. **Mandatory callout** (GitHub `> [!IMPORTANT]` alert): the write gate is a guardrail, not a security boundary. The env vars in the MCP config are real credentials; an AI agent with shell access can bypass the MCP tools and call the API directly with them. Hard read-only must be enforced at the source by scoping the API key/token itself to read-only permissions.
7. **`## Tools`.** One large code block (like the setup JSON, not a table): every tool name left-aligned with its one-line purpose, CLI-help style. For catalog-backed servers, explain the list/describe/call triple in one paragraph above the block and link to `mcp-core`.
8. **`## API coverage`.** Every single endpoint/report/operation the server covers, no sampling. Structure: a summary table of counts by category up top, then one collapsible `<details>` block per category containing a `Method | Path | Operation ID` table (or `Report | ID` for report catalogs). This section is **generated from the catalog by a script**, never hand-maintained; regenerate whenever the catalog changes. Besides being the honest coverage claim, every path string is a long-tail keyword.
9. **`## Contributing`.** One line: contributions and issues are welcome; open an issue first before submitting a PR.
10. **`## License`.** AGPL-3.0, free for personal and open-source use; commercial licensing and hosted versions available, contact `hello@nightsquawk.tech`, link COMMERCIAL.md. Include a **Copyright** subsection: for copyright concerns or takedown requests, contact `hello@nightsquawk.tech`. No footer after this section; License ends the README.

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
