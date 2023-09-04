# nvidia-driver周りのエラー時のTips

本書では，dockerを導入しているマシン上でnvidia-driverが壊れた場合の対応方法を述べる．
※nvidia-driverのインストール方法について修正した．過去の記事は[本リンク先](https://github.com/Renya-Kujirada/Infra-tips/blob/main/docs/202210252319/tips_nvidia_driver_old.md)にある．(2023/09/04更新)

## 事象

`nvidia-smi`を実行すると，以下のエラーがでてしまい，GPU情報が出力されなくなってしまった．
また，ubuntuのデュアルディスプレイ表示やdockerの利用ができなくなってしまった．rebootを試みても直らない．

```
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

## 原因

原因不明だが，検索すると以下が出てきた．

1. `apt-get upgrade` が影響している可能性
2. ubuntuの自動更新

## 対処

### nvidiaドライバ，cuda関連のドライバをアンインストール

```sh
sudo apt-get --purge remove nvidia-*
sudo apt-get --purge remove cuda-*
```

### nvidiaドライバのインストール

[CUDA Toolkit の公式Webサイト](https://developer.nvidia.com/cuda-downloads?target_os=Linux)を参考に，最新のドライバのみをinstallする．このinstall方法は，[Nvidia Docker公式のFAQ](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#how-do-i-install-the-nvidia-driver)にも記載がある．（なお，以下のコマンドは，Ubuntu 22.04で Installer Typeをdeb(local)とした場合である．）

```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.2.2/local_installers/cuda-repo-ubuntu2204-12-2-local_12.2.2-535.104.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-2-local_12.2.2-535.104.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-2-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-drivers
```

- ドライバ情報を確認．

```sh
nvidia-smi
```

### NVIDIA Container Runtimeのインストール

現状のままだと，dockerコンテナ上でGPUを利用しようとすると下記エラーが出てくる．これは，driverの削除時に，nvidia-dockerに関するソフトウェア（docker-container-runtime）が削除されているためである．なので，[nvidia-container-runtimeの公式リポジトリの手順](https://github.com/NVIDIA/nvidia-container-runtime#ubuntu-distributions)に従い，Nvidia Container Runtimeを再インストールするとよい．以下に手順を示す．

```sh
docker: error response from daemon: could not select device driver "" with capabilities: [[gpu]].
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

- Dockerを再起動．

```sh
service docker restart
```

### 問題解決できたことを確認

以上のステップでdocker上でGPUを利用できるはず．以下に簡単な確認方法を示す．

- TensorFlow公式のDockerイメージを利用してコンテナ上でGPUを利用してみる．

```sh
docker run --gpus all -it --rm --name tensorflow-gpu -p 8888:8888 tensorflow/tensorflow:latest-gpu-py3-jupyter
```

- ターミナル上に表示される下記のようなリンクをブラウザで開く．

```sh
http://127.0.0.1:8888/?token=xxxxxxxxxxxxxx
```

- Jupyter Notebookにアクセスできるため，下記コードを実行してGPU利用可否を確認．

```py
from tensorflow.python.client import device_lib
device_lib.list_local_devices()
```

## 対策

自動更新(バージョンアップ)の停止をするために，以下コマンドを実行．

```sh
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

「自動的に安定版の更新をダウンロードしてインストールしますか？」という画面表示が出てくるので，「いいえ」を選択．
自動更新が停止したことを確認するには，以下ファイルの内容を表示し，以下のように値が0となっていることを確認．

```sh
cat /etc/apt/apt.conf.d/20auto-upgrades

APT::Periodic::Update-Package-Lists "0";
APT::Periodic::Unattended-Upgrade "0";
```

## 参考

- [nvidia-smiでGPU情報が出力されなくなったときの対処法](https://jskangaroo.hatenablog.com/entry/2021/10/23/151151)
- [docker: Error response from daemon: could not select device driver “” with capabilities: [[gpu]].の対処方法](https://www.yurui-deep-learning.com/2021/08/17/docker-error-response-from-daemon-could-not-select-device-driver-with-capabilities-gpu/)
- [DockerでGPUを使おうとしたらError response from daemon: linux runtime spec devices: could not select device driver “” with capabilities: [[gpu]]](https://cocoinit23.com/docker-gpu-error-response-from-daemon-linux-runtime-spec-devices-could-not-select-device-driver-with-capabilities-gpu/)
- [DockerでのディープラーニングGPU学習環境構築方法](https://qiita.com/karaage0703/items/e79a8ad2f57abc6872aa#%E6%89%8B%E5%8B%95apt%E3%81%A7%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)
- [Ubuntuをちょっと使いやすくする設定集](https://qiita.com/karaage0703/items/705f1b750c486f00d554#%E8%87%AA%E5%8B%95%E6%9B%B4%E6%96%B0%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E5%81%9C%E6%AD%A2)
