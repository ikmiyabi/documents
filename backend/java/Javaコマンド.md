# ヒープ領域のチューニング

|オプション|内容|
|:-:|:-:|
|`-Xms`|ヒープ領域の初期値|
|`-Xmx`|ヒープ領域の最大値|

```bash
java ... -Xms2048m -Xmx3072
```

## システムプロパティの設定

```bash
java -Dfile.encoding=UTF-8
```

のように設定

## クラスパスの設定

```bash
java -classpath [クラスパス]
java -cp [クラスパス]
```

のように設定