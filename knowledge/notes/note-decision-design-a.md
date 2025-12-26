---
id: note-decision-design-a
title: オンボーディングデザインA案の採用
created: 2025-12-11
source: [[2025-12-11_design_review]]
---

## Summary（3行）
- ジャンル選択ステップ追加（A案）を採用
- 8カテゴリから最低1つ、最大3つを選択
- 12/12からA/Bテスト開始

## Tags
#decision #design #onboarding #ab-test

## Links
- [[note-decision-ab-test-allocation]]
- [[note-metric-onboarding-result]]
- [[note-data-churn-analysis]]

## Body

デザインレビューで3案（A:ジャンル選択、B:チュートリアル、C:キュレーション推薦）を比較し、A案を採用した。

**選定理由**:
1. 離脱理由の最大要因「見たいコンテンツがない」（58%）に直接対処
2. データ分析結果（Day3離脱42%）と整合
3. 推薦精度向上との相乗効果が期待できる

**仕様**:
- 初回起動時に好きなジャンルを選択
- カテゴリ数: 8つ
- 選択数: 最低1つ、最大3つ
- スキップ不可（必須ステップ）

**懸念点**:
所要時間+15秒で離脱リスクあり → シンプルなUIで対処

## Action
- [x] A/Bテスト実装完了（佐藤、12/12）
