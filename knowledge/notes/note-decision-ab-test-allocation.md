---
id: note-decision-ab-test-allocation
title: A/Bテストのトラフィック配分を20%に決定
created: 2025-12-08
source: [[2025-12-08_weekly_sync]]
---

## Summary（3行）
- A/Bテストのトラフィック配分は20%に決定
- 10%では統計的有意性の確保に時間がかかりすぎる
- 2週間で有意な結果を得るための最低ライン

## Tags
#decision #experiment #ab-test #statistics

## Links
- [[note-metric-onboarding-result]]
- [[note-decision-success-metric]]
- [[note-risk-timeline-delay]]

## Body

週次MTGで、A/Bテストのトラフィック配分について議論。当初は既存ユーザー体験への影響を懸念して10%案もあったが、鈴木の統計分析により20%が必要と判断。

**10%配分の場合**:
- 有意な結果を得るまで4週間以上
- Q1目標達成が困難に

**20%配分の場合**:
- 2週間で統計的有意性（p < 0.05）を達成可能
- リスクは許容範囲内

チームとして「スピード優先」の意思決定を行った。

## Action
- [x] A/Bテスト設計書にトラフィック配分を反映（鈴木、12/12完了）
