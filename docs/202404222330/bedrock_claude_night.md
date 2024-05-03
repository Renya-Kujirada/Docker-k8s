# Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）の個人メモ

## movie

- [Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）](https://youtube.com/live/Aspb-QF3iDU)
- [Anthropic Keynote Session in JAWS Bedrock Claude Night on 2024/4/22](https://www.youtube.com/watch?v=yJg-SK9KkHg)
- [slide all](https://jawsug-ai.connpass.com/event/313318/presentation/)

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
- [Claude3 Technical Presentation](https://docs.google.com/presentation/d/e/2PACX-1vTOOynV_8_14nJZMBf4nDDikuF5aLH-2yzTAayBd9bEBgWB5J4WmwZ92fVziwEKROkhgpanN5E3vopI/pub?slide=id.g2c736259dac_63_0)

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
  - [retry decorator](https://github.com/aws-samples/amazon-bedrock-workshop/blob/main/02_KnowledgeBases_and_RAG/0_create_ingest_documents_test_kb.ipynb) を使うと良いかも？
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
- 言ってることは以下に似ている
  - [指示とデータの分離及び構造化](https://x.com/kazuneet/status/1781916223376388350)
  - [指示は最後に持ってきたほうが聞いてくれる感じあるので、データの中に指示を埋もれさせないためにタグ使うのは有効](https://x.com/tmokmss/status/1781922172627546377)

## その他(参考になるリンク)

- [AWS の生成 AI で社内文書検索！ Bedrock のナレッジベースで簡単に RAG アプリを作ってみよう](https://qiita.com/minorun365/items/24dfb0ea3afde6ed0a56)
- [AWS の生成 AI 最新機能ハンズオン！Bedrock の Knowledge Base と Agents に入門しよう](https://qiita.com/minorun365/items/86a3667290a8e5657f65)
- [[アップデート] 有害・危険なコンテンツをブロックする「Guardrails for Amazon Bedrock」が GA になりました！](https://dev.classmethod.jp/articles/guardrails-for-amazon-bedrock-general-availability/)
- [AWS 入門ブログリレー 2024〜Agents for Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-agents-for-amazon-bedrock/)
- [AWS 入門ブログリレー 2024〜Knowledge bases for Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-knowledge-bases-for-amazon-bedrock/)
- [AWS 入門ブログリレー 2024〜Amazon Bedrock 編〜](https://dev.classmethod.jp/articles/introduction-2024-aws-bedrock/)
- [AWS Marketplace の Pinecone を Amazon Bedrock のナレッジベースとして利用する](https://aws.amazon.com/jp/blogs/news/leveraging-pinecone-on-aws-marketplace-as-a-knowledge-base-for-amazon-bedrock/)
- [LLM RAG Paradigms: Naive RAG, Advanced RAG & Modular RAG](https://medium.com/@drjulija/what-are-naive-rag-advanced-rag-modular-rag-paradigms-edff410c202e)
- [Retrieval-Augmented Generation for Large Language Models: A Survey](https://arxiv.org/abs/2312.10997)
- [LangChain×Bedrock(実装の参考になりそう)](https://twitter.com/cyber__BOSE/status/1782246450770137301)
- [Python 約 30 行で作る Bedrock x Claude3 の Streaming チャットアプリ](https://qiita.com/cyberBOSE/items/cfaadabe2dd85039a740?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)
- [【Bedrock×Lambda】高精度なハイブリッド検索 RAG をサーバレスで実装（Slack 連携も可）](https://qiita.com/Naoki_Ishihara/items/662d70a9bd0dc3a8c9ce?utm_content=buffer0581a&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)
- [Bedrock(Claude 3)対応のマルチモーダルチャットボットを Chainlit と LangChain(LCEL)で構築する](https://qiita.com/hayao_k/items/a3f7a893e4f6b71dc0b7?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)
- [【検証してみた】Amazon Bedrock のナレッジベースにおける日本語性能を向上させる技術検証](https://www.fsi.co.jp/blog/10661/)
- [RAG の性能を改善するための 8 つの戦略](https://fintan.jp/page/10301/)
  - 性能改善については主に検索側と生成側から取り組む必要があるが，本記事では検索側に焦点を当てて解説している
- [RAG の実装戦略まとめ](https://qiita.com/jw-automation/items/045917be7b558509fdf2)
- [Agents for Amazon Bedrock の作成がより簡単になった！](https://acro-engineer.hatenablog.com/entry/2024/04/26/102947)
- [Agents for Amazon Bedrock の "ユーザー入力" を CloudFromation で有効にする](https://zenn.dev/akring/articles/1dbd1a3d6b1cf1)
- [[アップデート]Knowledge bases for Amazon Bedrock で複数データソースがサポートされました](https://dev.classmethod.jp/articles/knowledge-bases-for-amazon-bedrock-multiple-data-sources/)
- [Anthropic Claude - Prompt Design 大全](https://qiita.com/kiiwami/items/4a62a3dcbedeb141e605)
- [【Command R+】オープンソース界最強 LLM が GPT-4 レベルの性能を達成](https://weel.co.jp/media/tech/command-r-plus/)
  - Cohere のトークンナイザは日本語に最適化されており，[Claude に比べると約 1.7 分の 1 程度のトークン数](https://x.com/Ishihara_Naok1/status/1785102407556595896)となる
  - コンテキストウィンドウが 128K?

---

## その他(公式ドキュメント)

### 機能リリース watching

- [Document history for the Amazon Bedrock User Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/doc-history.html)

---

## 公式リポジトリ/workshop

### Bedrock

- [amazon-bedrock-samples](https://github.com/aws-samples/amazon-bedrock-samples)
- [generative-ai-use-cases-jp](https://github.com/aws-samples/generative-ai-use-cases-jp)

### RAG

#### Knowledge Base(オススメ)

- [Knowledge Bases for Amazon Bedrock Workshop(オススメ)](https://github.com/aws-samples/amazon-bedrock-workshop)
  - バックエンドとしては OpenSearch Serverless, RDS, Redis Enterpise Cloud, Pinecone が使える
- [Rag Architecture using Amazon Bedrock and OpenSearch(オススメ)](https://github.com/aws-samples/rag-using-langchain-amazon-bedrock-and-opensearch)
- [amazon-bedrock-samples-knowledge-base](https://github.com/aws-samples/amazon-bedrock-samples/tree/main/knowledge-bases)

#### Kendra

- [jp-rag-sample](https://github.com/aws-samples/jp-rag-sample)
- [Amazon Kendra を利用した Retrieval Augmented Generation (RAG) ハンズオン](https://catalog.us-east-1.prod.workshops.aws/workshops/6708bce5-6aa3-4acb-89f7-85c39c006c8c/en-US)

#### Llamaindex

- https://github.com/aws-samples/amazon-bedrock-rag-workshop

### Amazon Q

- [Amazon Q Business workshop (Innovate on enterprise data with generative AI & Amazon Q Business application)](https://catalog.workshops.aws/amazon-q-business/en-US)

### LangChain

- [LangChain を用いた 4 種類の RAG 質問応答 chain の実装と性能比較](https://zenn.dev/aidemy/articles/97d5fb6ac03a4f)

---

## その他(最近の機能リリース)

### 2024/04/24

- [Bedrock で Cohere Command R+が利用可能になる予定](https://twitter.com/ajassy/status/1782879689369149773)

### 2024/04/23

#### feature

- Bedrock Agent で Claude3(Haiku/Sonnet)がサポート
- Bedrock Knowledge Base のデータソースが複数選択可能に
- Knowledge Base の設定無しに，Chat でドキュメントをアップロードしてそのドキュメントを踏まえてチャット可能に
  - File types: PDF, MD, TXT, DOC, DOCX, HTML, CSV, XLS, XLSX (Max. 10 MB)
- [Bedrock Agent のアクショングループを定義可能に](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-how.html)
- [SageMaker などで学習したカスタムモデルを Bedrock で import 可能(preview)](https://aws.amazon.com/jp/blogs/aws/import-custom-models-in-amazon-bedrock-preview/)
  - Llama2/3、Mistral ベースのモデルを import し API 形式で利用可能
- [Guardrails for Bedrock が利用可能に](https://aws.amazon.com/jp/blogs/aws/guardrails-for-amazon-bedrock-now-available-with-new-safety-filters-and-privacy-controls/)
  - 安全フィルターおよびプライバシー制御（マスキング）機能
  - FT したモデルにも適用可能
- [Agents for Amazon Bedrock: 簡素化された作成と構成エクスペリエンスの導入](https://aws.amazon.com/jp/blogs/aws/agents-for-amazon-bedrock-introducing-a-simplified-creation-and-configuration-experience/)
  - OpenAPI スキーマ(Agent が呼び出すことのできる API 操作の定義)が不要に．

#### model

- [Amazon Titan Image Generator が GA](https://aws.amazon.com/jp/blogs/aws/amazon-titan-image-generator-and-watermark-detection-api-are-now-available-in-amazon-bedrock/)
- [Bedrock で Llama 3 が利用可能に(バージニアとオレゴンのみ)](https://aws.amazon.com/jp/blogs/aws/metas-llama-3-models-are-now-available-in-amazon-bedrock/)
  - meta.llama3-8b-instruct-v1:0
  - meta.llama3-70b-instruct-v1:0
- [Amazon Titan Text Embeddings V2 が近日提供予定](https://aws.amazon.com/jp/blogs/machine-learning/new-capabilities-make-it-easier-to-use-amazon-bedrock-to-build-and-scale-generative-ai-applications-and-deliver-impact/)

#### source:

- [Document history for the Amazon Bedrock User Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/doc-history.html)
- [AWS News Blog](https://aws.amazon.com/jp/blogs/aws/)
- [Significant new capabilities make it easier to use Amazon Bedrock to build and scale generative AI applications – and achieve impressive results](https://aws.amazon.com/jp/blogs/machine-learning/new-capabilities-make-it-easier-to-use-amazon-bedrock-to-build-and-scale-generative-ai-applications-and-deliver-impact/)
- [Building scalable, secure, and reliable RAG applications using Knowledge Bases for Amazon Bedrock](https://aws.amazon.com/jp/blogs/machine-learning/building-scalable-secure-and-reliable-rag-applications-using-knowledge-bases-for-amazon-bedrock/)
- [2024/4/23 Amazon Bedrock アップデート祭りメモ](https://qiita.com/hayao_k/items/3f08113c0ea56c4699aa?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share)

---

## 公式ブログ(LLMOps)

- [Enhance conversational AI with advanced routing techniques with Amazon Bedrock](https://aws.amazon.com/jp/blogs/machine-learning/enhance-conversational-ai-with-advanced-routing-techniques-with-amazon-bedrock/)
  - Agent for Amazon Bedrock，または LangChain でアプリケーションを実装する際のメリデメを述べている．
  - アーキテクチャ例も提示されており，参考になりそう．
- [Evaluate the text summarization capabilities of LLMs for enhanced decision-making on AWS](https://aws.amazon.com/jp/blogs/machine-learning/evaluate-the-text-summarization-capabilities-of-llms-for-enhanced-decision-making-on-aws/)
  - LLM による要約出力の評価方法について述べている
- [Amazon Bedrock のカスタムモデルを使用して Amazon Titan Image Generator G1 モデルをファインチューニングする](https://aws.amazon.com/jp/blogs/news/fine-tune-your-amazon-titan-image-generator-g1-model-using-amazon-bedrock-model-customization/)
  - Bedrock 上のモデルを FT する際の仕組みがわかりやすく解説されている．
  - データセットは外部に保存されることはなく，モデルの改善に利用されることは無い．
- [Amazon Bedrock で手軽に絵芝居を作れるシステムを開発してみた](https://aws.amazon.com/jp/builders-flash/202404/bedrock-eshibai-generation/?sc_channel=em&sc_campaign=builders_flash_mail_202404&sc_publisher=aws&sc_medium=em_builders_flash_mail_202404&sc_content=devadopt_ot_prodadp&sc_country=jp&sc_geo=japn&sc_outcome=devadopt&trkCampaign=builders_flash_mail_202404&trk=em_builders_flash_mail_202404&mkt_tok=MTEyLVRaTS03NjYAAAGSN5WeF-HRKm0ePEcbU52YS5IXFd9GVMIHo-CjEggVmGIeCCCQRS212JFSlaOVCRP8ahr45hxqD0GiCRTbwzjXt0H0H32s8Pw25kwkIKCzEzJ_fI7YX0Ox&awsf.filter-name=*all)
  - プロンプトチェーンを利用した具体例
  - [stability.ai のプロンプトガイド](https://beta.dreamstudio.ai/prompt-guide)も紹介されている
- [FMOps/LLMOps：生成系 AI の運用と MLOps との違い](https://aws.amazon.com/jp/blogs/news/fmops-llmops-operationalize-generative-ai-and-differences-with-mlops/)
  - FMOps におけるモデルの選定・ファインチューニング・評価の方法論が述べられている．
  - モデル評価時にはプロンプトカタログという評価用のテンプレートプロンプト集を利用しているのが興味深い

---

<details>
<summary>※BlackBeltの資料など</summary>
<br/>

- [Amazon OpenSearch Serverless AWS Black Belt Online Seminar](https://pages.awscloud.com/rs/112-TZM-766/images/AWS-Black-Belt_2023_AmazonOpenSearchServerless_0131_v1.pdf)
  - コレクション > インデックス > ドキュメントの概念がある
- [Amazon OpenSearch Service AWS Black Belt Online Semina](https://pages.awscloud.com/rs/112-TZM-766/images/AWS-Black-Belt_2023_Amazon-OpenSearch-Service-Basic_0131_v1.pdf)
- [Amazon OpenSearch Service 機能解説 – 検索編 AWS Black Belt Online Seminar](https://pages.awscloud.com/rs/112-TZM-766/images/AWS-Black-Belt_2023_Amazon-OpenSearch-Service-Advanced-Search_0131_v1.pdf)
- [Amazon OpenSearch Service のベクトルデータベース機能の説明](https://aws.amazon.com/jp/blogs/news/amazon-opensearch-services-vector-database-capabilities-explained/)
- [OpenSearch を使⽤したベクトル検索](https://pages.awscloud.com/rs/112-TZM-766/images/20231005-Analytics-03-AWS.pdf)
- [Amazon OpenSearch Serverless による手軽なログ分析](https://aws.amazon.com/jp/blogs/news/log-analytics-the-easy-way-with-amazon-opensearch-serverless/)
- [2023 年 1 月の AWS Black Belt オンラインセミナー資料及び動画公開のご案内](https://aws.amazon.com/jp/blogs/news/2023-01-aws-blackbelt/)

</details>
<br/>

## ※見ていくべき技術スタック

- Knowledge Base(RAG)
- Advanced RAG
- Agents
- LangChain
- security(Guardrails)
- backup(opensearch の自動スナップショットなど)
