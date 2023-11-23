# Infra-tips
Tips about docker, dev-container(vscode), k8s, nvidia-driver, git, Ubuntu.

## [Docker on Vscode](https://renya-kujirada.github.io/Infra-tips/docs/202209172125/tips_dev-container.html)

Vscodeのdev-containerを利用する際のTips

## [OneDriveを活用したGit運用](https://renya-kujirada.github.io/Infra-tips/docs/202209202058/tips_git.html)

業務などでGitサーバーが利用できない場合，OneDriveをGitサーバーの代替として利用する際のTips

## [nvidia-driver周りのエラー時の解決方法](https://renya-kujirada.github.io/Infra-tips/docs/202210252319/tips_nvidia_driver.html)

dockerを導入しているマシン上でnvidia-driverが壊れた場合(`nvidia-smi`で以下のエラーが発生する場合)のTips

```sh
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

## [Line for Ubuntu](https://renya-kujirada.github.io/Infra-tips/docs/202211220117/tips_line_for_ubuntu.html)

LINEをUbuntuでアプリのように利用したい場合のTips

## [Chrome Remote Desktop on Ubuntu](https://renya-kujirada.github.io/Infra-tips/docs/202301031921/tips_chrome_remote_desktop.html)

ubuntuサーバにremote desktop接続したい場合のTips．team viewerと異なり，remote 接続時にrebootしても接続できるためおすすめ．

## [AWS Cloud9 IDE を利用したDeep Learning開発環境を構築する方法](https://renya-kujirada.github.io/Infra-tips/docs/202309032358/tips_cloud9.html)

AWS Cloud9上でのDeep Learning開発環境を構築するためのTips．CloudFormation templateを利用し，Deep Learning AMIからEC2インスタンスを作成後に，SSH環境のCloud9を構築する．

## [AWS CodeWhispererが収集するデータについての調査内容](https://renya-kujirada.github.io/Infra-tips/docs/202309151938/tips_codewhisperer.html)

CodeWhispererを業務適用しても，AWS側にコーディング内容が共有されないかどうかを調査した．
