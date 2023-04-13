# devcontainer

## devcontainerとは

- Dockerfileはコンテナの構成を定義
- devcontainerはコンテナ内の開発環境を定義（エディタの拡張機能やデバッグツール等）（Dockerfileではできない）
- VSCodeのDevContainer機能が使えるため，コンテナ上で編集したファイルがローカルにも反映される（一番重要かも）
  - Dockerfileのみの場合，毎回`docker cp`でローカルにコピーしてくる必要があるらしい
- まとめると，Dockerfileだけでは表現しきれない部分をdevcontainerフォルダを用いて表現する

## devcontainer.json

- devcontainerフォルダにdevcontainer.jsonは必須
