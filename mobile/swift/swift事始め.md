# swiftメモ

* delegateについて
* push通知について
* UserNotification
* @escapeについて(非同期)
* extension
* appdelegateの使い所
* UNUserNotificationcenter.current()
  * アプリまたはアプリ拡張の共有ユーザー
  * 通知センターにインスタンスを返す

## デリゲート(delegate)

1. プロトコル
   - 任せる処理をメソッドとして定義
2. 処理を任せるクラス
   - 処理の流れを記述
3. 処理を任されるクラス
   - デリゲートメソッドを実装

```bash
TableView.delegate = self
// TableViewインスタンスのデリゲート先をViewController(今のクラス)に設定している
```

## フォルダの構成

ファイル|内容
:--:|:--:
AppDelegete | アプリの状態に応じて動作する処理
ViewController | 画面に関する処理
Main.storybord | 画面を編集するファイル
Assets | アイコンなどを保存
LaunchScreen | アプリが立ち上がったときに表示される画面
info.plist | アプリに関する設定をまとめるファイル

## NotificationCenterの使い方

1. NotificationCenterに通知を登録する

```swift
NotificationCenter.default.addObserver(self,
                   selector: #selector(type(of: self).notified(notification:)),
                   name: Notification.Name.UIApplicationDidBecomeActive,
                   object: nil)
```
