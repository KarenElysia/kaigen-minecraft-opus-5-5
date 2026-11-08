# システム一覧

| ファイル | 責務 | 主な入出力・連携 |
|---|---|---|
| `wc_game.c` / `wc_game.h` | エントリーポイント、ゲームループ、モード遷移、入力、スクリプトコマンド | 全システムを呼ぶ。モード: LOADING / MENU / PLAYING / PAUSED / INVENTORY / SETTINGS / ERROR |
| `wc_world.c` | チャンク格子、ストリーミング、ジョブスケジューリング | gen / light / mesh を呼ぶ。`WcEditStore` と `WcMeshStore` を保持 |
| `wc_gen.c` | 地形生成: ノイズ、バイオーム、洞窟、鉱石、木、水、スポーン地点 | `wc_blocks.c` のノイズを使う |
| `wc_blocks.c` | ブロック定義、シンプレックスノイズ、草・葉・水の色 | 生成・メッシュ・アイコンが参照 |
| `wc_light.c` | 空光とブロック光の伝播・逆伝播（3×3 チャンク窓） | ブロック変更時に `wc_light_block_changed` |
| `wc_mesh.c` | セクション（16³）単位のメッシュ化、面バケット分け | 出力は quad レコード。角の計算は `shaders/wc_quad.glsl` |
| `wc_mesh_store.c` | GPU メッシュプール（最大 32 プール × 2^20 quad） | `wc_render.c` が描画 |
| `wc_render.c` / `wc_render.h` | 全描画パス、ターゲット、パイプライン | TECHNICAL_ARCHITECTURE.md の描画パス |
| `wc_textures.c` | 16×16 の手続きテクスチャ（albedo、normal+height、specular） | `wc_icons.c` が流用 |
| `wc_icons.c` | インベントリ用アイソメトリックアイコンを CPU でラスタライズ | UI が使用 |
| `wc_player.c` | 一人称物理（AABB 対ボクセル、ダッシュ、スニーク、水泳、飛行）、レイキャスト | `wc_world.c` を参照 |
| `wc_entities.c` | パーティクル、ホタル、手に持ったブロック | G-buffer に描画 |
| `wc_audio.c` | 手続き効果音（破壊・設置・足音・水しぶき）、雷、雨 | エンジンの `procgen/pg_audio.h` |
| `wc_ui.c` | メニュー、設定、HUD、インベントリ、統計パネル | エンジン UI |
| `wc_touch.c` | モバイルのタッチ操作 | `wc_ui.c` のボタン配置 |
| `wc_settings.c` | 画質プリセット（LOW / MEDIUM / HIGH / ULTRA / CUSTOM）と描画設定への変換 | `wc_render.c` |
| `wc_storage.c` | プレイヤーの編集をチャンクごとに記録 | `wc_world.c` が再生成時に適用 |

## スクリプトコマンド（`--commands` 用）

`wc_game.c` が登録: `wc_view`（位置・向き・時刻・飛行・スケール）、`wc_play`、`wc_mode`、`wc_preset`、`wc_setblock`、`wc_seed`、`wc_hud`。
定点スクリーンショットの検証に使う。
