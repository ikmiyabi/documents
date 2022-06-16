# git logいろいろ

```bash
# グラフ化して表示する
git log --graph

# 修正ファイルも表示
git log --stat

# 各コミットの差分を表示

git log -p

# エイリアスの設定
git config --global alias.lg "log --graph --decorate"

# git logを短く見やすく表示
git log -50 --date=short --pretty="format:%C(YELLOW)%h %C(GREEN)%cd %C(CYAN)%an%C(RED)%d %C(reset)%s"
# 実際はaliasに設定して使用する
git config --global alias.lg 'log -50 --date=short --pretty="format:%C(YELLOW)%h %C(GREEN)%cd %C(CYAN)%an%C(RED)%d %C(reset)%s"'
# gitを打つのもめんどくさい人はこちら
alias lg='git log -50 --date=short --pretty="format:%C(YELLOW)%h %C(GREEN)%cd %C(CYAN)%an%C(RED)%d %C(reset)%s"'

#リモート追跡ブランチを最新の状態にする
git fetch

#指定のブランチに移動する
git checkout master

#リモートブランチ一覧表示
git branch -r

# ローカルブランチとリモートブランチ対応一覧表示
git branch -vvv

# リモートの内容を表示
git remote -v

# masterブランチを最新にする
git pull origin master

# ブランチを作成する
git branch develop/2018**** origin/master

# カレントブランチ切り替える
git checkout develop/2018****

# ブランチを作成して切り替える
git branch -b develop/2018**** origin/master

# 空のコミットを打ち、git上に履歴を残す
# -mでコメントをつけて空コミットする
git commit --allow-empty -m "Start develop/2018****"

git log

git push origin develop/2018****

# リモート追跡ブランチを更新する
git fetch -p
# ブランチ確認
git branch
#ブランチ作成
git branch feature/DEV-1160-**** origin/develop/20170222
#ブランチの切り替え
git checkout feature/DEV-1160-****
#ブランチが作成されたことを確認（-vvvで詳細を表示）
git branch -vvv

#ブランチの状態確認
git status
# 差分確認（add前の差分確認）
git diff
#修正したファイルをインデックスに追加
git add ファイル名

# ファイルの追加・変更履歴を残すファイルを確定する
#変更点を確認
git status
#差分確認（add後の差分確認）
git diff --cached
#コミットする（コミット前に確認！）
git commit

#ブランチの状態確認
git status
#ログの確認
git log
#直前のコミットの差分確認
git show
#特定のコミットの差分確認
git show [ハッシュ値]

# ローカルのmasterブランチを更新する
git fetch origin
git checkout master
git pull origin master

# ローカルのdevelopブランチを更新する
git checkout develop/20170330
git pull origin develop/20170330

# ローカルでdevelopブランチからmasterブランチへとマージする（変更を反映させる）
git merge --no-ff master

# ビルドできるか確認
bundle exec rake gradle:clean-build

# ログを確認してプッシュする（リモートブランチへと反映させる）
git log -5
git push origin develop/20170330

# 困った時のgit stash
git stash (save)         #差分を一時退避させる
git stash list        #一時退避させた差分の一覧を見る
git stash pop [number]        #一時退避させた差分を元に戻す

# git blameで犯人探し
git blame [ファイル名]        #各行を修正した人物がわかる

# ブランチの削除（名前を間違えて作成した時など）
git branch -d [ブランチ名]

# ブランチの強制削除（マージ済みでないブランチも削除）
git branch -D [ブランチ名]

# gitの設定
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com

# 色の設定
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
```