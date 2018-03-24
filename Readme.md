# cakephp3 docker template

2018.03.23

- cakephp3.5
- Web (ubuntu xenial/apache/php)
- MySql
- phpMyAdmin

ubuntuで``php7.0``がインストールされる。バージョンが異なるときは、Dockerfileのphp.iniのコピー先を変更する。

## build

```bash
docker-compose up -d

# サービスを指定してビルドする場合
docker-compose build web
```

## アプリケーション

### ソース配置

projectにソースを格納
```bash
# cloneする前に空にする。
rm ./web/project/index.html
git clone https://github.com/xxxx.git ./web/project
```

- ``mysql``を使用するときは、``app.php``のhostに``mysql``を指定
- ``sqlite``を使用するときは、``/var/www/html``ディレクトリ、``db.sqlite``に777を設定

### 設定

コンテナ起動後にコンテナ内でcomposer操作、DB等を設定する。

```bash
dokcer exec -it web /bin/bash

## inside container
composer -n install
chmod +x bin/cake

chgrp -R www-data logs tmp
chmod -R g+rw logs tmp

# chgrp -R www-data webroot/files
# chmod -R g+rw webroot/files

bin/cake migrations migrate
bin/cake migrations seed
```

## その他

```bash
docker rm `docker ps -a -q`
```

- アップロードなどで日本語のファイル名は格納しないこと。(localeがPOSIXになっている) ``urlencode``する。
- 初回phpmyadminに接続できないときは、コンテナを作成しなおす。