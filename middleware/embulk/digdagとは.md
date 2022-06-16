# Digdagとは？

* バッチの実行などのワークフローエンジン

## Digdagのインストール

```bash
sudo curl -o ~/bin/digdag -L "https://dl.digdag.io/digdag-latest"
sudo chmod +x ~/bin/digdag
```

## Digdagサーバーの実行

```bash
digdag server -c ~/.config/digdag/config
```

## 設定はdigファイルで管理する

* 書式はymlファイルとほぼ一緒
  ※ymlファイルでない理由はmapのキーのキーの順番を維持するため(らしい)
* ファイル名 = ワークフローの名前となる(hoge.dig → hoge)

## digファイルの書き方

* タスクとオペレータ、変数定義を記述する
  * タスク(+XXXXX:)
    →１つの処理単位を書く
  * オペレータ(XXXX>:)→実行する処理を書く
  * 変数定義
* 定義した変数は `${～}` で取得する
```bash
sh >: echo ${hoge}
```
* timezone, session-uuidなどのビルドイン変数が利用できる
* タスクの並列実行は_parallel: trueを指定する
* バックグラウンド実行は `_background: true` を指定する
* エラー通知は `_error:`メッセージでワークフロー失敗時に実行する


## Digdagのインストール

```sh
curl -o ~/bin/digdag --create-dirs -L "https://dl.digdag.io/digdag-latest"
chmod +x ~/bin/digdag
```

## パスを通す

.zshrcに以下を追記する(記載済みの場合は不要)

```sh
export PATH="$HOME/bin:$PATH"
```

## ワークフローの作成

- 以下コマンドを実行し、workflow.digファイルを作成する

```sh
digdag init workflow
```

digファイルはymlファイルと同じ構造
※拡張子がymlではなくdigなのは普通のymlと異なりmapのキーの順番が維持される必要があるため

## ワークフローの実行

```sh
digdag run workflow.dig --project workflow
```

## Digdagサーバーを起動させる

- オンメモリで実行する場合

```sh
digdag server --memory
```

- databaseにデータを保存する場合

```sh
digdag server --database db
```

## Digdag

プロジェクトをアーカイブし、サーバーにアップロードする

```sh
digdag push sample_workflow --project workflow
```

## 参考
- [Digdagコマンド](https://docs.digdag.io/command_reference.html)