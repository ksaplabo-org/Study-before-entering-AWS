# 現場入場前勉強  
AWSの色々なサービスの基本的な学習を行い、そのアウトプットを行う。  

## 目次

- [API Gateway](APIGateway/readme.md)
- [CloudFormation](CloudFormation/readme.md)
- [CloudFront&S3](CloudFront&S3/readme.md)
- [ECS Fargate](ECS,Fargate/readme.md)
- [Glue](Glue/readme.md)
- [Kinesis](Kinesis/readme.md)
- [Route53](Route53/readme.md)
- [SQS](SQS/readme.md)
- [VPC](VPC/readme.md)

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



