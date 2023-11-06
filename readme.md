# 現場入場前勉強  

AWSの以下のサービスについて勉強していく。  
- Cloud Formation  
- IAM  
- Lambda  
- Fargate  
- Code Commit  

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