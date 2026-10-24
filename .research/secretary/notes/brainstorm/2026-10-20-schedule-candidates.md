---
project: ddpm-noise-schedule
date: 2026-10-20
status: concluded
tags: [brainstorm, ddpm, noise-schedule]
---

# 比べるノイズスケジュールの候補

## 出発点

「ノイズスケジュールを変えると生成の質が上がるか」を調べたい。まず、何と何を比べるかを決める。

## 候補

- linear（Ho et al., 2020）：β を 1e-4 から 0.02 まで線形に増やす。DDPM の元の設定で、比べる相手（ベースライン）にする
- cosine（Nichol & Dhariwal, 2021）：ᾱ_t を cosine で決める。s = 0.008、β の上限 0.999。後半でノイズが急に増えすぎないとされる（[論文メモ](../../../lab/projects/ddpm-noise-schedule/papers/2026-10-20-improved-ddpm.md)）
- sigmoid：第3の候補として挙げた

## 結論

- linear と cosine の2つで比べる
- sigmoid は入れない。3つ以上で比べると差の原因を切り分けにくく、問いは linear との比較だけで答えられるため

## 気になること（未決）

- 学習やサンプリングが不安定になったときにどう扱うか。比べる2つで扱いが違うと公平でなくなるので、比べる前に決めておきたい
  - 学習率を下げる（スケジュールの条件は変えずに済む）
