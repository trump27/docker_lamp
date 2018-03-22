# cakephp3 docker template

- cakephp3.5
- Web(ubuntu/apache/php)
- MySql
- phpMyAdmin

## build

```bash
docker-compose up -d
```

## ソース設定

### ソース配置

projectにソースを格納
```bash
rm ./web/project/index.html
git clone https://github.com/xxxx.git ./web/project
```

- ``mysql``を使用するときはhost=mysqlを指定
- ``sqlite``を使用するときは、``/var/www/html``ディレクトリ、``db.sqlite``に777を設定

### 設定

```bash
dokcer exec -it web /bin/bash

## container
composer -n install
chmod +x bin/cake
bin/cake migrations migrate
bin/cake migrations seed
```

## other

```bash
docker rm `docker ps -a -q`
```
