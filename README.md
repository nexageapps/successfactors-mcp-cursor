# SuccessFactors MCP for Cursor

Cursor plugin for [SuccessFactors MCP](https://github.com/nexageapps/mcp_tool_for_sfsf).
Installs like Gmail or Calendar: **Customize** → enable `successfactors-mcp` →
tools such as `search_employee` appear.

The bundled MCP URL is the public DEMOCO demo:

```text
https://heisenberglupenix-successfactors-mcp.hf.space/mcp
```

No SuccessFactors password in chat. Anonymous `/mcp` stays on DEMOCO.

## Sideload (this folder)

```bash
mkdir -p ~/.cursor/plugins/local
ln -sfn "$(pwd)" ~/.cursor/plugins/local/successfactors-mcp
```

Reload Cursor. Enable `successfactors-mcp` in Customize. Ask: *Who is Jane
Smith's manager?*

## Push to a dedicated GitHub repo (Marketplace)

Do **not** submit the full server repo to the Cursor Marketplace. Cursor
clones the Git URL you publish. This folder is the plugin; the parent repo
is the Python server.

`gh repo create` fails with `createRepository` on GitHub App tokens. Create
the empty public repo in the browser as **nexageapps** (no README):
[github.com/new](https://github.com/new) → `successfactors-mcp-cursor`.

Do **not** push from Cursor Cloud (`cursor[bot]` gets 403). On your machine
as **nexageapps**:

```bash
git clone -b cursor/cursor-mcp-config-c134 https://github.com/nexageapps/mcp_tool_for_sfsf.git
cd mcp_tool_for_sfsf/cursor-plugin
git init
git checkout -B main
git add .
git commit -m "feat: SuccessFactors DEMOCO Cursor plugin"
git remote add origin https://github.com/nexageapps/successfactors-mcp-cursor.git
git push -u origin main
```

Then submit `https://github.com/nexageapps/successfactors-mcp-cursor` at
[cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
Cursor reviews public listings by hand.

Team / Enterprise: **Dashboard → Plugins → Import from Repo** with that URL.

## Files

| File | Role |
| ---- | ---- |
| `.cursor-plugin/plugin.json` | Plugin manifest |
| `mcp.json` | Streamable HTTP MCP |
| `skills/successfactors-hr/SKILL.md` | Agent guidance |
| `assets/cursor-plugin-logo.svg` | Logo |

Server source, Joule artifacts, and Hugging Face deploy live in
[nexageapps/mcp_tool_for_sfsf](https://github.com/nexageapps/mcp_tool_for_sfsf).
# successfactors-mcp-cursor
