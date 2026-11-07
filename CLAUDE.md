@AGENTS.md

# WebCraft — ゲーム開発方針

## 優先順位

AGENTS.md のハードルール（libc禁止、グローバル禁止、lock-step、エンジン不可侵）> 本ファイル > docs/。

## 開発の進め方

- 作業は docs/ROADMAP.md の現フェーズの範囲だけ行う。フェーズ完了時は下の「作業報告」形式で報告し、承認を待つ。
- 実装前に docs/SYSTEMS_DOCUMENTATION.md と docs/LESSONS_LEARNED.md を読む。
- 完了条件: `hz/hzbuild` 成功、`--commands` スクリプトでのスクリーンショット確認、該当 docs の更新。
- 性能予算: デスクトップ 60fps、モバイル 30fps。性能に触れる変更は前後の F3 計測値を docs/OPTIMIZATION_LOG.md に記録する。
- 不具合は場当たりで直さず根本原因を調べ、docs/BUG_TRACKER.md と docs/LESSONS_LEARNED.md に残す。
- 外部ライブラリは使えない。技術調査は「エンジン内の既存機能」（wiki/index.md、hz-* スキル）を対象にする。

## 修正指示を受けたら

1. 意図を確認し、現在の実装が期待と違う理由を分析する。
2. 修正し、同じ問題が他の箇所にないか検索する。
3. 再利用できるルールを docs/USER_PREFERENCES.md に「明示」と「推測」を分けて記録する。

## ユーザーに確認する判断

- ゲームルールの追加・削除、マネタイズ、公開方針。
- エンジン（`src/engine/`, `src/lib/`, `src/os/`）の変更が必要な場合。触らずに報告する。

## サブエージェントの作業範囲

複数のエージェントが同じファイルを同時に編集しない。担当は docs/DEVELOPMENT_WORKFLOW.md の「ファイル所有」に従う。
`wc.h`、`wc_game.h`、`wc_game.c` の変更とビルド確認は統合担当（メインセッション）だけが行う。

## 作業報告の形式

【完了した作業】【動作確認】【品質評価】【未解決事項】【次のフェーズ】【ユーザーへの確認事項】
