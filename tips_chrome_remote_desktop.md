# chrome remote desktopのTips

本書では，ubuntuでchrome remote desktopを利用する方法を記載する．

なお，windows laptopからubuntu serverに接続することを想定している．

## install方法

- ubuntu側で，[google公式ドキュメント](https://support.google.com/chrome/answer/1649523#linux-crd&zippy=%2Clinux-%E3%81%A7-chrome-%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88-%E3%83%87%E3%82%B9%E3%82%AF%E3%83%88%E3%83%83%E3%83%97%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B)を見ながら設定を行う．
- ubuntu側はlog outしておく（ここ重要）
- win側で接続できるはず


## uninstall方法

- ubuntu側でloginしようとすると，無限ループに陥ると思われる．なので，帰省時以外で利用しない場合はuninstallしておくことを推奨する．
- [本shell](https://github.com/Renya-Kujirada/Infra-tips/blob/main/src/chrome-remote-desktop/uninstall.sh)を実行してuninstall
  - 再度installする場合は[本shell](https://github.com/Renya-Kujirada/Infra-tips/blob/main/src/chrome-remote-desktop/install.sh)を実行
