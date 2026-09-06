# Chronista Plugins

Chronista Club の公開プラグインカタログ。Claude Code、Codex、Grok Build から同じ 4 件を導入できる。

この repo は登録簿で、本体は各プラグイン repo で管理する。配布元は本体のリリース済み `main`。版は本体 manifest を正本とし、カタログには複製しない。

## Getting Started

カタログを一度登録し、使いたいプラグインを入れる。導入後は **新しいセッション** を開く。

他の 3 件も、コマンドの `chronista-style` をプラグイン名に置き換える。hooks の依存ツール・信頼設定、記憶サービスへの接続は [chronista-style の導入ガイド](https://github.com/chronista-club/plugin-chronista-style/blob/main/docs/guide/01-installation.md) を参照。

### Claude Code

```bash
claude plugin marketplace add chronista-club/chronista-plugins
claude plugin install chronista-style@chronista-plugins
```

### Codex

```bash
codex plugin marketplace add chronista-club/chronista-plugins --ref main
codex plugin add chronista-style@chronista-plugins
```

### Grok Build

`--trust` は hooks と MCP を動かすために必要。Grok は入れただけでは無効なので `enable` する。

```bash
grok plugin marketplace add chronista-club/chronista-plugins
grok plugin install chronista-style@chronista-plugins --trust
grok plugin enable chronista-style
```

確認:

```bash
grok plugin list
```

TUI から入れる場合は `/marketplace`。

## プラグイン

| プラグイン | 内容 |
|---|---|
| [chronista-style](https://github.com/chronista-club/plugin-chronista-style) | 開発フロー、共有スキル、hooks、検証規律 |
| [team-bucciarati](https://github.com/chronista-club/plugin-team-bucciarati) | 調査・テスト・レビューを担う品質チーム |
| [vantage-point](https://github.com/chronista-club/plugin-vantage-point) | board・lane・wire と開発フロー |
| [creo-memories](https://github.com/chronista-club/plugin-creo-memories) | セッションとホストをまたぐ外部記憶 |

Gemini 対応は対象外。

## 旧配布先からの移行

旧 `chronista-club/claude-plugins` と、この repo の marketplace 名はどちらも `chronista-plugins`。旧登録がある環境では、Getting Started のコマンドだけで切替が完了するとは扱わない。

利用設定の退避、旧登録の解除、新登録からの再導入、更新確認を一つの切替作業として行う。Codex の `chronista-style@personal` を利用中の場合も重複読込を確認する。

新しい本体 repo を開発の正本とし、旧 repo は現状のまま残す。旧側へ新しい変更を同期する運用は行わない。

## カタログの構成

- `.claude-plugin/marketplace.json`: Claude Code 用
- `.agents/plugins/marketplace.json`: Codex 用
- `.grok-plugin/marketplace.json`: Grok Build 用（remote は `url` + 40 文字 `sha`）

3 ファイルは同じプラグイン本体を指す。Grok は Claude カタログの `"source": "github"` をインストール候補に載せないため、Grok 用だけ SHA pin の登録簿を持つ。本体 `main` を進めたら Grok カタログの `sha` も更新する。

カタログの `main` を公開用、`nightly` を開発用とする。

## ライセンス

この登録簿は [MIT](LICENSE)。各プラグインのライセンスは本体 repo を参照。
