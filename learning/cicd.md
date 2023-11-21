# CI/CD構築ハンズオン  

リポジトリへのソースコードのコミットをトリガーに、ビルド、デプロイが自動実行され  
コンテナにソースの修正内容が反映されていることを確認する  

1. ソースコードをpush  
2. Codepipelineが変更を検知し、CI/CDパイプラインをスタート  
3. CodeBuildがDockerイメージをビルドし、ECRにpush  
4. CodeDeployがECRのDockerイメージをECSクラスターにデプロイ  

全体図
![](./cicdimg/1.png)  

1. CodeCommitリポジトリ作成  
2. S3にソース用意  
3. CodeBuild、CodeDeploy用のIAMロール作成  
4. Blue/Greenデプロイ用サービス作成  


### CodeCommitリポジトリ作成  

ポータル画面からCodeCommimtへ移動  
- 設定項目は名前だけ ctn-cicd-hdon-coderep  

### git環境の構築  

Cloud9上で行っていく  
AWSの認証ヘルパー機能を使うことで、gitへのアクセス時に認証を毎回行わないで済む  

- 認証ヘルパーを利用できるようにする  
  Cloud9のcliで以下のコマンドを実行する  
  git config --global credential.helper '!aws codecommit credential-helper $@'  
  git config --global credential.UseHttpPath true  

  個人名設定  
  git config --global user.name "xxx" # ご自身のお名前を設定ください  
  git config --global user.email "xxx" # ご自身のEメールアドレスを設定ください  

  リポジトリのクローン  
  git clone xxx # CodeCommit 画面からコピーしてください  


### ビルド定義・デプロイ定義・タスク定義の作成  

- ビルド定義ファイル  
```yaml
version: 0.2
phases:
  #ECRリポジトリへのログインを行う
  pre_build:
    commands:
      - $(aws ecr get-login --region $AWS_DEFAULT_REGION --no-include-email)
      - REPOSITORY_URI=各自ご自身のURIに置き換えてください！
      - IMAGE_TAG=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)
  #biuldを実施する箇所
  build:
    commands:
      - docker build -t $REPOSITORY_URI:latest .
      - docker tag $REPOSITORY_URI:latest $REPOSITORY_URI:$IMAGE_TAG
  #イメージをECRにPUSH
  post_build:
    commands:
      - docker push $REPOSITORY_URI:latest
      - docker push $REPOSITORY_URI:$IMAGE_TAG
      - printf '{"Version":"1.0","ImageURI":"%s"}' $REPOSITORY_URI:$IMAGE_TAG > imageDetail.json
#imageDetail.jsonの出力を行う
artifacts:
    files: imageDetail.json
```


