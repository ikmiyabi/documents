# インストール

## ElasticBeansTalkを使ったデプロイ方法

* AWS CLIをインストールする

```bash
brew install awscli

# 下記コマンドでインストールされたことを確認
aws --version
#->aws-cli/1.16.310 Python/3.7.6 Darwin/19.2.0 botocore/1.13.46
```

* EB CLIをインストールする

```bash
brew install awsebcli

# 下記コマンドで正常にインストールされたことを確認
eb --version
#-> EB CLI 3.16.0 (Python 3.8.1)
```

* AWSの設定を登録

```bash
aws configure
```

* AWS S3の環境を設定

```bash
aws s3 ls
#-> 2020-01-05 16:55:11 elasticbeanstalk-ap-northeast-1-539128883705
```

* Gradleでビルドを実施

```bash
gradle build
```

* AWS Elastic BeansTalkを開始

```bash
eb init
```

* AWS コンソール上でElastic BeansTalkの設定を行う

```bash
eb deploy Test
```
