# heroku入門 ～herokuを使ってWebアプリケーションを10分でデプロイする～
## herokuとは

* herokuとはカスタムアプリケーションをクラウド環境で運用するためのPaas(Platform as a Service：サービスとしてのプラットフォーム)
* インフラ部分にはAWS(Amazon Web Service)を利用している
* デプロイや管理を容易にするためのツール
* 拡張性と耐障害性を実現するアプリケーション実行環境
* プラットフォームの拡張を可能にするアドオンエコシステムを備えている
* 開発者はアプリケーションの本質的な価値の創造に集中して取り組める

## 対象の言語

* 元々はRubyのプログラマの間で有名なプラットフォームだが、最近はいろいろなプログラミング言語やフレームワークに対応している
* Ruby(Ruby on Rails)
* Java(Spring Boot)
* Python(Django)
* PHP(Laravel)

## 参考
* [B2B スタートアップの初期は Heroku でいいんじゃないかって話](https://findy-code.io/engineer-lab/b2b-startup-heroku)
* [Herokuアプリケーションの実行プラットフォーム「Dyno」を徹底的に理解する](https://codezine.jp/article/detail/8344)
* [Rails アプリのインフラを AWS から heroku に移行した話](https://sakagami3.com/entry/2015/05/03/191208)
* [なぜ AWS を捨てて Heroku を選んだのか](https://shelfy.co.jp/shelf/product_post/584)
* [HerokuでRailsを運用するメリットデメリットについて](https://www.daily-dev.net/entry/2017/01/20/Rails%E7%92%B0%E5%A2%83%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B_heroku_vs_AWS_%E3%81%BE%E3%81%A8%E3%82%81)
* [Herokuのメリット、デメリット | Qiita](https://qiita.com/shu_0115/items/0106198f7a0be2f2a509)

## Herokuの哲学

「開発者の生産性を最大化させる」

## The 12 Factor app

Herokuの創業者の一人であるAdam WigginsはモダンなWebアプリケーションを設計・実装・運用するために考慮すべき12のポイントとしてまとめたもの
よかったら見てね

## Herokuの歴史

2007年 Heroku Gardenという名前でRails用のブラウザ統合開発環境のようなサービスをリリース。
2009年 Gitによるリソース管理プロセスそのものをデプロイの手続きとする
2010年 salesforce.comによる買収
2011年 Java言語への対応

## Herokuのメリット

楽

これがherokuを使う理由の全てです。
他のメリットも一応挙げていきますがとってつけた理由です。

* 設定からデプロイまでが VPS や AWS と比べると圧倒的に楽
* デプロイ時間が少ない
* 簡単
* アドオンによる連携がすぐにできる

## Herokuのデメリット

# やれるheroku-Javaアプリケーション開発

※Webセミナーのメモ
https://developer.salesforce.com/events/webinars/herokujava_0414

## アジェンダ

* heokuの基本
* heorokuのJavaサポート
* herokuへのJavaアプリケーションのデプロイ方法
* JVM言語のサポート
* Javaアプリケーションの外部サービスとの接続

## herokuが考えるアプリケーション開発の姿

* インフラの業務管理ではなくアプリケーション開発に集中するべき
* モダンなWebアプリを開発するのに必要な考慮点をシンプルにする

実際にやるとしたら？
以下のようなことを考えないといけない
* AWS?
* OSを考える(Linux?)
* Docker?
* Storage
* ネットワーク
...


→以下のようにシンプルにする

* デプロイ
* manage
* scale

# The twelve Factor App

* 現代的なアプリケーションを設計、構築、運用するための12の方法論
* Herokuの創業者のアダム・ウィギンスがプラットフォームサービス上で稼働する数百のアプリの特性から得た知見をまとめたもの

良いアプリケーションがどういう特性を持っているかまとめたもの (良いアプリケーションの設計思想)

https://12factor.net/ja/

# herokuが提供する機能

* Runtime(Dyno)
herokuが管理(LinuxのUbuntu)。コンテナベースのプロセスエンジンで、サーバーまるまる一個提供しているわけではない、一つの仮想サーバーに対し4つくらいのDynoが動いている

* Developer Experience(DX)
アプリケーションのモニタリング
CD（継続的デリバリ）
など

* Data Services and Ecosystem
RDBはPostgreSQL。KVSであればRedisを提供している。
MongoDBやMySQLを追加したければ、サードパーティーのアドオンを使用する。
herokuが提供しているデータソースは二つ

# herokuダッシュボード
heroku上で稼働するアプリを統合的に管理

Dynoの拡張とアドオンの追加
ダッシュボードから簡単に実行可能

# Dynoのロール

Webサーバー以外にもバッチプロセスやスケジューラなど

# herokuのDynoの考え方

一つのアプリに対して複数のDynoが配備され、ルータによりラウンドロビンする。
欠けたコンテナはすぐに別のサーバー上で起動され、ルーティングが変更。

※ここはスライド参照した方が分かりやすい

ステートレスなアプリケーションの開発を推奨している

# Heroku Private Spaces

単純にサーバーを占有したという場合には「Heroku Private Spaces」というサービスを提供している。

# Herokuのアプリケーションデプロイ方法

Gitを利用して、コード自体をPushする。で終わり

処理の流れ
アプリ実行環境の判別→依存ライブラリなどのインストール・セットアップ

git push されたコードを自動認識してくれる
node.jsの場合、package.jsonで判別など

## herokuが標準でサポートしている言語
開発者が意識しなくても、Herokuがランタイムの保守管理を行う
* node.js
* Ruby
* Java
* PHP
* Python
* Go
* Scala
* Clojure

# BuildPack
コンテナに任意のランタイムを利用できるようにするためのしくみ
３つのコマンドでビルドをコントロール
bin/detect：アプリにBuildPackが適用できるかを判別する
bin/compile：アプリを実行可能な状態にコンパイルや変換を行う
bin/release：ランタイムに必要なメタデータの付与

herokuが標準でサポートしている言語=heroku自身が管理しているビルドパック

BuildPackの一覧に関しては上から順番に全てなめていきます。

Javaの場合は、基本的にmavenでビルドするのが前提

pom.xmlがあるかどうかを判定
なかったらgradle,grails

もし対応するものがなかった場合は、自分で作ることも出来る。あるいは他の人が作った物を使う事が出来る


# Javaを利用する方法

maven：pom.xml
gradle：build.gradle

のどちらかがあるとJavaのアプリケーションとして認識される

# BuildPackは明示することは可能

CLI
```bash
heroku buildpacks:set heroku/node.js
heroku buildpacks:remove heroku/node.js
```

app.json
```json
{
  "buildpacks": [
    {"url": "https://github.com/heroku/heroku-buildpack-pgbouncer"},
    {"url": "heroku/ruby"}
  ]
}
```

herokuへのJavaのデプロイ方法

1. maven or gradleによってプロジェクトを構成
2. Javaのプログラムを作成
3. ProcfileによってMainとなるプログラムを指定
4. HerokuアプリをCreateして、Gitでデプロイ

通常と異なるのは、3以降

サーブレットコンテナを起動してそこにデプロイをするのが通常の流れだが、実行可能な
embedded.tomcat
embedded.jetty
netty

# maven or gradleによってプロジェクトを構成
Getting-startedリポジトリを提供しているのでそれを利用
https://github.com/heroku/gradle-getting-started

# Procfileとは

herokuは内部でForeman（ライブラリ）を利用

```bash
$ foreman start -c web=2 -p 3000 -e
```

https://github.com/ddollar/foreman

Procfileをベースにプロセスの複数起動や、並列起動を管理するツール

# heroku toolbelt
herokuのコマンドラインツール

# herokuのダッシュボードのページの機能

パイプライン
レビュー→ステージング→本番

ステージングに関してはgithubのリポジトリ


