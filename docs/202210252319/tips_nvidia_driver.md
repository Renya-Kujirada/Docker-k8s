# nvidia-driver 周りのエラー時の Tips

本書では，docker を導入しているマシン上で nvidia-driver が壊れた場合の対応方法を述べる．
※nvidia-driver のインストール方法について修正した．過去 ver の記事は[本リンク先](https://github.com/Renya-Kujirada/Infra-tips/blob/main/docs/202210252319/)直下にある．(2024/01/21 更新)

## 事象

`nvidia-smi`を実行すると，以下のエラーがでてしまい，GPU 情報が出力されなくなってしまった．
また，ubuntu のデュアルディスプレイ表示や docker container 内での GPU の利用ができなくなってしまった．reboot を試みても直らない．

```
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

## 原因

原因不明だが，検索すると以下が出てきた．

1. `apt-get upgrade` が影響している可能性
2. ubuntu の自動更新

## 対処

### nvidia ドライバ，cuda 関連のドライバをアンインストール

```sh
sudo apt-get --purge remove nvidia-*
sudo apt-get --purge remove cuda-*
```

### nvidia ドライバのインストール

[CUDA Toolkit 公式 インストール手順](https://developer.nvidia.com/cuda-downloads?target_os=Linux)を参考に，最新のドライバのみを install する．具体的には，公式手順の最後のコマンド`sudo apt-get -y install cuda-toolkit-12-3`を`sudo apt-get -y install cuda-drivers`に変更するだけである．公式~~この install 方法は，[Nvidia Docker 公式の FAQ](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#how-do-i-install-the-nvidia-driver)にも記載がある．~~

**2024/01/21 追記**: [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-container-toolkit)リポジトリに統合されたため，FAQ は閲覧できなくなっていた．

以下のコマンドは，Ubuntu 22.04 で Installer Type を deb(local)とした場合である．

```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.3.2/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.2-545.23.08-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.2-545.23.08-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-drivers
```

- ドライバ情報を確認．

```sh
nvidia-smi
```

### NVIDIA Container Runtime のインストール

現状のままだと，docker コンテナ上で GPU を利用しようとすると下記エラーが出てくる．エラー内容から，Docker が NVIDIA のコンテナランタイムフック（nvidia-container-runtime-hook）を見つけらていないことがわかる．これは，driver の削除時に，nvidia-docker に関するソフトウェア（docker-container-runtime）が削除されているためである（と推測している）．~~なので，[nvidia-container-runtime の公式リポジトリの手順](https://github.com/NVIDIA/nvidia-container-runtime#ubuntu-distributions)に従い，Nvidia Container Runtime を再インストールするとよい．以下に手順を示す．~~

**2024/01/21 追記**: [NVIDIA Container Toolkit](https://github.com/NVIDIA/nvidia-container-toolkit)リポジトリに統合されたため，手順 は閲覧できなくなっていた．しかし，`sudo apt-get install nvidia-container-runtime`を実行し，`service docker restart`すると問題は解消した．ただし，普通に`docker restart`もしくは`sudo reboot`すれば直ったかもしれない．

以下は，2023/09/04 時点で閲覧できたリポジトリ内の手順である．

```sh
docker: Error response from daemon: exec: "nvidia-container-runtime-hook": executable file not found in $PATH.
```

- リポジトリの設定を行う．以下のように，任意のパスで以下のスクリプトを作成し実行するとよい．

```sh
$ cat nvidia-container-runtime-script.sh

curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt-get update

$ sh nvidia-container-runtime-script.sh
```

- 以下コマンドで，再度インストール．

```sh
sudo apt-get install nvidia-container-runtime
```

- Docker を再起動．

```sh
service docker restart
```

### 問題解決できたことを確認

以上のステップで docker 上で GPU を利用できるはず．以下に簡単な確認方法を示す．

- Nvidia 公式の Pytorch Docker イメージを利用してコンテナを立て，コンテナ内 GPU を利用してみる．

```sh
#!/bin/bash
docker run --gpus all -it --rm nvcr.io/nvidia/pytorch:23.12-py3
```

- `python3`を実行し，下記コードを実行して GPU 利用可否を確認．

```py
>>> import torch
>>> torch.cuda.is_available()
True
>>> exit()
```

## 対策

自動更新(バージョンアップ)の停止をするために，以下コマンドを実行．

```sh
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

「自動的に安定版の更新をダウンロードしてインストールしますか？」という画面表示が出てくるので，「いいえ」を選択．
自動更新が停止したことを確認するには，以下ファイルの内容を表示し，以下のように値が 0 となっていることを確認．

```sh
cat /etc/apt/apt.conf.d/20auto-upgrades

APT::Periodic::Update-Package-Lists "0";
APT::Periodic::Unattended-Upgrade "0";
```

## 参考

- [nvidia-smi で GPU 情報が出力されなくなったときの対処法](https://jskangaroo.hatenablog.com/entry/2021/10/23/151151)
- [docker: Error response from daemon: could not select device driver “” with capabilities: [[gpu]].の対処方法](https://www.yurui-deep-learning.com/2021/08/17/docker-error-response-from-daemon-could-not-select-device-driver-with-capabilities-gpu/)
- [Docker で GPU を使おうとしたら Error response from daemon: linux runtime spec devices: could not select device driver “” with capabilities: [[gpu]]](https://cocoinit23.com/docker-gpu-error-response-from-daemon-linux-runtime-spec-devices-could-not-select-device-driver-with-capabilities-gpu/)
- [Docker でのディープラーニング GPU 学習環境構築方法](https://qiita.com/karaage0703/items/e79a8ad2f57abc6872aa#%E6%89%8B%E5%8B%95apt%E3%81%A7%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)
- [Ubuntu をちょっと使いやすくする設定集](https://qiita.com/karaage0703/items/705f1b750c486f00d554#%E8%87%AA%E5%8B%95%E6%9B%B4%E6%96%B0%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E5%81%9C%E6%AD%A2)
- [【Ubuntu】Docker で GPU を使うまでの環境構築](https://lilaboc.work/archives/29112270.html)
- [NVIDIA Docker って今どうなってるの？ (20.09 版)](https://medium.com/nvidiajapan/nvidia-docker-%E3%81%A3%E3%81%A6%E4%BB%8A%E3%81%A9%E3%81%86%E3%81%AA%E3%81%A3%E3%81%A6%E3%82%8B%E3%81%AE-20-09-%E7%89%88-558fae883f44)
- [New Docker CLI API Support for NVIDIA GPUs under Docker Engine 19.03.0 Pre-Release](https://collabnix.com/introducing-new-docker-cli-api-support-for-nvidia-gpus-under-docker-engine-19-03-0-beta-release/)
