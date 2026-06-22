---
name: find-game-ui-assets
description: ゲームUI素材（アイコン・ボタン・パネル・ゲージ・装飾・グラデーション等のSVG/PNG）を探してプロジェクトに保存したいときに使う。「決定ボタンが欲しい」「コインのアイコンを入れて」「青いHPゲージを探して」など、ゲーム向けUIアセットの取得・ダウンロード要求で発動する。全アセットは CC0（商用可・帰属不要）。
---

# Find Game UI Assets

Free Game UI Assets ライブラリ（約2,100点のゲームUI向け SVG / 512px PNG）から、ユーザーの要望に合う素材を検索し、プロジェクトに保存する。**全アセットは CC0 1.0**（パブリックドメイン相当、商用利用可・帰属表示不要・改変自由）。

このプラグインには MCP サーバ `game-ui-assets` が同梱されており、インストール時に自動登録される。以下の MCP ツールを使う:

- `search_assets` — 素材を検索（主役）
- `get_asset` — 1件の詳細メタデータ
- `download_svg` — SVG ソース本体を取得（保存用）
- `list_taxonomy` — 種別・カテゴリ一覧（検索軸の確認）

## ワークフロー

### 1. 要望を検索クエリに分解する

タグは**英語のみ**。ユーザーの要望（日本語可）を英語キーワードに翻訳し、**3要素に分離**して `search_assets` に渡す。ここが最重要。

- `query` … **主題の名詞だけ**（例: `sword`, `coin`, `heart`, `confirm`, `shield`）
- `asset_type` … 種別（`icon` / `button` / `panel` / `decoration` / `noise` / `shape` / `gauge` / `gradation`）
- `color` … 色系統（`reds` / `yellows` / `greens` / `cyans` / `blues` / `purples` / `mono`。button/panel/gauge のみ）

**重要**: `query` に `icon` / `button` などの種別語や色名を混ぜない。タグに該当文字列が無く 0 件になりやすい。

| ユーザーの要望 | 呼び出し |
|----------------|----------|
| 「剣のアイコン」 | `search_assets(query="sword", asset_type="icon")` |
| 「赤い決定ボタン」 | `search_assets(query="confirm", asset_type="button", color="reds")` |
| 「青いHPゲージ」 | `search_assets(query="hp", asset_type="gauge", color="blues")` |
| 「木目調のパネル」 | `search_assets(query="wood", asset_type="panel")` |

種別やカテゴリが不明なときは、先に `list_taxonomy` で利用可能な種別・カテゴリを確認する。

### 2. 候補を提示する

ヒットした候補（`name` / `tags` / `svg_url` / `png_url`）をユーザーに簡潔に提示し、どれを保存するか確認する。0 件なら別のキーワード（同義語・上位語）で再検索するか、`query` を外して `asset_type` + `color` だけで広げる。

### 3. 保存する

保存先はユーザーに確認する（未指定ならプロジェクト内の `assets/` や `public/` 等の妥当な場所を提案）。

- **SVG**: `download_svg(name)` で SVG ソース本体（テキスト）を取得し、`{保存先}/{name}.svg` として書き出す。
- **PNG（512px）が必要な場合**: `get_asset(name)` の `png_url` を取得し、その URL をダウンロードして `{保存先}/{name}.png` に保存する（`curl -L -o ...` 等）。

複数素材をまとめて頼まれた場合は、各 `name` について上記を繰り返す。

### 4. ライセンスを一言添える

全アセットは **CC0 1.0** なので帰属表示は不要だが、保存後に「これらの素材は CC0（商用可・帰属不要）です」と一言伝える。クレジットの記載義務はない。

## フォールバック（MCP ツールが使えない場合）

何らかの理由で MCP ツールが利用できないときは、公開 REST API / CDN を直接叩いてもよい（認証不要・CC0）:

```bash
# 検索
curl -s "https://game-ui-assets-api.yurinchi2525.workers.dev/assets?q=sword&type=icon&limit=10"
# SVG 本体を保存
curl -s -L -o sword.svg "https://cdn.freegameui.net/svg/icons/item/ic_item_sword-iron_01.svg"
```

レスポンスの各アイテムは `svg_url` / `png_url` / `license` を含む。
