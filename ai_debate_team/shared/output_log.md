# Output Log — エージェント出力履歴

## フォーマット
各エージェントの出力はセッションごとに以下の形式で記録される。

```
---
[SESSION_ID]: {セッションID}
[TIMESTAMP]: {タイムスタンプ}
[AGENT]: {エージェント名}
[TURN]: {ターン番号 / N/A}
[OUTPUT]:
{出力内容}
---
```

## 記録対象
- ThemeCurator の分析結果
- StrategyArchitect の設計書
- 各ターンの SophistryEngine / EverymanVoice の発言
- CognitiveTuner のスコアと判定
- ConsistencyGuard の矛盾チェック結果
- Rhetorician のブラッシュアップ後テキスト
- PunchlineSmithy の候補一覧と採用結果

## 注意
このログはMetaCommentatorが参照する。
解説モード時は使用された詭弁タイプをここから抽出する。
