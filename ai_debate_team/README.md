# AI Debate Team — 詭弁擁護コンテンツ生成システム

## コンセプト
「一見無茶苦茶だが、読者がツッコミながらも納得してしまう」会話型コンテンツを生成する多エージェントシステムです。

正しさを証明するのではなく、**「本来通らなかった主張を、詭弁によって通してしまう体験」**を提供します。

---

## システム全体像

```
ai_debate_team/
│
├── orchestrator/               # 全体制御（司令塔）
│   ├── prompt.md               # 実行フロー・終了条件
│   └── router.md               # エージェント呼び出し条件・差し戻しルール
│
├── layer1_design/              # コンテンツ設計層
│   ├── theme_curator/          # テーマ設計
│   │   ├── prompt.md           # 役割・出力フォーマット
│   │   ├── bias_mapper.md      # 偏見の6分類と強度定義
│   │   └── target_profile.md  # 対象プロファイルテンプレート
│   └── strategy_architect/    # 構成設計
│       ├── prompt.md           # 役割・出力フォーマット
│       ├── argument_tree.md    # 論点展開ツリー設計ガイド
│       ├── emotion_curve.md    # 読者感情設計ガイド
│       └── pivot_points.md     # 裏切りポイント設計
│
├── layer2_dialogue/            # 対話生成層
│   ├── sophistry_engine/       # 詭弁エンジン（主役）
│   │   ├── prompt.md           # 役割・詭弁カタログ30種
│   │   ├── disguise_tactics.md # 詭弁を見えにくくする技法
│   │   └── escalation.md       # 段階的追い詰め手順（6段階）
│   └── everyman_voice/         # 一般人の声
│       ├── prompt.md           # 役割・4段階抵抗レベル
│       ├── breaking_points.md  # 揺らぐトリガー一覧
│       └── persona_variants.md # 読者層別ペルソナ4種
│
├── layer3_quality/             # 品質調整層
│   ├── cognitive_tuner/        # 違和感チューナー（60/40バランス管理）
│   │   ├── prompt.md           # 評価プロセス・差し戻し指示
│   │   ├── balance_rubric.md   # ターン別目標スコア表
│   │   └── red_flags.md        # RED/YELLOW/GREEN判定基準
│   ├── rhetorician/            # 言葉職人
│   │   ├── prompt.md           # 調整項目（リズム・語感・比喩・間）
│   │   ├── rhythm_patterns.md  # 文体リズムパターン5種
│   │   ├── metaphor_bank.md    # 比喩・アナロジーストック
│   │   └── voice_calibration.md# 口語度・知性度チューニング
│   └── punchline_smithy/       # パンチライン職人
│       ├── prompt.md           # 5タイプ・生成プロセス・アーカイブ
│       └── timing_rules.md     # 配置タイミングルール
│
├── layer4_meta/                # メタ監視層
│   ├── consistency_guard/      # 一貫性番人
│   │   ├── prompt.md           # 矛盾3分類・修正ガイドライン
│   │   └── claim_tracker.md    # 主張記録テンプレート・矛盾パターン辞書
│   └── meta_commentator/       # メタ実況者（オプション）
│       ├── prompt.md           # 解説モード・3レベル
│       └── reader_guide.md     # 納得のメカニズム6パターン
│
└── shared/                     # 全エージェント共有
    ├── state.json              # セッション状態管理
    ├── output_log.md           # エージェント出力履歴
    └── theme_brief.md          # テーマ共有シート
```

---

## エージェント一覧

| エージェント | レイヤー | 主な責務 |
|---|---|---|
| Orchestrator | 制御 | 全体フロー制御・差し戻し判断 |
| ThemeCurator | L1 | テーマ分析・偏見マッピング・擁護角度の抽出 |
| StrategyArchitect | L1 | 感情曲線設計・論点ツリー・裏切りポイント設計 |
| SophistryEngine | L2 | 詭弁構築（30種以上）・段階的追い詰め |
| EverymanVoice | L2 | 読者代弁・4段階の抵抗・自然な揺らぎ |
| CognitiveTuner | L3 | 納得60/違和感40のバランス管理・差し戻し |
| Rhetorician | L3 | リズム・語感・比喩・間の調整 |
| PunchlineSmithy | L3 | 締めの一文・ターン内パンチライン |
| ConsistencyGuard | L4 | 矛盾検出・主張記録・RED/YELLOW/GREENフラグ |
| MetaCommentator | L4 | 解説モード（オプション）・詭弁の種明かし |

---

## クイックスタート

### 最小構成で始める場合（推奨）
まず以下の3エージェントだけで試作してください：

```
ThemeCurator → StrategyArchitect → [SophistryEngine ⇔ EverymanVoice] → CognitiveTuner
```

品質に満足したら、Rhetorician・PunchlineSmithy・ConsistencyGuardを追加します。

### フルセッションの実行手順
詳細は `HOW_TO_RUN.md` を参照してください。

---

## 設計思想

### なぜ60/40なのか
- 納得度70%以上 → 「これは正論だ」になり、詭弁体験が消える
- 納得度50%以下 → 「ただのおかしな話」になり、読者が離れる
- **40%の違和感が「なんか納得したくなかったけど...」というモヤを生む**
- このモヤこそがコンテンツの記憶に残る部分

### なぜ詭弁を意図的に使うのか
このシステムは詭弁を「悪用」するのではなく、「体験させる」ことが目的です。
MetaCommentatorの解説モードにより、読者は「なぜ自分が納得しそうになったのか」を学べます。
批判的思考のトレーニングとしての側面も持っています。
