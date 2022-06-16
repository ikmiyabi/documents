# gitの設定ファイルの参照場所

- ググれば色々出てくるけどとりあえず公式を見ること

https://git-scm.com/book/ja/v1/Git-%E3%81%AE%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA-Git-%E3%81%AE%E8%A8%AD%E5%AE%9A

要約すると、

- 最初に見るのは/etc/gitconfig
    — systemの設定はココ
- 次に見るのは~/.gitconfig
    — globalの設定はココ
- 最後に見るのは.git/config
    — localの設定はここ

git configコマンド使えば楽に設定できる

例）

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

## 色の設定

```bash
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
```

## aliasの設定

```bash
# git stやgit co でコマンド実行できるようになる
git config --global alias.co "checkout"
git config --global alias.st "status"
git config --global alias.br "branch"
git config --global alias.cm "commit"
```

## シェルにgitブランチを表示させる
- .bashrcに以下を追加する

```bash:.bashrc
# gitブランチを表示する
function parse_git_branch {
    git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ [\1]/'
}
function promps {
    local  BLUE="\[\e[1;34m\]"
    local  RED="\[\e[1;31m\]"
    local  GREEN="\[\e[1;32m\]"
    local  WHITE="\[\e[00m\]"
    local  GRAY="\[\e[1;37m\]"

    case $TERM in
        xterm*) TITLEBAR='\[\e]0;\W\007\]';;
        *)      TITLEBAR="";;
    esac
    local BASE="\u@\h"
    PS1="${TITLEBAR}${GREEN}${BASE}${WHITE}:${BLUE}\W${GREEN}\$(parse_git_branch)${BLUE}\$${WHITE} "
}
promps
```