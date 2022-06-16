## バリデーションの作成

* 存在チェックする(presence)

```ruby
validates :column, presence: true
```

* 長さを制限する(length)

```ruby
validates :column, maximum: 255
validates :column, minimum: 3
validates :column, in: 3..255
validates :column, is: 8
```

* 空を許可する(allow_blank)

```ruby
validates :column, allow_blank: true
```

* 数値のみを許可する(numericality)

```ruby
validates :column, numericality: true
# 整数のみ
validates :column, numericality: {only_integer: true}
```

* 特定のフォーマットにマッチするかどうか

```ruby
validates :column, format: { with: 正規表現 }
```

* 特定のフォーマットにマッチするかどうか

```ruby
validates :column, uniquieness: true
# 大文字・小文字を区別しない
validates :column, uniquieness: { case_sensitive: false }
```

* エラーメッセージは `message.errors` に格納される
* 以下はrailsデフォルトのエラーメッセージ表示の書き方

```html
<% if message.errors.any? %>
<div id="error_explanation">
  <h2><%= pluralize(message.errors.count, "error") %> prohibited this message from being saved:</h2>

  <ul>
    <% message.errors.full_messages.each do |message| %>
      <li><%= message %></li>
    <% end %>
  </ul>
</div>
<% end %>
```
