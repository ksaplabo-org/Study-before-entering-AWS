# 目次

- [BashScript](#bashscript)
- [S3バケットの一覧を取得するスクリプト](#s3バケットの一覧を取得するスクリプト)
- [S3バケット名からテストを行う]
- [名前に規則性がある複数リソースのデプロイ](#名前に規則性がある複数リソースのデプロイ)
- [Stackのステータスを取得するスクリプト](#stackのステータスを取得するスクリプト)

## BashScript

AWS CLIを使ってAWS操作を行うことができるが、それをスクリプト化することでAWS操作を簡略化できる。  
スクリプトはどのコンソールを使っても同じだが、ここではUbuntuでのBashScriptを紹介する。  

## S3バケットの一覧を取得するスクリプト

```sh
#!/bin/bash

# AWS CLI を使って S3 バケット一覧を取得
aws s3api list-buckets
```
上記をscript1.shに保存して以下を実行
```sh
# スクリプトに実行権限を付与
chmod +x script1.sh

# スクリプト実行
bash script1.sh
```

これを実行すると以下の結果を得る  
```json
{
    "Buckets": [
        {
            "Name": "backet1",
            "CreationDate": "2024-11-09T02:14:49.000Z"
        },
        {
            "Name": "backet2",
            "CreationDate": "2024-11-12T05:32:30.000Z"
        },
        ...
    ]
}
```

例えば、S3バケット名の一覧をテスト仕様書に添付したいときは  
上記の結果だと、そのままコピーすることはできない。  

そこで以下のように記載する。  
```sh
#!/bin/bash

# AWS CLI を使って S3 バケット一覧を取得し、バケット名のみ表示
aws s3api list-buckets --query "Buckets[].Name" --output text
```

こうすることにより、S3バケット名だけを取得することができる。  
上記はシェルスクリプトというより、AWS CLIの紹介になった。。。  




## S3バケット名からテストを行うスクリプト

バケット名取得後、任意のバケット名があることを確認するためには以下のようなスクリプトを使用する。  
```sh
#!/bin/bash

# 確認したいバケット名
TARGET_BUCKET="test-backet"

# S3バケット名の一覧を取得
BUCKET_LIST=$(aws s3api list-buckets --query "Buckets[].Name" --output text)

# バケット名が一覧に含まれているか確認
if echo "$BUCKET_LIST" | grep -q "^${TARGET_BUCKET}$"; then
  echo "Bucket '$TARGET_BUCKET' exists."
  exit 0
else
  echo "Bucket '$TARGET_BUCKET' does not exist."
  exit 1
fi

```
テストを行う際はこのようにスクリプトを使用すると便利である。  


## 名前に規則性がある複数リソースのデプロイ

例えば、script-lambda-001,script-lambda-002,,,のように、Lambdaを100個デプロイする際にスクリプトは役に立つ  

```sh
#!/bin/bash

# デプロイするLambdaの基本名
BASE_NAME="script-lambda"

# デプロイしたい個数
TOTAL=100

# デプロイ用のZIPファイル名 (Lambdaのソースコード)
LAMBDA_ZIP="lambda-source.zip"

# S3バケット名 (Lambdaコードのアップロード先)
S3_BUCKET="your-s3-bucket-name"

# リージョン
AWS_REGION="us-east-1"

# LambdaのIAMロール
LAMBDA_ROLE_ARN="arn:aws:iam::123456789012:role/your-lambda-role"

# 1から100までの連番でループ
for i in $(seq -w 1 $TOTAL); do
  LAMBDA_NAME="${BASE_NAME}-${i}"
  echo "Deploying $LAMBDA_NAME..."

  # Lambdaをデプロイ
  aws lambda create-function \
    --function-name "$LAMBDA_NAME" \
    --runtime nodejs18.x \
    --role "$LAMBDA_ROLE_ARN" \
    --handler index.handler \
    --code S3Bucket="$S3_BUCKET",S3Key="$LAMBDA_ZIP" \
    --region "$AWS_REGION"

  echo "$LAMBDA_NAME deployed."
done

echo "All $TOTAL Lambda functions have been deployed."

```
このようのfor文を使うことで、簡単にデプロイすることができる。  
実際の現場では、命名規則にがあり、リソース名に規則性があることが多いため、よく使うことが多い。  


## Stackのステータスを取得するスクリプト

```sh
#!/bin/bash

# 使用するAWSプロファイル名を指定
AWS_PROFILE="default"  # 必要に応じて変更してください

# CloudFormationのスタックを取得し、COMPLETE以外を表示
aws cloudformation list-stacks \
  --profile "$AWS_PROFILE" \
  --query "StackSummaries[?StackStatus!='DELETE_COMPLETE' && !contains(StackStatus, 'COMPLETE') && ParentId==null].[StackName, StackStatus]" \
  --output text

```

出力例
```sh
$ bash list_incomplete_stacks.sh

test-stack-api-gateway	ROLLBACK_IN_PROGRESS
test-stack-lambda	UPDATE_IN_PROGRESS

```

これでスタックが100個あってもすぐに分かるようになります。