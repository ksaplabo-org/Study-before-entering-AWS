※手順はないため苦戦中  
以下の環境を作成する  
![img](./img/2.png)  

各種機能やパラメータを確認して行っていく  
![img](./img/env.dio.svg)  

- VPCの作成  

  ポータル画面から作成を行う。  
  ここでは、VPC設定時の各種パラメータを紹介  
  
  - 作成するリソース  
    VPCのみとVPCなどがあり、VPCなどを選択すれば、VPCにくっつくsubnetなどが同時に作成可能であるが、ここでは勉強のため１つずつ作成していく  
  
  - 名前タグ  
    vpcの名前。名前の後ろに-vpcがつく  
    今回はecs-practiceと設定  

  - IPv4 CIDR ブロック  
    手動でIPアドレスを入れるのと、もう片方がよくわからない  
    IPアドレスは「10.0.0.0/24」とする。（ホスト部はサブネットの数に影響する。後述）  

  - IPv6 CIDR ブロック  
    無しを選択。機能はわかっていない  

  - テナンシー  
    デフォルトを選択。機能は不明  
  
  上記の設定でVPCを作成  


- Subnetの作成  

  前提条件  
  - VPCのIPアドレスは10.0.0.0/24  
  - Publish Privateで二つずつ作成。AZをまたぐ（図の通り）  
  - Publicの方にNAT Gatewayを立てる  
  
  ポータル画面から作成していく。  
  - VPCを選択  

  - サブネット名  
    ecs-public-01  
  - AZ  
    ap-northeast-1a  
  - IPv4 VPC CIDR block  
    デフォルトのまま。10.0.0.0/24  
  - IPv4 subnet CIDR block  
    このサブネットは10.0.0.0/28
  
  さらに新しいサブネットを追加。  
  - サブネット名  
    ecs-public-02  
  - AZ  
    ap-northeast-1c  
  - IPv4 VPC CIDR block  
    デフォルトのまま。10.0.0.0/24  
  - IPv4 subnet CIDR block  
    このサブネットは10.0.0.16/28

  privateの方も追加する  
  - サブネット名  
    ecs-private-01  
  - AZ  
    ap-northeast-1a  
  - IPv4 VPC CIDR block  
    デフォルトのまま。10.0.0.0/24  
  - IPv4 subnet CIDR block  
    このサブネットは10.0.0.32/28

  - サブネット名  
    ecs-private-02  
  - AZ  
    ap-northeast-1c  
  - IPv4 VPC CIDR block  
    デフォルトのまま。10.0.0.0/24  
  - IPv4 subnet CIDR block  
    このサブネットは10.0.0.64/28

__サブネットに振り分けるIPアドレスに苦戦した__  
__IPアドレスを２進数で考えると分かりやすかったため、メモを残しておく__    
```
IPを二進数で表すとわかりやすい
vpc(10.0.0.0/24)
00001010 00000000 00000000 / 00000000

subnet(10.0.0.0/28)
00001010 00000000 00000000 0000/0000
subnet(10.0.0.16/28)
00001010 00000000 00000000 0001/0000
subnet(10.0.0.32/28)
00001010 00000000 00000000 0010/0000
subnet(10.0.0.64/28)
00001010 00000000 00000000 0100/0000
```


- インターネットゲートウェイの作成  
  ポータル画面から作成  

  - 名前はecs-igw  
  
  作成時のパラメータはこれだけ  

  - VPCにアタッチ  
  アクションからVPCへのアタッチを行う  


- サブネットのルートテーブルを作成  

  ポータル画面からecs-public-01のサブネットを選択して、ルートテーブルの設定を行う  
  
  - ルートテーブルの名前を変更しておく  
    ecs-public-rt  
  
  - ルートの編集を行う  
    デフォルトで入っているものは、VPC内の通信は自由に行ってもいいよというもの  

    デフォルトゲートウェイをIGWに向けるルートを作りたい  
    - 送信先  
      0.0.0.0/0  
    - ターゲット  
      インターネットゲートウェイを指定して、作ったigwを指定する  

  これで、PublicSubnetは本当にPublicSubnetになった  


ここからPrivateSubnetのための設定を行っていく。  

- NAT Gatewayの作成  
  ポータル画面からNAT Gatewayの作成を行っていく  

  - 名前  
    ecs-practice-ngw-01  
  - サブネット  
    ecs-public-01を指定  
  - Elastic IP 割り当て  
    割り当てボタンを押して割り当てる  
    Elastic IPが何なのかは不明  

- PrivateSubnet用のルートテーブルを作成  
  - 名前  
    ecs-private-rt1  
  - VPC  
    ecs-practice-vpcを選択  
  
  作成後、サブネットのルートテーブルに以下の設定を行う  
  - 送信先  
    0.0.0.0/0  
  - ターゲット  
    ecs-practice-ngw-01（PublicSubnetにあるngw）  

  さらにその後、サブネットの関連付けを行う  
  - ecs-private-01を関連付けさせる  

  ※PrivateSubnet2用も同じ手順でやっておく  

※補足(参考：https://qiita.com/Lamaglama39/items/ddaedcd6946bd4375a32)  

サブネットとルートテーブルの明示的な関連付けの仕様  
- サブネットに明示的なルートテーブルの関連付けを設定していない場合、自動的にデフォルトのルートテーブルが設定される  
- サブネットに明示的に関連付けされるルートテーブルは１つのみ  


- セキュリティグループの作成  

  参考サイトから、以下の設定のセキュリティグループを作成する  
  - ALB用  
    - Ingress:80:ALL  
    - Egress:ALL:ALL  
  - ECS用  
    - Ingres:80:from ALB sg  
    - Egress:ALL:ALL  

  そもそもセキュリティグループとは  
  VPC上に構築したEC2などのリソースに対して適用できる仮想ファイアーウォール機能  
  セキュリティグループには以下の特徴がある  
  - ホワイトリスト  
    許可したもの以外すべてをブロック  
  - ステートフル  
    通信の行きと帰りをいっぺんに設定できる⇔ステートレスは通信の行きと帰りを別々に設定する  


  予想で次のセキュリティグループを作成する  
  - セキュリティグループ名  
    ecs-practice-alb-sg  
  - 説明  
    alb-sg
  - VPC  
    ecs-practice-vpc  
  - インバウンドルール  
    - タイプ  
      カスタムTCP  
    - ポート番号  
      80  
    - ソース  
      Anywhere-IPv4  
  - アウトバウンドルール  
    - タイプ  
      すべてのTCP  
    - 送信先  
      Anywhere-IPv4  
  
  - セキュリティグループ名  
    ecs-practice-ecs-sg  
  - 説明  
    alb-sg
  - VPC  
    ecs-practice-vpc  
  - インバウンドルール  
    - タイプ  
      カスタムTCP  
    - ポート番号  
      80  
    - ソース  
      カスタム  
      ecs-practice-alb-sg(セキュリティグループを指定できる)
  - アウトバウンドルール  
    - タイプ  
      すべてのTCP  
    - 送信先  
      Anywhere-IPv4

※メモ  
```
・インターネットゲートウェイ
　VPCの外と通信が可能になる
　VPCにIGWをアタッチする
　PublicSubnetは外から入れる、外にも出れる
　Privaeは外には出れるが、中には入れない　
・ルートテーブル
　サブネットごとに設定するもの
　Public
　→デフォルトゲートウェイをIGWに向ける
　　→直接設定した以外の他のすべての行き先のこと
　Private
　　→PrivateのでデフォルトゲートウェイはPublicのNATGatewayになる
　　　厳密には、PrivateSubnet→NAT Gateway→IGW
・NAT Gateway
　　Privateから来た時にPrivateIPをグローバルに変換して、外でも使えるようにする

デフォルトゲートウェイをIGWに設定してあるルートテーブルを持ったサブネットをPublicSubnetという
```