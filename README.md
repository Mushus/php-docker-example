# php-docker-example

phpのdocker開発環境

## 環境構築

### 前準備

1. docker
1. docker-compose

が導入されていること

### 環境構築

1. `.env.example` を `.env` にコピー
1. `.env`の設定で環境が立ち上がります

### docker基本操作

開発環境立ち上げ
```
# docker-compose up -d
```

開発環境停止
```
# docker-compose down
```

### Laravelの環境構築

このgitリポジトリ自体が環境、プロジェクトフォルダになります

* composer をインストール
  - https://getcomposer.org
* *Composer Create-Project* を参考に本リポジトリをプロジェクトルートに指定し作成
  - https://readouble.com/laravel/

### ネットワーク

dockerコンテナ間通信は以下のホスト:ポートで接続可能です。

* mysql ... rdb:3306
* redis ... kvs:6379
* httpd ... php:8080

ex. `http://php:8080/`

ホストからコンテナへの通信は以下のホスト:ポートで接続可能です。

* mysql ... localhost:3306
* redis ... localhost:6379
* httpd ... localhost:8080

ex. `http://localhost:8080/`
