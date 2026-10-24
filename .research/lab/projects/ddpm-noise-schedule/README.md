---
project: ddpm-noise-schedule
status: active
summary: linear と cosine のノイズスケジュールを同じ条件で比べる。比較実験の spec は承認済み、評価指標の spec は下書き。linear のベースラインは seed 3 つで SW = 1.950 ± 0.129。比較スクリプト（cosine と compare.py）はこれから。
implementation_repository: YukiOgata-nitech/ddpm-noise-schedule
created: 2026-10-20
last_updated: 2026-10-24
---

# DDPM のノイズスケジュールの比較

## 概要

拡散モデル（DDPM）で、ノイズスケジュールを linear から cosine に変えると生成の質が上がるかを、2次元のトイデータ（swiss roll）で調べる。CPU だけで1回の学習が数秒で終わる小さな設定にして、条件をそろえた比較を何度でもやり直せるようにする。

## 研究の問い・手法・評価

- 問い：cosine スケジュールは linear スケジュールより生成の質が上がるか
- 手法：提案側は cosine（Nichol & Dhariwal, 2021。s = 0.008、β の上限 0.999）、ベースラインは linear（Ho et al., 2020。β を 1e-4 から 0.02 まで線形）。データ・モデル・T・学習の設定・サンプリングはそろえ、変えるのはスケジュールだけ
- 評価：生成した 2,000 点と本物の 2,000 点の sliced Wasserstein 距離（元のスケールのまま測る）を、seed 3 つの平均と標準偏差で比べる

## 実装環境

- 実装リポジトリ：`YukiOgata-nitech/ddpm-noise-schedule`
- 研究の文脈の正本：この README と、同じプロジェクトの `specs/`、`experiments/`、`meetings/`、`materials/`、`papers/`

## マイルストーン

- [ ] linear と cosine を同じ条件で比べる
- [ ] 評価指標を決める
- [ ] ゼミで中間報告する

## 現在の状況

2026-10-20 に比べるスケジュールの候補を洗い出し、linear と cosine の2つに絞った（[壁打ち](../../../secretary/notes/brainstorm/2026-10-20-schedule-candidates.md)）。sigmoid も候補に挙げたが、比較に入れないことにした。

2026-10-21 に比較実験の約束事を [spec](specs/2026-10-21-schedule-comparison-spec.md) にまとめ、承認された。

2026-10-22 のゼミで、生成した点には本物の点との1対1の対応が無いので、点の集まりどうしの距離で測るよう指摘を受けた（[記録](meetings/2026-10-22-seminar.md)）。これを受けて評価指標を見直し、FID・IS ではなく sliced Wasserstein 距離を使う方向にした（[壁打ち](../../../secretary/notes/brainstorm/2026-10-21-metric.md)）。報告の仕方は [評価指標の spec](specs/2026-10-23-metric-spec.md)（下書き）にまとめている。

2026-10-24 に linear のベースラインを seed 3 つで測った（SW = 1.950 ± 0.129、[記録](experiments/2026-10-24-linear-baseline.md)）。cosine の追加と比較スクリプトはこれからで、seed 比較の実験はそれ待ち（[記録](experiments/2026-10-24-seed-comparison.md)）。
