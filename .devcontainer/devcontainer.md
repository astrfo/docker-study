# devcontainer

## devcontainerとは

- Dockerfileはコンテナの構成を定義
- devcontainerはコンテナ内の開発環境を定義（エディタの拡張機能やデバッグツール等）（Dockerfileではできない）
- VSCodeのDevContainer機能が使えるため，コンテナ上で編集したファイルがローカルにも反映される（一番重要かも）
  - Dockerfileのみの場合，毎回`docker cp`でローカルにコピーしてくる必要があるらしい
- まとめると，Dockerfileだけでは表現しきれない部分をdevcontainerフォルダを用いて表現する

## devcontainer.json

- devcontainerフォルダにdevcontainer.jsonは必須

## devcontainer.jsonの項目

### name

Dev Containerの名前．どの名前で作業しているか明確にする．

### dockerFile

コンテナのビルドに使用されるDockerfileのパスを指定．通常は`"DockerFile"`を使う．

### extensions

インストールする拡張機能のリストを指定．コンテナ内で使用される拡張機能を事前に指定することができる．

### settings

VSCodeの設定を決められる．例えばシェルの指定など．

### mounts (1番重要？)

ローカルとコンテナのファイル共有をするために指定．  
ローカルを指定することでコンテナで生成されたファイルをローカルにも反映させることができる．
