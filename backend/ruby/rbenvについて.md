# rbenvについて
## rbenvとは

* rubyのバージョン管理ツール
* rubyのバージョンの切り替えを行う

## rvmとの違い

* ruby本体はついてこない。必要な場合はruby-buildを用意する。
* rvmより速く、コンパクト
* プラグインなどを追加出来る

## コマンド

|コマンド|内容|
|:-:|:-:|
|`rbenv versions`|バージョンを確認する|
|`rbenv install バージョン]`|指定したバージョンのrubyをインストールする|
|`rbenv local バージョン`|バージョンの切り替えを行う|
|`rbenv rehash`|設定を再読み込みする|
