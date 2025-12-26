# Knowledge Repository Demo

**外部脳（Second Brain）のデモ用リポジトリ**

忙しいPM・経営者が「必要な情報を必要なときに取り出せる」体験を実現するナレッジ管理システム。

---

## 概要

このリポジトリは **Collect → Distill → Connect → Use** のワークフローを実装した「外部脳」のデモです。

```
┌─────────────────────────────────────────────────────────────┐
│                      Knowledge Flow                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📥 COLLECT        📝 DISTILL       🔗 CONNECT      🎯 USE  │
│  ─────────        ──────────       ──────────      ────────│
│  inbox/           notes/           maps/           projects/│
│  ・議事録          ・1ノート1アイデア  ・テーマ別索引     ・実務適用 │
│  ・メモ            ・要点化          ・関連発見        ・意思決定 │
│  ・情報源          ・リンク付け       ・俯瞰           ・アクション│
│                                                             │
│           ───────>  ───────>  ───────>  ───────>            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## ディレクトリ構造

```
.
├── README.md                    # このファイル
├── knowledge/
│   ├── inbox/                   # 📥 COLLECT: 生の議事録・メモ
│   │   ├── 2025-12-01_kickoff_meeting.md
│   │   ├── 2025-12-08_weekly_sync.md
│   │   ├── 2025-12-15_incident_review.md
│   │   └── 2025-12-22_stakeholder_alignment.md
│   │
│   ├── notes/                   # 📝 DISTILL: アトミックノート
│   │   ├── note-decision-*.md   # 意思決定
│   │   ├── note-metric-*.md     # 指標・KPI
│   │   ├── note-risk-*.md       # リスク
│   │   └── ...                  # 15+ ノート
│   │
│   ├── maps/                    # 🔗 CONNECT: MOC（索引）
│   │   ├── map-project-overview.md
│   │   ├── map-decisions.md
│   │   └── map-risks-and-mitigations.md
│   │
│   └── projects/                # 🎯 USE: 案件フォルダ
│       └── churn-reduction-2025/
│           ├── README.md
│           ├── decisions.md
│           ├── roadmap.md
│           ├── risks.md
│           └── open-questions.md
│
└── .claude/
    ├── commands/                # Slash Commands
    │   ├── distill.md
    │   ├── moc.md
    │   ├── ask.md
    │   ├── weekly-review.md
    │   └── capture.md
    │
    └── agents/                  # Subagents
        ├── note-distiller.md
        ├── knowledge-qa.md
        └── moc-builder.md
```

---

## Slash Command 一覧

| コマンド | 説明 | 呼び出すSubagent | 例 |
|---------|------|-----------------|-----|
| `/distill` | inboxメモをアトミックノートに分割 | **note-distiller** | `/distill 2025-12-01_kickoff_meeting.md` |
| `/moc` | テーマ別MOC（索引）を生成・更新 | **moc-builder** | `/moc decisions` |
| `/ask` | 質問に根拠リンク付きで回答 | **knowledge-qa** | `/ask 意思決定は何？根拠は？` |
| `/weekly-review` | 週次の棚卸しと要約 | （直接実行） | `/weekly-review` |
| `/capture` | 30秒でinboxに入れるテンプレ | （直接実行） | `/capture 新しいアイデア` |

---

## Subagent 一覧

```
┌─────────────────────────────────────────────────────────────┐
│                  司令塔（メインClaude）                       │
│     ・全体を俯瞰、ユーザーと対話                              │
│     ・Subagentに作業を委譲                                   │
└───────────────────┬─────────────────────────────────────────┘
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
┌───────────┐ ┌───────────┐ ┌───────────┐
│note-      │ │knowledge- │ │moc-       │
│distiller  │ │qa         │ │builder    │
├───────────┤ ├───────────┤ ├───────────┤
│inbox→notes│ │質問応答    │ │索引構築    │
│1ノート1概念 │ │根拠リンク  │ │関連発見    │
│要点化      │ │不足指摘    │ │俯瞰整理    │
└───────────┘ └───────────┘ └───────────┘
```

| Subagent | 役割 | 入力 | 出力 |
|----------|------|------|------|
| **note-distiller** | inbox→アトミックノート化 | 議事録 | notes/へ保存するMD案 |
| **knowledge-qa** | 質問応答（根拠付き） | 質問文 | 結論→根拠→補足→次アクション |
| **moc-builder** | MOC構築・更新 | テーマ | maps/へ保存するMD案 |

---

## デモの進め方

### クイックデモ（3分）

```
/ask 来週までに対応すべきリスクは？
```

これだけで以下が自動的に行われる：

1. **knowledge-qa** Subagentが起動
2. notes/, maps/, projects/ を横断検索
3. 根拠リンク付きで回答を生成

**実行結果**:
```markdown
## 結論
スケジュール遅延リスクとベンダー契約が最優先。Phase1の遅延がQ1目標未達に
直結する構造であり、RecoTech社との契約条件交渉（期限: 12/25）が喫緊の対応事項。

## 根拠
- [[note-risk-timeline-delay]]: Phase1遅延→Phase2遅れ→Phase3カット→Q1未達の連鎖リスク
- [[note-open-vendor-selection]]: RecoTech社契約条件を12/25までに確定する必要あり
- [[note-risk-scope-creep]]: スコープ拡大禁止の方針。追加要望は「次PJ候補リスト」へ

## 補足
ログ欠損インシデント（12/14）の再発防止策は完了済み（[[note-risk-log-loss]]）。
アラート設定、ログローテーション修正、設定変更PRレビュー必須化が導入された。

## 次アクション
- [ ] RecoTech社と契約条件交渉完了（田中、12/25）
- [ ] 交渉結果を経営に報告（田中、12/26）
- [ ] 週次MTGでスケジュールリスクを確認（田中、継続）

---
**参照ノート**: [[note-risk-timeline-delay]], [[note-open-vendor-selection]],
[[note-risk-scope-creep]], [[note-risk-log-loss]]
```

**ポイント**: 「推測で埋めない」ため、ノートにない情報は「不明」と回答する

---

### フルデモ（7分）

#### Step 1: 生の議事録を見せる（1分）

```bash
cat knowledge/inbox/2025-12-11_design_review.md
```

「107行の議事録。情報の宝庫だが、このままでは再利用しにくい。」

---

#### Step 2: /distill で自動分割（2分）

```
/distill 2025-12-11_design_review.md
```

**note-distiller** Subagentが起動し、以下を自動実行：

| 処理 | 内容 |
|------|------|
| 1. 読み込み | inbox/2025-12-11_design_review.md |
| 2. 抽出 | 8カテゴリに分類しながらアイデアを抽出 |
| 3. 重複チェック | 既存notes/と照合（重複はスキップ） |
| 4. 変換 | テンプレートに従いノート形式に変換 |
| 5. 確認 | ユーザーに保存確認 |

**出力例**:
```
## /distill 結果

### 分析サマリー
| 状態 | 内容 |
|------|------|
| 重複（スキップ） | 意思決定「A案採用」→ note-decision-design-a.md 既存 |
| 新規抽出 | 4件 |

### 抽出したノート（4件）

1. **note-insight-design-alternatives** - 不採用デザイン案の比較
   - Summary: B案・C案は推薦に直接寄与せず不採用
   - Links: [[note-decision-design-a]], [[note-data-churn-analysis]]

2. **note-risk-onboarding-friction** - オンボーディング摩擦リスク
   - Summary: ジャンル選択+15秒で離脱増加の可能性
   - Links: [[note-decision-design-a]]

3. **note-open-genre-ui-detail** - ジャンル選択UI詳細
   - Summary: アイコン・配置の詳細が未確定
   - Links: [[note-open-log-method]]

4. **note-data-implementation-estimate** - 実装工数見積もり
   - Summary: A案3日、B案2日、C案1日
   - Links: [[note-team-structure]]

### 確認
上記のノートを knowledge/notes/ に作成してよいですか？
```

**ポイント**: 「1ノート1アイデア」「コピペ禁止（自分の言葉で要約）」「Links必須」

---

#### Step 3: /moc で索引を更新（2分）

```
/moc decisions
```

**moc-builder** Subagentが起動し、以下を自動実行：

| 処理 | 内容 |
|------|------|
| 1. 収集 | notes/note-decision-*.md を全取得 |
| 2. 差分検出 | 既存MAPと比較、新規ノートを発見 |
| 3. 構造設計 | サマリー表、セクション分け、未決事項 |
| 4. 生成 | テンプレートに従いMOCを生成 |
| 5. 確認 | ユーザーに保存確認 |

**出力例**:
```
## /moc decisions 結果

### 差分分析
| 状態 | ノート |
|------|--------|
| 既存 | 5件 |
| 新規発見 | note-decision-design-a（12/11 デザインA案採用）|

### 更新後のMOC（抜粋）

# 意思決定マップ

> **このMOCで分かること**: いつ、何を、なぜ決めたか

## サマリー（5件 → 6件に更新）

| # | 日付 | 決定事項 | ノート |
|---|------|---------|--------|
| 1 | 12/01 | 成功指標の定義 | [[note-decision-success-metric]] |
| 2 | 12/08 | A/Bテスト配分20% | [[note-decision-ab-test-allocation]] |
| 3 | 12/08 | フェーズ優先順位 | [[note-decision-phase-order]] |
| 4 | 12/11 | デザインA案採用【NEW】| [[note-decision-design-a]] |
| 5 | 12/22 | 追加予算承認 | [[note-decision-budget-approval]] |
| 6 | 12/22 | 撤退基準 | [[note-decision-exit-criteria]] |

### 確認
knowledge/maps/map-decisions.md を更新してよいですか？
```

**ポイント**: 「リンク最低8本」「未決事項セクション必須」「入口として読みやすく」

---

#### Step 4: /ask で知識を活用（2分）

```
/ask 離脱率改善PJの成功指標は何に決まった？根拠は？
```

**knowledge-qa** Subagentが起動：

```
## 結論
7日間継続率 +6pt（58%→64%）、視聴時間 +3分（12分→15分）を目標に設定。

## 根拠
- [[note-decision-success-metric]]: キックオフMTGでチーム合意
- [[note-metric-retention-7day]]: LTVとの相関分析結果

## 補足
計測期間は6週間（2025-01-15まで）。鈴木のデータ分析で7日間継続率が
LTVと最も相関することが判明し、6pt改善でLTV約8%向上の試算。

## 次アクション
- [ ] 1/15に最終判定、結果を経営MTGで報告

---
**参照ノート**: [[note-decision-success-metric]], [[note-metric-retention-7day]]
```

**ポイント**: 「推測で埋めない（情報がなければ『不明』と明示）」「根拠リンク必須」

---

## Slash Command と Subagent の関係

```
┌─────────────────────────────────────────────────────────────────────┐
│                          ユーザー                                    │
│                            │                                        │
│                      Slash Command                                  │
│                     ┌──────┴──────┐                                 │
│                     ▼             ▼                                 │
│              ┌──────────┐  ┌──────────┐                             │
│              │ /distill │  │  /ask    │  ...                        │
│              └────┬─────┘  └────┬─────┘                             │
│                   │             │                                   │
│          Subagent │を起動       │ Subagentを起動                     │
│                   ▼             ▼                                   │
│           ┌─────────────┐ ┌─────────────┐                           │
│           │note-distiller│ │knowledge-qa │                          │
│           ├─────────────┤ ├─────────────┤                           │
│           │・inbox読込   │ │・notes検索  │                           │
│           │・カテゴリ分類│ │・根拠抽出   │                           │
│           │・重複チェック│ │・回答生成   │                           │
│           │・ノート生成  │ │・不足指摘   │                           │
│           └─────────────┘ └─────────────┘                           │
│                   │             │                                   │
│                   ▼             ▼                                   │
│              knowledge/     ユーザーへ                               │
│              notes/へ保存    回答を返す                              │
└─────────────────────────────────────────────────────────────────────┘
```

### なぜこの構成が便利なのか？

| 観点 | 効果 |
|------|------|
| **標準化** | 誰がやっても同じ品質のノートが作れる |
| **効率化** | 107行の議事録 → 4つのノート（5分で完了） |
| **一貫性** | テンプレートに従うため、フォーマットが統一される |
| **発見** | 重複チェック・差分検出で、関連ノートを自動発見 |
| **信頼性** | 「推測で埋めない」ルールで、誤情報を防ぐ |

---

## 追加デモ（オプション）

### /capture - 30秒でメモを残す

```
/capture 新機能アイデア
```

**実行結果**:
```markdown
## /capture 結果

### テンプレート

# 新機能アイデア

**日時**: 2025-12-26
**文脈**: {どんな状況で思いついたか}

---

## アイデアの概要
（3行以内で）

## 背景・きっかけ
-

## 期待される効果
-

## 懸念・リスク
-

## 次のステップ
- [ ] {まず何をすべきか}

---
*関連: [[...]]*

### 保存先
`knowledge/inbox/2025-12-26_idea_new-feature.md`

---
このテンプレートをinboxに作成してよいですか？
```

**ポイント**: 入力キーワード「アイデア」から自動でテンプレートタイプを判定

---

### /weekly-review - 週次の棚卸し

```
/weekly-review
```

**実行結果**:
```markdown
# 週次レビュー（2025-12-26）

## 1. inbox 棚卸し

### Distill候補（要処理）
| ファイル | 理由 |
|---------|------|
| 2025-12-11_design_review.md | 不採用案・UI詳細は未ノート化 |
| 2025-12-18_kpi_review.md | 未処理 |

### アーカイブ候補
| ファイル | 理由 |
|---------|------|
| 2025-12-01_kickoff_meeting.md | 主要ノート作成済み |
| 2025-12-08_weekly_sync.md | 主要ノート作成済み |
| 2025-12-15_incident_review.md | note-risk-log-loss 作成済み |
| 2025-12-22_stakeholder_alignment.md | 予算承認・撤退基準ノート作成済み |

## 2. 今週の意思決定

| 日付 | 決定事項 | ノート |
|------|---------|--------|
| 12/22 | 追加予算350万円承認 | [[note-decision-budget-approval]] |
| 12/22 | 撤退基準（+1pt未満で中止） | [[note-decision-exit-criteria]] |
| 12/11 | デザインA案採用 | [[note-decision-design-a]] |

## 3. 未決事項（期限注意）

| 項目 | 期限 | 残り日数 | 担当 |
|------|------|---------|------|
| RecoTech契約条件 | 12/25 | **-1日（超過）** | 田中 |
| ログ取得方式 | 12/10 | 超過 | 佐藤 |
| クラウド移行 | 1月中 | 余裕あり | インフラ |

## 4. 要注意リスク

| リスク | ステータス | 次アクション |
|--------|-----------|-------------|
| スケジュール遅延 | ⚠️ 監視中 | 週次MTGで確認継続 |
| スコープ拡大 | ✅ 抑制中 | 追加要望は次PJ候補へ |
| ログ欠損 | ✅ 対策完了 | アラート設定済み |

## 5. 次週のアクション

| アクション | 担当 | 期限 | ステータス |
|-----------|------|------|-----------|
| RecoTech社契約交渉完了 | 田中 | 12/25 | **要確認** |
| エンジニア追加手配 | 田中 | 12/26 | 未着手 |
| PoC計画書作成 | 鈴木 | 12/27 | 未着手 |
| オンボーディング本番反映 | 佐藤 | 12/28 | 未着手 |

---
**処理候補**:
- `/distill 2025-12-18_kpi_review.md` を実行しますか？
- `projects/churn-reduction-2025/README.md` を更新しますか？
```

**ポイント**: inbox棚卸し、未決事項の期限チェック、リスク状況を一覧化

---

## デモ用の質問例

| カテゴリ | 質問例 |
|---------|--------|
| **意思決定** | 「離脱率改善PJの成功指標は何に決まった？根拠は？」 |
| **未決事項** | 「まだ決まっていないことは何？期限は？」 |
| **リスク** | 「来週までに対応が必要なリスクは？」 |
| **進捗** | 「今週完了したことと、来週の予定は？」 |
| **データ** | 「推薦改善に必要なデータ要件は？」 |
| **体制** | 「誰が何を担当している？」 |
| **経緯** | 「A/Bテストの方針はいつどう決まった？」 |

---

## このRepoを自分用に転用する方法

### 最小のカスタム手順

1. **inbox/ をクリア**して自分の議事録を入れる
2. **notes/ をクリア**して `/distill` で再生成
3. **maps/ をクリア**して `/moc` で再生成
4. **projects/** のフォルダ名を変更し、自分の案件情報を入れる

### カスタマイズポイント

- `notes/` のタグ体系を自分のドメインに合わせる
- `maps/` のMOCテーマを追加（技術、組織、顧客など）
- `.claude/commands/` に独自コマンドを追加
- `.claude/agents/` のSubagentを調整

---

## 設計原則

1. **1ノート1アイデア**：検索・再利用しやすい粒度
2. **リンクで繋ぐ**：孤立したノートを作らない
3. **Summary必須**：3行で要点が分かる
4. **推測で埋めない**：不明点は明示、追加調査を促す
5. **型で効率化**：Slash Command + Subagent で手順を標準化

---

## 作成されたファイル一覧

### knowledge/inbox/（4ファイル）
| ファイル | 内容 |
|---------|------|
| 2025-12-01_kickoff_meeting.md | キックオフMTG議事録 |
| 2025-12-08_weekly_sync.md | 週次進捗MTG議事録 |
| 2025-12-15_incident_review.md | 障害レビュー議事録 |
| 2025-12-22_stakeholder_alignment.md | 経営MTG議事録 |

### knowledge/notes/（17ファイル）
| カテゴリ | ファイル数 | 例 |
|---------|-----------|-----|
| decision | 5 | note-decision-success-metric, note-decision-budget-approval |
| metric | 3 | note-metric-retention-7day, note-metric-onboarding-result |
| risk | 3 | note-risk-log-loss, note-risk-timeline-delay |
| data | 2 | note-data-recommendation-log, note-data-churn-analysis |
| open | 3 | note-open-log-method, note-open-vendor-selection |
| other | 1 | note-team-structure |

### knowledge/maps/（3ファイル）
| ファイル | 内容 |
|---------|------|
| map-project-overview.md | プロジェクト全体像 |
| map-decisions.md | 意思決定の索引 |
| map-risks-and-mitigations.md | リスクと対応の索引 |

### knowledge/projects/churn-reduction-2025/（5ファイル）
| ファイル | 内容 |
|---------|------|
| README.md | プロジェクト概要・今週の状況 |
| decisions.md | 意思決定ログ |
| roadmap.md | ロードマップ |
| risks.md | リスク一覧 |
| open-questions.md | 未決事項 |

### .claude/commands/（5ファイル）
| コマンド | 説明 |
|---------|------|
| distill.md | inboxをアトミックノート化 |
| moc.md | MOC生成・更新 |
| ask.md | 質問応答 |
| weekly-review.md | 週次レビュー |
| capture.md | クイックキャプチャ |

### .claude/agents/（3ファイル）
| エージェント | 役割 |
|-------------|------|
| note-distiller.md | ノート分割の専門家 |
| knowledge-qa.md | 質問応答の専門家 |
| moc-builder.md | 索引構築の専門家 |

---

## よくある質問

### Q: Obsidianとの違いは？
A: Obsidianはツール、これは「運用の型」です。Obsidianでも使えます。

### Q: 既存の議事録システムとどう連携する？
A: 議事録をinbox/に入れて `/distill` するだけ。

### Q: チームで使える？
A: Gitで共有すれば複数人で使えます。コンフリクトはMergeで解決。

### Q: どのくらいのノート数が適切？
A: 数百〜数千ノートでも、MOCとリンクがあれば問題なし。

---

*このリポジトリは架空のプロジェクト「離脱率改善PJ」を題材にしたデモです。*
*会社名・人名はすべて仮名です。*
