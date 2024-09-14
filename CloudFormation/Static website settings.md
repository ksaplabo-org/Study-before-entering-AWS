# Amazon S3 での静的ウェブサイトの設定  

参考：https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html  

CloudFormationで行う前に、コンソールからのデプロイを試す。  

1. バケットの作成  
   - バケット名：myawsbacket-tanaka  
   - リージョン：ap-northeast-1  

   ※チュートリアルではその他の設定がデフォルトのままであるが、一応他の設定も確認  
   - オブジェクトの所有者：ACL無効(推奨)  
   このバケット内の権限的なもの。無効にすれば所有者は自分だけになり、他のアカウントではアクセス等できなくなる。有効にすることは推奨されていなく、Policyから権限付与するのが今の推奨みたい。  
   [ドキュメント情報](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/userguide/acl-overview.html)  

   - このバケットのアクセス設定：パブリックアクセスをすべてブロック  
     S3へのアクセス制御は3つある  
     ACL  
     バケットポリシー  
     IAMポリシー  
     参考：https://qiita.com/ryo0301/items/791c0a666feeea0a704c  

    - バケットのバージョニング：無効  
      オブジェクトの複数のバリアントを同じバケット内に保持する機能  
      (バリアント：同じオブジェクトの異なるバージョンのこと)  

    - デフォルトの暗号化:S3 マネージドキーを使用したサーバー側の暗号化（SSE-S3）  
    オブジェクトに対する暗号化の設定  
    参考：https://dev.classmethod.jp/articles/lim-s3-sse-2021/  

    - バケットキー  
      デフォルトの暗号化でSSE-KMSを使っているときに、コストを安くできる機能  
      参考：https://qiita.com/Regryp/items/5c45207223182691498f

2. 静的ウェブサイトホスティングを有効にする  
   作成したバケットを開き、プロパティ＞静的ウェブサイトホスティング＞編集から、静的ウェブサイトホスティングを有効にする。  

   - ホスティングタイプ：静的ウェブサイトをホスト  
   - インデックスのドキュメント:index.html  
   - エラードキュメント：error.html  

   変更の保存を押す。  

とりあえず、あとはチュートリアル通り行えば、index.htmlを公開できる。  

## 気になる  
チュートリアルでは全世界に向けてバケットを公開していたが  
普通そんなことはしない。  
特定のIPアドレスからしかアクセスできないようにするためにはどのようなサービスを使って設定すればいいのか。  

許可したいIP：https://www.cman.jp/network/support/go_access.cgi

**方法1：ポリシーで許可する**  
以下のバケットポリシーを追加すると可能  
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "IPAllow",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::[バケット名]/*",
            "Condition": {
                "IpAddress": {
                    "aws:SourceIp": "許可したいIPアドレス"
                }
            }
        }
    ]
}
```