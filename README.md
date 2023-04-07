# docker-study

## Dockerとは？
- コンテナという仮想環境を構築する
- 同じ環境を共有するため，環境の違い(OSやバージョン)があっても問題なく動かせる
- Dockerfileを作成して環境構築する

## Dockerコマンド

### コンテナ一覧
```
docker ps       #起動中のコンテナのみ
docker ps -a    #全てのコンテナを表示
```

### イメージ一覧
```
docker images
```

### イメージの作成
Dockerfileを元にimageを作成
```
docker build -t [image名] .     #最後の"."はDockerfileのあるディレクトリ
```

### コンテナを起動
作成したイメージからコンテナを起動する
```
docker run -it [image名]:[version] /bin/bash
#"-it"は"-i"と"-t"の両方，意味はコンテナを起動しっぱなしにする
#"[image名]:[version]"は"[リポジトリ名]:[version]"が一般的？例：docker-study:latest, ubuntu:14.04
#最後の"/bin/bash"はコンテナ起動時に最初に動かすコマンドらしい(シェルを起動しないとその後のコマンドが打てないかららしい)
```

### コンテナを削除
```
docker rm [コンテナID]
```

### イメージを削除
`docker rm`コマンドを使用した後，imageを削除するのに使用する
```
docker rmi [imageID]
```

### コンテナに再度入る
コンテナからデタッチする方法は`ctrl+p+q`で下記はアタッチする方法
```
docker attach [コンテナID]
```

### コンテナのログ確認
```
docker logs [コンテナID]
```

### コンテナの停止
`docker ps -a`でSTATUSがExitedになってれば停止
```
docker stop [コンテナID]
```


## 参考資料
- [Docker ドキュメント日本語化プロジェクト](https://docs.docker.jp/)
- [dockerのコンテナとイメージの違い](https://hacknote.jp/archives/56650/)
- [Dockerコマンド よく使うやつ](https://qiita.com/Esfahan/items/52141a2ad741933d7d4c)
- [Docker run や exec コマンドにつける /bin/bashや/sbin/initについて](https://teratail.com/questions/58523)
