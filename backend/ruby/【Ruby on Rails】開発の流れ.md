# RubyonRailsとは？

* プログラミング言語Rubyで記述されたフレームワーク
* デンマークのプログラマーであるデイヴィッド・ハイネマイヤー・ハンソン氏が2004年にOSSとして公開
* 主な特徴は下記の3つ

1. MVCアーキテクチャ

処理をモデル(Model), ビュー(View)、コントローラ(Controller)の3つの役割に分ける考え方。

2. 同じことを繰り返さない(DRY原則: Dont Repeat Yourself)

設定などの作業はできるだけ一度で済むようになっていたり、同じコードを繰り返し書かずにすむように設計されている。

3. 設定より規約(CoC: Convention over Configuration)

様々な規約を設けることで、細かい設定を記述する手間がかからないようになっている。

# Ruby on Railsの導入
## 前準備(Macの場合)

* railsをインストールする
* rbenv, ruby-buildをインストールする
* mysqlをインストールする
* bundlerをインストールする

```bash
# homebrewで各種ソフトウェアを追加する
brew install mysql
brew install rbenv
brew install ruby-build

# ruby2.5.1をインストールする
rbenv install 2.5.1
# rubyのバージョンを2.5.1に指定する
rbenv local 2.5.1
# rubyのバージョンの確認
rbenv versions

# bundlerをインスールする
gem install bundler
```

## railsプロジェクトを作成する

```bash
rails new rails_app --database=mysql --skip-bundle
```

* --databaseオプションを指定しない場合はSQLiteになる
* --skip-bundleオプションをつけると、最初の `bundle install` をスキップする
* --skip-testオプションをつけると、テストコードを作成しない

## プロジェクトで使用するdbを作成する

```bash
# dbを作成する
rails db:create
# mysqlにログインして確認する
rails db
mysql> show databases;
```

## gitの初期設定と最初のコミットを行う

* 事前にGitHubやGitLabでリポジトリを作成しておく

```git
git init
git remote add origin [リポジトリ名]
git add .
git commit -m "Start [rails_app] project"
```

# モデルの開発
## モデルを作成する

```bash
rails g model Customer name:string age:string comment:text
#ファイルを確認し、問題なければマイグレートを実行する
rails db:migrate
```

## scaffoldでモデル・コントローラ・ビューをまとめて作成する

```bash
rails g scaffold Company name:string url:string
rails db:migrate
```


## カラムの追加

```bash
rails g migration AddCommentToCustomer comment:text
```

すること
* modelの修正: バリデーションの追加
* routerの修正: ページが増える場合は修正
* controllerの修正: ストロングパラメータの許可を追加
* viewの修正:  フォーム、一覧、詳細に表示される個所を修正

# ルーティングの設定
## ルーティング設定を行う

* `config/routes.rb` を修正することでルーティングの設定を行う

```ruby
Rails.application.routes.draw do
  # CRUD
  get 'customers/:id', to: 'customers#show'
  post 'customers', to: 'customers#create'
  put 'customers/:id', to: 'customers#update'
  delete 'customers/:id', to: 'customers#destroy'

  # index: show の補助ページ
  get 'customers', to: 'customers#index'

  # new: 新規作成用のフォームページ
  get 'customers/new', to: 'customers#new'

  # edit: 更新用のフォームページ
  get 'customers/:id/edit', to: 'customers#edit'
end
```

* RESTfulな画面のルーティングを行う場合、下記のようにすればまとめて設定できる

```ruby
Rails.application.routes.draw do
  root to: 'customers#index'
  resources :customers
end
```


## パスの設定

|ルーティング|リンク生成メソッドの例|生成されるリンク例|
|:-|:-|:-|
|index|employee_path||
|show|||
|new|||
|edit|||


# URLを深掘りするオプション

```ruby
  resources :users, only: [:index, :show, :new, :create] do
    member do
      get :followings
      get :followers
    end
    collection do
      get :search
    end
  end
```

# コントローラの開発
## コントローラを作成する

```bash
rails g controller Company
```

* helperが不要であれば、--no-helperオプションをつける
* assetsが不要であれば、--no-assetsオプションをつける

* 作成されたファイルにメソッドを追加する


app/controllers/customer_controller.rb

```ruby
before_action :set_message, only: [:show, :edit, :update, :destroy]
```

のようにして共通化することができる

* RESTfulな画面のルーティングを行う場合、下記のようにすればまとめて設定できる

```ruby
Rails.application.routes.draw do
  resources :customers
end
```

## 部品の共通化

* privateメソッドに処理をまとめる
* before_action を使用することで、Action実行前にまとめて実行させることができる

```ruby
before_action :set_message, only: [:show, :edit, :update, :destroy]
```

* パーシャル： `_form.html.erb` のように _ から始めて View の共通部を抜き出したものを使用する

```html
# 呼び出し側は下のようにして呼び出す
<%= render 'form', message: @message %>
```
