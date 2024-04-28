# RAG Survey

本ドキュメントでは，RAG に関する技術調査を行った結果を自分用にまとめる．

## 疑問点

- OpenSearch Serverless で Analyzer を設定している場合，各チャンクに対して Char Filter, Tokenizer, Token Filter が実行され，その後 Embedding が行われるのか？
- Knowledge Base で自身で特有のチャンキング戦略を取りたい場合（例えば，LangChain の RecursiveCharacterTextSplitterplitter を利用して各パラグラフでチャンキングしたい場合など），事前に文書を前処理で split して s3 に保存しておく必要があるのか？

## References

### Papers

- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
- [Japanese SimCSE Technical Report](https://arxiv.org/abs/2310.19349)

### Articles

- [LLM RAG Paradigms: Naive RAG, Advanced RAG & Modular RAG](https://medium.com/@drjulija/what-are-naive-rag-advanced-rag-modular-rag-paradigms-edff410c202e)
- [RAG の性能を改善するための 8 つの戦略](https://fintan.jp/page/10301/)
  - RAG の性能改善には検索側と生成側から取り組む必要がある
  - 検索対象のチャンクと検索結果として返すチャンクを切り分ける戦略が有効なことがある
  - embedding は，OSS model である`Multilingual-E5-large`は高性能（openai の ada に匹敵）
  - RAG では temperature を 0 にする
- [RAG の実装戦略まとめ](https://qiita.com/jw-automation/items/045917be7b558509fdf2)
- [RAG での回答精度向上のためのテクニック集（基礎編）](https://zenn.dev/knowledgesense/articles/47de9ead8029ba)
- [simple-simcse-ja](https://github.com/hppRC/simple-simcse-ja)

### Bedrock

- [AWS の生成 AI で社内文書検索！ Bedrock のナレッジベースで簡単に RAG アプリを作ってみよう](https://qiita.com/minorun365/items/24dfb0ea3afde6ed0a56)
- [AWS の生成 AI 最新機能ハンズオン！Bedrock の Knowledge Base と Agents に入門しよう](https://qiita.com/minorun365/items/86a3667290a8e5657f65)
- [AWS 入門ブログリレー 2024〜Knowledge bases for Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-knowledge-bases-for-amazon-bedrock/)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)
- [【検証してみた】Amazon Bedrock のナレッジベースにおける日本語性能を向上させる技術検証](https://www.fsi.co.jp/blog/10661/)
