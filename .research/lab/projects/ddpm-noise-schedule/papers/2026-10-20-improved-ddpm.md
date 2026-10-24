---
project: ddpm-noise-schedule
date: 2026-10-20
tags: [paper, ddpm, cosine-schedule]
---

# Improved Denoising Diffusion Probabilistic Models（Nichol & Dhariwal, 2021）

## 要旨

DDPM の改良をまとめた論文。このプロジェクトに関係するのは cosine のノイズスケジュール。

## cosine スケジュール

- ᾱ_t = f(t) / f(0)、f(t) = cos²(((t/T + s) / (1 + s)) · π/2)
- s = 0.008。t = 0 付近で β が小さくなりすぎないためのずらし
- β_t = 1 − ᾱ_t / ᾱ_{t−1} は、t = T 付近で 1 に近づくので 0.999 で上限を付ける
- linear は後半でノイズが急に増え、最後の数ステップが情報をほとんど持たない。cosine はノイズの増え方がなだらか

## このプロジェクトでの使い方

- 論文どおりの定義（s = 0.008、上限 0.999）で使う。値を変えると、比べているのが論文の cosine ではなくなる
