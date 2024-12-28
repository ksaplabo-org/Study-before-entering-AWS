# AWS SAM

### 目次

### AWS SAMとは

```
Infrastructure as Code (IaC) を使用した、サーバーレスアプリケーション構築のためのオープンソースのフレームワークです
```
サーバレスアプリケーションの開発とデプロイを支援するためのフレームワーク  
Lambdaと一緒に、API GatewayやDynamoDBなどを短いテンプレートで作成できるようにしたもの  

※フレームワークなので、SAMテンプレートとはあるが、デプロイ方法がCFnと異なる。  


### AWS SAM CLIのインストール

今回実施する環境は以下の通り
Windows、VSCode、Powershell

インストール手順：[こちら](https://docs.aws.amazon.com/ja_jp/serverless-application-model/latest/developerguide/install-sam-cli.html)  

インストール手順のサイトから、msiをダウンロードし、インストーラーを実行  
インストール完了後、PCを再起動してPowershellでsam --versionを実行しインストールされていることを確認する
```shell
$ sam --version
SAM CLI, version 1.131.0
```

### Hello Worldアプリケーションをデプロイする

参考：https://docs.aws.amazon.com/ja_jp/serverless-application-model/latest/developerguide/serverless-getting-started-hello-world.html  

このチュートリアルでは以下のことを行う  
- サンプルの Hello World アプリケーションを初期化、構築、デプロイします。
- ローカル変更を行い、 に同期します AWS CloudFormation。
- 開発ホストでローカルテストを実行します。
- AWS クラウドからサンプルアプリケーションを削除します。

-------------------------------------------------------------  
- サンプルの Hello World アプリケーションを初期化する  
    (実行例)  
    ```shell
    $ sam init
    You can preselect a particular runtime or package type when using the `sam init` experience.
    Call `sam init --help` to learn more.

    Which template source would you like to use?
            1 - AWS Quick Start Templates
            2 - Custom Template Location
    Choice: 1

    Choose an AWS Quick Start application template
            1 - Hello World Example
            2 - Data processing
            3 - Hello World Example with Powertools for AWS Lambda
            4 - Multi-step workflow
            5 - Scheduled task
            6 - Standalone function
            7 - Serverless API
            8 - Infrastructure event management
            9 - Lambda Response Streaming
            10 - Serverless Connector Hello World Example
            11 - Multi-step workflow with Connectors
            12 - GraphQLApi Hello World Example
            13 - Full Stack
            14 - Lambda EFS example
            15 - DynamoDB Example
            16 - Machine Learning
    Template: 1

    Use the most popular runtime and package type? (python3.13 and zip) [y/N]: y

    Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: y
    X-Ray will incur an additional cost. View https://aws.amazon.com/xray/pricing/ for more details

    Would you like to enable monitoring using CloudWatch Application Insights?
    For more info, please view https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-application-insights.html [y/N]: y
    AppInsights monitoring may incur additional cost. View https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/appinsights-what-is.html#appinsights-pricing 
    for more details

    Would you like to set Structured Logging in JSON format on your Lambda functions?  [y/N]: y
    Structured Logging in JSON format might incur an additional cost. View https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html#monitoring-cloudwatchlogs-pricing for more details

    Project name [sam-app]:

    Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)

        -----------------------
        Generating application:
        -----------------------
        Name: sam-app
        Runtime: python3.13
        Architectures: x86_64
        Dependency Manager: pip
        Application Template: hello-world
        Output Directory: .
        Configuration file: sam-app\samconfig.toml

        Next steps can be found in the README file at sam-app\README.md


    Commands you can use next
    =========================
    [*] Create pipeline: cd sam-app && sam pipeline init --bootstrap
    [*] Validate SAM template: cd sam-app && sam validate
    [*] Test Function in the Cloud: cd sam-app && sam sync --stack-name {stack-name} --watch
    ```
    AWS クイックスタートテンプレート1を選択  
    Hello World Exampleテンプレート1を選択  
    その他（ログ回り）はすべてYesで進めると、[sam-app](./sam-app)というフォルダがクローンされる 

    ***重要なファイル***  
    [hello_world/app.py](./sam-app/hello_world/app.py) Lambdaのコード  
    [hello_world/requirements.txt](./sam-app/hello_world/requirements.txt) Pythonに必要なモジュール  
    [samconfig.toml](./sam-app/samconfig.toml) AWS SAM CLIが使用するパラメーターを保存するアプリケーションの設定ファイル  
    [template.yaml](./sam-app/template.yaml) IaCのコード  


- サンプルの Hello World アプリケーションを構築する
    (実行例)  
    ```shell
    $ cd sam-app
    $ sam build