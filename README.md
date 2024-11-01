# ロールポリシーのデプロイ (AWS SAM利用)

このプロジェクトは、Lambda関数の実行を行うためのIAMロールとマネージドポリシーを設定し、AWS SAM (Serverless Application Model) を使用してデプロイを管理します。

## プロジェクト構成

- **template.yaml**: IAMリソースを定義するファイル。
  - **ChatbotRole**: `nfl-chatbot` という名前のIAMロール。AWS Chatbotサービスに対してこのロールを引き受け、Lambda関数を実行する権限を付与します。
  - **GuardrailPolicy**: `nfl-guardrail` という名前のマネージドポリシー。名前が `nfl-` で始まるLambda関数に対して、特定の実行アクションを許可します。

- **samconfig.toml**: SAMデプロイメント用のパラメータを定義するファイル。
  - **stack_name**: デプロイするスタック名 (role-policy)
  - **region**: AWSリージョン (ap-northeast-1)
  - **s3_bucket**: SAMアーティファクトを保存するS3バケット (samdeploy-bucket)
  - **capabilities**: デプロイ時の能力 (CAPABILITY_NAMED_IAM)。名前付きIAMリソースを作成するために必要です。

## 事前準備

- **AWS CLI** および **AWS SAM CLI** がインストールされていること。
- **S3バケット**がSAMデプロイメントアーティファクト用に設定されていること。

## デプロイ手順

sam deploy --template-file template.yaml --config-file samconfig.toml --capabilities CAPABILITY_NAMED_IAM
