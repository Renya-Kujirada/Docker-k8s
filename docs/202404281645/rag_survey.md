# RAG Survey

本ドキュメントでは，RAG に関する技術調査を行った結果を自分用にまとめる．

## Papers

- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
- [Japanese SimCSE Technical Report](https://arxiv.org/abs/2310.19349)
- [how to survey](https://speakerdeck.com/a1da4/xin-ru-sheng-xiang-ketiyutoriaru-wen-xian-nosabeiv2?slide=17)
  - [参考](https://speakerdeck.com/kaityo256/how-to-survey)
- [Seven Failure Points When Engineering a Retrieval Augmented Generation System](https://arxiv.org/abs/2401.05856)
  - [tweet](https://x.com/hedgehog051/status/1791150826817569261)
- [RAGAS: Automated Evaluation of Retrieval Augmented Generation](https://arxiv.org/abs/2309.15217)

## My Important Article（Ragas）

- [LLM RAG Paradigms: Naive RAG, Advanced RAG & Modular RAG](https://medium.com/@drjulija/what-are-naive-rag-advanced-rag-modular-rag-paradigms-edff410c202e)
- [RAG の性能を改善するための 8 つの戦略](https://fintan.jp/page/10301/)
  - RAG の性能改善には検索側と生成側から取り組む必要がある
  - 検索対象のチャンクと検索結果として返すチャンクを切り分ける戦略が有効なことがある
  - embedding は，OSS model である`Multilingual-E5-large`は高性能（openai の ada に匹敵）
  - RAG では temperature を 0 にする
- [RAG の実装戦略まとめ](https://qiita.com/jw-automation/items/045917be7b558509fdf2)
- [RAG での回答精度向上のためのテクニック集（基礎編）](https://zenn.dev/knowledgesense/articles/47de9ead8029ba)
- [RAG の評価：評価の必要性と問題点](https://tech.beatrust.com/entry/2024/05/01/RAG%E3%81%AE%E8%A9%95%E4%BE%A1%EF%BC%9A%E8%A9%95%E4%BE%A1%E3%81%AE%E5%BF%85%E8%A6%81%E6%80%A7%E3%81%A8%E5%95%8F%E9%A1%8C%E7%82%B9)
- [Retrieval-Augmented Generation システムの改善方法の紹介](https://aitc.dentsusoken.com/column/Retrieval-Augmented_Generation)
- [RAG における Metrics-Driven Development を調べる](https://www.nogawanogawa.com/entry/metrics_driven_development)
- [simple-simcse-ja](https://github.com/hppRC/simple-simcse-ja)

## Advanced RAG

- [Create a multimodal assistant with advanced RAG and Amazon Bedrock](https://aws.amazon.com/jp/blogs/machine-learning/create-a-multimodal-assistant-with-advanced-rag-and-amazon-bedrock/)
- [Amazon Kendra と Amazon Bedrock で構成した RAG システムに対する Advanced RAG 手法の精度寄与検証](https://aws.amazon.com/jp/blogs/news/verifying-the-accuracy-contribution-of-advanced-rag-methods-on-rag-systems-built-with-amazon-kendra-and-amazon-bedrock/)
- [Python 3.12 で増えた並列処理と、これまでの並列処理の挙動を比べてみる](https://qiita.com/ShotaOki/items/3198eb695e1c6aa8cdaa)
- [【未経験者大歓迎】RAG 超入門：AWS が推奨する RAG を体験するハンズオン](https://qiita.com/moritalous/items/61f91039c13aeb9a51eb)
  - Command R+を利用している．非常に参考になる
- [LangChain への OpenAI の RAG 戦略の適用](https://note.com/npaka/n/n62cd25213679)
- [RAG (検索拡張生成) のさまざまな手法 (パターン)](https://netweblog.wordpress.com/2023/11/08/llm-advanced-rag-methods/)
- [RAG の実案件に取り組んできた今までの知見をまとめてみた](https://dev.classmethod.jp/articles/rag-knowledge-on-real-projects/)
- [【Bedrock×Lambda】高精度なハイブリッド検索 RAG をサーバレスで実装（Slack 連携も可）](https://qiita.com/Naoki_Ishihara/items/662d70a9bd0dc3a8c9ce?utm_content=buffer7dfba&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)
- [What is a Vector Database?](https://www.nvidia.com/en-us/glossary/vector-database/)
  - 距離の説明あり
- [【AI Shift Advent Calendar 2023】RAG を強化する](https://www.ai-shift.co.jp/techblog/4037)

## Advanced RAG(実装)

- [Corrective RAG (CRAG)](https://github.com/langchain-ai/langgraph/blob/main/examples/rag/langgraph_crag.ipynb)
- [LangGraph とは？サンプルコードをもとにわかりやすく解説](https://book.st-hakky.com/data-science/langgraph-intro/)
- [【Python】ChatGPT ＋ Google Custom Search API で Bing のチャットボットを再現してみた](https://qiita.com/keisuke-okb/items/3c0f82612dfc38535e53)
- [claude3 の知識を google search で強化する](https://zenn.dev/sikmi_tech/articles/cf007fcd16c643)
- [Corrective RAG](https://github.com/nohanaga/busho-index/blob/main/crag_azure_ai_search_bing.ipynb)
- [LangChain v0.2 で RAG を構築](https://note.com/npaka/n/ne892b713bd45?sub_rt=share_h)
- [LangChain v0.2 で 単純な LLM アプリケーションを構築](https://note.com/npaka/n/n24d48303a496?sub_rt=share_h)

## Eval RAG

- [build-an-automated-large-langurage-model-evaluation-pipeline-on-aws](https://github.com/aws-samples/build-an-automated-large-langurage-model-evaluation-pipeline-on-aws)
- [Amazon Bedrock モデル評価の「人間ベースの評価」を試してみた](https://qiita.com/sugino-k/items/c7213d4a5a1ec93ee9e0)
- [**社内規程集について回答してくれる生成 AI を評価してみた〜生成 AI のアーキテクチャ「RAG」の評価プロセス**](https://www.lac.co.jp/lacwatch/people/20240118_003651.html)
- [Tweet](https://x.com/SnowGushiGit/status/1785901559735632146)
- [openai/simple-evals](https://github.com/openai/simple-evals)
- [LLM プロダクト開発における独自評価基準とデータセットの作り方の考察](https://zenn.dev/seya/articles/ba06e37d226182)
- [LLM による LLM の評価とその評価の評価について](https://zenn.dev/seya/articles/b34345aab2949e)
- [Bedrock Embeddings モデルの日本語データセット性能比較（Titan Embeddings G1/V2、Cohere Embed）](]https://qiita.com/cyberBOSE/items/2efcde0307ea069772c9?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)

## Pinecone

- [Amazon Bedrock と Pinecone でマルチモーダル検索を行う](https://acro-engineer.hatenablog.com/entry/2024/05/08/100000)
- [Amazon Bedrock の Knowledge Base を Pinecone 無料枠で構築してみた](https://benjamin.co.jp/blog/technologies/bedrock-knowledgeaase-pinecone/)
- [[Rust] Amazon Bedrock のナレッジベースで Pinecone 使って RAG る](https://dev.classmethod.jp/articles/rust-bedrock-pinecode-rag/)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)

## Knowledge Base for Amazon Bedrock

- [Amazon Bedrock + Anthropic Claude 3 開発体験ワークショップ](https://catalog.us-east-1.prod.workshops.aws/workshops/7271111a-22bd-40e7-971a-817b0c083c67/ja-JP)
- [Knowledge Bases for Amazon Bedrock (with OpenSearch Serverless)を SAM で実装してみた](https://dev.classmethod.jp/articles/sam-knowledge-base-for-bedrock-with-oss/)
- [AWS の生成 AI で社内文書検索！ Bedrock のナレッジベースで簡単に RAG アプリを作ってみよう](https://qiita.com/minorun365/items/24dfb0ea3afde6ed0a56)
- [AWS の生成 AI 最新機能ハンズオン！Bedrock の Knowledge Base と Agents に入門しよう](https://qiita.com/minorun365/items/86a3667290a8e5657f65)
- [AWS 入門ブログリレー 2024〜Knowledge bases for Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-knowledge-bases-for-amazon-bedrock/)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)
- [【検証してみた】Amazon Bedrock のナレッジベースにおける日本語性能を向上させる技術検証](https://www.fsi.co.jp/blog/10661/)
- [Amazon Bedrock for Knowledge base を試す](https://zenn.dev/kun432/scraps/c3d65c44e60755)
- [Knowledge Bases for Amazon Bedrock がハイブリッド検索をサポート](https://aws.amazon.com/jp/blogs/news/knowledge-bases-for-amazon-bedrock-now-supports-hybrid-search/)
  - キーワード検索とセマンティック検索を組み合わせている
- [Amazon Bedrock、Amazon Aurora を組み合わせた RAG で回答精度の向上に取り組んでみた！① 概要編](https://qiita.com/Naoki_Ishihara/items/9f1b852917de19141847)
  - RAG の評価にも言及している
- [RetrieveAndGenerate の sessionId パラメーターはセッション保持以外にクエリ書き換えも行ってくれる](https://dev.classmethod.jp/articles/retrieve-and-generate-sessionid-parameter-session-query-rewrite/)
- [Amazon Bedrock KnowledgeBase の API を Lambda と API Gateway で利用してみた](https://benjamin.co.jp/blog/technologies/bedrock-knowledgebase-api-lambda/)
- [RAG architecture with Voyage AI embedding models on Amazon SageMaker JumpStart and Anthropic Claude 3 models](https://aws.amazon.com/jp/blogs/machine-learning/rag-architecture-with-voyage-ai-embedding-models-on-amazon-sagemaker-jumpstart-and-anthropic-claude-3-models/)

## Agents for Amazon Bedrock Return of Control

- [サンプルコードで理解する Agents for Amazon Bedrock の Return of Control](https://qiita.com/hayao_k/items/3478b43d73f576a591a1?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)
- [Agents for Amazon Bedrock の「Return of Control」機能の可能性を考察する](https://qiita.com/nasuvitz/items/2eb13a8b75e78cf11e8a)

## Agent for Amazon Bedrock

- [Agents for Amazon Bedrock にインスタンスの情報を収集させる](https://iret.media/104390?utm_campaign=3.0%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E3%83%96%E3%83%AD%E3%82%B0&utm_content=297413134&utm_medium=social&utm_source=twitter&hss_channel=tw-106958965)
- [Agents for Amazon Bedrock で Web サイトにチャットボット機能を足してみる](https://zenn.dev/akring/articles/55fe4c6b9b1614)
- [LLM エージェントのデザインパターン、Agentic Design Patterns を理解する](https://zenn.dev/loglass/articles/b9ee37737deb85)

## フィルタリング

- [【Bedrock】ナレッジベースのメタデータ検索用の metadata.json を自動作成してみた](https://qiita.com/hedgehog051/items/267014126f0e910a1adb)

## Custom Library

- [LangChain を使わない](https://tech-blog.abeja.asia/entry/advent-2023-day13)
- [taikinman/langrila](https://github.com/taikinman/langrila)
- [pdf から text を抜き出す試行錯誤のメモ](https://note.com/kan_hatakeyama/n/n1773c588ecb4)

## Command R+

- [Amazon Bedrock に Cohere Command R と Command R+ が来たよ！RAG がすげーよ！](https://qiita.com/moritalous/items/16797ea9d82295f40b5e)
- [Cohere の Command R/R+ において 128k input tokens は短いのか長いのか](https://qiita.com/kazuneet/items/3958eb42f45e7a8b9072)
- [Cohere Command R and Command R+ models](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-cohere-command-r-plus.html)
- [Retrieval Augmented Generation (RAG)](https://docs.cohere.com/docs/retrieval-augmented-generation-rag)
- [[アップデート] Amazon Bedrock で新モデル「Cohere Command R/R+」が利用可能になったので、RAG で使ってみた](https://dev.classmethod.jp/articles/amazon-bedrock-cohere-command-r-rag/)
- [Amazon Bedrock で Cohere Command のプロンプトの奥地に迫る](https://qiita.com/moritalous/items/7ce39c46fcddb9870476)

## Claude3

- [Run scalable, enterprise-grade generative AI workloads with Cohere Command R & R+, now available in Amazon Bedrock](https://aws.amazon.com/jp/blogs/aws/run-scalable-enterprise-grade-generative-ai-workloads-with-cohere-r-r-now-available-in-amazon-bedrock/)
- [Anthropic Claude Messages API](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-anthropic-claude-messages.html)
- [Amazon Bedrock + Anthropic Claude 3 開発体験ワークショップ](https://catalog.us-east-1.prod.workshops.aws/workshops/7271111a-22bd-40e7-971a-817b0c083c67/ja-JP)

## Amazon Titan Text V2

- [Amazon Titan Text V2 now available in Amazon Bedrock, optimized for improving RAG](https://aws.amazon.com/jp/blogs/aws/amazon-titan-text-v2-now-available-in-amazon-bedrock-optimized-for-improving-rag/)

## Amazon Q

- [Amazon Q Business Application の設定方法（2024/5/1 更新）](https://qiita.com/Neville/items/8bc10b1b7a29faae1c6b)

## Amplyfy

- [AWS Amplify の新世代 Gen2 で生成 AI アプリをサクッとデプロイ！](https://qiita.com/minorun365/items/5cfb4ff874e90332f7ec)
- [Amplify 🩷 Bedrock 〜生成 AI 入門〜](https://speakerdeck.com/minorun365/amplify-bedrock-sheng-cheng-airu-men?slide=29)

## 実験管理

- [Langfuse](https://x.com/MLBear2/status/1785816270748926414)

## bedrock studio

- [Bedrock Studio がプレビューリリース！早速試しました！！（構築方法と機能の紹介）](https://qiita.com/moritalous/items/c1839948c836f5a8c853?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)
- [Amazon Bedrock Studio (プレビュー) を使用した生成 AI アプリケーションの構築](https://aws.amazon.com/jp/blogs/news/build-generative-ai-applications-with-amazon-bedrock-studio-preview/)

## preprocess

- [RAG/LLM の前処理：PyMuPDF4LLM を使用して PDF を Markdown へ変換する](https://qiita.com/cyberBOSE/items/c276d273bfc20881adfc?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)

## LangChain

## Qiita

- [Bedrock と LCEL で AdvancedRAG のクエリ拡張をやってみる](https://qiita.com/cyberBOSE/items/89a86aa4677d3b9b2ef9)
- [LCEL （LangChain Expression Language）完全に理解した - Amazon Bedrock API で始める LLM 超入門 ⑨](https://qiita.com/cyberBOSE/items/fd65de9f857d36180fa5)
- [Bedrock(Claude 3)対応のマルチモーダルチャットボットを Chainlit と LangChain(LCEL)で構築する](https://qiita.com/hayao_k/items/a3f7a893e4f6b71dc0b7)

## AWS 公式

- [LLM による検索キーワードの書き換え・拡張](https://catalog.us-east-1.prod.workshops.aws/workshops/7271111a-22bd-40e7-971a-817b0c083c67/ja-JP/rag/advanced)

## 海外

- [I Built an Insanely Complex RAG Flow with LangGraph – You Won't Believe How Easy It Is](https://youtu.be/NZbgduKl9Zk?si=lAmmsWfe00ZrNbnW)
- [langgaph-course](https://github.com/emarco177/langgaph-course)
- [LangChain <> MistralAI Cookbooks](https://github.com/mistralai/cookbook/tree/main/third_party/langchain)

## others

- [Bedrock と LCEL で AdvancedRAG のクエリ拡張をやってみる](https://qiita.com/cyberBOSE/items/89a86aa4677d3b9b2ef9)
- [LCEL (LangChain Expression Language) 完全に理解した - Amazon Bedrock API で始める LLM 超入門 ⑨](https://qiita.com/cyberBOSE/items/fd65de9f857d36180fa5)
- [[翻訳] LangChain Expression Language を使い始める](https://qiita.com/taka_yayoi/items/f09678fe6dcd57c8d2b3)
- [LangChain-AWS](https://python.langchain.com/v0.1/docs/integrations/platforms/aws/)
- [【LangChain(LCEL)】3 つの Runnable 〇〇を理解する](https://blog.serverworks.co.jp/langchain-runnable-memo-1)
- [Amazon Bedrock で入門する LangChain](https://qiita.com/moritalous/items/60bcae924812a18d65b0)
- [実装例](https://github.com/os1ma/langchain-test-sample-20240513/blob/main/src/generate_markdown_recipe_chain.py)
- [【LangChain ゆる勉強会#5】LangChain のテスト関連機能を動かす【ランチタイム開催】](https://www.youtube.com/watch?v=BX9AgTxLLHY)
- [【LangChain ゆる勉強会#6】LangGraph のチュートリアルを動かしながら解説](https://studyco.connpass.com/event/318741/)

## RAGOps(実例)

- [運用の中で育てながら改善できる 「RAGOps」テンプレートをリリース](https://exawizards.com/exabase/studio/ragops/)

## Prompt Engineering

- [次世代 LLM の自律タスク実行に向けた高度なプロンプトエンジニアリングと実用例の紹介](https://developers.cyberagent.co.jp/blog/archives/46619/)

## 疑問点(自分用)

<details>
<summary>疑問点</summary>
<br/>

- OpenSearch Serverless で Analyzer を設定している場合，各チャンクに対して Char Filter, Tokenizer, Token Filter が実行され，その後 Embedding が行われるのか？
- Knowledge Base で自身で特有のチャンキング戦略を取りたい場合（例えば，LangChain の RecursiveCharacterTextSplitterplitter を利用して各パラグラフでチャンキングしたい場合など），事前に文書を前処理で split して s3 に保存しておく必要があるのか？
  - [Zenn の記事](https://zenn.dev/kun432/scraps/c3d65c44e60755)では，QA の CSV ファイルの各行を別ファイルとして書き出している．

</details>
<br/>
