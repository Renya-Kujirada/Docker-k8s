# tips_dev-container

## rootlessコンテナ環境について

- 基本的に，Dockerコンテナを起動し，コンテナ内部に入るとrootになる．
- つまり，コンテナ内部でファイルを作成すると，そのファイルの所有権はrootになるため，コンテナから抜けた後のファイルの扱いが面倒になる．
- Dockerfile内で，下記のようにあらかじめ一般ユーザを作成してユーザを指定すると便利．不要な特権は避けた方が良い．
- [VSCodeのDocker環境をRoot以外のユーザで実行する](https://e-penguiner.com/vscode-developent-environment-docker-without-root/)
- [Dockerfile運用例](https://www.forcia.com/blog/002273.html)
- [sudo権限を付与する方法)](https://zukucode.com/2019/06/docker-user.html)
```
RUN useradd -m -d /home/dev-user -s /bin/bash dev-user
USER dev-user
```
