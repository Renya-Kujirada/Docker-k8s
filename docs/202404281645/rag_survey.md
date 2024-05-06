# RAG Survey

本ドキュメントでは，RAG に関する技術調査を行った結果を自分用にまとめる．

## Papers

- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
- [Japanese SimCSE Technical Report](https://arxiv.org/abs/2310.19349)

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
- [RAG における Metrics-Driven Development を調べる](https://www.nogawanogawa.com/entry/metrics_driven_development)
- [simple-simcse-ja](https://github.com/hppRC/simple-simcse-ja)

## Advanced RAG

- [Amazon Kendra と Amazon Bedrock で構成した RAG システムに対する Advanced RAG 手法の精度寄与検証](https://aws.amazon.com/jp/blogs/news/verifying-the-accuracy-contribution-of-advanced-rag-methods-on-rag-systems-built-with-amazon-kendra-and-amazon-bedrock/)
- [Python 3.12 で増えた並列処理と、これまでの並列処理の挙動を比べてみる](https://qiita.com/ShotaOki/items/3198eb695e1c6aa8cdaa)
- [【未経験者大歓迎】RAG 超入門：AWS が推奨する RAG を体験するハンズオン](https://qiita.com/moritalous/items/61f91039c13aeb9a51eb)

  - Command R+を利用している．非常に参考になる

- [LangChain への OpenAI の RAG 戦略の適用](https://note.com/npaka/n/n62cd25213679)
- [RAG (検索拡張生成) のさまざまな手法 (パターン)](https://netweblog.wordpress.com/2023/11/08/llm-advanced-rag-methods/)

## Eval RAG

- [Tweet](https://x.com/SnowGushiGit/status/1785901559735632146)
- [openai/simple-evals](https://github.com/openai/simple-evals)

## Pinecone

- [Amazon Bedrock の Knowledge Base を Pinecone 無料枠で構築してみた](https://benjamin.co.jp/blog/technologies/bedrock-knowledgeaase-pinecone/)
- [[Rust] Amazon Bedrock のナレッジベースで Pinecone 使って RAG る](https://dev.classmethod.jp/articles/rust-bedrock-pinecode-rag/)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)

## Bedrock RAG

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

## Agents for Amazon Bedrock Return of Control

- [サンプルコードで理解する Agents for Amazon Bedrock の Return of Control](https://qiita.com/hayao_k/items/3478b43d73f576a591a1?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)
- [Agents for Amazon Bedrock の「Return of Control」機能の可能性を考察する](https://qiita.com/nasuvitz/items/2eb13a8b75e78cf11e8a)

## Agent for Amazon Bedrock

- [Agents for Amazon Bedrock で Web サイトにチャットボット機能を足してみる](https://zenn.dev/akring/articles/55fe4c6b9b1614)
- [LLM エージェントのデザインパターン、Agentic Design Patterns を理解する](https://zenn.dev/loglass/articles/b9ee37737deb85)

## custom library

- [LangChain を使わない](https://tech-blog.abeja.asia/entry/advent-2023-day13)
- [taikinman/langrila](https://github.com/taikinman/langrila)

## Command R+

- [Amazon Bedrock に Cohere Command R と Command R+ が来たよ！RAG がすげーよ！](https://qiita.com/moritalous/items/16797ea9d82295f40b5e)
- [Cohere の Command R/R+ において 128k input tokens は短いのか長いのか](https://qiita.com/kazuneet/items/3958eb42f45e7a8b9072)
- [Cohere Command R and Command R+ models](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-cohere-command-r-plus.html)
- [Retrieval Augmented Generation (RAG)](https://docs.cohere.com/docs/retrieval-augmented-generation-rag)
- [[アップデート] Amazon Bedrock で新モデル「Cohere Command R/R+」が利用可能になったので、RAG で使ってみた](https://dev.classmethod.jp/articles/amazon-bedrock-cohere-command-r-rag/)

## Claude3

- [Run scalable, enterprise-grade generative AI workloads with Cohere Command R & R+, now available in Amazon Bedrock](https://aws.amazon.com/jp/blogs/aws/run-scalable-enterprise-grade-generative-ai-workloads-with-cohere-r-r-now-available-in-amazon-bedrock/)
- [Anthropic Claude Messages API](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-anthropic-claude-messages.html)
- [Amazon Bedrock + Anthropic Claude 3 開発体験ワークショップ](https://catalog.us-east-1.prod.workshops.aws/workshops/7271111a-22bd-40e7-971a-817b0c083c67/ja-JP)

## Amazon Titan Text V2

- [Amazon Titan Text V2 now available in Amazon Bedrock, optimized for improving RAG](https://aws.amazon.com/jp/blogs/aws/amazon-titan-text-v2-now-available-in-amazon-bedrock-optimized-for-improving-rag/)

## Amazon Q

- [Amazon Q Business Application の設定方法（2024/5/1 更新）](https://qiita.com/Neville/items/8bc10b1b7a29faae1c6b)
- [Amplify 🩷 Bedrock 〜生成 AI 入門〜](https://speakerdeck.com/minorun365/amplify-bedrock-sheng-cheng-airu-men?slide=29)

## Amplyfy

- [AWS Amplify の新世代 Gen2 で生成 AI アプリをサクッとデプロイ！](https://qiita.com/minorun365/items/5cfb4ff874e90332f7ec)

## 実験管理

- [Langfuse](https://x.com/MLBear2/status/1785816270748926414)

## 疑問点(自分用)

<details>
<summary>prompt_template.yamlの中身（例）</summary>
<br/>

- OpenSearch Serverless で Analyzer を設定している場合，各チャンクに対して Char Filter, Tokenizer, Token Filter が実行され，その後 Embedding が行われるのか？
- Knowledge Base で自身で特有のチャンキング戦略を取りたい場合（例えば，LangChain の RecursiveCharacterTextSplitterplitter を利用して各パラグラフでチャンキングしたい場合など），事前に文書を前処理で split して s3 に保存しておく必要があるのか？

  - [Zenn の記事](https://zenn.dev/kun432/scraps/c3d65c44e60755)では，QA の CSV ファイルの各行を別ファイルとして書き出している．

- 疑問点（retrieve_and_generate の返り値について）

`response = bedrock_agent_client.retrieve_and_generate`[1] の返り値につきまして，以下の違いをご教示いただきたいです．

- (a) response['citations'][0]['generatedResponsePart']['textResponsePart']['text']
- (b) response['output']['text']

以下の公式ドキュメント[2][3]によると，(a)は「引用部を含む，生成されたテキスト（の一部？）」であり，(b)は「knowledge base のクエリから生成されたレスポンス」と明記されております．しかし，複数回`retrieve_and_generate`を実行しましたが，上記(a)と(b)は同値でした．こちらにつきまして，(a)と(b)の差分は無いのかどうかご教示いただけますと幸いです．

よろしくお願いいたします．

[1]: https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent-runtime_RetrieveAndGenerate.html
[2]: https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent-runtime_RetrieveAndGenerateOutput.html#bedrock-Type-agent-runtime_RetrieveAndGenerateOutput-text
[3]: https://docs.aws.amazon.com/bedrock/latest/APIReference/API_agent-runtime_TextResponsePart.html#bedrock-Type-agent-runtime_TextResponsePart-text

</details>
<br/>
