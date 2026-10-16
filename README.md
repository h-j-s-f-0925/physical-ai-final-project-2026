# Physical AI 最終課題：SmolVLA × LIBERO-Long

## 概要

学習済みのSmolVLA（Vision-Language-Actionモデル）を使用し、LIBERO-Longのロボット操作タスクを実行・評価するプロジェクトです。

複数のタスクを自動実行し、成功・失敗の記録と実動作動画の生成を行います。

## 目的

- AIによるロボットの複合タスク実行を検証する
- 複数タスクの評価・結果記録・動画生成を自動化する
- 成功例と失敗例を比較し、課題を考察する

## 使用技術

| 項目 | 技術 |
|---|---|
| AIモデル | SmolVLA |
| シミュレーション | LIBERO-Long（LIBERO-10） |
| 実行環境 | Google Colab（GPU） |
| 開発言語 | Python |
| 評価フレームワーク | LeRobot 0.5.1 |
| 動画処理 | FFmpeg |

追加学習は行わず、公開済みの学習済みモデルを使用しています。

## 実行方法

1. `PAI_FinalProject_SmolVLA_LIBERO_Long.ipynb` をGoogle Colabで開く
2. ランタイムをGPUに設定する
3. Notebookのセルを上から順番に実行する
4. `CONFIG` で評価するタスクを指定する
5. `EvaluationPipeline(CONFIG).run()` を実行する
6. 評価結果と生成された動画を確認する

初回実行時は、必要なライブラリとAIモデルを取得します。

## 評価結果

LIBERO-Longの5タスクを各1回実行し、4タスクで成功、1タスクで失敗しました。

成功したタスクだけでなく、失敗したタスクも分析対象として記録しています。

## 出力ファイル

- `task_summary.csv`：評価結果の一覧
- `task_summary.json`：評価結果の詳細
- `clips/`：タスクごとの動画
- `PAI_LIBERO_Long_1x_montage.mp4`：複数タスクを結合した動画

出力先はColab上の `/content/libero_long_eval/` です。

動画は独立したタスクの録画を結合したもので、シミュレーションの動作時間に合わせて再生速度を調整しています。

## 工夫した点

- `dataclass` とクラスを用いた処理の責務分離
- 複数タスクの一括評価と実行結果の再利用
- 成功・失敗を含む評価結果の保存
- 録画FPSとシミュレーション制御周期の違いを考慮した動画生成

## 参考資料

- [LeRobot公式ドキュメント](https://huggingface.co/docs/lerobot/v0.5.1/libero)
- [LIBERO GitHub](https://github.com/Lifelong-Robot-Learning/LIBERO)
- [SmolVLAモデル](https://huggingface.co/HuggingFaceVLA/smolvla_libero)
