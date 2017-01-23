# Role_$links一覧取得
### 概要
Roleに紐付いたODataリソースを一覧取得する
以下のODataリソースを指定することができる
* Account
* ExtCell
* ExtRole
* Relation

### 必要な権限
未稿
### 制限事項
* リクエストヘッダのAcceptは無視される
* リクエストヘッダのContent-Typeは全てapplication/jsonとして扱う
* リクエストボディはjson形式のみ受け付ける
* レスポンスヘッダのContent-Typeはapplication/jsonのみをサポートし、レスポンスボディはjson形式とする
* $formatクエリオプションは無視される

<br>
### リクエスト
#### リクエストURL
##### Association with the account
```
/{Cell_name}/__ctl/Role(Name='{role_name}',_Box.Name='{box_name}')/$links/_Account
または、
/{Cell_name}/__ctl/Role(Name='{role_name}')/$links/_Account
または、
/{Cell_name}/__ctl/Role('{role_name}')/$links/_Account
```
##### Association with the ExtCell
```
/{Cell_name}/__ctl/Role(Name='{role_name}',_Box.Name='{box_name}')/$links/_ExtCell
または、
/{Cell_name}/__ctl/Role(Name='{role_name}')/$links/_ExtCell
または、
/{Cell_name}/__ctl/Role('{role_name}')/$links/_ExtCell
```
##### Association with the ExtRole
```
/{Cell_name}/__ctl/Role(Name='{role_name}',_Box.Name='{box_name}')/$links/_ExtRole
または、
/{Cell_name}/__ctl/Role(Name='{role_name}')/$links/_ExtRole
または、
/{Cell_name}/__ctl/Role('{role_name}')/$links/_ExtRole
```
##### Association with the relation
```
/{Cell_name}/__ctl/Role(Name='{role_name}',_Box.Name='{box_name}')/$links/_Relation
または、
/{Cell_name}/__ctl/Role(Name='{role_name}')/$links/_Relation
または、
/{Cell_name}/__ctl/Role('{role_name}')/$links/_Relation
```
※ _Box.Nameパラメタを省略した場合は、nullが指定されたものとする
#### メソッド
GET
#### リクエストクエリ
以下のクエリパラメタが利用可能です。

|クエリ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|dc_cookie_peer<br>|クッキー認証値<br>|認証時にサーバから返却されたクッキー認証値<br>|×<br>|Authorizationヘッダの指定が無い場合のみ有効<br>クッキーの認証情報を利用する場合に指定する<br>|_

[$select クエリ](192_$select_Query.html)

[$expand クエリ](191_$expand_Query.html)

[$format クエリ](190_$Format_Query.html)

[$filter クエリ](189_$filter_Query.html)

[$inlinecount クエリ](193_$inlinecount_Query.html)

[$orderby クエリ](186_$orderby_Query.html)

[$top クエリ](187_$top_Query.html)

[$skip クエリ](188_$Skip_Queryhtml)

[全文検索(q)クエリ](194_Full_Text_Search_Query.html)

#### リクエストヘッダ
|ヘッダ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override<br>|メソッドオーバーライド機能<br>|任意<br>|×<br>|POSTメソッドでリクエスト時にこの値を指定すると、指定した値がメソッドとして使用されます。<br>|
|X-Override<br>|ヘッダオーバライド機能<br>|${上書きするヘッダ名}:${値} &#160;<br>|×<br>|通常のHTTPヘッダの値を上書きします。複数のヘッダを上書きする場合はX-Overrideヘッダを複数指定します。<br>|
|X-Dc-RequestKey<br>|イベントログに出力するRequestKeyフィールドの値<br>|半角英数、-(半角ハイフン)と_(半角アンダーバー)<br>最大128文字<br>|×<br>|指定がない場合、PCS-${UNIX時間}を設定する<br>V1.1.7以降で対応<br>|
|Authorization<br>|OAuth2.0形式で、認証情報を指定する<br>|Bearer {TokenValue}<br>|×<br>|※認証トークンは認証トークン取得APIで取得したトークン<br>|
|Accept<br>|レスポンスボディの形式を指定する<br>|application / json<br>|×<br>|省略時は[application/json]として扱う<br>|
#### リクエストボディ
なし
#### リクエストサンプル
なし

<br>
### レスポンス
#### ステータスコード
200
#### レスポンスヘッダ
|ヘッダ名<br>|概要<br>|備考<br>|
|:--|:--|:--|
|X-Dc-Version<br>|APIの実行バージョン<br>|リクエストが処理されたAPIバージョン<br>|
|Access-Control-Allow-Origin<br>|クロスドメイン通信許可ヘッダ<br>|返却値は"*"固定<br>|
|Content-Type<br>|返却されるデータの形式<br>|&#160;<br>|
|DataServiceVersion<br>|ODataのバージョン<br>|&#160;<br>|
#### レスポンスボディ
|オブジェクト<br>|項目名<br>|Data Type<br>|備考<br>|
|:--|:--|:--|:--|
|ルート<br>|d<br>|object<br>|オブジェクト{1} &#160;<br>|
|{1}<br>|results<br>|array<br>|オブジェクト{2}の配列<br>|
|{2}<br>|uri<br>|string<br>|紐付いているODataリソースへのURL<br>|
#### エラーメッセージ一覧
[エラーメッセージ一覧](198_Error_Messages.html)を参照

#### レスポンスサンプル
```json
{
  "d": {
    "results": [
      {
        "uri": "https://fqdn/cell_name/__ctl/Role(Name='role_name',_Box.Name=null)"
      },
      {
        "uri": "https://fqdn/cell_name/__ctl/Role(Name='role_name',_Box.Name='box1')"
      }
    ]
  }
}
```

<br>
### CURLサンプル
#### CURLコマンド(UNIX)
```sh
curl "https://fqdn/Cell_name/__ctl/Role(Name='role_name',_Box.Name=null)/$links/_Box" -X GET -H 'Authorization:Bearer auth_token' -H 'Accept: application/json'
```
<br>
<br>
<br>
###### Copyright 2017    FUJITSU LIMITED