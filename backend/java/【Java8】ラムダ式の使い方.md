# 【Java8】ラムダ式の使い方
## ラムダ式とは？

- JDK1.8で導入された構文
- インターフェースを実装したインスタンスの生成を簡単にした式
- 処理を引数に渡せてかんたん！

- 関数方インターフェースの実装を簡潔に書けるようにするためのもの

```java
@FunctionalInterface
public interface IntFunc {
  public abstract int func(int x);
}
```

ラムダ式を使用しない場合、以下のように書くことになります。

```java
IntFunc intFunc1 = new IntFunc(){
  @Override
  public int func(int x){
    return x+x;
  }
}
```

ラムダ式に書き換えた場合、以下のようになります。

```java
IntFunc intFunc2 = (int x) -› {return x+x;};
```

型を省略できるので以下のように省略できます。

```java
IntFunc intFunc3 = (x) -> {return x+x;};
```

```java
IntFunc intFunc4 = x -› x+x;
```

実際に。。。

shiva-frontend/src/main/java/shiva/frontend/conversion/AbstractConversion.java
```java
inquiryList.forEach(inquiry -> {
    insertInquiryCount += inquiryService.insert(inquiry);
    insertEnqueteCount += registEnquete(inquiry);
});
```


## 関数型インターフェースとは？
- 抽象メソッドが1つだけ定義されているインターフェース

## 実際に使ってみる
```java
// 関数型インターフェース
@FunctionalInterface
public interface Runnable {
  public abstract void run();
}

// 関数型インターフェースの実装
Runnable runner = new Runnable() {
  @Override
  public void run() {
  	System.out.println("Hello Lambda!");
  }
}

runner.run(); //Hello Lambda!
```

ラムダ式を使うと、
Class instance = 引数 -> { 処理 };
のように書ける


```java
// 関数型インターフェース
Runnable runner = () -> { System.out.println("Hello Lambda!"); };

runner.run(); //Hello Lambda!
```

```java
// 引数ありの場合はカッコを省略できる
Runnable runner = name -> { System.out.println("Hello " + name + "!"); };

runner.run("Java8"); //Hello Java8!
```