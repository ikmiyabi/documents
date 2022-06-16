## Vueインスタンスとは

Vue.jsの様々な機能をまとめたVueインスタンス

```js
new Vue({
  el: #app
});
```

## Vueインスタンスのプロパティ

プロパティ | 内容
:-: | :-:
el | vueインスタンスを結びつけるHTMLを指定
data | vue.jsで扱うデータを保持
methods | vueで使用するメソッドを定義
computed | 算出プロパティを定義
template | コンポーネントを定義
components | 外部モジュールとして取り込んだコンポーネントを登録

```js
new Vue({
  el: #app
  data() {
    return {
      count: 0;
    };
  }
});
```

## Mustache(マスタッシュ構文)

{{text}}のような記述のこと

```js
<body>
  <div id="app">
    <p>{{text}}</p>
  </div>
</body>
```

## 差分レンダリング

HTMLの一部が変更された時、データが変更された部分だけレンダリングする機能

仮想DOM: 差分レンダリングを行うために保持しているデータ
※Document Object Model