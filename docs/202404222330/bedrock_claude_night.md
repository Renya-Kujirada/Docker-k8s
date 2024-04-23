# Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）の個人メモ

## movie

- [Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）](https://youtube.com/live/Aspb-QF3iDU)
- [Anthropic Keynote Session in JAWS Bedrock Claude Night on 2024/4/22](https://www.youtube.com/watch?v=yJg-SK9KkHg)

## Anthropic キーノートセッション

### 個人的超重要 Tips

- [Experimental metaprompt tool](https://anthropic.com/metaprompt-notebook)
  - Claude がプロンプトテンプレートを代わりに書いてくれるツール
- [Anthropic prompt library](https://docs.anthropic.com/claude/page/prompts)
  - 60 以上の最適化済みのプロンプトが用意されているので，Bedrock で Claude3 使うときに参考にしたい．
- [Anthropic's Claude3 model card](https://anthropic.com/claude-3-model-card)
  - モデルの技術詳細や評価，能力等を説明している
- [Anthropic cookbook](https://anthropic.com/cookbook)
  - 公式のコードや実装の例
- [Claude user guide documentation](https://anthropic.com/docs)
  - プロンプトエンジニアリングの Tips

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

[slide](https://speakerdeck.com/yukiogawa/bedrock-claude3woshi-tuteshi-chang-dui-ying-wodxhua-wojian-tao-sitemita)

- 容易に RAG は構築できるので，まずは試すと良い（プレイグラウンドで試せる）
- その後，本格的にアプリ構成を考えれば良い．
  - エージェント，ナレッジベース，lambda 作成，会話履歴の管理
- PDCA から DCAP のマインドが大事

## LT② 会社に関する RAG をサーバレスで作成してみた

[slide](https://speakerdeck.com/sonoda_mj/bedrocknotoo-many-requestjie-jue-sitemita)

- API 利用時はリトライ機構が大事
  - 指数バックオフ機構（1 回につき 2^(retry_count - 1)遅らせる）
- Bedrock を利用するリージョンを分散すると良い
- 予算があればプロビジョンドスループットを購入すると良い
  - 1 ヶ月単位で購入
- フロントエンドは Amplify, バックエンドは Lambda Adapter, Bedrock, Pinecone も利用している

## LT③ Anthropic Cookbook のおすすめレシピ

[slide](https://speakerdeck.com/schroneko/anthropic-cookbook-noosusumeresipi)

- cookbook には大きく 4 種の項目でノートブックが紹介されている

  - misc: Claude の機能や使い方
  - multimodal: 画像や音声などの扱い方
  - third_party: 外部サービスやライブラリとの連携方法
  - tool_use: ツールを使わせたり特定のタスクを行わせる方法

- 以下のノートブックが初見ではおすすめ
  - read_web_pages_with_haiku.ipynb: XML 特有のプロンプトの書き方がわかる
  - how_to_enable_json_mode.ipynb: json 出力させるためのプロンプトでの工夫がわかる
  - best_practices_for_vision.ipynb: API で画像を入力する方法，step by step で指示すると画像ファイル名と画像ファイルの中身が異なっていてもうまく画像認識させられる

### スライド中で紹介された参考になりそうな記事

- [君は Anthropic Tools を知っているか?](https://qiita.com/schroneko/items/a4098baa29580ec906b8)
- [Context Window のお話](https://speakerdeck.com/schroneko/context-window-noohua)

## LT④ Claude3 を使って RAG の一番の悩みポイントを解決してみた

[slide](https://dev.classmethod.jp/articles/lt-at-jaws-ug-bedrock-claude-night/)

- powerpoint 上でのテキストの読む順番は，生成 AI 側では判断しづらい
- powerpoint を Claude3 で markdown でまとめさせると，人間が読む順番で文字起こしできるのは良い idea
- 画像自体を文章として説明させる，PDF のヘッダー・ページ数などもよしなに無視してくれる．
- Amazon Titan の multi modal embedding はまだ日本語対応してない

### スライド中で紹介された参考になりそうな記事

- [Claude3 を使って人間が読むようにパワポ資料を読み込んでみる](https://dev.classmethod.jp/articles/read-powerpoint-document-with-claude-3/)
- [【Bedrock / Claude】AWS オンリーで RAG を使った生成 AI ボットを構築してみた【Kendra】](https://dev.classmethod.jp/articles/implement-rag-with-aws-services/)
- [Claude3 で認識できる文字のサイズを簡単に調べてみた](https://dev.classmethod.jp/articles/simple-examination-on-recognizable-char-size-with-claude-3/)
- [Claude3 と Azure AI Document Intelligence を使ってドキュメント読み取りの精度をあげてみた](https://dev.classmethod.jp/articles/fix-claude3-text-recognition-mistake-with-azure-document-intelligence/)

## LT⑤ 来てくれ Claude 3! Agents for Amazon Bedrock のモデル比較或いはチューニングの話

[slide](https://speakerdeck.com/hedgehog051/lai-tekureclaude-3-agents-for-amazon-bedrocknomoderubi-jiao-huo-ihatiyuningunohua)

- ナレッジベースは Claude3(Haiku, Sonnet)で利用可能
- 詳細プロンプト: エージェント作成時に用意されるプロンプトテンプレートセット
  - 前処理：ユーザーの入力をカテゴリー A~E に分類するようエージェントに指示
    - A: 悪意があるか
    - B: エージェントに提供されている関数，API に関連する情報を取得しようとしている
    - C: エージェントに提供された関数では提供できない質問
    - D: エージェントに提供された関数のみを利用して回答できる質問
    - E: 質問ではなく，エージェントがユーザーに訪ねた質問への回答となる入力
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

## その他(参考になるリンク)

- [AWS の生成 AI で社内文書検索！ Bedrock のナレッジベースで簡単に RAG アプリを作ってみよう](https://qiita.com/minorun365/items/24dfb0ea3afde6ed0a56)
- [AWS の生成 AI 最新機能ハンズオン！Bedrock の Knowledge Base と Agents に入門しよう](https://qiita.com/minorun365/items/86a3667290a8e5657f65)
- [AWS 入門ブログリレー 2024 〜Knowledge bases for Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-knowledge-bases-for-amazon-bedrock/)
- [AWS 入門ブログリレー 2024〜Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-aws-bedrock/)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)
- [LLM RAG Paradigms: Naive RAG, Advanced RAG & Modular RAG](https://medium.com/@drjulija/what-are-naive-rag-advanced-rag-modular-rag-paradigms-edff410c202e)
- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
- [LangChain×Bedrock(実装の参考になりそう)](https://twitter.com/cyber__BOSE/status/1782246450770137301)
- [Bedrock(Claude 3)対応のマルチモーダルチャットボットを Chainlit と LangChain(LCEL)で構築する](https://qiita.com/hayao_k/items/a3f7a893e4f6b71dc0b7?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)
