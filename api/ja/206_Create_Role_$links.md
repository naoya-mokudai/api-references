# Role_$links登録
### 概要
Roleに$linksで指定したODataリソースを紐付ける
* Account
* ExtCell
* ExtRole
* Relation

### 必要な権限
なし

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
/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name='{BoxName}')/$links/_Account
```
または、
```
/{CellName}/__ctl/Role(Name='{RoleName}')/$links/_Account
```
または、
```
/{CellName}/__ctl/Role('{RoleName}')/$links/_Account
```
##### Association with the ExtCell
```
/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name='{BoxName}')/$links/_ExtCell
```
または、
```
/{CellName}/__ctl/Role(Name='{RoleName}')/$links/_ExtCell
```
または、
```
/{CellName}/__ctl/Role('{RoleName}')/$links/_ExtCell
```
##### Association with the ExtRole
```
/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name='{BoxName}')/$links/_ExtRole
```
または、
```
/{CellName}/__ctl/Role(Name='{RoleName}')/$links/_ExtRole
```
または、
```
/{CellName}/__ctl/Role('{RoleName}')/$links/_ExtRole
```
##### Association with the relation
```
/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name='{BoxName}')/$links/_Relation
```
または、
```
/{CellName}/__ctl/Role(Name='{RoleName}')/$links/_Relation
```
または、
```
/{CellName}/__ctl/Role('{RoleName}')/$links/_Relation
```
※ \_Box.Nameパラメタを省略した場合は、nullが指定されたものとする

#### メソッド
POST

#### リクエストクエリ

|クエリ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|p_cookie_peer<br>|クッキー認証値<br>|認証時にサーバから返却されたクッキー認証値<br>|×<br>|Authorizationヘッダの指定が無い場合のみ有効<br>クッキーの認証情報を利用する場合に指定する<br>|
&#160;

#### リクエストヘッダ

|ヘッダ名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override<br>|メソッドオーバーライド機能<br>|任意<br>|×<br>|POSTメソッドでリクエスト時にこの値を指定すると、指定した値がメソッドとして使用されます。<br>|
|X-Override<br>|ヘッダオーバライド機能<br>|${上書きするヘッダ名}:${値}<br>|×<br>|通常のHTTPヘッダの値を上書きします。複数のヘッダを上書きする場合はX-Overrideヘッダを複数指定します。<br>|
|X-Personium-RequestKey<br>|イベントログに出力するRequestKeyフィールドの値<br>|半角英数、-(半角ハイフン)と_(半角アンダーバー)<br>最大128文字<br>|×<br>|指定がない場合、PCS-${UNIX時間}を設定する<br>V1.1.7以降で対応<br>|
|Authorization<br>|OAuth2.0形式で、認証情報を指定する<br>|Bearer {UnitUserToken}<br>|×<br>|※認証トークンは認証トークン取得APIで取得したトークン<br>|
|Content-Type<br>|リクエストボディの形式を指定する<br>|application / json<br>|×<br>|省略時は[application/json]として扱う<br>|
|Accept<br>|レスポンスボディの形式を指定する<br>|application / json<br>|×<br>|省略時は[application/json]として扱う<br>|
#### リクエストボディ
##### Format
JSON

|項目名<br>|概要<br>|有効値<br>|必須<br>|備考<br>|
|:--|:--|:--|:--|:--|
|uri<br>|紐付けるODataリソースのURI<br>|桁数：1&#65374;1024<br>URIの形式に従う<br>scheme：http / https / urn<br>|○<br>|&#160;<br>|

#### リクエストサンプル
```json
{"uri":"https://{UnitFQDN}/Cell/__ctl/Box('{BoxName}')"}
```
<br>
### レスポンス
#### ステータスコード
204

#### レスポンスヘッダ

|ヘッダ名<br>|概要<br>|備考<br>|
|:--|:--|:--|
|DataServiceVersion<br>|ODataのバージョン<br>|<br>|
|Access-Control-Allow-Origin<br>|クロスドメイン通信許可ヘッダ<br>|返却値は"*"固定<br>|
|X-Personium-Version<br>|APIの実行バージョン<br>|リクエストが処理されたAPIバージョン<br>|

#### レスポンスボディ
なし

#### エラーメッセージ一覧
[エラーメッセージ一覧](200_Error_Messages.html)を参照

#### レスポンスサンプル
なし
<br>
### CURLサンプル

```sh
curl "https://{UnitFQDN}/{CellName}/__ctl/Role('{RoleName}')/\$links/_Box" -X POST -i -H 'Authorization: Bearer {UnitUserToken}' -H 'Accept: application/json' -d "{\"uri\":\"https://{UnitFQDN}/{CellName}/__ctl/Box('{BoxName}')\"}"
```
<br>
<br>
<br>
###### Copyright 2017    FUJITSU LIMITED