# jQueryあれこれ
## ボタンを入力するたびに処理を実行させる処理
[事例]
- 文字入力・削除を行う毎にフォームのメールアドレスチェックを行い、形式が正しいかどうかを判定する
- 形式が合っている場合は確定ボタンを活性にする（押せるようにする）
- 形式が間違っている場合は確定ボタンを非活性にする（押せないようにする）

## prop()とattr()の違い

- .prop()はプロパティを取得・設定する
- .attr()は属性を取得・設定する

<参考>
- [jQueryでチェックボックスをチェック：prop()とattr()の違い](http://uxmilk.jp/10061)


- DOMとは何か：DOMを操作してhtmlのタグの内容を変化させる
- jQueryの読み込み位置は重要、読み込めていないと未定義となる
- onloadで読み込み直後に実行させることができる
- 下記ようにすればタグ付けしなくても読み込み直後に実行させることができる（全て同じ意味）

```js
$(document).ready(function(){
    // 実行したい処理
});

$().ready(function(){
    // 実行したい処理
});

$(function(){
    // 実行したい処理
});
```

- onchange属性でフォームの内容が削除されたタイミングで変更
- oninput属性でフォームに文字を入力・削除されるごとのタイミングで変更

- タグ内のテキストを変更する
$(#id_aaa).text("変更後のテキスト");
$(#id_aaa).text("");

- DOMを削除してタグごと削除する
```js
$(#id_aaa).remove();
```
- classの属性値を変更する
```js
$(#id_aaa).attr("class", "hoge");
```
- class属性自体を削除する
```js
$(#id_aaa).removeAttr("class");
```

- disabled属性値自体を追加する
```js
$(#id_aaa).prop("disabled", true);
```
- disabled属性自体を追加する
```js
$(#id_aaa).prop("disabled", false);

if($('#aaa').length){
    // id="aaa"が存在する場合の処理
}else{
    // id="aaa"が存在しない場合の処理
}
```
