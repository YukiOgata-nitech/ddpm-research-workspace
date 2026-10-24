---
project: ddpm-noise-schedule
spec_type: evaluation
status: draft
title: 評価指標と報告の仕方
created: 2026-10-23
last_updated: 2026-10-23
source_brainstorm: ../../../../secretary/notes/brainstorm/2026-10-21-metric.md
related_spec: 2026-10-21-schedule-comparison-spec.md
implementation_repository: YukiOgata-nitech/ddpm-noise-schedule
---

# 評価指標と報告の仕方 spec（下書き）

## 目的

決めた評価指標を、何をどう報告するかの約束事として固める。

## 決定事項（案）

- 指標：生成した 2,000 点と評価用の本物の 2,000 点の sliced Wasserstein 距離（`metrics.py`、小さいほど良い）
- seed 3 つ（0, 1, 2）の平均と標準偏差を報告する。seed によるばらつきまで示し、差が偶然ではないかを読めるようにする

## 未決

- 射影の方向の数（今は 128）で値がどれくらい揺れるか
