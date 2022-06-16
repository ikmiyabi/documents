# Amazon Correttoのインストール

## Homebrew Caskを使用してインストールする(Macの場合)

### Homebrewがインストールされていない人は[こちら](https://brew.sh/index_ja)からインストール
> HomebrewはMacOS用のパッケージマネージャで、Homebrew Caskはその拡張機能。
> 普通に使う分にはMacのCLIでパッケージ（ソフトウェア）のインストールや管理ができるツールという認識で良い。

```bash
brew cask install corretto
# javaのバージョンを確認する
java --version
# 以下のように表示されればOK
# openjdk 11.0.5 2019-10-15 LTS
# OpenJDK Runtime Environment Corretto-11.0.5.10.2 (build 11.0.5+10-LTS)
# OpenJDK 64-Bit Server VM Corretto-11.0.5.10.2 (build 11.0.5+10-LTS, mixed mode)
```

### 設定が反映されない場合

- 環境設定のJAVA_HOMEを確認する

```bash
# java_homeコマンドにより、現在のJAVA_HOMEの設定を確認する
/usr/libexec/java_home

# バージョンを指定してMacにインストールされているJava11のJDKを表示する
/usr/libexec/java_home -v 11
# 以下のようにamazon-corretto11のjdkが表示されることを確認する
# /Library/Java/JavaVirtualMachines/amazon-corretto-11.jdk/Contents/Home

# JAVA_HOMEにjava11(amazon corretto 11)を設定
export JAVA_HOME=`/usr/libexec/java_home -v 11`
```

(参考)
- [MacでのJAVA_HOME設定
](https://qiita.com/seri_k/items/e978c1339ce51f13e297)
