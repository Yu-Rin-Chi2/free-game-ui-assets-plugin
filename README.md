# Free Game UI Assets — Claude Code Plugin

Just ask your AI for "a red confirm button" or "a coin icon" and it searches the **[Free Game UI Assets](https://free-ui-assets.yurinchi2525.com)** library (~2,100 game UI SVGs / 512px PNGs), then saves the best match straight into your project.

- **All assets are CC0 1.0** — commercial use allowed, no attribution required, free to modify
- **MCP server bundled** — installing the plugin auto-registers the remote MCP (no separate setup)
- **Skill bundled** — built-in search strategy (noun → query / kind → type / color → color) so you reliably land the asset you want

## Install

```bash
# 1. Add the marketplace
claude plugin marketplace add Yu-Rin-Chi2/free-game-ui-assets-plugin

# 2. Install the plugin (MCP + Skill come together)
claude plugin install game-ui-assets@free-game-ui-assets
```

After installing, the MCP server `game-ui-assets` is auto-registered. Run `/mcp` to check the connection.

## Usage

Just ask Claude directly:

```
I need a coin icon. Save it to assets/.
Find a blue HP gauge and add it to public/ui/ as SVG.
Show me a few wooden panels.
```

The skill triggers automatically and walks through search → candidates → save.

## What's included

| Type | Name | Contents |
|------|------|----------|
| MCP server | `game-ui-assets` | `search_assets` / `get_asset` / `download_svg` / `list_taxonomy` (Streamable HTTP) |
| Skill | `find-game-ui-assets` | Search-and-save workflow for game UI assets |

## Use from other clients (MCP only)

From other MCP-capable clients (Cursor / Claude Desktop / ChatGPT, etc.), register this Remote MCP to get the same tools:

```
https://mcp.freegameui.net/mcp
```

## License

- **Assets**: CC0 1.0 Universal (public domain). Free to use, modify, and redistribute for any purpose, commercial or not.
- **This plugin**: [LICENSE](LICENSE) (CC0 1.0)
