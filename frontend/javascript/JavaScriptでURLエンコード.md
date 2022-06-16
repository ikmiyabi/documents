# JavaScriptでのURLエンコード

- 方法は以下の二つ
    - encodeURI(param)を用いる
    - encodeURIComponent(param)を用いる
- 違いは+や:などの特殊文字もエンコードするかどうか
    - +や:などもエンコードさせたい場合はencodeURIComponentを使う（通常これを用いることの方が多いはず）
- 他escape()というものもあるがこれは少々特殊で、全角文字列をUnicodeに変換する

[実例]
```js
// encodeURIComponentを用いる（特殊文字もURLエンコード）
function show1(){
var param = 'test+あ?@test.jp';
console.log(encodeURIComponent(param));
}
show1();

// encodeURIComponentを用いる（特殊文字はURLエンコードしない）
function show2(){
var param = 'test+あ?@test.jp';
console.log(encodeURI(param));
}
show2();

// escapeを用いる（特殊文字はURLエンコード、２バイト文字はUnicodeへ）
function show3(){
var param = 'test+あ?@test.jp';
console.log(escape(param));
}
show3();
```
[結果]
```
test%2B%E3%81%82%3F%40test.jp
test+%E3%81%82?@test.jp
test+%u3042%3F@test.jp
```
[参考]
- [JavaScriptのエスケープあれこれ](http://www.techscore.com/blog/2013/10/15/javascript%E3%81%AE%E3%82%A8%E3%82%B9%E3%82%B1%E3%83%BC%E3%83%97%E3%81%82%E3%82%8C%E3%81%93%E3%82%8C/)

