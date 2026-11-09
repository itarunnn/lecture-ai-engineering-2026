# lec03 実行と演習の記録

## 目的

第3回のエージェントを、利用可能な OpenAI API 残高で実行し、演習の `make_quiz` を追加する。実際のモデル挙動を受講者が確認して解答へ記録する。

## 現状と範囲

- `app/agent.py` は `GoogleModel` を固定している。`app/config.py` の既定モデルは Gemini のままにする。
- `AIE_MODEL=openai:gpt-6-luna` を指定したときだけ OpenAI Responses モデルを選ぶ。
- API キーは Windows PC の実行シェルの `OPENAI_API_KEY` 環境変数から読み、コード・コミットへ保存しない。
- `pydantic-ai-slim==2.57.0` の OpenAI extra を依存関係に追加する。既存の固定版は上げない。
- `documents/` の授業資料は未追跡ファイルとして保全し、PR には含めない。
- `make_quiz(lecture: int) -> str` は指定した回の用語を1つ選び、用語集の定義を正解として返す。用語がない回でも説明を返す。

## 確認

1. モデル選択とキー未設定時の案内を先にテスト化し、失敗を確認する（済）。
2. 実装後に対象テストと全テストを Python 3.12 で実行した（全体20件が成功）。
3. API キーを使わないツール一覧に `make_quiz` を含む3件が表示された。
4. 2026-11-09、受講者が Windows PC から OpenAI `gpt-6-luna` で確認した。提示された `--trace` には `get_lecture_summary(2)`、`make_quiz(2)`、`search_glossary("事前学習")` がこの順にあり、`requests=4`、`tool_calls=3`。この実測を `lectures/03/answer.md` に記録した。
5. 第1回の回答との比較と、宿題のレベル選択・実施が残る。解答が揃ってから、本人の fork の `lec03` から `main` へ PR を作る。
