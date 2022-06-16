# printとechoの違い
## printは戻り値を返し、echoは戻り値を返さない

```php
$output = print "Hello World";
$output = echo "Hello World"; // エラー
```

## 速度はechoの方が早い

* echoは戻り値を返さないため、printより速度が早い

## echoは引数の複数指定ができる、printはできない

```php
print "Hello", "World"; // エラー
echo "Hello", "World";
```