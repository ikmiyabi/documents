# AWSの設定
## TL;DR
```sh
sudo yum update -y
sudo yum install git -y
sudo amazon-linux-extras install docker -y
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
git clone https://github.com/weseek/growi-docker-compose.git
sudo amazon-linux-extras install docker
sudo systemctl start docker
cd growi-docker-compose
vi docker-compose.yml
sudo docker-compose up -d
```

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
