# AWSセキュリティ

## AWS責任共有モデル

セキュリティにおいてAWS側が責任を負う部分とユーザー側が責任を負う部分を明確にしたモデル

- クラウド内のセキュリティはユーザーが担当する
  - AWSが用意するセキュリティサービスを適切に活用することでセキュリティを管理
- クラウド本体のセキュリティはAWSが担当する。

![AWS責任共有モデル](https://raw.githubusercontent.com/bamv-ikeda/knowledge/master/aws/_image/AWS%E3%81%AE%E8%B2%AC%E4%BB%BB%E5%85%B1%E6%9C%89%E3%83%A2%E3%83%87%E3%83%AB.jpg)

画像引用元: [【公式】AWS責任共有モデル](https://aws.amazon.com/jp/compliance/shared-responsibility-model/)

## AWSクラウドのセキュリティ

AWSセキュリティのメリットは以下の4点

1. データの保護
2. コンプライアンスの要件の準拠
3. コスト削減
4. 迅速なスケーリング

## AWSの責任範囲

### 物理的なセキュリティ

1. 環境レイヤー
   - 自然災害（洪水、異常気象、地震等）などの環境リスクを軽減するための設置場所
   - 各リージョンのデータセンター群は互いに独立・隔離されている
2. 物理的な境界防御レイヤー
   - 保安要員、防御壁、侵入検知などによる物理的な防御
3. インフラストラクチャレイヤー
   - インフラとして建物や各種機器、それらの運用に関わるシステム
   - ユーザーのデータの保護のための発電設備や消火施設
4. データレイヤー
   - アクセス制限や特権の分離

### ハイパーバイザーのセキュリティ管理

仮想化を実現するハイパーバイザはAWSがセキュリティを担当

ハイパーバイザとは

> コンピュータ用語における、ハイパーバイザ (hypervisor) とは、コンピュータの仮想化技術のひとつである仮想機械（バーチャルマシン）を実現するための、制御プログラムである。

引用元: [ハイパーバイザ - Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%BC%E3%83%90%E3%82%A4%E3%82%B6#:~:text=%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF%E7%94%A8%E8%AA%9E%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%80%81%E3%83%8F%E3%82%A4%E3%83%91%E3%83%BC%E3%83%90%E3%82%A4%E3%82%B6,%E3%81%AE%E3%80%81%E5%88%B6%E5%BE%A1%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%A0%E3%81%A7%E3%81%82%E3%82%8B%E3%80%82)

### 管理プレーン

管理プレーンの保護はユーザーがセキュリティを担当

※管理プレーンとは、クラウドを管理する面（プレーン）、つまり管理コンソールなどの総称

1. IDとパスワードの管理
   - 情報流出によるクラウド利用＆請求はユーザーの過失
   - 権限の強いアカウントにはMFA（Multi-Factor Authentication、多要素認証）を利用してアカウントの保護が可能
2. ルートアカウント
   - すべての操作が可能な、最も強い権限のアカウント
   - 通常作業は別アカウントに適切な権限を割り当てて利用すること
3. キーペアの管理
   - EC2などのインスタンスのログインEC2公開鍵暗号方式によるキーペアを利用する
   - キーペアは共有するのではなく、利用者ごとに公開鍵を設定するべき
4. APIキー
   - Webブラウザではユーザー名／パスワード を利用するが、コマンド・プログラムではAPIキー（アクセスキー／シークレットアクセスキー） を利用する。
   - APIキーはユーザー単位で発行可能
   - ルートアカウントへの発行はリスクが高いため推奨しない。
   ソースコードへのAPIキー埋め込みは推奨しない。環境変数や認証ファイルでの設定が適切。
   - 現在はAPIキーの利用そのものが推奨されていない。IAMの利用が推奨される。

### APIキーの管理

ユースケース | 利用方法 | 認証方法
- | - | -
Webブラウザ | AWSマネジメントコンソール | ユーザー名/パスワード
コマンド | AWS CLI | アクセスキー/シークレットアクセスキー
プログラム | AWS SDK | アクセスキー/シークレットアクセスキー

- APIはユーザー名/パスワードと同等の権限を持つため、ルートアカウントのAPIキーは発行しないこと
- APIキーはユーザーが適切に管理し、必要な権限のみを付与すること

## マネージドでないサービス

Amazon EC2やAmazon VPCなどのマネージドでないサービスではユーザーがセキュリティを担当

※IaaS(Infrastructure as a Service)のAWSサービスはユーザーがroot、Administrator権限を持つため

- EC2などのコンピューティングサービスのOS層以上はユーザーの責任
- ファイアウォール（セキュリティグループ）の設定内容はユーザーの責任

## マネージドなサービス

Amazon RDSやAmazon DynamoDBなどのマネージドサービスではAWSとユーザーでセキュリティを分担

- リソースへのアクセスコントロールと、アカウント認証情報の保護のみがユーザーがセキュリティを担当
- ユーザーから見えないサービスのプラットフォーム部分(OSやDBのパッチ適用、ファイアウォールの設定)はAWSがセキュリティを担当

## セキュリティのベストプラクティス

1. 転送中のデータの保護
   - 適切なプロトコルや暗号化アルゴリズムを選択する(例：FTPではなくSCPを使用する)
   - 脆弱性のアル暗号化アルゴリズムを選択しない
2. 蓄積データの保護
   - 蓄積データをサービス外に出力する場合はアクセスコントロールに配慮する(例：DBへの登録時にアプリケーション上でデータの暗号化やマスク処理を行う)
3. AWS資格情報の保護
   - ルートアカウントは使用しない
   - ユーザーごとにIAMユーザーを作成する
   - 必要最小限の権限のみを付与する
4. アプリケーションの安全性の確保
   - SQLインジェクション、OSコマンドインジェクション、クロスサイトスクリプティングなどの既知の攻撃に対する対策を行う
   - IPA(独立行政法人 情報処理推進機構)などから出ている脆弱性関連情報をチェックする
   - Amazon Inspectorなどを活用し、定期的な脆弱性診断を行う

