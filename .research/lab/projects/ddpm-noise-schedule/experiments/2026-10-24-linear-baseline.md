---
project: ddpm-noise-schedule
record_type: evidence
status: done
created: 2026-10-24
last_updated: 2026-10-24
spec: ../specs/2026-10-21-schedule-comparison-spec.md
implementation_repository: YukiOgata-nitech/ddpm-noise-schedule
implementation_reference_commit: 34d26ee9018dd8ab02ce2bb4d6d6ee7d0dd09cfe
---

# linear のベースライン

## 結論

linear スケジュールの sliced Wasserstein 距離は、seed 3 つで 1.950 ± 0.129（平均 ± 標準偏差）。cosine と比べるときの基準にする。

## 条件

- `baseline.py`（spec の B1・B2 の条件。T = 200、3,000 ステップ、元のスケールで測る）
- CPU

## 結果

| seed | SW |
|---|---|
| 0 | 1.768 |
| 1 | 2.052 |
| 2 | 2.031 |
| 平均 ± 標準偏差 | 1.950 ± 0.129 |
