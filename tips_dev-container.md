# tips_dev-container
- 基本的に，Dockerコンテナを起動し，コンテナ内部に入るとrootになる．
  - つまり，コンテナ内部でファイルを作成すると，そのファイルの所有権はrootになるため，コンテナから抜けた後のファイルの扱いが面倒になる．
  - Dockerfile内で，下記のようにあらかじめ一般ユーザを作成してユーザを指定おくと便利．
  - [VSCodeのDocker環境をRoot以外のユーザで実行する](https://e-penguiner.com/vscode-developent-environment-docker-without-root/)

```
RUN useradd -m -d /home/dev-user -s /bin/bash dev-user
USER dev-user
```
