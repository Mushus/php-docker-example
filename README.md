# php-docker-example

phpのdocker開発環境

## 環境構築

### 前準備

#### vagrant版

1. vagrant
1. VirtualBox

がインストールされていること

#### docker直接版

1. docker
1. docker-compose

が導入されていること

### 環境構築

#### docker直接版

1. `.env.example` を `.env` にコピー
1. (プラグインが入ってないときに限り)`vagrant plugin install dotenv`
1. (プラグインが入ってないときに限り)`vagrant plugin install vagrant-vbguest`
1. `vagrant up`

dockerが入ったvagrant環境が完成しました。

#### vagrant版

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

composer が欲しい時は以下のコマンドで取得できるかと思います。
コンテナ名は `docker ps` コマンドで取得できます

```
# docker exec [PHPのコンテナ名] -it "curl -sS https://getcomposer.org/installer | php"
```

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
