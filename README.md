# Infra-tips
Tips about docker, dev-container(vscode), k8s, nvidia-driver, git, Ubuntu.

## [Docker on Vscode](https://ren8k.github.io/Infra-tips/docs/202209172125/tips_dev-container.html)

Vscodeのdev-containerを利用する際のTips

## [OneDriveを活用したGit運用](https://ren8k.github.io/Infra-tips/docs/202209202058/tips_git.html)

業務などでGitサーバーが利用できない場合，OneDriveをGitサーバーの代替として利用する際のTips

## [nvidia-driver周りのエラー時の解決方法](https://ren8k.github.io/Infra-tips/docs/202210252319/tips_nvidia_driver.html)

dockerを導入しているマシン上でnvidia-driverが壊れた場合(`nvidia-smi`で以下のエラーが発生する場合)のTips

```sh
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

## [Line for Ubuntu](https://ren8k.github.io/Infra-tips/docs/202211220117/tips_line_for_ubuntu.html)

LINEをUbuntuでアプリのように利用したい場合のTips

## [Chrome Remote Desktop on Ubuntu](https://ren8k.github.io/Infra-tips/docs/202301031921/tips_chrome_remote_desktop.html)

ubuntuサーバにremote desktop接続したい場合のTips．team viewerと異なり，remote 接続時にrebootしても接続できるためおすすめ．

## [AWS Cloud9 IDE を利用したDeep Learning開発環境を構築する方法](https://ren8k.github.io/Infra-tips/docs/202309032358/tips_cloud9.html)

AWS Cloud9上でのDeep Learning開発環境を構築するためのTips．CloudFormation templateを利用し，Deep Learning AMIからEC2インスタンスを作成後に，SSH環境のCloud9を構築する．

## [AWS CodeWhispererが収集するデータについての調査内容](https://ren8k.github.io/Infra-tips/docs/202309151938/tips_codewhisperer.html)

CodeWhispererを業務適用しても，AWS側にコーディング内容が共有されないかどうかを調査した．

## [VSCode Dev Containers を利用した AWS EC2 上での開発環境構築手順](https://ren8k.github.io/Infra-tips/docs/202312311851/tips_remote_dev_on_ec2_with_vscode.html)

AWS上で開発する際，社内プロキシ等が原因でVSCodeから容易にRemote SSHできず，開発IDEとしてVSCodeを利用できない事例を多数見てきました．
これにより，チーム開発時に，各メンバが異なるIDE（異なるLinter, Formatter）を利用する結果，チームとしての開発効率が低下する課題がございました．
そこで，以下のTipsを整理し，[本リポジトリ](https://github.com/ren8k/aws-ec2-devkit-vscode)にまとめました．

- SSM経由でVSCodeからEC2にセキュアにSSH接続する方法
- チーム開発時のIDEとしてVSCodeを利用し，Flake8，Black，Mypyを共通的に利用する方法
- AWS Deep Learning Containers Images をベースに Dev Containers上で開発するための方法

本Tipsは，EC2上でのSageMaker Pipelineの開発やSageMaker Training Jobの実行のみならず，HuggingFace等の多様なFMを推論するための環境を，
EC2上のコンテナにクイックに構築したいケースにも利用できます！（特に，SageMaker Jumpstartで提供されていないモデルを実行する際などにはオススメです！）

なお，[本リポジトリ](https://github.com/ren8k/aws-ec2-devkit-vscode)では，開発チームメンバ全員に導入することを主眼としており，丁寧に解説しております．

本Tipsがどなたかのお役に立てれば幸いです．

## [SageMaker Training Job Template](https://ren8k.github.io/Infra-tips/docs/202403312357/tips_sagemaker_training_job.html)

昨今，AWS Bedrockなどで生成AIの利用が活発化しておりますが，業務などのPoCにおいて，機械学習を利用するケースはまだ多い印象があります．特に，PoCで様々なハイパーパラメーターの設定で実験を行う場合，SageMaker Training JobとSageMaker Experimentsを利用した実験管理・学習実行が非常に有効です． 

しかし，これらを実際のPoCなどで迅速に利用可能な実装例・テンプレートは多いとは言えず，特に，Pythonスクリプトベースの実装例などは少ないと感じました．（AWS公式リポジトリには沢山Jupyter Notebookでの解説実装はございます）  

そこで，実務や Kaggle での SageMaker の利用経験を基に，ローカルで開発した機械学習コードをスムーズにSageMaker Training Jobで利用可能なテンプレートを作成しました．私のこれまでのSageMakerのナレッジ・運用ノウハウを全て詰め込んだテンプレート・ドキュメントを作成できたと自負しておりますので，是非ご覧いただければ幸いです．
