# Free Game UI Assets — Claude Code Plugin

AI に「赤い決定ボタンが欲しい」「コインのアイコンを入れて」と頼むだけで、**[Free Game UI Assets](https://free-ui-assets.yurinchi2525.com)** ライブラリ（約2,100点のゲームUI向け SVG / 512px PNG）から最適な素材を検索し、プロジェクトに保存できる Claude Code プラグインです。

- **全アセット CC0 1.0** — 商用利用可・帰属表示不要・改変自由
- **MCP サーバ同梱** — プラグインを入れるだけでリモート MCP が自動登録される（別途セットアップ不要）
- **Skill 同梱** — 検索のコツ（名詞=query / 種別=type / 色=color）を内蔵し、狙った素材に確実に到達

## インストール

```bash
# 1. マーケットプレイスを追加
claude plugin marketplace add Yu-Rin-Chi2/free-game-ui-assets-plugin

# 2. プラグインをインストール（MCP + Skill がまとめて入る）
claude plugin install game-ui-assets@free-game-ui-assets
```

インストール後、MCP サーバ `game-ui-assets` が自動登録されます。`/mcp` で接続状態を確認できます。

## 使い方

Claude にそのまま頼むだけです。

```
コインのアイコンが欲しい。assets/ に保存して。
青いHPゲージを探して、public/ui/ に SVG で入れて。
木目調のパネルを3種類くらい見せて。
```

Skill が自動で発動し、検索 → 候補提示 → 保存まで誘導します。

## 同梱物

| 種別 | 名前 | 内容 |
|------|------|------|
| MCP サーバ | `game-ui-assets` | `search_assets` / `get_asset` / `download_svg` / `list_taxonomy`（Streamable HTTP） |
| Skill | `find-game-ui-assets` | ゲームUI素材の検索・保存ワークフロー |

## 他のクライアントで使う（MCP 単体）

Cursor / Claude Desktop / ChatGPT など他の MCP 対応クライアントからは、以下の Remote MCP を登録すれば同じツールが使えます。

```
https://game-ui-assets-mcp.yurinchi2525.workers.dev/mcp
```

## ライセンス

- **アセット**: CC0 1.0 Universal（パブリックドメイン相当）。商用・非商用問わず自由に利用・改変・再配布できます。
- **このプラグイン**: [LICENSE](LICENSE)（CC0 1.0）
