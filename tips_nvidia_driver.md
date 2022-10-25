# nvidia-driver周りのエラー時のTips

## nvidia-smi実行時にGPU情報が出力されない

### 事象

`nvidia-smi`を実行すると，以下のエラーがでてしまい，ubuntuのデュアルディスプレイ表示やdockerの利用ができなくなってしまった．

```
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```

### 原因
