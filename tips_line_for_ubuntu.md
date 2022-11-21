# UbuntuでLINEをアプリのように利用する方法

## 手順

- chromeをubuntuにinstall

```sh
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb

```
 
- [chrome ウェブストア-line](https://chrome.google.com/webstore/search/line?hl=ja)でLINEを追加

- chromeのURLに`chrome://extensions/`を入力し，右上のデベロッパーモードをONにする
  - IDとversionを覚えておく
  - 私の場合，IDとversionは以下だった．
    - ID: ophjlpahpchlmihnnnihgmmeilfjmjjc
    - version: 2.5.7_0
    
- 下記コマンドを実行し，現在あるAppを表示しておく

```sh
cd /home/"username"/.local/share/applications
ls
```

- chromeのURLに`chrome-extension://"LINEのID(先程のID)"/index.html`を入力し，`その他のツール(L) > ショートカットを作成...`からショートカットを作成．名前はLINEとする．

- 再度下記コマンドを実行し，新たに作成された`chrome-"app-id"-Default.desktop`を覚えておく．
  - 私の場合，app-id = pbpoojghcbigbheeamegjbdailkaeglfであった．

- LINEのアイコン画像を任意のディレクトリにコピー（ここではPicturesディレクトリにコピーしたとする．）
  - この処理を実施た理由は後述する．

```sh
cp /home/"username"/.config/google-chrome/Default/Extensions/"ID"/"version"/res/img/line_logo_128x128_on.png ~/Pictures/
```

- `/home/"username"/.local/share/applications/chrome-"app-id"-Default.desktop`を編集し，Iconのpathをコピーした画像pathにする．
  - 画像pathは`/home/"username"/.config/google-chrome/Default/Extensions/"ID"/"version"/res/img/line_logo_128x128_on.png`でも良いが，
  アプリ側のアップデートの度にバージョンが変わり，ディレクトリ名も変わってしまうため，不変的なpathを指定したいというモチベーションでPicturesディレクトリにコピーした．

```sh
vi /home/"username"/.local/share/applications/chrome-pbpoojghcbigbheeamegjbdailkaeglf-Default.desktop

#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Terminal=false
Type=Application
Name=LINE
Exec=/opt/google/chrome/google-chrome --profile-directory=Default --app-id=pbpoojghcbigbheeamegjbdailkaeglf
Icon=/home/renya/Pictures/img/line_logo_128x128_on.png
StartupWMClass=crx_pbpoojghcbigbheeamegjbdailkaeglf

```

## 参考

https://qiita.com/north_redwing/items/357bf0cfbc17990a5276
