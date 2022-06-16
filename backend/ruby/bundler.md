# bundlerについて
## bundlerとは

gemの管理管理ツール。Gemfileにインストールしたいgemを記述し、それを元にbundlerを使用してインストールを行う。
bundler本体以外のgemは基本的にbundler経由でのインストール推奨。

※gemはRuby言語用のライブラリ

```bash
# bundler自体をインストール
gem install bundler

# Gemfileにインストールするgemを記述する
vi Gemfile

# パスを指定してgemをインストール(次回以降はオプションをしていしなくてOK)
# bundle/configにパスが記載されている
# bundle install --systemとした場合、システムにインストール
bundle install --path vendor/bundle
```
