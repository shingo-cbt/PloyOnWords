# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## このリポジトリについて

「PloyOnWords」は、詭弁を使って世間の偏見に喧嘩を売るコンテンツ生成システムです。
コードは存在せず、すべてのエージェントはMarkdownファイルで定義されたプロンプトで動作します。
Claude Code自身がエージェントを順番に実行することで、コンテンツを生成します。

## セッションの実行方法

テーマを受け取ったら `HOW_TO_RUN.md` の手順に従い、以下の順序でエージェントを実行する：

```
【任意】AngleConverter → ThemeCurator → StrategyArchitect → [SophistryEngine ⇔ EverymanVoice ⇔ CognitiveTuner] × 6ターン → Rhetorician → PunchlineSmithy
```

- **AngleConverter**: 日常の観察・メモをテーマ候補に変換する前段ツール。「テーマが決まっていない」「角度を探したい」ときに使う。
- テーマが決まっている場合はThemeCuratorから開始してよい。

完走後は `EXPORT_X_NOTE.md` に従い、X用（140字）とNote用（独白形式）を出力する。

## エージェント構成と参照ファイル

各エージェントを実行する前に、そのエージェントの `prompt.md` と関連ファイルを必ず読み込む。

| エージェント | 参照ファイル |
|---|---|
| AngleConverter | `layer0_input/angle_converter/prompt.md`, `angle_patterns.md` |
| ThemeCurator | `layer1_design/theme_curator/prompt.md`, `bias_mapper.md`, `target_profile.md` |
| StrategyArchitect | `layer1_design/strategy_architect/prompt.md`, `argument_tree.md`, `emotion_curve.md`, `pivot_points.md` |
| SophistryEngine | `layer2_dialogue/sophistry_engine/prompt.md`, `disguise_tactics.md`, `fallacy_library.md` |
| EverymanVoice | `layer2_dialogue/everyman_voice/prompt.md`, `breaking_points.md` |
| CognitiveTuner | `layer3_quality/cognitive_tuner/prompt.md`, `balance_rubric.md` |
| Rhetorician | `layer3_quality/rhetorician/prompt.md` |
| PunchlineSmithy | `layer3_quality/punchline_smithy/prompt.md`, `timing_rules.md` |

## SophistryEngineのキャラクター（最重要）

「知的な遊び人」として振る舞う。詭弁を楽しんでいる自覚がある。

```
トーン指標:
  仰々しさ　 ███░░░ 3/6
  自信　　　 ██████ 6/6（根拠がなくても断言する）
  言葉遊び　 █████░ 5/6
  感情　　　 █░░░░░ 1/6（ほぼ無表情）
```

各ターンで必ず以下の言葉遊びの型を1つ以上使う：
- **ひっくり返し型**: 相手の言葉をそのまま使って意味を逆転
- **勝手に定義型**: 言葉の定義を自分で決めて話を進める
- **一段飛ばし着地型**: 小さな事実 → 大きすぎる結論へ直接飛ぶ
- **承認→引っくり返し型**: 「そうですね」から始めて全く違う場所に着地

## 品質管理ルール（CognitiveTuner）

- 目標: 納得度60% / 違和感40%
- 許容範囲: 納得度50〜70%
- これを外れたらSophistryEngineまたはEverymanVoiceに差し戻す
- EverymanVoiceはターン6までにL3（部分同意）以上に到達させる

## Note出力（独白形式）のルール

- SophistryEngineの一人語りとして構成する
- EverymanVoiceの発言は「〜という声が聞こえてきます」「〜そういう主張ですよね？」の形でSophistryEngineの口から語る
- タイトル＝採用パンチライン
- CognitiveTunerのスコア・詭弁タグは出力しない
- 末尾に採用パンチラインを `>` 引用で置く

## テーマ選定の基準

良いテーマの条件：
1. 「擁護したら軽く叩かれそう」だが「炎上するほどではない」
2. 批判する側が無自覚に同じことをしている（鏡像型が使える）
3. 嫌いな理由を言語化できない人が多い

## shared/state.json

セッション中の状態を管理するテンプレート。実際の実行時に値を埋めて参照する。
