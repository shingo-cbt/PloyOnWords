# HOW_TO_RUN.md — 実行ガイド

## セッション開始の手順

### Step 0: テーマを決める
ユーザーがテーマを指定するか、ThemeCuratorにジャンルを渡して候補を出させます。

**テーマの例**:
- 「遅刻」「昼寝」「先延ばし」（行動・習慣系）
- 「セロリ」「レバー」「パクチー」（食べ物系）
- 「人見知り」「飽き性」「ネガティブ思考」（気質系）
- 「満員電車」「深夜のコンビニ」「マニュアル車」（環境・モノ系）

---

### Step 1: ThemeCuratorを起動する

**入力プロンプト例**:
```
あなたはThemeCuratorエージェントです。
prompt.md・bias_mapper.md・target_profile.mdを参照してください。

テーマ: 「先延ばし（プロクラスティネーション）」

以下を出力してください：
- 一般認識サマリー
- 偏見マッピング（種類・強度）
- 擁護可能な角度（上位3つ）
- 意外な事実・反転ポイント
- 地雷論点
- 推奨する詭弁タイプ
```

---

### Step 2: StrategyArchitectを起動する

**入力プロンプト例**:
```
あなたはStrategyArchitectエージェントです。
prompt.md・argument_tree.md・emotion_curve.md・pivot_points.mdを参照してください。

ThemeCuratorの出力（下記）を受け取り、6ターン構成での設計書を作成してください。

[ThemeCuratorの出力をここに貼る]

出力: 勝ち筋・感情曲線・論点ツリー・裏切りポイント・詭弁の使用順序
```

---

### Step 3: 対話ループを回す（各ターン）

#### 3a: SophistryEngineのターン

**入力プロンプト例**:
```
あなたはSophistryEngineエージェントです。
prompt.md・disguise_tactics.md・escalation.mdを参照してください。

[theme_brief.mdの内容]
[StrategyArchitectの設計書]
[前ターンのEverymanVoiceの発言: なければ「なし」]
[今ターンの指示: Stage 1 / 使用詭弁: 定義のすり替え]

ターン1の発言を生成してください。
使用詭弁タイプと隠蔽レベルも明記すること。
```

#### 3b: EverymanVoiceのターン

**入力プロンプト例**:
```
あなたはEverymanVoiceエージェントです。
prompt.md・breaking_points.md・persona_variants.mdを参照してください。

ペルソナ: Persona A（素直な懐疑派）
現在の抵抗レベル: L1

SophistryEngineの発言:
[SophistryEngineの出力を貼る]

L1の状態で反論してください。感情的・直感的に。論理的すぎないこと。
```

#### 3c: CognitiveTunerのチェック

**入力プロンプト例**:
```
あなたはCognitiveTunerエージェントです。
prompt.md・balance_rubric.md・red_flags.mdを参照してください。

ターン1の評価をしてください。

SophistryEngine発言: [貼る]
EverymanVoice発言: [貼る]
現在のターン: 1（目標納得度30〜40%）

納得度スコア・違和感スコア・バランス判定・差し戻し指示を出力してください。
```

#### 3d: ConsistencyGuardのチェック（3ターンごと）

**入力プロンプト例**:
```
あなたはConsistencyGuardエージェントです。
prompt.md・claim_tracker.mdを参照してください。

ターン1〜3の全発言（SophistryEngine分）を確認し、
矛盾フラグ（GREEN/YELLOW/RED）と検出された矛盾を出力してください。

[累積発言テキストを貼る]
```

---

### Step 4: Rhetorician でブラッシュアップ

**入力プロンプト例**:
```
あなたはRhetoricianエージェントです。
prompt.md・rhythm_patterns.md・metaphor_bank.md・voice_calibration.mdを参照してください。

以下の対話テキストをブラッシュアップしてください。
- 内容・論点・詭弁の種類は変えない
- リズム・語感・比喩・間（ま）を調整する
- 口語度: 中（「賢い友人」ゾーン）

[全対話テキストを貼る]
```

---

### Step 5: PunchlineSmithyで締める

**入力プロンプト例**:
```
あなたはPunchlineSmithyエージェントです。
prompt.md・timing_rules.mdを参照してください。

テーマ: [テーマ名]
勝ち筋: [StrategyArchitectの勝ち筋を貼る]
ブラッシュアップ済み対話: [Rhetorician出力を貼る]

最終パンチライン候補を3つ生成してください（タイプ別）。
推奨候補と理由も明記すること。
```

---

### Step 6（オプション）: MetaCommentatorで解説

**入力プロンプト例**:
```
あなたはMetaCommentatorエージェントです。
prompt.md・reader_guide.mdを参照してください。

解説レベル: LEVEL-2（スタンダード）

[完成した対話テキスト]
[CognitiveTunerの全ターンスコア]
[ConsistencyGuardのclaim_tracker記録]

「種明かし」セクションを生成してください。
```

---

## 差し戻し発生時のプロンプト例

### CognitiveTunerからSophistryEngineへの差し戻し
```
CognitiveTunerより差し戻し指示:
- 理由: 詭弁がバレすぎている（違和感が悪い違和感になっている）
- 指示: 同じ論点を「承認から入る」形式で書き直してください。
  EverymanVoiceの反論を一度「そうですね」と受けてから覆す構造にすること。

[元の発言を貼る]
```

---

## チェックリスト（セッション終了前）

- [ ] EverymanVoiceがL3以上に到達している
- [ ] 使用された詭弁が3種類以上ある（ConsistencyGuard記録参照）
- [ ] CognitiveTunerの最終スコアが55〜65%の範囲内
- [ ] 同じ詭弁が連続して使われていない
- [ ] パンチラインが30字以内に収まっている
- [ ] ConsistencyGuardのフラグがGREEN（またはYELLOW以下）
