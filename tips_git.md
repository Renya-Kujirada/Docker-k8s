# GitのTips

本書では，業務などでGitサーバーが利用できない場合のGit運用に関するTipsを共有する．

## OneDriveを活用したGit運用方法

Gitサーバーの代替としてOneDriveを活用し，OneDrive上にリモートリポジトリを配置することで，Gitでソース管理する方法を示す．なお，VSCodeを利用する前提であることに注意されたい．

### OneDrive上での作業

- OneDrive上に，リモートリポジトリを配置するためのディレクトリを作成し，移動する．なお，説明のため，`\OneDrive\Document\myRemoteRepository`上にリモートリポジトリを作成したと仮定する．
```sh
mkdir remote.git
cd remote.git
```

- 空のベアリポジトリを作成する
  - ベアリポジトリ：ワーキングディレクトリ（ファイルそのもの）を持たず，更新情報のみ保持する．リモートリポジトリはベアリポジトリでなければならない．

```sh
git init --shared --bare
```

### local上での作業

- local上で，VSCodeを利用しGitリポジトリを新規作成する．
- readme.mdなど適当なファイルを作成しコミットを実行する（別に空コミットでも構わない）．
- local上で，VSCodeを利用しremote repositoryを設定する．
  - ctrl + shft + p でコマンドパレットを開き，Git Add Remoteと入力．
- リモートリポジトリのURL（ファイルパス）を入力する．その際，リモートリポジトリの名前はoriginなどにする．

```sh
# windowsの場合
C:\Users\<username>\OneDrive\Document\myRemoteRepository\remote.git

# wslの場合
/mnt/c/Users/<username>/OneDrive/Document/myRemoteRepository/remote.git
```

- local上でリモートリポジトリにpushする．
  - 設定したリモートリポジトリのURLは下記コマンドで確認できる．
  ```sh
  git remote -v
  ```
### 第三者が開発に参画する場合
- 作業用リポジトリをクローンすれば良い．その際，OneDriveのフォルダ名にスペース文字が含まれる場合，スペース文字をエスケープするようリモートリポジトリのpathを指定する．
  - 前提として，リモートリポジトリが格納されているOneDriveディレクトリを第三者に共有する必要がある．
  - VSCodeのGit cloneの機能ではうまくできなかった．
```sh
# windowsの場合
git clone "C:\Users\<username>\OneDrive\Document\myRemoteRepository\remote.git"

# wslの場合
git clone "/mnt/c/Users/<username>/OneDrive/Document/myRemoteRepository/remote.git"
```

## Git mergeの仕方などのTips

fast-forwardを行わないマージ方法を示す．

- masterブランチにチェックアウトする．

```sh
git checkout master
```
- マージコミットを新規作成する（fast-forwardしない）よう，merge commitを明示的に行う．
  - masterブランチの状態が変更されていない場合，masterブランチは単純に統合するブランチに移動するだけで変更内容を取り込むことができる．このようなマージをfast-forwardマージと呼び，git mergeコマンドで下記のように引数を明示しなければ，fast-forwardでマージされる．
  - ブランチがそのまま残るため，統合するブランチで行った作業の特定が容易になるというメリットがある．
```sh
git merge --no-ff <branch>
```

## おすすめのVSCodeのextension

- Git graph: Gitのツリーログを視覚的に見やすくしてくれる．
- Git Extension: Git LensやGit Historyなど，変更ログがわかりやすくなる機能を一括で入れてくれる．
