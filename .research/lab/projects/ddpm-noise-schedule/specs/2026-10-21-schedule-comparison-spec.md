---
project: ddpm-noise-schedule
spec_type: experiment
status: approved
approval: approved
title: linear と cosine のノイズスケジュールの比較実験
created: 2026-10-21
last_updated: 2026-10-21
source_brainstorm: ../../../../secretary/notes/brainstorm/2026-10-20-schedule-candidates.md
implementation_repository: YukiOgata-nitech/ddpm-noise-schedule
---

# linear と cosine のノイズスケジュールの比較実験 spec

## 目的

2つのノイズスケジュールを同じ条件で比べ、「cosine は linear より生成の質が上がるか」に答える。

## 決定事項

### B1 データ・モデル・T・学習の設定を両者でそろえる

- データ：swiss roll（学習用 2,000 点は seed 0、評価用 2,000 点は seed 100）
- モデル：`ddpm.py` の `Denoiser`（隠れ層 128 の MLP）
- 拡散のステップ数 T = 200
- 学習：3,000 ステップ、バッチサイズ 256、学習率 1e-3
- サンプリング：`ddpm.py` の `sample`
- 変えるのはスケジュールだけ。スケジュール以外の差が結果に混ざらないようにする

### B2 評価はデータの元のスケールのまま測る

距離の値の意味をそろえ、ベースラインの結果や README の基準と比べられるようにする。

### B3 cosine は論文どおりの定義（β の上限 0.999）で使う

s = 0.008、β の上限 0.999。比べているのが本来の cosine だと言えるようにし、結論を cosine そのものについて述べられるようにする。

## 実装

- `ddpm.py` の `get_betas` に cosine を足す
- linear と cosine を seed 3 つで学習して測る `compare.py` を作る
