# Router — エージェント呼び出し条件

## 各エージェントの呼び出しタイミング

| エージェント | 呼び出し条件 | 優先度 |
|---|---|---|
| ThemeCurator | セッション開始時（必須） | 最高 |
| StrategyArchitect | ThemeCurator完了後（必須） | 最高 |
| SophistryEngine | 各対話ターンの先攻（必須） | 高 |
| EverymanVoice | SophistryEngine出力後（必須） | 高 |
| CognitiveTuner | 各ターン終了後（必須） | 高 |
| ConsistencyGuard | 3ターンごと、または矛盾の兆候があるとき | 中 |
| Rhetorician | 対話ループ完了後（必須） | 中 |
| PunchlineSmithy | Rhetorician完了後（必須） | 中 |
| MetaCommentator | ユーザーが「解説モード」を要求したとき | 低 |

## 差し戻しルール

### CognitiveTuner による差し戻し
- 納得度スコア < 50% → SophistryEngine に「もっと共感を引き出す角度で」と指示して再生成
- 納得度スコア > 75% → SophistryEngine に「詭弁をもっと露骨にして違和感を増やす」と指示
- 違和感が「ただおかしい」に傾いた場合 → EverymanVoice に「もっと素直に揺らぐ」と指示

### ConsistencyGuard による差し戻し
- 矛盾フラグ「RED」→ SophistryEngine に該当ターンを再生成させる
- 矛盾フラグ「YELLOW」→ Rhetorician に表現でカバーするよう指示

## ループ制御

```
MAX_TURNS = 8          # 対話の最大ターン数
MIN_TURNS = 4          # 最低限必要なターン数
TARGET_RESISTANCE = L3 # EverymanVoiceの目標抵抗レベル
```

## 緊急停止条件
- SophistryEngine が同じ詭弁を3回以上繰り返した場合
- EverymanVoice が L4（完全降伏）に早期到達した場合（3ターン以内）
- CognitiveTuner が「破綻」判定を出した場合
