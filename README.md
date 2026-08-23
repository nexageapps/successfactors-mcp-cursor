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

**Push from your laptop as GitHub user `nexageapps`.** Cursor Cloud cannot
do this: it authenticates as `cursor[bot]`, which can write
`nexageapps/mcp_tool_for_sfsf` but not `successfactors-mcp-cursor`
(HTTP **403**). `gh repo create` also fails there (`createRepository` is
denied for GitHub App tokens).

1. In the browser, signed in as **nexageapps**, create an empty public repo
   (no README, no `.gitignore`, no license) if it does not already exist:
   [github.com/new](https://github.com/new) → `successfactors-mcp-cursor`.
2. On your machine (HTTPS PAT with write access to `nexageapps`, or SSH as
   that user). Start in **your home directory**, not inside `cursor-plugin`
   and not in Cursor Cloud. Skip any `cd cursor-plugin` when the prompt
   already ends in `cursor-plugin`.

```bash
cd ~
git clone -b cursor/cursor-mcp-config-c134 https://github.com/nexageapps/mcp_tool_for_sfsf.git
cd mcp_tool_for_sfsf/cursor-plugin
git init
git add .
git commit -m "feat: SuccessFactors DEMOCO Cursor plugin"
git branch -M main
git remote add origin https://github.com/nexageapps/successfactors-mcp-cursor.git
# SSH: git remote add origin git@github.com:nexageapps/successfactors-mcp-cursor.git
git push -u origin main
```

If `git init` / `git commit` / `git remote add` already ran, only
`git push -u origin main` is needed. Confirm with `git remote -v`.

Optional: skip git and upload the plugin files in the GitHub UI
([Add file → Upload files](https://github.com/nexageapps/successfactors-mcp-cursor/upload)).
Include `.cursor-plugin/plugin.json`, `mcp.json`,
`skills/successfactors-hr/SKILL.md`, `assets/cursor-plugin-logo.svg`,
`README.md`, and `LICENSE`.

3. Submit `https://github.com/nexageapps/successfactors-mcp-cursor` at
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
| `LICENSE` | MIT |

Server source, Joule artifacts, and Hugging Face deploy live in
[nexageapps/mcp_tool_for_sfsf](https://github.com/nexageapps/mcp_tool_for_sfsf).
