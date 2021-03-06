# AWS IAM

## IAM(Identity and Access Management)とは

AWSのサービスを利用するための権限を管理するためのサービス

- セキュリティの観点から、通常はルートアカウントではなくIAMを利用する
- グローバルサービスのため、複数リージョンで共通利用可能
- IAMでは、IAMユーザーやIAMグループを作成することができ、IMユーザー(グループ)ごとに権限（IAMポリシー）やAPIキーを設定できる
  - APIキーの利用は非推奨
  - セキュリティ観点から必要最小限の権限のみ与えること
- APIキーは各IAMユーザー(グループ)ごとに2つ発行できる
  - キーの入れ替えの際に入れ替えが終わるまでの間、権限がなくなってしまうのを防止するため

### IAMロール

- APIキーの代わりにIAMロールの利用が推奨されている
- ユーザー、アプリケーション、サービスに対しIAMロールを付与することで権限を与える
- IAMロールとAWSリソース（例：EC2、Lambda）を直接紐づけるため、キー管理が不要

参考: https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/id_roles.html

