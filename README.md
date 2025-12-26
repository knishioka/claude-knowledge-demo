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

| コマンド | 説明 | 例 |
|---------|------|-----|
| `/distill` | inboxメモをアトミックノートに分割 | `/distill 2025-12-01_kickoff_meeting.md` |
| `/moc` | テーマ別MOC（索引）を生成・更新 | `/moc decisions` |
| `/ask` | 質問に根拠リンク付きで回答 | `/ask 意思決定は何？根拠は？` |
| `/weekly-review` | 週次の棚卸しと要約 | `/weekly-review` |
| `/capture` | 30秒でinboxに入れるテンプレ | `/capture 新しいアイデア` |

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

## デモの進め方（5〜7分）

### Step 1: inboxの議事録を確認
```bash
# 生の議事録を開く
cat knowledge/inbox/2025-12-01_kickoff_meeting.md
```

### Step 2: /distill でアトミックノート生成
```
/distill 2025-12-01_kickoff_meeting.md
```
→ 1ノート1アイデアに分割された notes/ が生成される

### Step 3: /moc で索引を作成
```
/moc decisions
```
→ 意思決定の索引が maps/map-decisions.md に生成される

### Step 4: /ask で質問に回答
```
/ask 意思決定は何？根拠は？
```
→ 結論 + 根拠リンク + 補足 + 次アクション形式で回答

### Step 5: 回答を notes に戻す（フィードバックループ）
```
/distill （/askの回答を選択して）
```
→ 新しい知見がナレッジベースに蓄積

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

## デモシナリオ詳細（7分版）

### 1. 導入（1分）
「これは忙しいPMや経営者が、必要な情報を必要なときに取り出せる『外部脳』のデモです。」

- Collect → Distill → Connect → Use の流れを説明
- 架空プロジェクト「離脱率改善PJ」を題材に

### 2. 生の情報（inbox）を見せる（1分）
```bash
cat knowledge/inbox/2025-12-01_kickoff_meeting.md
```
「議事録は情報の宝庫ですが、そのままでは再利用しにくい。」

### 3. アトミックノート（notes）を見せる（1分）
```bash
cat knowledge/notes/note-decision-success-metric.md
```
「1ノート1アイデアに分解すると、検索・再利用しやすくなります。」

### 4. 索引（maps）を見せる（1分）
```bash
cat knowledge/maps/map-decisions.md
```
「MOCで全体像を俯瞰。どこに何があるか一目で分かります。」

### 5. 質問応答のデモ（2分）
```
/ask 意思決定は何？根拠は？
```
「結論→根拠→補足→次アクションの形式で回答。推測で埋めず、根拠リンク必須。」

```
/ask 来週までのリスクは？
```

### 6. フィードバックループ（1分）
「新しい知見は `/distill` でノート化。知識が蓄積されます。」

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
