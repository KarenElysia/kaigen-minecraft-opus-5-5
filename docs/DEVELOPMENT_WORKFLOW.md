# 開発ワークフロー

## 前提

- `hz` はプロジェクト直下に置くエンジンへのリンクで、リポジトリには含まれない（クローズドベータ）。
- `.claude/skills`・`agents`・`hooks` は現在、元の開発者の Windows PC の絶対パスへのリンクになっている。エンジンを手元に用意した後に張り直す（BUG_TRACKER 参照）。

## ビルドと実行

```
hz/hzbuild                       # この PC 向けビルド（Windows は hz\hzbuild）
hz/hzbuild run                   # ビルドして実行
hz/hzbuild --release run         # 最適化ビルド
hz/hzbuild wasm --release run    # WebAssembly ビルド、http://localhost:3000
hz/hzbuild shaders               # シェーダーのみ
```

初回ビルドで全バックエンドのシェーダーがコンパイルされる。

## 1 タスクの流れ

1. docs/ROADMAP.md で現フェーズとタスクを確認する。
2. SYSTEMS_DOCUMENTATION.md と LESSONS_LEARNED.md を読む。
3. 作業用ブランチで実装し、`hz/hzbuild` を通してコンパイルエラーをすべて直す。
4. `--commands` スクリプトで定点スクリーンショットを撮り、変更前と比べる。
5. 該当する docs（CHANGELOG、OPTIMIZATION_LOG、BUG_TRACKER など）を更新する。
6. PR を作り、ユーザーが確認してマージする。

## ファイル所有（サブエージェントの担当）

| 担当 | ファイル |
|---|---|
| ワールド | `wc_gen.c`, `wc_world.c`, `wc_light.c`, `wc_blocks.c` |
| ゲームプレイ | `wc_player.c`, `wc_entities.c`, 今後追加するモブ・クラフト関連 |
| UI | `wc_ui.c`, `wc_touch.c`, `wc_icons.c` |
| 描画 | `wc_render.c`, `wc_render.h`, `wc_mesh*.c`, `wc_textures.c`, `shaders/` |
| 統合（メインセッション） | `wc.h`, `wc_game.h`, `wc_game.c`, ビルド確認, docs/ |
