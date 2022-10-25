# nvidia-driver周りのエラー時のTips

## nvidia-smi実行時にGPU情報が出力されない

### 事象

`nvidia-smi`を実行すると，以下のエラーがでてしまい，ubuntuのデュアルディスプレイ表示やdockerの利用ができなくなってしまった．
rebootを試みても直らない．

```
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

### 原因

原因不明だが，検索すると以下が出てきた．

1. apt-get upgrade が影響している可能性
2. ubuntuの自動更新

### 対処

#### nvidiaドライバ，cuda関連のドライバをアンインストール

```sh
sudo apt-get --purge remove nvidia-*
sudo apt-get --purge remove cuda-*
```

#### nvidiaドライバのインストール

`sudo ubuntu-drivers autoinstall`でインストールしてもよいが，失敗する事例をよく聞く（？）ので自分は手動でインストールした．
以下に手順を示す．

- 以下コマンドでインストールするべきドライバを確認する．
`ubuntu-drivers devices`

- 以下は表示例．基本的にはrecommendedと表記されているものをインストールすれば良い（が，私の場合はうまくいかなかった．）
```
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00002204sv000010DEsd00001454bc03sc00i00
vendor   : NVIDIA Corporation
model    : GA102 [GeForce RTX 3090]
driver   : nvidia-driver-520 - third-party non-free
driver   : nvidia-driver-510-server - distro non-free
driver   : nvidia-driver-515-open - distro non-free
driver   : nvidia-driver-520-open - third-party non-free recommended
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-510 - third-party non-free
driver   : nvidia-driver-470 - distro non-free
driver   : nvidia-driver-515-server - distro non-free
driver   : nvidia-driver-515 - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```

- 自身のGPUの型番を以下のコマンドで調べ，[nvidiaのサイト](https://www.nvidia.com/Download/index.aspx)で対象ドライバのバージョンを検索．
  - 自分の場合は，515.76だった．
`sudo lshw -C display`

- 以下コマンドで指定のバージョンのドライバをインストール．(以下は515のバージョンをインストールする場合の例．Tab補完可．)
`sudo apt install nvidia-driver-515`

- `sudo reboot`で再起動．

- `nvidia-smi`でドライバ情報を確認．

#### NVIDIA Container Runtimeのインストール

現状のままだと，dockerコンテナ上でGPUを利用しようとすると下記エラーが出てくる．以下に対処手順を示す．

```
docker: error response from daemon: could not select device driver "" with capabilities: [[gpu]].
```

- 任意のパスで以下のスクリプトを作成し，実行．

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

- driverの削除時に，nvidia-dockerに関するソフトウェアが削除されているため，再度インストール．

`sudo apt-get install nvidia-container-runtime`

- Dockerを再起動．

`service docker restart`

#### 問題解決できたことを確認

以上のステップでdocker上でGPUを利用できるはず．以下に簡単な確認方法を示す．

- TensorFlow公式のDockerイメージを利用してコンテナ上でGPUを利用してみる．

`docker run --gpus all -it --rm --name tensorflow-gpu -p 8888:8888 tensorflow/tensorflow:latest-gpu-py3-jupyter`

- ターミナル上に表示された下記のようなリンクをブラウザで開く．
`http://127.0.0.1:8888/?token=xxxxxxxxxxxxxx`

- Jupyter Notebookにアクセスできるため，下記コードを実行してGPU利用可否を確認．
```py
from tensorflow.python.client import device_lib
device_lib.list_local_devices()
```

### 対策

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

### 参考
- [nvidia-smiでGPU情報が出力されなくなったときの対処法](https://jskangaroo.hatenablog.com/entry/2021/10/23/151151)
- [docker: Error response from daemon: could not select device driver “” with capabilities: [[gpu]].の対処方法](https://www.yurui-deep-learning.com/2021/08/17/docker-error-response-from-daemon-could-not-select-device-driver-with-capabilities-gpu/)
- [DockerでGPUを使おうとしたらError response from daemon: linux runtime spec devices: could not select device driver “” with capabilities: [[gpu]]](https://cocoinit23.com/docker-gpu-error-response-from-daemon-linux-runtime-spec-devices-could-not-select-device-driver-with-capabilities-gpu/)
- [Ubuntuをちょっと使いやすくする設定集](https://qiita.com/karaage0703/items/705f1b750c486f00d554#%E8%87%AA%E5%8B%95%E6%9B%B4%E6%96%B0%E3%83%90%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%82%A2%E3%83%83%E3%83%97%E3%81%AE%E5%81%9C%E6%AD%A2)
