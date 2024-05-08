# Infra-tips

Tips about docker, dev-container(vscode), k8s, nvidia-driver, git, Ubuntu.

## [Docker on Vscode](https://ren8k.github.io/Infra-tips/docs/202209172125/tips_dev-container.html)

Vscode の dev-container を利用する際の Tips

## [OneDrive を活用した Git 運用](https://ren8k.github.io/Infra-tips/docs/202209202058/tips_git.html)

業務などで Git サーバーが利用できない場合，OneDrive を Git サーバーの代替として利用する際の Tips

## [nvidia-driver 周りのエラー時の解決方法](https://ren8k.github.io/Infra-tips/docs/202210252319/tips_nvidia_driver.html)

docker を導入しているマシン上で nvidia-driver が壊れた場合(`nvidia-smi`で以下のエラーが発生する場合)の Tips

```sh
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

## [Line for Ubuntu](https://ren8k.github.io/Infra-tips/docs/202211220117/tips_line_for_ubuntu.html)

LINE を Ubuntu でアプリのように利用したい場合の Tips

## [Chrome Remote Desktop on Ubuntu](https://ren8k.github.io/Infra-tips/docs/202301031921/tips_chrome_remote_desktop.html)

ubuntu サーバに remote desktop 接続したい場合の Tips．team viewer と異なり，remote 接続時に reboot しても接続できるためおすすめ．

## [AWS Cloud9 IDE を利用した Deep Learning 開発環境を構築する方法](https://ren8k.github.io/Infra-tips/docs/202309032358/tips_cloud9.html)

AWS Cloud9 上での Deep Learning 開発環境を構築するための Tips．CloudFormation template を利用し，Deep Learning AMI から EC2 インスタンスを作成後に，SSH 環境の Cloud9 を構築する．

## [AWS CodeWhisperer が収集するデータについての調査内容](https://ren8k.github.io/Infra-tips/docs/202309151938/tips_codewhisperer.html)

CodeWhisperer を業務適用しても，AWS 側にコーディング内容が共有されないかどうかを調査した．

## [VSCode Dev Containers を利用した AWS EC2 上での開発環境構築手順](https://ren8k.github.io/Infra-tips/docs/202312311851/tips_remote_dev_on_ec2_with_vscode.html)

AWS 上で開発する際，社内プロキシ等が原因で VSCode から容易に Remote SSH できず，開発 IDE として VSCode を利用できない事例を多数見てきました．
これにより，チーム開発時に，各メンバが異なる IDE（異なる Linter, Formatter）を利用する結果，チームとしての開発効率が低下する課題がございました．
そこで，以下の Tips を整理し，[本リポジトリ](https://github.com/ren8k/aws-ec2-devkit-vscode)にまとめました．

- SSM 経由で VSCode から EC2 にセキュアに SSH 接続する方法
- チーム開発時の IDE として VSCode を利用し，Flake8，Black，Mypy を共通的に利用する方法
- AWS Deep Learning Containers Images をベースに Dev Containers 上で開発するための方法

本 Tips は，EC2 上での SageMaker Pipeline の開発や SageMaker Training Job の実行のみならず，HuggingFace 等の多様な FM を推論するための環境を，
EC2 上のコンテナにクイックに構築したいケースにも利用できます！（特に，SageMaker Jumpstart で提供されていないモデルを実行する際などにはオススメです！）

なお，[本リポジトリ](https://github.com/ren8k/aws-ec2-devkit-vscode)では，開発チームメンバ全員に導入することを主眼としており，丁寧に解説しております．

本 Tips がどなたかのお役に立てれば幸いです．

## [SageMaker Training Job Template](https://ren8k.github.io/Infra-tips/docs/202403312357/tips_sagemaker_training_job.html)

昨今，AWS Bedrock などで生成 AI の利用が活発化しておりますが，業務などの PoC において，機械学習を利用するケースはまだ多い印象があります．特に，PoC で様々なハイパーパラメーターの設定で実験を行う場合，SageMaker Training Job と SageMaker Experiments を利用した実験管理・学習実行が非常に有効です．

しかし，これらを実際の PoC などで迅速に利用可能な実装例・テンプレートは多いとは言えず，特に，Python スクリプトベースの実装例などは少ないと感じました．（AWS 公式リポジトリには沢山 Jupyter Notebook での解説実装はございます）

そこで，実務や Kaggle での SageMaker の利用経験を基に，ローカルで開発した機械学習コードをスムーズに SageMaker Training Job で利用可能なテンプレートを作成しました．私のこれまでの SageMaker のナレッジ・運用ノウハウを全て詰め込んだテンプレート・ドキュメントを作成できたと自負しておりますので，是非ご覧いただければ幸いです．

## [Bedrock Claude Night（JAWS-UG AI/ML 支部 × 東京支部コラボ）の個人メモ](https://ren8k.github.io/Infra-tips/docs/202404222330/bedrock_claude_night.html)

大変参考になったので自分用にメモしました．

## [RAG Survey](https://ren8k.github.io/Infra-tips/docs/202404281645/rag_survey.html)

RAG についての調査メモです．

## [Knowledge Bases for Amazon Bedrock を利用した RAG のベースライン](https://ren8k.github.io/Infra-tips/docs/202405021217/aws_bedrock_rag_baseline.html)

Knowledge Bases for Amazon Bedrock を利用した RAG の Python 実装（ベースライン）を公開しました．紹介しているリポジトリでは，boto3 のみを利用して実装しており，利用する LLM を容易に切り替えられるようシンプルな設計にしております．加えて，LLM の設定・プロンプトなどは yaml ファイルで管理しております．Command R+や， Claude3 Opus での streaming chat も可能です．

## [Knowledge Bases for Amazon Bedrock を利用した Advanced RAG のベースライン](https://ren8k.github.io/Infra-tips/docs/202405061900/aws_bedrock_advanced_rag_baseline.html)

先日公開された AWS 公式の Advanced RAG の技術検証ブログの再現実装を行い，その Python 実装（ベースライン）を公開しました．紹介しているリポジトリでは，Bedrock を利用してクエリ拡張，検索結果の関連度評価を行うことが可能です．また，Claude3 Haiku に加え，Command R+を利用した Advanced RAG を検証することも可能です．
