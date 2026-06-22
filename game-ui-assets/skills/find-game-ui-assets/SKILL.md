---
name: find-game-ui-assets
description: Use when the user wants game UI assets (icons, buttons, panels, gauges, decorations, gradations, etc. as SVG/PNG) and wants them found and saved into their project. Triggers on requests like "I need a confirm button", "add a coin icon", "find a blue HP gauge". All assets are CC0 (commercial use OK, no attribution required).
---

# Find Game UI Assets

Search the Free Game UI Assets library (~2,100 game UI SVGs / 512px PNGs) for assets matching the user's request and save them into their project. **All assets are CC0 1.0** (public domain — commercial use allowed, no attribution required, free to modify).

This plugin bundles the `game-ui-assets` MCP server, which is auto-registered on install. Use these MCP tools:

- `search_assets` — search for assets (primary tool)
- `get_asset` — full metadata for one asset
- `download_svg` — fetch the raw SVG source (for saving)
- `list_taxonomy` — list asset types and categories (to discover search axes)

## Workflow

### 1. Turn the request into a search query

Tags are **English only**. Translate the user's request (any language) into English keywords and **split it into three parts** for `search_assets`. This is the most important step.

- `query` … **the subject noun only** (e.g. `sword`, `coin`, `heart`, `confirm`, `shield`)
- `asset_type` … the kind (`icon` / `button` / `panel` / `decoration` / `noise` / `shape` / `gauge` / `gradation`)
- `color` … color group (`reds` / `yellows` / `greens` / `cyans` / `blues` / `purples` / `mono`; button/panel/gauge only)

**Important**: Do NOT put kind words (`icon`, `button`) or color names into `query`. Those strings rarely appear in tags, so an AND match easily returns zero results.

| User request | Call |
|--------------|------|
| "a sword icon" | `search_assets(query="sword", asset_type="icon")` |
| "a red confirm button" | `search_assets(query="confirm", asset_type="button", color="reds")` |
| "a blue HP gauge" | `search_assets(query="hp", asset_type="gauge", color="blues")` |
| "a wooden panel" | `search_assets(query="wood", asset_type="panel")` |

When the type or category is unclear, call `list_taxonomy` first to see the available types and categories.

### 2. Present candidates

Show the matched candidates (`name` / `tags` / `svg_url` / `png_url`) to the user concisely and confirm which to save. If there are zero results, retry with different keywords (synonyms or broader terms), or drop `query` and search with just `asset_type` + `color`.

### 3. Save

Confirm the destination with the user (if unspecified, suggest a sensible location such as `assets/` or `public/`).

- **SVG**: call `download_svg(name)` to get the raw SVG source (text) and write it to `{dest}/{name}.svg`.
- **PNG (512px) if needed**: get `png_url` from `get_asset(name)` and download that URL to `{dest}/{name}.png` (e.g. `curl -L -o ...`).

When asked for multiple assets, repeat the above for each `name`.

### 4. Mention the license

All assets are **CC0 1.0**, so no attribution is required — but after saving, briefly tell the user "these assets are CC0 (commercial use OK, no attribution needed)." There is no credit obligation.

## Fallback (when MCP tools are unavailable)

If the MCP tools cannot be used for any reason, you may call the public REST API / CDN directly (no auth, CC0):

```bash
# search
curl -s "https://game-ui-assets-api.yurinchi2525.workers.dev/assets?q=sword&type=icon&limit=10"
# save the raw SVG
curl -s -L -o sword.svg "https://cdn.freegameui.net/svg/icons/item/ic_item_sword-iron_01.svg"
```

Each response item includes `svg_url` / `png_url` / `license`.
