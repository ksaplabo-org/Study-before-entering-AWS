# 現場入場前勉強  

AWSの以下のサービスについて勉強していく。  
- Cloud Formation  
- IAM  
- Lambda  
- Fargate  
- Code Commit  
- API Gateway  
- Route53  

### Cloud Formation  

Infrastructure as code  
AWSのシステム構成をJSONやYAMLなどのコードで記述し、テンプレート化し  
構成管理、修正、再利用を簡単にするためのサービス  

主な用語  
- テンプレート  
  リソースの構築内容を定義するファイル  
  json,yamlの形式で記述可能  
  おすすめはyaml(jsonだとコンマや波かっこのつけ忘れがあるとすぐにエラーになって修正が面倒)  
- スタック  
  テンプレートを利用してCloudFormationによってプロビジョニングされるAWSリソースの集合体  

参考：https://qiita.com/tep731/items/0436a69f538cf051771f  

実際に色々触ってみた→[こちら](./Cloud%20Formation/readme.md)  


### IAM  

AWS Identity and Access Management  

主な用語  
- IAM Policy  
  - 管理ポリシー  
    AWSがデフォルトで用意しているポリシー  
    いろんな場面で使用可能  
    例）S3に対する全許可権限→AmazonS3FullAccess  
  - インラインポリシー  
    自分でJSONを記述するポリシー  
    ある特定のリソースに対する特定の権限のため、他で利用することはできない。  

- IAM Role  
  複数のポリシーを1つのロールに付与して、そのロールをリソースなどにアタッチする。といった、複数のポリシーをまとめたもの  

### Lambda  

サーバが不要でコードを実行できる  
思い付きで出来そうなことを試してみる  
[こちら](./Lambda/readme.md)  

### Fargate  

### サービス連携  
Route53→API Gateway Endpoint→API Gateway（Firewall）→Internet Gateway  
SQS→Lambda→Fargate→API Gateway  
CodeCommit→push→Cloudwatch Event→CodePipeline＆Codebiuld  
  Codepipeline→CloudFormation  
  Codebiuld→ECR  

### AWS VPC  
以下のサイトを参考にAWS VPCの学習を行う。  
参考：https://qiita.com/c60evaporator/items/2f24d4796202e8b06a77  
詳細は[こちら](./VPC/readme.md)  


### AWS SQS  

概要  
マイクロサービス、分散システム、およびサーバレスアプリケーション用の完全マネージド型メッセージキュー  

もう少し詳しく  
→blackbeltの記事 https://www.slideshare.net/AmazonWebServicesJapan/20190717-aws-black-belt-online-seminar-amazon-simple-queue-service  

SQSについての詳細は[こちら](./SQS/readme.md)  


### ECS,Fargate  

ECS：Elastic Container Sercice  
AWSのコンテナーベースサービス  
この辺りの用語が混乱を招きやすいためここで整理する  

```
Q ECSとは
A Elastic Container Service
  フルマネージドのコンテナオーケストレーションサービス
```

ECSやFargateの詳細は[こちら](./ECS,Fargate/readme.md)  

また、某学習サイトで学んだ内容を[こちら]()にアウトプットする  
(これにはCICDの内容も含まれる)


### Route53  

AWSのドメインサービスであることはわかるが  
詳しいところまで分からないと、プロジェクトではついていけない  
そのため用語等を整理する  



