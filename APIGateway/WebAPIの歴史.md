WebAPIの歴史は以下のように進展してきました¹²:

1. **RPC (Remote Procedure Call)**: 異なるシステム間で機能の呼び出しを行えるようにする手順を定めた規格が作られました。これにはCORBA, DCOM, RMI, WMIなどが含まれます。

2. **SOAP**: プロトコルの複雑性とオーバーヘッドが大きく、双方の負荷が高くあまり普及されませんでした。SOAPは規格が決まっており、RESTは設計思想という大きな違いが存在します。

3. **REST**: HTTP上でリソースに対応するURIへの操作としての追加・編集・削除をHTTPメソッドのGET・POST・DELETE等を結びつけてやり取りします。とてもシンプルであり、拡張性も高いことから最も多く使われています。

4. **GraphQL**: RESTだとリソースの数だけHTTPアクセスしなければならないという問題がありました。これを解決するために、GraphQLが誕生しました。

5. **gRPC**: HTTPでやっていることが無駄だという考えから、独自のプロトコルに戻る動きがありました。これがgRPCの誕生につながりました。

これらの進展は、WebAPIが情報サービスの提供と利用の両面から進化してきた結果です²。それぞれのステップは、特定の問題を解決するための新しいアプローチを提供してきました。

ソース: Bing との会話 2024/1/27
(1) API・WebAPIって何？歴史からSOAP, REST, GraphQL, gRPC .... https://qiita.com/tsudaryo1715/items/3ebb0c5233e480ee5407.
(2) Web API の過去・現在・未来 - 国立情報学研究所 / National .... https://tsukuba.repo.nii.ac.jp/record/30888/files/ISTA_64-5.pdf.
(3) いまさら聞けない「WebAPIとは？」 －基礎・利用方法・API連携 .... https://www.ashisuto.co.jp/eai_blog/article/201712_eai_webapi.html.
(4) undefined. http://e-words.jp/w/REST.html.