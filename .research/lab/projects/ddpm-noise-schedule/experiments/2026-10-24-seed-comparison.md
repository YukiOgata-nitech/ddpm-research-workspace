---
project: ddpm-noise-schedule
record_type: experiment-plan
status: pending
created: 2026-10-24
last_updated: 2026-10-24
spec: ../specs/2026-10-21-schedule-comparison-spec.md
evidence: 2026-10-24-linear-baseline.md
implementation_repository: YukiOgata-nitech/ddpm-noise-schedule
---

# seed 3 つで linear と cosine を比較する

## 目的

研究の問い「cosine は linear より生成の質が上がるか」に、数字で答える。

## 状況

比較スクリプト待ち。cosine の追加と `compare.py` ができたら実行する。

## やること

- linear の sliced Wasserstein 距離（平均 ± 標準偏差）。ベースラインの記録と一致するかも確かめる
- cosine の sliced Wasserstein 距離（平均 ± 標準偏差）
- cosine が linear より小さいか（質が上がったか）を、標準偏差も見て判断する
