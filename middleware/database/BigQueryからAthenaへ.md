# BigQueryからAthenaへの移行メモ
## Athenaとは？

### そもそもAthenaとは？

* S3上のデータに対して、標準SQLにインタラクティブなクエリを投げてデータの分析を行うことができるサービス
* AthenaのクエリエンジンはPrestoをベースにしている
* パフォーマンス向上＆コスト削減目的のため、データをパーティションに分割している

### Athenaの特徴
* サーバーレスでインフラ管理の必要なし
* 大規模データに対しても高速なクエリ
* 事前のデータロードなしにS3に直接クエリ
* スキャンしたデータに対しての従量課金
* JDBC / API / CLI(CommandLineInterface) からクエリ可能
https://www.slideshare.net/AmazonWebServicesJapan/presto-amazon-athena

### Prestoとは？

https://aws.amazon.com/jp/emr/details/presto/
レイテンシーでアドホックなデータ分析用に最適化されたオープンソースの分散 SQL クエリエンジン
* Facebookが開発している分散SQLエンジン
* ペタスケールのデータに対しインタラクティブ（対話的）な検索が必要に
  * それまではHive中心
  * 2013年11月オープンソース化
* Prestoの特徴
  * CPU使用効率・スピード重視（アドホック検索）
  * インメモリ処理
  * Javaによる実装
  * 教科書的なRDBMSの実装
  * ANSI SQLベース

# BigQueryからAmazon Athenaへのチューニングメモ
## 1. _PARTITIONTIMEをdtに変更

|BigQuery|Athena|
|:-|:-|
|_PARTITIONTIME(timestamp)|dt(varchar)|

## 2. FORMAT_DATEをDATE_FORMATに変更

※関数名だけじゃなく、引数の位置も異なる

|BigQuery|Athena|
|:-|:-|
|FORMAT_DATE('%Y-%m-%d', [日時])|DATE_FORMAT([日時] ,'%Y-%m-%d')|


## 3. 現在の日付

|BigQuery|Athena|
|:-|:-|
|CURRENT_DATE()|CURRENT_DATE|


## 4. INTERVALの直後の数字には' 'をつける

|BigQuery|Athena|
|:-|:-|
|INTERVAL 3 DAY|INTERVAL '3' DAY|


## 5. AthenaのINTERVALはWEEKが使用できない(?)ので注意

|BigQuery|Athena|
|:-|:-|
|INTERVAL 1 WEEK|INTERVAL '7' DAY|


## 6. 日時の差はAthenaは引き算で表示できる

|BigQuery|Athena|
|:-|:-|
|DATE_SUB(CURRENT_DATE(),INTERVAL 30 DAY)|CURRENT_DATE - INTERVAL '30' DAY|


## 7. Athenaでは'hoge'と"hoge"は区別される

※ダブルクオートの場合、カラムを探しにいく（らしい）

|BigQuery|Athena|
|:-|:-|
|path = "/images/hoge.gif"|path = '/images/hoge.gif'|


## 8. SUBSTR([文字列], [開始位置], [終了位置])

・開始位置はどちらも1からスタート
・開始位置を0にした場合、BigQueryは1扱いになるが、Prestoだと失敗する（文字列が取得できない）

|BigQuery|Athena|
|:-|:-|
|SUBSTR(log_time, 0, 13)|SUBSTR(log_time, 1, 13)|


## 9. DATE(log_time)のlog_timeはvarcharなのでcastに失敗するため、timestamp型にcastする<br>※または日時型にトリミングする

|BigQuery|Athena|
|:-|:-|
|DATE(log_time)|DATE(cast(log_time as timestamp))<br>※DATE(SUBSTR(log_time, 1, 13))でも可|


## 10. prestoの場合、整数同士の割り算は整数が返却されるため、DOUBLE型にcastしてから割る<br>

|BigQuery|Athena|
|:-|:-|
|select (10 / 5)|select (cast(10 as DOUBLE) / 5)|


## 11. LIKE 演算子を最適化

|BigQuery|Athena|
|:-|:-|
|referer LIKE '%mmid%' OR referer LIKE '%bdid%' OR referer LIKE '%follow_mail%' OR referer LIKE '%target%')|regexp_like(referer, 'mmid &#124;bdid&#124;follow_mail&#124;target')|


## 12. int64はBIGINTへ変更

|BigQuery|Athena|
|:-|:-|
|int64|BIGINT|