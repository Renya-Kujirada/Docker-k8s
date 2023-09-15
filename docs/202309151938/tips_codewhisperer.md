# AWS CodeWhispererが収集するデータについての調査内容

本ドキュメントでは，CodeWhispererのデータの取り扱い（コーディング内容がAWSに共有されるのかどうか）について調査した内容を備忘としてまとめておく．なお，本ドキュメントの情報は執筆日時点（2023/09/15）の情報であることに留意されたい．

## TL;DR

- 以下の場合，CodeWhispererはコーディング内容を収集・AWSに共有しない
  - Cloud9を利用する場合
  - CodeWhisperer Professional版を利用する場合
- CodeWhisperer Individual版でも，コーディング内の共有を拒否することが可能

## CodeWhispererとは

リアルタイムでコードを生成・提案することで，コーディングを補助するためのサービスである．（Github CopilotのAWS版だと思えばイメージしやすい）


## CodeWhispererが収集するデータについて

ユーザードキュメント[[1]](https://docs.aws.amazon.com/ja_jp/codewhisperer/latest/userguide/sharing-data.html) によると，CodeWhispererは，サービス向上のために，テレメトリとコンテンツを収集する可能性がある．ここで，テレメトリとは，サービスの使用状況のことであり，具体的には，CodeWhispererが提案したコードを受け入れたか否か等の情報である．コンテンツとは，CodeWhispererが提案を生成するために読み取ったコード部および，提案したコード自体のことである．

例えば，業務などでCodeWhispererを利用したい場合，コーディングした内容をCodeWhispererに収集されたくないと思うだろう．この場合，どのようにCodeWhispererを利用すればよいのか疑問に思ったため調査した．

ユーザードキュメント[[1]](https://docs.aws.amazon.com/ja_jp/codewhisperer/latest/userguide/sharing-data.html) の Opting out of sharing your content に答えが書いてあった．(AWS公式のFAQにはこの情報は載っておらず，どこに情報が掲載されているのか探すのに時間がかかってしまった．．)

- Cloud9を利用する場合，CodeWhispererはコンテンツ共有を行わない．
- CodeWhisperer Professional版も同様に，コンテンツ共有を行わない．
- CodeWhisperer Individual版であっても，設定変更することでコンテンツ共有をopt out可能．

## 参考

- [Getting started](https://docs.aws.amazon.com/ja_jp/codewhisperer/latest/userguide/getting-started.html)
- [Amazon CodeWhisperer のよくある質問](https://aws.amazon.com/jp/codewhisperer/faqs/)
- [With VS Code and JetBrains](https://docs.aws.amazon.com/ja_jp/codewhisperer/latest/userguide/getting-started-with-toolkits.html)
