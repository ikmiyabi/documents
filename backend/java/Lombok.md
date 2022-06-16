# Lombokとは

## Lombokとは

Javaのgetter/setterなどの定型コードを、コンパイル時に補完するライブラリである。下記の例のように、アノテーションを付与することで、コンパイル時にLombokがコードを自動的に生成するため、コーディング量を削減する事ができる。

```Java
import lombok.Data;

@Data
public class Test {
    private int id;
    private String name;
    private boolean available;
}
```

## Mavenプロジェクトでの利用方法

統合開発環境はSTSを前提とする。

```xml
<properties>
  <lombok.version>1.14.8</lombok.version>
</properties>

<dependencies>
  <dependency>
    <groupId>org.projectlombok</groupId>
    <artifactID>lombok</artifactID>
    <version>${lombok.version}</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```