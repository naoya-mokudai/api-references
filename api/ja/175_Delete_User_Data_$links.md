# ユーザデータ_$links削除
### 概要
ユーザデータとの$link情報を削除する
### 必要な権限
なし
### 制限事項
* リクエストヘッダのContent-Typeは全てapplication/jsonとして扱う
* リクエストボディはjson形式のみ受け付ける
* レスポンスヘッダのContent-Typeはapplication/jsonのみをサポートし、レスポンスボディはjson形式とする
* $formatクエリオプションにatom または xmlを指定した場合、エラーとはならないが、レスポンスボディのデータの保証はない
* ユーザデータ制限事項
	- Edm.DateTime型のプロパティの有効範囲のチェックが適切に行われない
	- Edm.DateTime型の配列は未サポート
	- Edm.DateTime型のプロパティにSYSUTCDATETIME()を指定した場合、設定されるシステム時間が異なる場合がある
      - リクエストボディでの設定時とDefaultValueでの設定時（\__published、\__updatedは後者のタイミング）
	- 1つのEntityTypeに対して作成出来るのは、DynamicProperty・DeclaredProperty・ComplexTypeProperty合わせて400個まで

<br>
### リクエスト
#### リクエストURL
```
ユーザデータとの$links
/{Cell_name}/{Box_name}/{Collection_name}/{EntityType_name}('{usedata_id}')/$links/_{EntityType_name}('{usedata_id}')
```
#### メソッド
DELETE
#### リクエストクエリ
##### 共通リクエストクエリ
|ヘッダ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|dc_cookie_peer<br>|クッキー認証値<br>|認証時にサーバから返却されたクッキー認証値<br>|×<br>|Authorizationヘッダの指定が無い場合のみ有効クッキーの認証情報を利用する場合に指定する<br>|
##### OData 共通リクエストクエリ
なし
#### リクエストヘッダ
##### 共通リクエストヘッダ
|ヘッダ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override<br>|メソッドオーバーライド機能<br>|任意<br>|×<br>|POSTメソッドでリクエスト時にこの値を指定すると、指定した値がメソッドとして使用される<br>|
|X-Override<br>|ヘッダオーバライド機能<br>|${上書きするヘッダ名}:${値}<br>|×<br>|通常のHTTPヘッダの値を上書きします。複数のヘッダを上書きする場合はX-Overrideヘッダを複数指定する<br>|
|X-Dc-RequestKey<br>|イベントログに出力するRequestKeyフィールドの値<br>|半角英数、-(半角ハイフン)と_(半角アンダーバー)<br>最大128文字<br>|×<br>|指定がない場合、PCS-${UNIX時間}を設定する<br>V1.1.7以降で対応<br>|
##### OData共通リクエストヘッダ
|ヘッダ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|Authorization<br>|OAuth2.0形式で、認証情報を指定する<br>|Bearer {TokenValue}<br>|×<br>|※認証トークンは認証トークン取得APIで取得したトークン<br>|
##### OData削除クエストヘッダ
|ヘッダ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|If-Match<br>|対象ETag値を指定する <br>|ETag値<br>|×<br>|省略時は[*]として扱う <br>|
#### リクエストボディ
##### Format
JSON

|項目名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|uri<br>|紐付けるODataリソースのURI<br>|桁数：1&#65374;1024<br>URIの形式に従う<br>scheme：http / https / urn<br>|○<br>|<br>
#### リクエストサンプル
```json
{"uri":"https://fqdn/Cell_name/__ctl/Box_name/collection_name/entitytype('id')"}
```

<br>
### レスポンス
#### ステータスコード
204
#### レスポンスヘッダ
##### 共通レスポンスヘッダ
|ヘッダ名<br>|概要<br>|備考<br>|
|:--|:--|:--|
|X-Dc-Version<br>|APIの実行バージョン<br>|リクエストが処理されたAPIバージョン<br>|
|Access-Control-Allow-Origin<br>|クロスドメイン通信許可ヘッダ<br>|返却値は"*"固定<br>|
##### OData $links レスポンスヘッダ
|ヘッダ名<br>|概要<br>|備考<br>|
|:--|:--|:--|
|DataServiceVersion<br>|ODataのバージョン<br>|<br>|
#### レスポンスボディ
なし
#### エラーメッセージ一覧
[エラーメッセージ一覧](198_Error_Messages.html)を参照
#### レスポンスサンプル
なし

<br>
### CURLサンプル
#### CURLコマンド(UNIX)
```sh
curl "https://fqdn/cell_name/box_name/collection_name/entity_name('userid')/$links/_entitylinkname('userlinkid')"-X DELETE -v -k \
-H 'Authorization:Bearer auth_token' -H 'If-Match: *'
```
<br>
###### Copyright 2017    FUJITSU LIMITED