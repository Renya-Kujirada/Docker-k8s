# tips_dev-container
- 基本的に，Dockerコンテナを起動し，コンテナ内部に入るとrootになる．
  - つまり，コンテナ内部でファイルを作成すると，そのファイルの所有権はrootになるため，コンテナから抜けた後のファイルの扱いが面倒になる．
  - 
  - [VSCodeのDocker環境をRoot以外のユーザで実行する](https://e-penguiner.com/vscode-developent-environment-docker-without-root/)
