# 目次
- [パイプライン作成時のIAM権限](#パイプライン作成時のiam権限)
  - [状況](#状況)
  - [試したこと](#試したこと)
  - [解決](#解決)
- [APIGW&Lambda統合時のエラー]()



# パイプライン作成時のIAM権限

～背景～  
CodePipelineを使用したパイプラインを１から作成している  
ソース、ビルドまではパイプラインが起動することができたが、デプロイでエラーが起きる。  
その原因究明と解決を行う。  

お試し中のパイプライン⇒[ch5_Pipeline.yml](ch5_Pipeline.yml)  


### 状況

デプロイフェーズのエラー内容  
```
arn:aws:sts::xxxxxxx:assumed-role/TanakaBuildProjectRole/xxxxxxx is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::tanaka-s3bucket" because no session policy allows the s3:ListBucket action (Service: Amazon S3; Status Code: 403; Error Code: AccessDenied; 
```
※TanakaBuildProjectRole⇒パイプライン全体で使用しているRole  
エラーの内容は、TanakaBuildProjectRoleにS3バケット（tanaka-s3bucket）に対するs3:ListBucket権限がない。  
という内容になっている。


### 試したこと

①  
S3バケットのバケットポリシーにS3BucketPolicy（コメントアウトされている部分）を追加。  
⇒エラーの内容は変わらず。  

②  
CloudFormation用のロールを作成し、それを使用  
⇒エラーの内容は変わらず。  

③  
CodeStar（現在廃止）で自動作成されるパイプラインのロールをそのまま使用  
⇒エラーの内容は変わらず。  

④  
CodeBuildで使用しているIAM Roleにフル権限＆バケットポリシーを全許可  
⇒エラーの内容は変わらず。  

### 解決  

権限の問題ではなく、アーティファクトの設定ミス。  
buildspec.ymlで出力アーティファクトを定義していないため、CodeBuild終了時のアーティファクトが  
自動で作成された名前で出力されていた。  
その為、次のCodeDeployでアーティファクトが取得できないことが原因だった。 

```yml
artifacts:
  files:
    - template-export.yml
```
バケットポリシーなどはなくても実行できた。


# APIGW&Lambda統合時のエラー

～背景～  
ApiGatewayとLambdaをデプロイするのだが、APIGWの統合リクエストにLambdaを設定する際    
デプロイが行えるが、APIGWからのリクエストが必ずエラーになる。  
対処方法としては、APIGWでタイムアウト値を適当な値に変更し保存することで解消される。（何かしらAPIGWの更新が必要）    
その原因究明と解決を行う。  

お試し中のリソース⇒[ch_Api.yml](./ch_Api.yml)  

