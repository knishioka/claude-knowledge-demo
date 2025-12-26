---
id: note-decision-phase-order
title: 施策フェーズの優先順位決定
created: 2025-12-08
source: [[2025-12-08_weekly_sync]]
---

## Summary（3行）
- Phase1: オンボーディング改善（12月）
- Phase2: 推薦アルゴリズム改善（1月前半）
- Phase3: プッシュ通知最適化（1月後半）

## Tags
#decision #roadmap #priority #planning

## Links
- [[note-decision-success-metric]]
- [[note-data-recommendation-log]]
- [[note-risk-scope-creep]]

## Body

3つの施策候補（オンボーディング、推薦、プッシュ）の優先順位を決定した。

**オンボーディングを最優先にした理由**:
1. 実装工数が最も小さい（2週間）
2. 新規ユーザーのDay3離脱が42%と突出しており、最も効果が期待できる
3. 推薦改善のデータ収集と並行できる

**推薦を2番目にした理由**:
- 離脱理由調査で「見たいコンテンツがない」が58%と最多
- ただしデータ準備に時間がかかるため、Phase1から並行してログ収集を開始

**プッシュを最後にした理由**:
- 効果は期待できるが、他2つより優先度が低い
- 時間が足りなければスコープから外す可能性あり

## Action
- [x] ロードマップを更新（田中、12/09完了）
