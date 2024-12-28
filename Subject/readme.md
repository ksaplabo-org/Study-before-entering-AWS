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

S3バケットのバケットポリシーにS3BucketPolicy（コメントアウトされている部分）を追加。  
⇒エラーの内容は変わらず。  

CloudFormation用のロールを作成し、それを使用  
⇒エラーの内容は変わらず。  

CodeStar（現在廃止）で自動作成されるパイプラインのロールをそのまま使用  


