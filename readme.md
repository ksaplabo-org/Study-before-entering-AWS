# 現場入場前勉強  

AWSの以下のサービスについて勉強していく。  
- Cloud Formation  
- IAM  
- Lamnda  
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
IAM Policy IAM Role  