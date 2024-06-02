# Glueの基礎  

参考サイトは[こちら](https://www.slideshare.net/slideshow/20190806-aws-black-belt-online-seminar-aws-glue/161761881)（BlackBelt）  

## Glueとは

様々なデータソースのメタデータを管理する  
フルマネージドでサーバレスなETLサービス  

メタデータ：データに付随しているデータ（作成日付や作成者など）  
フルマネージド：インフラストラクチャ管理などを勝手にやってくれること  
ETL：Extract（抽出）、Transform（変換）、Load（書き出し）の頭文字。様々な形式のデータを統一して保存する処理のこと  

## やってみた  

[こちら](https://zenn.dev/hisamitsu/articles/6c233d6d0f0817)のサイトを参考にGlueを使ってみた。  

- 以下のcsvデータ([guletest.csv](./gluetest.csv))を適当なS3バケットに置く    
```json
id,before_family_name,before_given_name
1,やまもと,いちろう
2,ささき,じろう
3,こいけ,さぶろう
4,さとう,しろう
5,たなか,ごろう
6,なかむら,ろくろう
7,かとう,しちろう
8,やまだ,はちろう
9,みうら,きゅうろう
10,ふじい,じゅうろう
11,さいとう,じゅういちろう
```

<img src="./img/1.png" width="50%">

- Glueマネジメントコンソール>Data Catalog>Crawlersからクローラーを新規に作成していく  

- Add Data sourceでS3を選択し、先ほどのcsvのS3パスを入力する。  

- 画面に従いRole,outputのdatabaseも作成

- クローラーの作成が完了  

<img src="./img/1.png" width="50%">