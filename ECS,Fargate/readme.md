# ECS,Fargate  

現場前研修にベストなサイトを見つけた  
https://qiita.com/K5K/items/2bab270b8fad24505303  

Nginxのサーバをコンテナで立てる  
![img](./img/1.png)  

手順は以下の通り  
- NWリソース作成  
- コンテナイメージの作成、ECRへPUSH  
- ALBの作成  
- クラスターの作成  
- タスク定義の作成  
- サービスの作成  

### NWリソース作成  
詳細は[こちら](./makenetwork.md)  

### コンテナイメージの作成、ECRへPush  

※参考手順ではローカル環境でLinuxが使えること、Dockerがあることが前提  



