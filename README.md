<h1 align="center">nexageapps's SuccessFactors MCP (Demo)</h1>

<p align="center">
  <strong>Give your AI agent secure access to SAP SuccessFactors.</strong><br />
  Cursor plugin for the public DEMOCO demo. No SuccessFactors password in chat.
</p>

<p align="center">
  <a href="https://github.com/nexageapps/mcp_tool_for_sfsf"><img src="https://img.shields.io/badge/server-mcp_tool_for_sfsf-412991?style=flat-square" alt="Product repo" /></a>
  <a href="https://huggingface.co/spaces/HeisenbergLupenix/successfactors-mcp"><img src="https://img.shields.io/badge/Hugging%20Face-DEMOCO%20Space-FFD21E?style=flat-square&logo=huggingface&logoColor=black" alt="Hugging Face" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" alt="License: MIT" /></a>
</p>

<p align="center">
  <a href="https://community.sap.com/t5/artificial-intelligence-blogs-posts/your-ai-agent-wants-to-talk-to-successfactors-start-with-the-security/ba-p/14469334"><img src="https://img.shields.io/badge/Blog-SAP%20Community-008FD3?style=for-the-badge&logo=sap&logoColor=white" alt="Blog" /></a>
  <a href="https://community.sap.com/t5/artificial-intelligence-blogs-posts/your-ai-agent-wants-to-talk-to-successfactors-start-with-the-security/ba-p/14469334"><img src="https://img.shields.io/badge/SAP%20Community-Start%20with%20the%20Security-008FD3?style=for-the-badge&logo=sap&logoColor=white" alt="SAP Community" /></a>
  <a href="https://community.sap.com/t5/artificial-intelligence/gh-p/ai"><img src="https://img.shields.io/badge/space-Artificial%20Intelligence-0A6ED1?style=for-the-badge" alt="Artificial Intelligence Space" /></a>
</p>

<p align="center">
  <a href="https://community.sap.com/t5/artificial-intelligence-blogs-posts/your-ai-agent-wants-to-talk-to-successfactors-start-with-the-security/ba-p/14469334">Your AI Agent Wants to Talk to SuccessFactors: Start with the Security</a>
</p>

Cursor plugin for [SuccessFactors MCP](https://github.com/nexageapps/mcp_tool_for_sfsf).
Installs like Gmail or Calendar: **Customize** → enable `successfactors-mcp` →
tools such as `search_employee` appear.

The bundled MCP URL is the public DEMOCO demo:

```text
https://heisenberglupenix-successfactors-mcp.hf.space/mcp
```

Anonymous `/mcp` stays on DEMOCO. This listing is the thin plugin repo, not
the Python server.

## Sideload

```bash
mkdir -p ~/.cursor/plugins/local
ln -sfn "$(pwd)" ~/.cursor/plugins/local/successfactors-mcp
```

Reload Cursor. Enable `successfactors-mcp` in Customize. Ask: *Who is Jane
Smith's manager?*

## Marketplace

Submit `https://github.com/nexageapps/successfactors-mcp-cursor` at
[cursor.com/marketplace/publish](https://cursor.com/marketplace/publish).
Cursor reviews public listings by hand. After it is listed, install from
Customize like Gmail.

Team / Enterprise: **Dashboard → Plugins → Import from Repo** with that URL.

Do **not** submit the full server repo. Cursor clones the Git URL you
publish.

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

## Maintainers

Refresh this repo from the product tree on a laptop as GitHub user
`nexageapps`. Cursor Cloud cannot push here (`cursor[bot]` gets HTTP 403).

Always delete `/tmp/sfsf-mcp` first (a leftover clone makes `git clone`
fail and `cp` copy stale files). Pull `main` before you push (`! [rejected]
main -> main (fetch first)` means GitHub already has commits you do not,
often `.DS_Store`). `git add` without a new `git commit` does not push
anything.

```bash
cd ~/successfactors-mcp-cursor
git pull origin main

rm -rf /tmp/sfsf-mcp
git clone -b cursor/cursor-mcp-config-c134 https://github.com/nexageapps/mcp_tool_for_sfsf.git /tmp/sfsf-mcp
rsync -a --exclude .git /tmp/sfsf-mcp/cursor-plugin/ ./

git status
git add .
git commit -m "docs: refresh Cursor plugin from product repo"
git push origin main
```

Or upload `.cursor-plugin/plugin.json`, `mcp.json`,
`skills/successfactors-hr/SKILL.md`, `assets/cursor-plugin-logo.svg`,
`README.md`, and `LICENSE` in the GitHub UI
([Upload files](https://github.com/nexageapps/successfactors-mcp-cursor/upload)).
