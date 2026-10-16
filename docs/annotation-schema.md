# ダンス動画アノテーション形式

この文書は初期仕様。実際のデータを注釈しながら更新する。JSONLでは1行を動画区間または評価タスク1件に対応させ、動画本体ではなく識別子と利用条件を参照する設計を基本とする。

## レコード例

    {
      "record_id": "dance-001-segment-01",
      "video": {
        "video_id": "dance-001",
        "source": "REPLACE_WITH_SOURCE",
        "license": "RECORD_LICENSE",
        "start_seconds": 0.0,
        "end_seconds": 5.0
      },
      "observation": {
        "actions": [
          {
            "description": "両腕を肩より上に上げる",
            "body_parts": ["left_arm", "right_arm"],
            "start_seconds": 1.2,
            "end_seconds": 2.0,
            "evidence": ["00:01.2-00:02.0"]
          }
        ],
        "trajectory": null,
        "rhythm_relation": "unknown",
        "visibility_limitations": ["一部フレームで手が遮蔽される"]
      },
      "interpretation": {
        "hypotheses": [],
        "confidence": null,
        "evidence": []
      },
      "annotation": {
        "annotator_id": "annotator-01",
        "guideline_version": "0.1.0"
      }
    }

これは形式を示す例であり、実在動画についての観察結果ではない。

## フィールド

| フィールド | 意味 |
|---|---|
| record_id | レコードの一意なID |
| video.video_id | 動画ID |
| video.source / license | 出典と利用条件 |
| start_seconds / end_seconds | 評価対象区間 |
| observation.actions | 観察可能な動作と時刻 |
| observation.trajectory | 移動軌跡。不明ならnull |
| observation.rhythm_relation | 音楽との関係。不明ならunknown |
| visibility_limitations | 遮蔽、画角、画質などの制約 |
| interpretation.hypotheses | 意味・意図・様式に関する候補 |
| interpretation.confidence | 解釈の確信度。不明ならnull |
| interpretation.evidence | 仮説を支える証拠 |
| annotation | 注釈者とガイドラインの版 |

## 注釈ルール

- 映像で直接確認できる動きは observation に書く。
- 意図、感情、文化的意味、ジャンルの判断は interpretation に書く。
- 見えない身体部位や音声情報を推測で補わない。
- 複数の解釈があり得る場合は候補を複数保持する。
- 時間範囲は可能な限り動画タイムスタンプで示す。
- 注釈者間の意見の違いを削除せず記録する。
- 公開前に個人情報、ライセンス、再識別リスクを確認する。