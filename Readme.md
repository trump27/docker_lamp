# cakephp3 docker template

- cakephp3.5
- Web(ubuntu/apache/php)
- MySql
- phpMyAdmin

## 準備

projectにソースを格納
```bash
rm ./web/project/empty
git clone https://github.com/xxxx.git ./web/project
```

## build

```bash
docker-compose up -d
```
## other

```bash
docker rm `docker ps -a -q`
docker rm
```