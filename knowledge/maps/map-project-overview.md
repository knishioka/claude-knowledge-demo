# 離脱率改善PJ 全体マップ

> **このMOCで分かること**: プロジェクトの全体像、目標、進捗、主要リンク

---

## プロジェクト概要

**目的**: 動画配信アプリ「StreamX」の離脱率改善
**期間**: 2025年12月〜2026年1月（Q1末まで）
**成功指標**: [[note-decision-success-metric]]

| 指標 | 現状 | 目標 | 進捗 |
|------|------|------|------|
| 7日間継続率 | 58% | 64%（+6pt） | +4.6pt達成（Phase1完了時点） |
| 視聴時間 | 12分 | 15分（+3分） | 測定中 |

---

## 体制

[[note-team-structure]]

| 役割 | 担当 |
|------|------|
| PM | 田中 |
| データ | 鈴木 |
| エンジニア | 佐藤 |
| デザイン | 山田 |
| 事業責任者 | 高橋 |

---

## フェーズと進捗

[[note-decision-phase-order]]

| フェーズ | 期間 | 施策 | ステータス |
|---------|------|------|-----------|
| Phase1 | 12月 | オンボーディング改善 | **完了** |
| Phase2 | 1月前半 | 推薦アルゴリズム改善 | 準備中 |
| Phase3 | 1月後半 | プッシュ通知最適化 | 未着手 |

---

## 主要な意思決定

→ 詳細は [[map-decisions]]

| 日付 | 決定事項 | ノート |
|------|---------|--------|
| 12/01 | 成功指標の定義 | [[note-decision-success-metric]] |
| 12/08 | A/Bテスト20%配分 | [[note-decision-ab-test-allocation]] |
| 12/08 | フェーズ優先順位 | [[note-decision-phase-order]] |
| 12/22 | 追加予算350万円承認 | [[note-decision-budget-approval]] |
| 12/22 | 撤退基準の設定 | [[note-decision-exit-criteria]] |

---

## 主要なリスク

→ 詳細は [[map-risks-and-mitigations]]

| リスク | 影響度 | 対応状況 | ノート |
|--------|--------|---------|--------|
| ログ欠損 | 高 | 対策実施済み | [[note-risk-log-loss]] |
| スケジュール遅延 | 高 | 監視中 | [[note-risk-timeline-delay]] |
| スコープ拡大 | 中 | 禁止方針 | [[note-risk-scope-creep]] |

---

## 成果

| 施策 | 効果 | ノート |
|------|------|--------|
| オンボーディング改善 | +4.6pt | [[note-metric-onboarding-result]] |

---

## 未決事項（Open Questions）

| 項目 | 期限 | 担当 | ノート |
|------|------|------|--------|
| ログ取得方式 | 12/10 | 佐藤 | [[note-open-log-method]] |
| RecoTech社契約条件 | 12/25 | 田中 | [[note-open-vendor-selection]] |
| クラウド移行 | 1月中 | インフラ | [[note-open-infra-cloud]] |

---

## 関連リンク

- **inbox**: [[2025-12-01_kickoff_meeting]] / [[2025-12-08_weekly_sync]] / [[2025-12-15_incident_review]] / [[2025-12-22_stakeholder_alignment]]
- **project**: [[projects/churn-reduction-2025/README]]
- **他のMOC**: [[map-decisions]] / [[map-risks-and-mitigations]]
