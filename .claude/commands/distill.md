---
description: inboxメモをアトミックノートに分割して notes/ に保存
argument-hint: "<inbox-file-name>"
---

# /distill コマンド

あなたは「note-distiller」サブエージェントとして、inbox のメモを「1ノート1アイデア」のアトミックノートに分割します。

## 入力
- `$ARGUMENTS`: inbox ファイル名（例: `2025-12-01_kickoff_meeting.md`）

## 処理手順

### Step 1: inbox ファイルを読み込む
`knowledge/inbox/$ARGUMENTS` を読み込んでください。

### Step 2: アイデアを抽出する
以下のカテゴリに分類しながら、独立したアイデアを抽出してください:
- **decision**: 意思決定（何を、なぜ決めたか）
- **metric**: 指標・KPI（定義、現状、目標）
- **risk**: リスク（内容、影響、対策）
- **data**: データ要件（何が必要か、どう取得するか）
- **open**: 未決事項（何が決まっていないか、いつ決めるか）
- **action**: アクション（誰が、いつまでに、何をするか）
- **stakeholder**: ステークホルダーの意見・懸念
- **insight**: 分析結果・示唆

### Step 3: 各アイデアをノート形式に変換する

以下のテンプレートに従ってください:

```markdown
---
id: note-{category}-{short-name}
title: {人間が読めるタイトル}
created: {YYYY-MM-DD}
source: [[{inbox-file-name}]]
---

## Summary（3行）
- ...
- ...
- ...

## Tags
#{tag1} #{tag2} #{tag3}

## Links
- [[関連ノート1]]
- [[関連ノート2]]

## Body
（自分の言葉で要点化。コピペ禁止。なぜ/背景/意図も1段落で）

## Action（必要なら）
- [ ] {担当/期限つきタスク}
```

### Step 4: 重複チェック
既存の `knowledge/notes/` にある同じトピックのノートがあれば、新規作成ではなく更新を提案してください。

### Step 5: 出力
生成したノートの一覧を表示し、ユーザーに確認を求めてください。

## 制約
- **コピペ禁止**: 元のテキストをそのまま使わず、自分の言葉で要約する
- **Links必須**: 最低1つ、可能なら2つ以上の関連ノートをリンクする
- **Summary必須**: 必ず3行で要点をまとめる
- **Actionは必要な場合のみ**: 明確なタスクがある場合のみ記載

## 出力例

```
## /distill 結果

### 抽出したノート（5件）

1. **note-decision-success-metric** - 成功指標の定義
   - Summary: 7日間継続率+6pt、視聴時間+3分を目標に設定
   - Links: [[note-metric-retention-7day]]

2. **note-risk-timeline-delay** - スケジュール遅延リスク
   - Summary: Phase1遅延がQ1目標に影響
   - Links: [[note-decision-phase-order]]

...

### 確認
上記のノートを `knowledge/notes/` に作成してよいですか？
```
