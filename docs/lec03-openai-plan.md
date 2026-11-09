# lec03 実行と演習の記録

## 目的

第3回のエージェントを、利用可能な OpenAI API 残高で実行し、演習の `make_quiz` を追加する。実際のモデル挙動を受講者が確認して解答へ記録する。

## 実装した範囲

- `AIE_MODEL=openai:gpt-6-luna` を指定したときは OpenAI Responses モデルを選び、それ以外では既定の Gemini モデルを使う。
- API キーは Windows PC の実行シェルの `OPENAI_API_KEY` 環境変数から読み、コード・コミットへ保存しない。
- `pydantic-ai-slim==2.57.0` の OpenAI extra を依存関係に追加し、既存の固定版は維持した。
- `documents/` の授業資料は未追跡ファイルとして保全し、PR には含めない。
- `make_quiz(lecture: int) -> str` は指定した回の用語を1つ選び、用語集の定義を正解として返す。用語がない回でも説明を返す。

## 確認

1. モデル選択とキー未設定時の案内を先にテスト化し、失敗を確認する（済）。
2. 実装後に対象テストと全テストを Python 3.12 で実行した（全体20件が成功）。
3. API キーを使わないツール一覧に `make_quiz` を含む3件が表示された。
4. 2026-11-09、受講者が Windows PC から OpenAI `gpt-6-luna` で確認した。提示された `--trace` には `get_lecture_summary(2)`、`make_quiz(2)`、`search_glossary("事前学習")` がこの順にあり、`requests=4`、`tool_calls=3`。この実測を `lectures/03/answer.md` に記録した。
5. 宿題は「基礎」を選択し、`INSTRUCTIONS` の回答末尾の指示を1行だけ変更した。同じ質問「LoRAとQLoRAの違いは？」の `--trace` 実行結果を前後で比較して `lectures/03/answer.md` に記録した。変更前は用語集検索1回で第2回を示し、変更後は検索2回で確認問題を出した。第1回の回答は `lectures/01/answer.md` に記録がなかったため、今回同じ OpenAI モデルをツールなしで直接呼び出し、エージェントとの比較を演習欄に記録した。全20件のテストが成功。次の一手は、本人の fork の `lec03` から `main` へ PR を作ること。
