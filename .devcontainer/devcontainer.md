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

```json
"name": "My Dev Container"
```

### dockerFile

コンテナのビルドに使用されるDockerfileのパスを指定．通常は`"DockerFile"`を使う．

```json
"dockerFile": "Dockerfile"
```

### extensions

インストールする拡張機能のリストを指定．コンテナ内で使用される拡張機能を事前に指定することができる．

```json
"extensions": [
    "ms-python.python",
    "dbaeumer.vscode-eslint",
    "ms-toolsai.jupyter"
]
```

### settings

VSCodeの設定を決められる．例えばシェルの指定など．

```json
"settings": {
    "terminal.integrated.shell.linux": "/bin/bash"
}
```

### mounts (1番重要？)

ローカルとコンテナのファイル共有をするために指定．  
ローカルを指定することでコンテナで生成されたファイルをローカルにも反映させることができる．

```json
"mounts": [
    "source=.,target=/workspace,type=bind,consistency=cached"
]
```

### remoteUser

コンテナで実行されるユーザーを指定．ユーザーの権限制限のために使われる．

```json
"remoteUser": "vscode"
```

### containerEnv

コンテナ内で使用される環境変数を定義．

```json
"containerEnv": {
    "NODE_ENV": "production",
    "PORT": "8080"
}
```
