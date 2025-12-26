---
id: note-risk-timeline-delay
title: スケジュール遅延リスク
created: 2025-12-08
source: [[2025-12-08_weekly_sync]]
---

## Summary（3行）
- Phase1の遅延がPhase2・3に連鎖するリスクあり
- ログ欠損インシデントで実験期間が2日延長
- Q1末の締め切りはタイト、バッファはほぼゼロ

## Tags
#risk #timeline #schedule #dependency

## Links
- [[note-decision-phase-order]]
- [[note-risk-log-loss]]
- [[note-decision-exit-criteria]]

## Body

**リスクの構造**:
```
Phase1遅延 → Phase2開始遅れ → Phase3圧縮/カット → Q1目標未達
```

**発生した遅延**:
| イベント | 影響 | 対応 |
|---------|------|------|
| ログ欠損（12/14） | 実験期間+2日 | 1/17→1/19完了予定 |

**残りバッファ**:
- Q1末（3/31）まで約3ヶ月
- 各フェーズの予備日はほぼゼロ
- さらなる遅延が発生するとPhase3カットの可能性

**対策**:
1. 週次MTGで遅延兆候を早期検知
2. 撤退基準（1/20判定）を設け、ダメなら早めに方針転換
3. スコープ拡大は厳禁（高橋から明言）

## Action
- [ ] 週次でスケジュールリスクを確認（田中、継続）
