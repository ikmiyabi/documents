# AWSの設定

[[toc]]

## gitのインストール
```sh
sudo yum update
sudo yum install git

# インストールされていることを確認
git version
```

## dockerのインストール

```sh
sudo amazon-linux-extras install docker
```

## docker-composeのインストール

- docker-composeの最新バージョンを確認する

`https://github.com/docker/compose/releases/`にてdocker-composeの最新バージョンを確認

- docker-composeをインストールする

```sh
# URLに最新のバージョンを指定し、docker-composeをインストールする（1.29.1は2021/04/15現在の最新バージョン）
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

# シンボリックリンクの作成
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

# インストールされていることを確認
docker-compose --version
```

## knowledgeのインストール
- docker-composeの作成

```sh
vi docker-compose.yml
```

- docker-composeの修正

```
version: '2'
services:
    app:
        image: koda/docker-knowledge:japanese
        #build: .
        volumes:
            - ./volumes/knowledge:/root/.knowledge
        ports:
            - 8080:8080
        restart: always
        depends_on:
            - "db"
    db:
        image: postgres:9
        environment:
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=admin123
            - POSTGRES_DB=knowledge_production
        volumes:
            #- ./volumes/initdb:/docker-entrypoint-initdb.d
            - ./volumes/postgres/data:/var/lib/postgresql/data
        restart: always
```