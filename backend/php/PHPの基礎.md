# PHPの基礎
## PHPとは

* Webに特化したサーバーサイドのスクリプト言語
  ※スクリプト言語とは、プログラムの記述や実行を比較的容易に出来る言語
* 用途はWebメイン、HTMLと合わせて使う
* インタープリタ形式
* データベースとの連携が楽だが、速度が遅い・セキュリティが脆いという欠点がある

## Hello World

* phpタブ `<?php ~ ?>` で囲んで記述する

```php
<?php
    echo 'Hello World!';
?>
```

## GETメソッド、POSTメソッド

test.html

```html
<html>
  <body>
    <form method="GET" action="test.php">
      お名前：<input type="text" name="username">
      <input type="submit" value="送信">
    </form>
  </body>
</html>
```

```php
<?php
  echo "こんにちは".$_GET["username"]."さん";
?>
```

注）「<」や「<」、「&」でバグが発生するのを回避するためには、htmlspecialchars関数を用いること

※POSTメソッドに変更するにはGETの部分をPOSTに変更すればよい

## isset関数

* 値が設定されているならtrueを返すメソッド

## dateメソッド

```php
echo date("Y-m-d");
// 2016-09-12等
```

## 変数の定義

|変数名|役割|
|:-:|:-:|
|$_REQUEST|HTTPのリクエストパラメータ|
|$_GET|HTTPのGETパラメータ|
|$_POST|HTTPのPOSTパラメータ|
|$_FILES|アップロードされたファイルの情報|
|$_SESSION|セッション|
|$_COOKIE|クッキー|

## 繰り返し文

* break;で繰り返し処理を中断する
* continue;でその会の処理を飛ばす

## 配列

* Javaの場合

```java
String fruits[] = {"りんご", "みかん", "バナナ"}
for (int i = 0; i < fruits.length; i++) {
    System.out.println(array[i]);
}
```

* PHPの場合

```php
$fruits = array("りんご", "みかん", "バナナ");
for ($i = 0; $i < count($fruits); $i++) {
    echo $fruits[$1]."<br>";
}
```

## ハッシュ(Hash)

* 連想配列やディクショナリ(Dictionary)とも呼ばれる

* Javaの場合

```java
HashMap<String, String> fruits = new HashMap<String, String>();
fruits.add("apple", "りんご");
fruits.add("orange", "みかん");
fruits.add("banana", "バナナ");
System.out.println(fruits.get("apple"));
// 結果はリンゴ
```

* PHPの場合

```php
$fruits = array(
    "apple" => "りんご";
    "orange" => "みかん";
    "banana" => "バナナ";
);
echo $fruits["apple"];
// 結果はりんご
```

## 文字列操作

* echo（文字列を標準出力する）

```php
echo 'welcome';
```

### シングルクォート「''」とダブルクォート「""」について

シングルクオート「''」については単純に文字列を出力する
ダブルクォート「""」についてはエスケープする

基本的にはシングルクォートを使用し、エスケープの必要がある際にはダブルクォートを用いるのが一般的

## ?>の省略

* 全てphpで書かれているphpのファイルについては?>は省略可能
* むしろ余分な空白が入ってしまうことから省略すること推奨されている
* phpを埋め込んでいるものについては省略不可

## print

* echoと同様文字列を標準出力する
* 一般的にはechoを用いる(echoの方が速度が速いため)

## ヒアドキュメント構文
* 「<<<」の後ろに指定した記号までの文字列を標準出力する

```php
echo <<< END
Welcome
to
PHP
END;
// 前にスペース等を入れてはいけない
```


## require

* 使い回す部分を別ファイルにまとめる(require文)

```php
require 'ファイル名';
```

## リクエストパラメータの取得

* $_REQUEST['リクエストパラメータ名']で指定したリクエストパラメータを取得する
* isset関数を用いればパラメータがしていされているのかどうか調べられる
* htmlspecialchars関数を使用することで<>などのhtmlの特殊文字を無効化し、文字列として取得することが出来る

## 変数・定数

* $nameのように$変数名のように宣言
* counst NAMEのように宣言する($は不要)

## 制御構文

### if文

```php
<?php
  if (isset($_REQUEST['mail'])) {
    echo 'メールを送信する';
  } else {
    echo 'メールを送信しない';
  }
```

### switch文

```php
<?php
  switch($_REQUEST['time']) {
    case 'morning':
      echo 'おはよう！';
      break;
    case 'afternoon':
      echo 'こんにちは！';
      break;
    case 'night':
      echo 'こんばんは！';
      break;
  }
```

### for文

```php
for ($i = 0; $i < 10; i++) {
  echo '結果：'.$i
}
```

### foreach文

```php
// 配列をforeach文で標準出力
$colors = ['red', 'blue', 'yellow', 'black', 'white'];
foreach ($colors as $color) {
  echo $color;
}

// ハッシュをforeach文で標準出力
$fruits = array(
    "apple" => "りんご";
    "orange" => "みかん";
    "banana" => "バナナ";
);
foreach ($fruits as $key => $value) {
  echo $key.': '.$value;
}
```

## PHPの配列

### 配列

* 配列の宣言は二つ方法がある

```php
$list = [2, 3, 5, 7];
$list = array(2, 3, 5, 7);
```

## 関数

* 日時の取得

```php
// タイムゾーンを指定する
date_default_timezone_set('Japan');

// フォーマットを指定して日時を表示する(2019/01/23 12:34:56)
date('Y/m/d H:i:s');
```

* 乱数の利用

```php
// 乱数を取得する
rand();

// 最小値、最大値を指定して乱数を取得する
rand(min, max);

// 乱数の最大値を取得する
getrandmax();
```

* 全角・半角の変換

```php
// 半角カナを全角かなへ変換する
mb_comvert_kana('カナ');

// 全角数字を半角数字に変換する
mb_convert_kana('３６５', n);
```

※マルチバイト文字列関数の一種。複数バイトの文字列を操作する関数のこと。戦闘にmbがつく

* 正規表現

|メソッド名|内容|
|:-:|:-:|
|`preg_match('パターン', '入力文字列')`|入力文字列が指定したパターンにがっちすればtrue(1)を返すメソッド|

```php
$postcode = $_REQUEST['postcode'];
$regexp = '/^[0-9]{7}$/';
if (preg_match($regexp, $postcode)) {
  echo $postcode.'は郵便番号です';
} else {
  echo $postcode.'は郵便番号ではありません';
}
```

* ファイル操作

|メソッド名|内容|
|:-:|:-:|
|`file_exist('ファイル名')`|指定したファイルが存在すればtrue、しなければfalseを返す|
|`file_get_contents('ファイル名')`|ファイルを読み込む関数|
|`file_put_contents('ファイル名', '文字列')`|ファイルに文字列を書き込む関数|
|`json_decode('文字列')`|json形式の文字列をPHPの文字列や配列のデータに変換する|
|`json_encode('値')`|文字列やデータをjson形式に変換する|

```php
$file_path = 'board.txt';
if (file_exists($file_path)) {
  $board = json_decode(file_get_contents($file_path));
}
$board[] = $_REQUEST['message'];
file_put_contents($file_path, json_encode($board));
foreach ($board as $message) {
  echo $message;
}
```

* ファイルのアップロード

```html
<form action="~" method="post" enctype="multipart/form-data">
```

※アップロードされたファイルは一時的なファイルに保存され、そのファイル名は `$_FILE['file']['tmp_name']` で取得できる

|メソッド名|内容|
|:-:|:-:|
|`is_uploaded_file('ファイル名')`|指定したファイルアップロードされたファイルか確認する|
|`mkdir('フォルダ名')`|指定したフォルダを作成する|
|`basename('パス')`|パスの末尾にあるフォルダ名や、ファイル名のみを取り出す|
|`move_uploaded_file('一時的なファイル, 保存先のファイル')`|アップロードされた一時的なファイルを保存先へ移動する。成功時にはtrueを返す|

## PHPのデータベース操作

* PDOクラス

DSN(Data Source Name)とはデータベースを識別するための情報

// DSN(Data Source Name)とはデータベースを識別するための情報
```php
$pdo = new PDO(
    'mysql:host=localhost;dbname=shop;charset=utf8',
    'username',
    'password');
// DSN(Data Source Name)とはデータベースを識別するための情報

foreach ($pdo->query('select * from product') as $row) {
  echo "<p>:$row['id']:$row['name']:$row['price']</p>";
}
```

* sql文の実行

```php
// sql文の準備
$sql = $pdo->prepare('select * from product where name = ?');
// sql文の実行
$sql->execute([$_REQUEST['keyword']]);
```

## サンプル

```php
<?php
/* PHPの基本文法 */

// 文字列の出力
print 'こんにちは'. PHP_EOL;
echo 'こんばんは', PHP_EOL;

// 変数の宣言
$number = 1;
var_dump($number);

$number = 1.2;
var_dump($number);
// 定数の宣言
const NAME = "miyabi";
var_dump(NAME);

// 配列
$list = [2, 3, 5, 7];
var_dump($list);

// 連想配列(ハッシュ)
$fruits = array(
    "apple" => "りんご",
    "orange" => "みかん",
    "banana" => "バナナ",
);
var_dump($fruits);
echo $fruits["apple"]."\n";

// bool型
$is_true = true;
var_dump($is_true);
$is_false = false;
var_dump($is_false);

// 乱数の利用
$random_number = rand(1, 10);

// if文
if ($random_number > 5) {
    echo "$random_number", "は5より大きいです", PHP_EOL;
} else {
    echo "$random_number", "は5以下です", PHP_EOL;
}
```