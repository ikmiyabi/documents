# リストを複数条件でソートする（java8）

## Java.util.streamの活用

```java
List<UserLog> resultUlList = ulList.stream()
    .sorted(Comparator.comparing(UserLog::getCreatedDate_YYYYMMDDHHMMSS).thenComparing(UserLog::getId).reversed())
    .collect(Collectors.toList());
```
1. streamメソッドでstream化する
2. Comparator（コンパレータ）にソート条件を指定する

```java
comparing(UserLog::getCreatedDate_YYYYMMDDHHMMSS)  // 一つ目のソート条件を指定
    .thenComparing(UserLog::getId)  // 二つ目のソート条件を指定
    .reversed()  // 逆順に変更
```

3. ```.collect(Collectors.toList())```でリストに収納する

## ラムダ式
- [今更聞けない？java8のラムダ式](http://www.casleyconsulting.co.jp/blog-engineer/java/%E4%BB%8A%E6%9B%B4%E8%81%9E%E3%81%91%E3%81%AA%E3%81%84%EF%BC%9Fjava8%E3%81%AE%E3%83%A9%E3%83%A0%E3%83%80%E5%BC%8F/)
- [関数型プログラミングって何、ラムダってなんだよ](http://qiita.com/lrf141/items/98ffbeaee42d30cca4dc)
- 「関数型インターフェースを簡単に書けるもの」と思っておけばいい
    - 関数型インターフェースは抽象メソッドを一つ持つインターフェースのこと(らしい)

```java
comparing(new Comparator<UserLog>(){
    @Override
    public Date compare(UserLog ul1,UserLog ul2){
        return ul2.getCreatedDate_YYYYMMDDHHMMS() - ul1.getCreatedDate_YYYYMMDDHHMMS();
    }
})
```
↑これが

```java
comparing(UserLog::getCreatedDate_YYYYMMDDHHMMSS)
```

↑こうなる