# Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）の個人メモ

## movie

[Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）](https://youtube.com/live/Aspb-QF3iDU)

## Anthropic キーノートセッション

### 個人的超重要 Tips

- Claude がプロンプトテンプレートを代わりに書いてくれるツール(metaprompt tool)

https://anthropic.com/metaprompt-notebook

- Anthropic が提供している prompt library．60 以上の最適化済みのプロンプトが用意されているので，Bedrock で Claude3 使うときに参考にしたい．

https://docs.anthropic.com/claude/page/prompts

- モデルの技術詳細や評価，能力等を説明しているモデルカード

https://anthropic.com/claude-3-model-card

- 公式のコードや実装の例

https://anthropic.com/cookbook

- プロンプトエンジニアリングの Tips など

https://anthropic.com/docs

### メモ

Claude3 は，，，

- コンテキストウィンドウの長さが最長
- 全てのモデルが画像対応
- task に応じてモデルも使い分けるとよい（model card なども参照せよ）
- ジェイルブレイクへの耐性が非常に高い
- llm-trustworthy-leaderboard（LLM 信頼性リーダーボード）において，GPT4（Score: 69）に比べ Claude2（Score: 85）は非常に優れていることが示されている（Claude3 はより優れている）
- HIPAA 準拠，SOC2 Type1 および Type2 の認証も取得済み
- AWS とのパートナーシップにより，セキュリティ認証の恩恵も受けられる
- 安全性と信頼性を最大化するには有力な選択肢となる

## LT① Bedrock Calude 3 を使って市場対応を DX 化してみた

※資料リンクが見つからなかったので，後日探します

- 容易に RAG は構築できるので，まずは試すと良い（プレイグラウンドで試せる）
- その後，本格的にアプリ構成を考えれば良い．
  - エージェント，ナレッジベース，lambda 作成，会話履歴の管理
- PDCA から DCAP のマインドが大事

## LT② 会社に関する RAG をサーバレスで作成してみた

https://speakerdeck.com/sonoda_mj/bedrocknotoo-many-requestjie-jue-sitemita

- API 利用時はリトライ機構が大事
  - 指数バックオフ機構（1 回につき 2^(retry_count - 1)遅らせる）
- Bedrock を利用するリージョンを分散すると良い
- 予算があればプロビジョンドスループットを購入すると良い
  - 1 ヶ月単位で購入
- フロントエンドは Amplify, バックエンドは Lambda Adapter, Bedrock, Pinecone も利用している

## LT③ Anthropic Cookbook のおすすめレシピ

https://speakerdeck.com/schroneko/anthropic-cookbook-noosusumeresipi

https://qiita.com/schroneko/items/a4098baa29580ec906b8
https://speakerdeck.com/schroneko/context-window-noohua

- cookbook には大きく 4 種の項目でノートブックが紹介されている

  - misc: Claude の機能や使い方
  - multimodal: 画像や音声などの扱い方
  - third_party: 外部サービスやライブラリとの連携方法
  - tool_use: ツールを使わせたり特定のタスクを行わせる方法

- 以下のノートブックが初見ではおすすめ
  - read_web_pages_with_haiku.ipynb: XML 特有のプロンプトの書き方がわかる
  - how_to_enable_json_mode.ipynb: json 出力させるためのプロンプトでの工夫がわかる
  - best_practices_for_vision.ipynb: API で画像を入力する方法，step by step で指示すると画像ファイル名と画像ファイルの中身が異なっていてもうまく画像認識させられる

## LT④ Claude3 を使って RAG の一番の悩みポイントを解決してみた

https://dev.classmethod.jp/articles/lt-at-jaws-ug-bedrock-claude-night/
https://dev.classmethod.jp/articles/read-powerpoint-document-with-claude-3/
https://dev.classmethod.jp/articles/implement-rag-with-aws-services/

https://dev.classmethod.jp/articles/simple-examination-on-recognizable-char-size-with-claude-3/
https://dev.classmethod.jp/articles/fix-claude3-text-recognition-mistake-with-azure-document-intelligence/

- powerpoint 上でのテキストの読む順番は，生成 AI 側では判断しづらい
- powerpoint を Claude3 で markdown でまとめさせると，人間が読む順番で文字起こしできるのは良い idea
- 画像自体を文章として説明させる，PDF のヘッダー・ページ数などもよしなに無視してくれる．
- Amazon Titan の multi modal embedding はまだ日本語対応してない

## LT⑤ 来てくれ Claude 3! Agents for Amazon Bedrock のモデル比較或いはチューニングの話

https://speakerdeck.com/hedgehog051/lai-tekureclaude-3-agents-for-amazon-bedrocknomoderubi-jiao-huo-ihatiyuningunohua

- ナレッジベースは Claude3(Haiku, Sonnet)で利用可能
- 詳細プロンプト: エージェント作成時に用意されるプロンプトテンプレートセット
  - 前処理：ユーザーの入力をカテゴリー A~E に分類するようエージェントに指示
    - A: 悪意があるか
    - B: エージェントに提供されている関数，API に関連するか
    - C: エージェントに提供された関数では提供できない質問
    - ，，，(TODO: 後ほどまとめ直したい．．．．)
  - オーケストレーション: ユーザーの入力に対してツールの使用とガイドラインに沿って回答を生成するようエージェントに指示
  - KB の回答生成：KB(ナレッジベース)への検索結果を使って回答生成する際のエージェントへの指示
  - 後処理：ユーザーにとってわかりやすいコンテキストを追加するタスクエージェントへの指示

## パネルディスカッション

- 有名な山の名前を教えてください，と Claude に日本語で聞くのと英語で聞くのとでは回答が異なる（日本語の場合は富士山，英語の場合はエベレスト）のは超面白い
- Claude の場合，プロンプト中では項目を列挙したり箇条書きにすると良い
- コンテキストウィンドウが非常に大きいので，例も多様に入れても OK だしむしろ入れるべき
- role も指示すべき
- Claude は XML タグを使えるように学習されているので，XML タグを利用してプロンプトを構造化し，プロンプトチェーンやロジックをより明確にすると良い．例えば，XML タグで利用して複雑なタスクを様々なセクションに分割すると良い
- モデルに考えるように頼んで答えだけを出力するように頼むのではなく，思考を書き出すスペースを与えなければならない(そうしなければ実際の思考は行われない)
- Claude のメッセージを一部予め埋め込むのも良い(そうすると途中から喋ってくれる)
- 長いコンテキストに対応する場合，ドキュメントや画像などは先頭に近い位置に配置し，タスクがどのようなものになるか，少しコンテキストを持たせると良い
  - 後ろの部分で指示や例を書く．

## その他

- [AWS の生成 AI で社内文書検索！ Bedrock のナレッジベースで簡単に RAG アプリを作ってみよう](https://qiita.com/minorun365/items/24dfb0ea3afde6ed0a56)
- [AWS の生成 AI 最新機能ハンズオン！Bedrock の Knowledge Base と Agents に入門しよう](https://qiita.com/minorun365/items/86a3667290a8e5657f65)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)
- [Advanced Rag](https://medium.com/@drjulija/what-are-naive-rag-advanced-rag-modular-rag-paradigms-edff410c202e)
- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
- [LangChain×Bedrock(実装の参考になりそう)](https://twitter.com/cyber__BOSE/status/1782246450770137301)
