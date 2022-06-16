# よく使うGitコマンド
## 確認系

```bash
# 作成・変更されたファイルを確認する
git status
```

|オプション|内容|
|---|---|
|--short|短く表示する|
|--branch|現在のブランチを表示する|


```bash
# コミットログを確認する
git log
```

|オプション|内容|
|---|---|
|--oneline|コミットログの先頭７桁のコミットIDを表示する|
|--decorate|コミットログのHEADの位置を表示する|
|--graph|コミットログをグラフで表示する|
|-[number]<br>-10|コミットログを指定した数だけ表示する<br>コミットログを10個表示する|
|--grep [word]|指定した文字のがコミットログに含まれるコミットを表示する|
|-p|修正した差分を表示する|
|--stat|変更したファイルを表示する|
|--author=[ユーザー名]|指定したユーザーのコミットを確認する|


```bash
git diff
```

|オプション|内容|
|---|---|
|--cached|インデックス(add済み)のファイルの差分を確認する|


```bash
git show
```

## 登録系

```bash
git add [ファイルパス]
```

```bash
git commit
```

|オプション|内容|
|---|---|
|--amend|コミットを上書きする|
|--allow-empty|空コミット(変更履歴なしのコミット)を行う|
|-m "commitメッセージ"|コミットメッセージを付けてcommitする|


```bash
git merge
```

```bash
git rebase
```

```bash
git cherry-pick
```

```bash
git revert
```

## ブランチ操作系

```bash
git branch
```

```bash
git checkout
```

## 取り消し系

```bash
git reset
```

```bash
git stash
```

|オプション|内容|
|---|---|
|save "コメント"|コメント付きで一時退避する|
|list|一時退避した差分を一覧を表示する|
|pop|退避させた差分を再度適用する|
|drop|退避させた差分を削除する|
|clear|退避させた差分を全て削除する|


```bash
git reflog
```

## 初期設定系

```bash
git init
```

```bash
git clone
```

```bash
git config
```

|オプション|内容|
|---|---|
|--list|設定内容を確認する|


## リモート操作系

```bash
git fetch
```

|オプション|内容|
|---|---|
|-p|リモートで削除済みのブランチを削除する|


```bash
git pull [リポジトリ名] [ブランチ名]
# デフォルト
git pull origin master
```

```bash
git push [リポジトリ名] [ブランチ名]
# デフォルト
git push origin master
```

# gitトラブルシューティング
## 困った時のgit stash
```bash
git stash (save)         #差分を一時退避させる
git stash list        #一時退避させた差分の一覧を見る
git stash pop [number]        #一時退避させた差分を元に戻す
```

## git blameで犯人探し
```bash
git blame [ファイル名]        #各行を修正した人物がわかる
```

## ブランチの削除（名前を間違えて作成した時など）
```bash
git branch -d [ブランチ名]
```

## ブランチの強制削除（マージ済みでないブランチも削除）
```bash
git branch -D [ブランチ名]
```