## 変数の宣言

```swift
var 変数名: データ型 = 初期値

// 例
var number: Int = 10
```


### 型推論による
右辺からデータ型を推測できるような場合は、型の指定を省略できる。
言語仕様レベルでデータ型を推測してくれる仕組みのことを型推論と呼ぶ。

```swift
var message = "Hello, World!" // String型
```

## 定数の宣言

```swift
let 定数名: データ型 = 値

// 例
let name: String = "Ichiro"
// 変数の宣言時と同様に型推論が働く
let name = "Ichiro"
```

## コメント

```swift
// 一行コメント
/*
    複数行コメント
*/
```

## データ型

データ型 | 保存できるデータ
:-: | :-:
Int8 | -128(2^7)〜127(2^7-1)の整数
Int16 | -32768(2^15)〜32767(2^15-1)の整数
Int32 | -2147483648(2^31)〜2147483647(2^31-1)の整数
Int64 | -9223372036854775808(2^63)〜9223372036854775807(2^63-1)の整数
Int | 32bitプラットフォームではInt32、64bitプラットフォームではInt64と同様
UInt8 | 0〜255(2^8-1)の整数
UInt16 | 0〜65535(2^16-1)の整数
UInt32 | 0〜4294967295(2^32-1)の整数
UInt64 | 0〜18446744073709551615(2^64-1)の整数
UInt | 32bitプラットフォームではInt32、64bitプラットフォームではInt64と同様
Float | 32bitの不動小数点
Double | 64bitの不動小数点。小数を取り扱う場合は主にこちらを使用する
String | 可変長文字列(複数の文字の連なり)
Characcter | 任意の一文字
Bool | 真偽値。trueまたはfalseのいずれか

### 数値型

- 数値型には2進数、8進数、16進数で宣言することも可能

```swift
let bin = 0b0111 // 2進数(binary number)
let bin = 0o16 // 8進数(octal number)
let bin = 0x1A // 16進数(hexadecimal number)
```

- 数値型のリテラルは_(アンダースコア)で区切ることができる。

```swift
let separatedNumber = 123_456_789
print (separatedNumber) //=>123456789
```

## タプル(Tuple)

- swiftでは複数の値をもつタプル型を宣言できる

```swift
let result: (Bool, String, Int) = (true, "iOS", 13)
// 省略形
let result = (true, "iOS", 13)

// データの使用
print(result.0) //=> True
print(result.1) //=> iOS
print(result.2) //=> 13
```

- タプルの値は以下のように、同時に別の変数に代入できる

```swift
let(isSuccess, name, version) = result
print(isSuccess) //=> True
print(name) //=> iOS
print(version) //=> 13
```

- タプルの値にラベルをつける

```swift
let result = (isSuccess:true, name:"iOS", version:13)

print(result.isSuccess) //=> True
print(result.name) //=> iOS
print(result.version) //=> 13
```

## 配列(Array)

- 配列の宣言

```swift
let oddNumbers = [1, 3, 5, 7, 9]
print(oddNumbers[1])
//=> 3

let fruits = ["Apple", "Banana", "Orange"]
print(fruits[0])
print(fruits[3])
//=> Apple
```

- 最初の要素、最後の要素を取得する
  - 取得結果はOptional型になることに注意

```swift
let fruits = ["Apple", "Banana", "Orange"]

print(fruits.first)
print(fruits.last)
```

- 配列の値を書き換える

```swift
fruit[2] = "Melon"
```

- 配列の要素の追加、挿入、削除

操作 | 処理
:-: | :-:
追加 | `配列.append(追加する要素)`
挿入 | `配列.insert(追加する要素, at: インデックス)`
削除 | `配列.remove(at: 削除する要素のインデックス)|`

```swift
var userIds = [10, 20, 30]

userIds.append(40)
userIds.insert(25, at: 2)
userIds.remove(at: 0)
print(userIds)
```

## 辞書(Dictionary)

- 初期化

```swift
var fruitNames = ["apple": "りんご", "banana": "ばなな", "orange": "みかん"]

// 追加(キーが存在する場合は上書きとなる)
fruitNames["grape"] = "ぶどう"
// 削除
fruitNames.removeValue(forKey: "apple")
```

## for文

- 通常のfor文

```swift
// 閉区間範囲演算子
for i in 1...5 {
    print(i)
}

// 半開区間範囲演算子
for i in 1..<5 {
    print(i)
}

// 2づつ増やすfor文
for i in stride(from: 10, to: 100, by: 2) {
    print(i)
}
```

## ビット演算子

演算子 | 内容 | 例
:-: | :-: | :-:
`<<` | 値を左へn桁シフトする
`>>` |値を左へn桁シフトする
`&` | AND演算(論理積)を行う
`|` | OR演算(論理和)を行う
`^` | XOR演算(排他論理和)を行う
`~` | NOR演算(ビット否定)を行う

```swift
let binaryNumber = 0b1100
print(binaryNumber >> 2) //=> 3(0b0011)
print(binaryNumber << 2) //=> 48(0b110000)

let x = 0b1100 // 12
let y = 0b0110 // 6
print(String(x | y, radix: 2)) //=> 14(0b1110)
print(String(x & y, radix: 2)) //=> 4(0b0100)
print(String(x ^ y, radix: 2)) //=> 10(0b1010)
```

## if文

```swift
if 条件式 {
    // 条件式がtrueだった時の処理
} else {
    // 条件式がfalseだった時の処理
}
```

- FizzBuzz

```swift
for i in 1...100 {
    if i % 15 == 0 {
        print("FizzBuzz")
    } else if i % 3 == 0 {
        print("Fizz")
    } else if i % 5 == 0 {
        print("Buzz")
    } else {
        print(i)
    }
}
```

## switch文

```swift
switch 条件式 {
case 値 1:
    // 式の値が1だった場合の処理
case 値 2:
    // 式の値が2だった場合の処理
default:
    // 式の値が1でも2でもなかった場合の処理
}
```

- 範囲演算子を使用する

```swift
let number = 5

switch number {
case 1...3:
    print("1...3")
case 4..<10:
    print("4..<10")
default:
    print("default")
}
```

## Optional

- swiftの通常データ型はそのままではnilを格納できない

```swift
var tel: String = nil //=> コンパイルエラー
```

- swiftにはデータ型の最後に?をつけることでnilを格納することができるOptional型を定義できる
  - このOptional型は元のデータ型とは全く異なる型である

```swift
var tel?: String? = nil
```

