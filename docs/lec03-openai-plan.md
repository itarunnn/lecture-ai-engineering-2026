# lec03 OpenAI 実行設定の計画

## 目的

第3回のエージェントを、利用可能な OpenAI API 残高で実行できるようにする。演習と宿題の解答は受講者が進める。

## 現状と範囲

- `app/agent.py` は `GoogleModel` を固定している。`app/config.py` の既定モデルは Gemini のままにする。
- `AIE_MODEL=openai:gpt-6-luna` を指定したときだけ OpenAI Responses モデルを選ぶ。
- API キーは Windows PC の実行シェルの `OPENAI_API_KEY` 環境変数から読み、コード・コミットへ保存しない。
- `pydantic-ai-slim==2.57.0` の OpenAI extra を依存関係に追加する。既存の固定版は上げない。
- `documents/` の授業資料は未追跡ファイルとして保全し、PR には含めない。

## 確認

1. モデル選択とキー未設定時の案内を先にテスト化し、失敗を確認する（済）。
2. 実装後に対象テストと全テストを Python 3.12 で実行する（対象4件、全体17件が成功）。
3. API キーを使わないツール一覧を確認した。実際の API 応答はキー設定後に確認する。
4. 解答と実行記録が揃ってから、本人の fork の `lec03` から `main` へ PR を作る。
