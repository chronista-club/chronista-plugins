# 旧リポジトリの archive 棚卸し

2026-09-07、ユーザー指示「fleetflowだけそのまま。それ以外はarchiveしよう」に従い、旧 5 repo の README に移行案内を追加して archive した。GitHub API の再取得で全 5 件の `archived: true`、FleetFlow と現行配布先の `archived: false` を確認した。

## 対象と移行先

所有者はすべて `chronista-club`。

| 旧 repo | 移行先 | 状態・残作業 |
|---|---|---|
| claude-plugins | chronista-plugins | 移行案内追加・archive 完了 |
| claude-plugin-chronista-style | plugin-chronista-style | 移行案内追加・archive 完了 |
| claude-plugin-team-bucciarati | plugin-team-bucciarati | 移行案内追加・archive 完了 |
| claude-plugin-vantage-point | plugin-vantage-point | 移行案内追加・archive 完了 |
| claude-plugin-creo-memories | plugin-creo-memories | 移行案内追加・archive 完了 |
| claude-plugin-fleetflow | 対応する新プラグイン repo なし | ユーザー指示で存続。repo・本体 CI とも変更なし |
| claude-plugin-ccwire | — | archive 済み |

`chronista-plugins`、4 つの `plugin-*`、サービス本体の `creo-memories` / `vantage-point` / `fleetflow` は存続対象。

## 確認できたこと

- 4 組の新旧 main の再帰ツリーを比較し、旧側だけに存在するファイルは 0 件。共通ファイルにはホスト共通化等の差分があるため、ファイルの存在だけで全内容の移植完了とは判定しない。
- [plugin-creo-memories #1](https://github.com/chronista-club/plugin-creo-memories/pull/1): 旧 #27 の F-2 移植は MERGED、表示された CI は SUCCESS。
- [creo-memories #864](https://github.com/chronista-club/creo-memories/pull/864): plugin-contract CI の新 repo 切替は MERGED、plugin-contract を含む表示された CI は SUCCESS。
- [旧 VP #18](https://github.com/chronista-club/claude-plugin-vantage-point/pull/18): OPEN。新 main の `hooks/scripts/lane-status.sh` には JSON encoder と `hookSpecificOutput` の修正が存在する。
- [旧 VP #9](https://github.com/chronista-club/claude-plugin-vantage-point/pull/9): OPEN。v0.19 向け conductor/performer への更新。新側 CHANGELOG には後続 v0.20 の整理、v0.22 の Main/Sub 同期、v0.24 の共通化がある。旧 PR の一括適用は巻き戻しになる。
- [旧カタログ #12](https://github.com/chronista-club/claude-plugins/pull/12): OPEN。chronista-style の説明文変更のみ。新カタログには現行の説明があるため、旧カタログに機能変更を加える必要はない。
- 旧 creo の Issue [#1](https://github.com/chronista-club/claude-plugin-creo-memories/issues/1) / [#2](https://github.com/chronista-club/claude-plugin-creo-memories/issues/2) は課金・件数制限。現在のサービス仕様との照合が必要で、実装済みとは未判定。

## 実行と検証

全 5 件の旧 README 本文を保持し、冒頭に保守終了・移行先・同名 marketplace の切替案内を追加した。GitHub から README を再取得し、準備した内容とのバイト一致を確認後、旧プラグイン 4 件、旧カタログの順で archive した。

| repo | README 更新 commit |
|---|---|
| claude-plugin-chronista-style | e0819bd79ee5579445a769e5e130f96f3aaa8fc6 |
| claude-plugin-team-bucciarati | 464b60cb4e526e8f2c61a9e9bc1949a93917c29f |
| claude-plugin-vantage-point | 22c5f43784320226c24b8f0c2d3985d3bef83845 |
| claude-plugin-creo-memories | 0e0786a934290276de3a1e2b1c8b6763b8a9c1ef |
| claude-plugins | 128e507b30b5cc0c3059fddf3c5f613f4970e1a9 |

未完 PR / Issue は履歴として保持し、一括終了・コメント送信は行っていない。上記の棚卸し結果と存続方針を creo に記録する。

## 別途残る案内の整理

今回の archive には含めず、以下の参照を記録する。

- `plugin-chronista-style` の旧カタログ／creo への案内。
- `plugin-creo-memories` README の「CI 切替は未実施」という古い記述。
- 組織プロフィール `.github/profile/README.md` の旧 repo への導線、`anycreative.tech/src/data/extra.ts` の参照。旧 README の移行案内を経由して新配布先へ到達できる。
- FleetFlow の release CI は旧プラグインとの版一致に依存する。今回は双方存続のため変更不要。

## 調査の範囲

組織の repo 一覧、対象 main のツリー、上記 PR / Issue、GitHub code search と現行ローカル repo の旧名参照を確認した。code search には索引更新の遅れがあるため、組織全体の全 branch・全参照を網羅したとは扱わない。手元の全ホストの再導入・実セッション確認は今回未実施。
