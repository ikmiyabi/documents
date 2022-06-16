# Java8: Optionalについて

- Optionalクラスを用いると、

```java
// before
Company manufactureCompany = Company.findByRootId$SiteType(companyRootId, SiteType.MANUFACTURE);
if (manufactureCompany == null) {
	throw new Exception("データ不整合 SUBテーブルにデータがありません。 companyRootId:["+companyRootId+"]");
}

// after
// 値をラップする
Optional<Company> opt = Optional.ofNullable(Company.findByRootId$SiteType(companyRootId, SiteType.MANUFACTURE));
// エクセプションが発生する場合の処理を指定する
Company manufactureCompany = opt.orElseThrow(() -> new Exception("データ不整合 SUBテーブルにデータがありません。 companyRootId:["+companyRootId+"]"));

// さらにまとめる
Company manufactureCompany = Optional.of(Company.findByRootId$SiteType(companyRootId, SiteType.MANUFACTURE))
		.orElseThrow(() -> new Exception("データ不整合 SUBテーブルにデータがありません。 companyRootId:["+companyRootId+"]"));
```

しかしJavaのOptionalは引数やフィールドに使うことは想定されていないらしく、メソッドの戻り値として使うことが想定されているらしい。
上記の作りの場合あくまで、.orElseThrow()が使えてnullチェックができるだけのもので、結局わかりにくくなってるだけじゃね？感がある。
以下のように呼び出し元ではなく、呼び出し先で戻り値にして記述することで呼び出し元にnullを考慮したコーディングを強制することができる。

```java
// Company.java
public static Optional<Company> findByRootId$SiteType(Integer rootId, SiteType siteType){
    return Optional.ofNullable(find().where(eq(companyRootId(), rootId), eq(siteType(),siteType)).getSingleResult());
}

// メソッドを呼び出す
Company manufactureCompany = Company.findByRootId$SiteType(companyRootId, SiteType.MANUFACTURE)
    	.orElseThrow(() -> new Exception("データ不整合 SUBテーブルにデータがありません。 companyRootId:["+companyRootId+"]"));
```
