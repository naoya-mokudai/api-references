# ExtCell Register

### Overview

create new ExtCell

### Required Privileges

auth

### Restrictions

* Accept in the request header is ignored
* Always handles Content-Type in the request header as application/json
* Only accepts the request body in the JSON format
* Only application/json is supported for Content-Type in the request header and the JSON format for the response body
* $formatQuery options ignored

<br>

### Request

#### Request URL

```
/{CellName}/__ctl/ExtCell
```

#### Request Method

POST

#### Request Query

|Query Name<br>|Overview<br>|Effective Value<br>|Required<br>|Notes<br>|
|:--|:--|:--|:--|:--|
|p_cookie_peer<br>|Cookie Authentication Value<br>|The cookie authentication value returned from the server during authentication<br>|No<br>|Valid only if no Authorization header specified<br>Specify this when cookie authentication information is to be used<br>|

#### Request Header

|Header Name<br>|Overview<br>|Effective Value<br>|Required<br>|Notes<br>|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override<br>|Method override function<br>|User-defined<br>|No<br>|If you specify this value when requesting with the POST method, the specified value will be used as a method.<br>|
|X-Override<br>|Header override function<br>|${OverwrittenHeaderName}:${Value}<br>|No<br>|Overwrite normal HTTP header value. To overwrite multiple headers, specify multiple X-Override headers.<br>|
|X-Personium-RequestKey<br>|RequestKey field value output in the event log<br>|Single-byte alphanumeric characters, hyphens ("-"), and underscores ("_")<br>Maximum of 128 characters<br>|No<br><br>|PCS-${UNIXtime} by default<br>Supported in V 1.1.7 and later<br>|
|Authorization<br>|Specifies authentication information in the OAuth 2.0 format<br>|Bearer {AccessToken}<br>|No<br>|* Authentication tokens are the tokens acquired using the Authentication Token Acquisition API<br>|
|Content-Type<br>|Specifies the request body format<br>|application/json<br>|No<br>|[application/json] by default<br>|
|Accept<br>|Specifies the response body format<br>|application/json<br>|No<br>|[application/json] by default<br>|

#### Request Body

|Item Name<br>|Overview<br>|Effective Value<br>|Required<br>|Notes<br>|
|:--|:--|:--|:--|:--|
|Url<br>|URL to Cell<br>|Number of digits: 1-1024<br>Follow URI format<br>scheme:http, https<br>Trailing slash (URL terminated /) Required<br>|Yes<br>|<br>|

#### Request Sample

```JSON
{
  "Url": "https://{UnitFQDN}/{CellName}/"
}
```

<br>

### Response

#### Response Code

201

#### Response Header

|Item Name<br>|Overview<br>|Notes<br>|
|:--|:--|:--|
|Content-Type<br>|Format of data to be returned<br>|<br>|
|Location<br>|URL to the resource that was created<br>|<br>|
|DataServiceVersion<br>|OData version<br>|<br>|
|ETag<br>|Resource version information<br>|<br>|
|Access-Control-Allow-Origin<br>|Cross domain communication permission header<br>|Return value fixed to "*"<br>|
|X-Personium-Version<br>|API version that the request is processed<br>|Version of the API used to process the request<br>|

#### Response Body

|Object<br>|Item Name<br>|Data Type<br>|Notes<br>|
|:--|:--|:--|:--|
|Root<br>|d<br>|object<br>|Object{1}<br>|
|{1}<br>|results<br>|array<br>|Array object {2}<br>|
|{2}<br>|__metadata<br>|object<br>|Object{3}<br>|
|{2}<br>|Url<br>|string<br>|URL of target Cell<br>|
|{3}<br>|etag<br>|string<br>|Etag value<br>|
|{2}<br>|__published<br>|string<br>|Creation date (UNIX time)<br>|
|{2}<br>|__updated<br>|string<br>|Update date (UNIX time)<br>|
|{1}<br>|__count<br>|string<br>|Get number of results in $inlinecount query<br>|

#### ExtCell specific response body

|Object<br>|Item Name<br>|Data Type<br>|Notes<br>|
|:--|:--|:--|:--|
|{3}<br>|type<br>|string<br>|CellCtl.ExtCell<br>|
|{2}<br>|Url<br>|string<br>|URL of target Cell<br>|

#### Error Messages

Refer to [Error Message List](004_Error_Messages.html)

#### Response Sample

```JSON
{
  "d": {
    "results": {
      "__metadata": {
        "uri": "https://{UnitFQDN}/{CellName}/__ctl/ExtCell('https://{UnitFQDN}/{ExtCellName}/')",
        "etag": "W/\"1-1486519006899\"",
        "type": "CellCtl.ExtCell"
      },
      "Url": "https://{UnitFQDN}/{ExtCellName}/",
      "__published": "/Date(1486519006899)/",
      "__updated": "/Date(1486519006899)/"
    }
  }
}
```

<br>

### cURL Command

```sh
curl "https://{UnitFQDN}/{CellName}/__ctl/ExtCell" -X POST -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'  -d '{"Url":"https://{UnitFQDN}/{CellName}/"}'
```

<br><br><br><br><br>

###### Copyright 2017 FUJITSU LIMITED