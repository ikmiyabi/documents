# sshを簡単に行う方法
## インスタンスにログインする際に指定するユーザー名やキー名を省略する

AWSではssh-keygenを行う必要はなく、キーペアをダウンロードしてsshを行う。
sshのコマンドは、以下のようにキーのパス、ユーザー名、ホスト名を指定する。

```sh
ssh -i <キーのパス> <ユーザ名>@<ホスト名>

# 実行例
ssh -i aws_sample.pem ec2-user@ec2-00-00-000-000.us-west-2.compute.amazonaws.com
```

このキーのパス、ユーザー名、ホスト名の指定を省略するために`.ssh/config`に設定を記載しておく。

```sh
vi .ssh/config
```

- 下記を追記する

```txt
Host aws_sample
  HostName ec2-00-00-000-000.us-west-2.compute.amazonaws.com
  User ec2-user
  IdentityFile aws_sample.pem
```

- 以降は下記コマンドでsshできる

```ssh
ssh aws_sample
```

参考: [【AWS】.ssh/config を利用して、ログイン時のコマンドを省略する](https://techblog.kyamanak.com/entry/2017/08/15/003500)
