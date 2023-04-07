# docker-study

## Dockerとは？

- コンテナという仮想環境を構築する
- 同じ環境を共有するため，環境の違い（OSやバージョン）があっても問題なく動かせる
- Dockerfileを作成して環境構築する

## Dockerコマンド

### コンテナ一覧

```bash
docker ps       #起動中のコンテナのみ
docker ps -a    #全てのコンテナを表示
```

### イメージ一覧

```bash
docker images
```

### イメージの作成

Dockerfileを元にimageを作成

```bash
docker build -t [image名] .     #最後の"."はDockerfileのあるディレクトリ
```

### コンテナを起動

作成したイメージからコンテナを起動する

```bash
docker run -it [image名]:[version] /bin/bash

#"-it"は"-i"と"-t"の両方，意味はコンテナを起動しっぱなしにする
#"[image名]:[version]"は"[リポジトリ名]:[version]"が一般的？例：docker-study:latest, ubuntu:14.04
#最後の"/bin/bash"はコンテナ起動時に最初に動かすコマンドらしい（シェルを起動しないとその後のコマンドが打てないかららしい）
```

### コンテナを削除

```bash
docker rm [コンテナID]
```

### イメージを削除

`docker rm`コマンドを使用した後，imageを削除するのに使用する

```bash
docker rmi [imageID]
```

### コンテナに再度入る

コンテナを起動したまま抜ける方法は`ctrl+p+q`で下記はアタッチする方法  
`ctrl+d`をするとSTATUSがExitedになり，コンテナが終了する  
VSCodeのデフォルトで設定されている`ctrl+q`のQuick Open Viewのショートカットを削除することで可能

```bash
docker attach [コンテナID]
```

### コンテナのログ確認

```bash
docker logs [コンテナID]
```

### コンテナの停止

`docker ps -a`でSTATUSがExitedになってれば停止

```bash
docker stop [コンテナID]
```

## Dockerfile

- どのようなイメージを作成するかを決められる
- Dockerfileを作成すれば同じ環境を構築可能

### FROM

ベースイメージを指定．FROMコマンドは必須らしい．  
例えばubuntuOSとpythonの両方指定する場合は，FROMはubuntuでpythonはRUNでinstallするとか．  
複数FROMはできない？

```dockerfile
FROM ubuntu:20.04   #ubuntuOSをベース
FROM python:3.9.13  #pythonをベース
```

### RUN

コマンドの実行

```dockerfile
#最低限installしておいた方がいいやつ
RUN apt-get -y update && apt-get upgrade -qqy && apt-get -y install \   #"\"は改行
    sudo \
    bash \
    git \
    vim
```

### ARG

変数の定義

```dockerfile
ARG python_version=3.9.13
FROM python:${python_version}
```

### WORKDIR

作業ディレクトリの指定．なかったら自動で作成してから移動してくれる．

```dockerfile
WORKDIR /home/astrfo    #何でもいい
```

### USER

このコマンド以降のコマンドを実行するユーザを指定する

```dockerfile
##ユーザを作成して変数usernameを定義
USER ${username}
```

### COPY

実行したいプログラムを作業ディレクトリ（WORKDIRで指定した場所）にコピーするときに使う

```dockerfile
COPY main.py /home/astrfo
```

### CMD

コンテナ実行時のデフォルト（初期設定）を指定するために使う  
ただし，Dockerfile内で1回しか使用できない

```dockerfile
CMD ["/bin/bash"]   #bashを起動する
```

## 参考資料

- [Docker ドキュメント日本語化プロジェクト](https://docs.docker.jp/)
- [dockerのコンテナとイメージの違い](https://hacknote.jp/archives/56650/)
- [Dockerコマンド よく使うやつ](https://qiita.com/Esfahan/items/52141a2ad741933d7d4c)
- [Docker run や exec コマンドにつける /bin/bashや/sbin/initについて](https://teratail.com/questions/58523)
- [Dockerのコンテナから抜ける in VSCode](https://qiita.com/Statham/items/c204e85067ea4dca2724)
