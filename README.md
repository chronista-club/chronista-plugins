# Chronista Plugins

Chronista Club の公開プラグインカタログ。Claude Code / Codex の2系統を基本とし、Grok Build は Claude 互換として差分を確認していく。

## プラグイン

| プラグイン | 内容 | 対応状況 |
|---|---|---|
| [chronista-style](https://github.com/chronista-club/plugin-chronista-style) | 開発フロー、共有スキル、hooks、検証規律 | Claude Code / Codex 向け本体をリリース済み。新カタログ経由の実機確認は後続。Grok は未検証 |
| [team-bucciarati](https://github.com/chronista-club/plugin-team-bucciarati) | 調査・テスト・レビューを担う品質チーム | Claude Code / Codex 向け本体をリリース済み。実機確認待ち。Grok は未検証 |
| [vantage-point](https://github.com/chronista-club/plugin-vantage-point) | board・lane・wire と開発フロー | Claude Code / Codex 向け本体をリリース済み。実機確認待ち。Grok は未検証 |
| [creo-memories](https://github.com/chronista-club/plugin-creo-memories) | セッションとホストをまたぐ外部記憶 | Claude Code / Codex 向け本体をリリース済み。実機確認待ち。Grok は未検証 |

この repo は登録簿で、本体は各プラグイン repo で管理する。配布元は本体のリリース済み `main`。版は本体 manifest を正本とし、カタログには複製しない。

4件の本体を新リポジトリへ移植済み。Gemini 対応は今回の対象外。

## 新規導入

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

他の3件も同じコマンドの `chronista-style` をプラグイン名へ置き換えて導入する。導入後は新しいセッション／スレッドを開始する。hooks の依存ツール・信頼設定、記憶サービスへの接続は [本体の導入ガイド](https://github.com/chronista-club/plugin-chronista-style/blob/main/docs/guide/01-installation.md) を参照。

### Grok Build

Claude 互換の構成を基本とする。専用のカタログは先に増やさず、スキル・MCP・hooks を実機で確認し、必要な差分だけ対応する。導入手順は確認後に追加する。

## 旧配布先からの移行

旧 `chronista-club/claude-plugins` と、この repo の marketplace 名はどちらも `chronista-plugins`。旧登録がある環境では、新規導入コマンドだけで切替が完了するとは扱わない。

利用設定の退避、旧登録の解除、新登録からの再導入、更新確認を一つの切替作業として行う。Codex の `chronista-style@personal` を利用中の場合も重複読込を確認する。4件とも新カタログに掲載済み。既存環境の切替と実セッションでの確認は次の作業として行う。

新しい本体 repo を開発の正本とし、旧 repo は現状のまま残す。旧側へ新しい変更を同期する運用は行わない。

## カタログの構成

- `.claude-plugin/marketplace.json`: Claude Code 用
- `.agents/plugins/marketplace.json`: Codex 用

両カタログは同じプラグイン本体を参照する。掲載時には配布構造とテストを検証し、各ホストの実機確認状況を明記する。カタログの `main` を公開用、`nightly` を開発用とする。

## ライセンス

この登録簿は [MIT](LICENSE)。各プラグインのライセンスは本体 repo を参照。
