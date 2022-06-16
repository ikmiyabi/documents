# Spring Integration
## Spring Integrationとは

* メッセージを中心として、複数のシステムを連携できるように設計されたフレームワーク


## Spring Integrationの構成要素

* Message
* Channel
* Endpoint

## Message

メッセージは下記のようにPayloadとHeaderで構成される

* Message
  * Header: Endpointで付与される情報
  * Payload: 任意の形式の情報(xmlや単純な文字列など)

## Channel

チャネルはEndpointから外部に送信したり、Endpointから受信するのに必要なもの。
二通りのタイプがある。

* Channel
  * Point-to-Point Channel: 1:1で送信
  * Publisher-Subscribe Channel: 1:nで送信

## Endppoint

エンドポイントは、Messageそのものを処理する部分であり、いくつかの種類がある。

アプリケーション連携のためのEndpointには二つのタイプがある。

* Adapter: 一方通行
* Gateway: inputとoutputがあり双方向

* Service Activator: Messageを引数にしてメソッドを実行する
* Router: HeaderやPayloadの情報からメッセージをルーティングする
* Spliter: 一つのメッセージを複数のメッセージに分割して、チャネルに送信する
* Aggregator: 複数のメッセージを一つのメッセージにまとめて、チャネルに送信する