# rubyメモ

## 使ってみて思うこと

* 書き方がいろいろあるため、コードの質がピンキリになる。書き手によって可読性・保守性が大きく変わってしまう。
* 標準ライブラリが充実している
* ||=、#{}など、記号が多く、検索するのが難しい場合がある
* Railsが便利
* javaよりコマンドラインとの連携が容易
* ENV[]、irbなど
* 定数の扱いが難しい
  * いちいちfreezeが必要だったり・・・

## 文字列展開には+ではなく#{}を使うこと

```ruby
name = "hoge"
puts "hello, " + name
#=> hello, hoge

puts "hello, #{hoge}"
```

* メリットは、可読性の向上とto_sを自動で行ってくれること

## シェルコマンドは``(バッククオート)で実行できる

```ruby
# lsコマンドをruby上で実行
puts `ls`

# サブシェルを実行
puts system (ls)

# 実行して終了する
puts exec (ls)
```

## require, require-relativeの違い

* requireは外部ファイルの読み込みを行う
* require-relativeは実行ファイルの相対パスを指定

※拡張子は省略可能

## 環境変数を呼び出す

```ruby
puts ENV['PATH']
```

## p, puts, printの違い

|コマンド|内容|
|:-:|:-:|
|`p`|値と型の情報を出力。デバッグ用|
|`puts`|内容を標準出力（改行有り）|
|`print`|内容を標準出力（改行無し）|

※pは戻り値も返す。puts, printはなし

## stringの連結

```ruby
str = "hoge"
str += "fuga"
puts str
#=> hogefuga

str="foo"
str << "bar"
puts str
#=> foobar
```

## ||=とは

* 値がnilであれば値を代入し、何か入っていれば何もしない

```ruby
hoge = nil
foo = "bar"

puts "hoge => #{hoge}" #=> 空文字
puts "foo => #{foo}" #=> bar

hoge ||= "fuga"
foo ||= "fuga"

puts "hoge => #{hoge}" #=> fuga
puts "foo => #{foo}" #=> bar
```


## シンボルとは

* ソース上では文字列、内部で整数として扱われる
* immutable(変更不可)
* 速度面でstringより有利なので、ハッシュのキーなどに使われる

## ベンチマークの取り方

* 標準ライブラリ `benchmark`を使う

```ruby
require 'benchmark'

Benchmark bm 10 do |r|
  # ベンチマーク1
  r.report "bm1" do
    # 計測する処理1
  end

  # ベンチマーク2
  r.report "bm2" do
    # 計測する処理2
  end
end
```

## CSVファイルを読み込む

* foreachで1行づつ読み込む

```ruby
require 'csv'

CSV.foreach("sample.csv") do |row|
  puts row
end
```

* 全体を1度に読み込む

```ruby
csv = CSV.read("sample.csv")
```

## シングルクォート、ダブルクォートの使い分け

* 基本的にはシングルクォートを使用する
* 式展開を行う際にはダブルクォートを使用する