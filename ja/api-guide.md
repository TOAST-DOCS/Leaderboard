## Game > Leaderboard > APIガイド

> **[注意]**<br>
> ゲームベースを介して自動的にアクティブ化されたリーダーボードは、以下の利用ガイドを参照して必要があります<br>
> [\[Gamebase api guide\]](/Game/Gamebase/ja/api-guide/#leaderboard)

Leaderboard APIはREST API形式で、次のようなAPIを提供します。

### HTTP API
- ユーザースコアの登録(単一 / 多数)
- ユーザースコアの獲得(単一 / 多数 / 範囲 / 特定のユーザの前後)
- ファクターにいるユーザー数の検索
- ユーザースコアの削除(単一)

<br>

## 事前準備
サーバーAPIを使用するためには次の情報を知っている必要があります。

### Server Address
サーバーAPI呼び出しサーバーアドレスは次のとおりです。アドレスはLeaderboardコンソールで確認できます。<br>

> https://api-leaderboard.cloud.toast.com

![図1 Server Address](http://static.toastoven.net/prod_leaderboardv2/renewal/jp/api_guide_202106_1-1.PNG)

### AppKey
アプリケーションキーはゲームサーバーから要請を送る時に必要な固有キーで、コンソールで確認できます。
> [注意]アプリケーションキーは外部に表示してはならず、変更できません。

![図2 AppKey](http://static.toastoven.net/prod_leaderboardv2/renewal/jp/api_guide_202106_2-1.PNG)

### 注意事項
すべてのAPIを使用するには **サービスを有効にした後、ファクターを登録**する必要があります。
Leaderboard APIは **クライアントで呼び出す時、アビューズなどのリスクがあるため、サーバーからのみ呼び出しすることを推奨します。**

<br>

## 共通

### HTTP Header
APIを呼び出す時、HTTP Headerに次の項目を設定する必要があります。

| Name | Required |	Value |
|---|---|---|
| Content-Type | mandatory | application/json; charset=UTF-8 |

### API Response
すべてのAPI要請レスポンスにHTTP 200 OKを渡します。 API要請が成功したかはResponse Bodyのheader項目を参照して判断できます。

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 2873495728794,
	...
}
```

### TransactionId
APIを呼び出しするサーバーで内部的にAPI要請を管理できる方法としてTransactionId機能を提供します。
呼び出しするサーバーでHTTP BodyにTransactionIdを設定してAPIを呼び出すと、Leaderboardサーバーはレスポンス結果に該当のTransactionIdを設定して結果を伝えます。TransactionIdは整数型で受け取ります。

### Time

ユーザーのアップデート時間はRFC 3339定義に従います。

> https://tools.ietf.org/html/rfc3339

<br>

## Get API

### Get total factor count

ファクターの合計数を検索します。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factor-count
```

**[Request Header]**

Common/HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factor-count?transactionId=12345
```

**[Response]**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "header": {
        "resultCode": 0,
        "resultMessage": "LEADERBOARD_OK",
        "isSuccessful": true
    },
    "transactionId": 0,
    "totalFactorCount": 5
}
```

### Get factor info

希望したのファクター情報を検索します。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors
```

**[Request Header]**

Common/HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| factor | int | mandatory | Factor ID |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors?transactionId=12345&factor=1
```

**[Response]**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "header": {
        "resultCode": 0,
        "resultMessage": "LEADERBOARD_OK",
        "isSuccessful": true
    },
    "transactionId": 12345,
    "factorInfo": {
        "resultCode": 0,
        "factor": 1,
        "period": "T",
        "description": "성능 테스트",
        "extra": "test",
        "orderType": "D",
        "scoreType": "U",
        "tieScoreType": "F",
        "resetDate": 0,
        "resetTime": 0,
        "maxSize": 100000000,
        "totalSize": 89,
        "resetInterval": 1,
        "nextResetDate": null,
        "utcTimeZone": "+09:00"
    }
}
```

### Get multiple factor info

希望多数のファクター情報を検索します。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors
```

**[Request Header]**

Common/HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| start | int | mandatory | 検索の開始位置。全ファクター数よりも小さくなければする |
| size | int | mandatory | 検索サイズ。最大1,000まで |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors?transactionId=12345&start=1&size=5
```

**[Response]**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "header": {
        "resultCode": 0,
        "resultMessage": "LEADERBOARD_OK",
        "isSuccessful": true
    },
    "transactionId": 12345,
    "resultInfo": {
        "resultCode": 0,
        "factorInfoList": [
            {
                "resultCode": 0,
                "factor": 1,
                "period": "T",
                "description": "성능 테스트",
                "extra": "test",
                "orderType": "D",
                "scoreType": "U",
                "tieScoreType": "F",
                "resetDate": 0,
                "resetTime": 0,
                "maxSize": 100000000,
                "totalSize": 89,
                "resetInterval": 1,
                "nextResetDate": null,
                "utcTimeZone": "+09:00"
            },
            {
                "resultCode": 0,
                "factor": 2,
                "period": "T",
                "description": "성능 테스트",
                "extra": "test",
                "orderType": "D",
                "scoreType": "U",
                "tieScoreType": "F",
                "resetDate": 0,
                "resetTime": 0,
                "maxSize": 100000000,
                "totalSize": 0,
                "resetInterval": 1,
                "nextResetDate": null,
                "utcTimeZone": "+09:00"
            },
            {
                "resultCode": 0,
                "factor": 3,
                "period": "T",
                "description": "성능 테스트",
                "extra": "test",
                "orderType": "D",
                "scoreType": "U",
                "tieScoreType": "F",
                "resetDate": 0,
                "resetTime": 0,
                "maxSize": 100000000,
                "totalSize": 0,
                "resetInterval": 1,
                "nextResetDate": null,
                "utcTimeZone": "+09:00"
            },
            {
                "resultCode": 0,
                "factor": 4,
                "period": "T",
                "description": "성능 테스트",
                "extra": "test",
                "orderType": "D",
                "scoreType": "U",
                "tieScoreType": "F",
                "resetDate": 0,
                "resetTime": 0,
                "maxSize": 100000000,
                "totalSize": 0,
                "resetInterval": 1,
                "nextResetDate": null,
                "utcTimeZone": "+09:00"
            }
        ]
    }
}
```

### Get user count in factor

希望する1個のファクターに登録されたユーザーの数を検索します。

**[Method, URI]**

```
GET  https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count
```

**[Request Header]**

Common/HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueまたはfalse(デフォルト値はfalse) <br> trueの場合、以前の周期のデータ検索 |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count?transactionId=12345&isPast=false
```

**[Response]**
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "header": {
    "resultCode": 0,
	"resultMessage": "LEADERBOARD_OK",
	"isSuccessful": true
  },
  "transactionId": 0,
  "resultInfo": {
	"resultCode": 0,
	"totalCount": 7
  }
}
```

| Key | Type | Description |
| --- | --- | --- |
| resultInfo | Object | 結果情報 |
| resultInfo.resultCode | int | エラーコード [\[LINK\]](/Game/Leaderboard/ja/error-code) |
| resultInfo.totalCount | int | ファクターに登録されたユーザー数 |

### Get single user info

希望する1名のユーザーの情報を検索できます。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | ユーザーID |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueまたはfalse(デフォルト値はfalse) <br> trueの場合、以前の周期のデータ検索 |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userId}&transactionId=12345&isPast=false
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 12345,
	"userInfo": {
		"resultCode": 0,
		"userId": "user1",
		"score": 1000,
		"rank": 2,
		"preRank": 0,
		"extra": "extra Data1",
		"date": "2017-01-02T16:28:51+09:00",
		"totalUserCountInFactor": 100
	}
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfo | Object | ユーザー情報 |
| userInfo.resultCode | int | エラーコード [\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfo.userId | String | ユーザーID |
| userInfo.score | Double | ユーザースコア |
| userInfo.rank | int | 今回の周期の順位 |
| userInfo.preRank | int | 以前の周期の順位 |
| userInfo.extra | String | ユーザーと一緒に保存されるExtra Data(最大16バイト) |
| userInfo.date | String | ユーザースコアがアップデートされた時間(RFC 3339) |
| userInfo.totalUserCountInFactor | int | ファクターに登録されたユーザー数 |

### Get multiple user info

希望する多数のユーザー情報を検索できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueの場合、以前の周期、 falseの場合、現在の周期のデータ検索 |
| isSort | bool | optional | trueの場合、順位を基準にソート、 falseの場合、入力したuserId順にデータ検索 |
| userIDsWithFactor | Array[[String, Array[String]]] | mandatory | 検索したFactorとユーザーリストの束 |
| userIDsWithFactor[].factor |	int | mandatory | 照会したいFactor ID|
| userIDsWithFactor[].userIds |	Array[String] | mandatory | 検索したいユーザーリスト |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
Content-Type: application/json

{
	"isPast": false,
	"isSort": false,
	"transactionId": 12345,
	"userIDsWithFactor": [
		{
			"factor": 1,
			"userIds": ["user1", "user2", "user3" ]
		},
		{
			"factor": 2,
			"userIds": ["user4", "user5", "user6" ]
		}
	]
}

```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 12345,
	"userInfosWithFactor": [
	{
		"resultCode": 0,
		"factor": 1,
		"userInfos": [
		{
			"resultCode": 0,
			"userId": "user1",
			"score": 1000,
			"rank": 2,
			"preRank": 0,
			"extra": "extra Data1",
			"date": "2017-01-02T16:42:31+09:00",
			"totalUserCountInFactor": 100
		},
		{
			"resultCode": 0,
			"userId": "user2",
			"score": 1100,
			"rank": 1,
			"preRank": 0,
			"extra": "extra Data2",
			"date": "2017-01-02T16:42:31+09:00",
			"totalUserCountInFactor": 100
		},
		{
			"resultCode": 462850,
			"userId": "user3",
			"score": 0,
			"rank": 0,
			"preRank": 0,
			"extra": "",
			"date": "1970-01-01T09:00:00+09:00",
			"totalUserCountInFactor": 100
		}]
	},
	{
		"resultCode": 0,
		"factor": 2,
		"userInfos": [
		{
			"resultCode": 0,
			"userId": "user4",
			"score": 1200,
			"rank": 3,
			"preRank": 0,
			"extra": "extra Data4",
			"date": "2017-01-02T16:42:28+09:00",
			"totalUserCountInFactor": 200
		},
		{
			"resultCode": 0,
			"userId": "user5",
			"score": 1300,
			"rank": 2,
			"preRank": 0,
			"extra": "extra Data5",
			"date": "2017-01-02T16:42:28+09:00",
			"totalUserCountInFactor": 200
		},
		{
			"resultCode": 462850,
			"userId": "user6",
			"score": 0,
			"rank": 0,
			"preRank": 0,
			"extra": "",
			"date": "1970-01-01T09:00:00+09:00",
			"totalUserCountInFactor": 200
		}]
	}]
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfosWithFactor | Array[Object] | ユーザー情報 |
| userInfosWithFactor[].resultCode | int | ファクターのエラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfosWithFactor[].factor | int | Factor ID |
| userInfosWithFactor[].userInfos | Array[Object] | ユーザースコア |
| userInfos[].resultCode | int | 該当ユーザーのコード。エラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfos[].userId | String | ユーザーID |
| userInfos[].score | double | ユーザースコア |
| userInfos[].rank | int | 今回の周期の順位 |
| userInfos[].preRank | int | 以前の周期の順位 |
| userInfos[].extra | String | ユーザーと一緒に保存されるExtra Data(最大16バイト) |
| userInfos[].date | String | ユーザースコアがアップデートされた時間(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | ファクターに登録されたユーザー数 |

### Get multiple user info by range

希望する範囲(順位)の順位情報を検索できる方法です。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueまたはfalse (デフォルト値はfalse) <br> trueの場合、以前の周期のデータ検索 |
| start | int | mandatory | 開始順位|
| size | int | mandatory | 取得するLeaderboard情報の個数|

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?transactionId=12345&isPast=false&start=1&size=3
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 0,
	"userInfosByRange": {
		"resultCode": 0,
		"factor": 1,
		"userInfos": [
		{
			"resultCode": 0,
			"userId": "user2",
			"score": 1100,
			"rank": 1,
			"preRank": 0,
			"extra": "extra Data2",
			"date": "2017-01-02T16:42:28+09:00",
			"totalUserCountInFactor": 200
		},
		{
			"resultCode": 0,
			"userId": "user1",
			"score": 1000,
			"rank": 2,
			"preRank": 0,
			"extra": "extra Data1",
			"date": "2017-01-02T16:42:28+09:00",
			"totalUserCountInFactor": 200
		},
		{
			"resultCode": 0,
			"userId": "test4",
			"score": 200,
			"rank": 3,
			"preRank": 0,
			"extra": "extraData",
			"date": "2017-01-02T16:42:28+09:00",
			"totalUserCountInFactor": 200
		}]
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfosByRange | Array[Object] | ユーザー情報 |
| userInfosByRange[].resultCode | int | ファクターのエラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfosByRange[].factor | int | ファクターID |
| userInfos[].resultCode | int | 該当ユーザーのコード。エラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfos[].userId | String | ユーザーID |
| userInfos[].score | double | ユーザースコア |
| userInfos[].rank | int | 今回の周期の順位 |
| userInfos[].preRank | int | 以前の周期の順位 |
| userInfos[].extra | String | ユーザーと一緒に保存されるExtra Data(最大16バイト) |
| userInfos[].date | String | ユーザースコアがアップデートされた時間(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | ファクターに登録されたユーザー数 |

### Get multiple user info by pivot user

基準ユーザの順位と上位、下位ユーザの順位情報を取得することができる方法です。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueまたはfalse (デフォルト値はfalse) <br> trueの場合、以前の周期のデータ検索 |
| userId | String | mandatory | 基準ユーザID |
| prevSize | int | mandatory | 基準ユーザランキングで照会することが上位ユーザサイズ <br> 最大 500 |
| nextSize | int | mandatory | 基準ユーザのランキングで照会するサブユーザサイズ <br> 最大 500 |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?transactionId=12345&isPast=false&userId=test4&prevSize=3&nextSize=3
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "header": {
        "resultCode": 0,
        "resultMessage": "LEADERBOARD_OK",
        "isSuccessful": true
    },
    "transactionId": 4,
    "userInfosByRange": {
        "resultCode": 0,
        "factor": 2,
        "userInfos": [
            {
                "resultCode": 0,
                "userId": "test7",
                "score": 700,
                "rank": 1,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test6",
                "score": 600,
                "rank": 2,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test5",
                "score": 500,
                "rank": 3,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test4",
                "score": 400,
                "rank": 4,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test3",
                "score": 300,
                "rank": 5,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test2",
                "score": 200,
                "rank": 6,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test1",
                "score": 100,
                "rank": 7,
                "preRank": 0,
                "extra": "",
                "date": "2019-04-17T14:18:44+09:00",
			    "totalUserCountInFactor": 200
            }
        ]
    }
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfosByRange | Array[Object] | ユーザー情報 |
| userInfosByRange[].resultCode | int | ファクターのエラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfosByRange[].factor | int | ファクターID |
| userInfos[].resultCode | int | 該当ユーザーのコード。エラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfos[].userId | String | ユーザーID |
| userInfos[].score | double | ユーザースコア |
| userInfos[].rank | int | 今回の周期の順位 |
| userInfos[].preRank | int | 以前の周期の順位 |
| userInfos[].extra | String | ユーザーと一緒に保存されるExtra Data(最大16バイト) |
| userInfos[].date | String | ユーザースコアがアップデートされた時間(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | ファクターに登録されたユーザー数 |

### Get selected rank user info

特定の順位のユーザを検索することができる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueまたはfalse (デフォルト値はfalse) <br> trueの場合、以前の周期のデータ検索 |
| userRanks | Array[Integer] | mandatory | ユーザ順位のリスト。最大20個まで。 |
| isSort | bool | optional | trueまたはfalse (デフォルト値はfalse) <br>trueの場合、順位を基準にソート、falseの場合、入力したrank list順にデータ検索 |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
Content-Type: application/json

{
	"transactionId": 1234,
	"isPast": false,
	"userRanks": [3,1,4,5,2,0]
	"isSort": false
}
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "LEADERBOARD_OK",
        "isSuccessful": true
    },
    "transactionId": 12345,
    "userInfosByRange": {
        "resultCode": 0,
        "factor": 1,
        "userInfos": [
            {
                "resultCode": 0,
                "userId": "test9999998",
                "score": 9999999.0,
                "rank": 3,
                "preRank": 0,
                "extra": "",
                "date": "2020-09-24T12:31:07+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test10000000",
                "score": 1.0000001E7,
                "rank": 1,
                "preRank": 0,
                "extra": "",
                "date": "2020-09-24T12:31:07+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test9999997",
                "score": 9999998.0,
                "rank": 4,
                "preRank": 0,
                "extra": "",
                "date": "2020-09-24T12:31:07+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test9999996",
                "score": 9999997.0,
                "rank": 5,
                "preRank": 0,
                "extra": "",
                "date": "2020-09-24T12:31:07+09:00",
			    "totalUserCountInFactor": 200
            },
            {
                "resultCode": 0,
                "userId": "test9999999",
                "score": 1.0E7,
                "rank": 2,
                "preRank": 0,
                "extra": "",
                "date": "2020-09-24T12:31:07+09:00",
			    "totalUserCountInFactor": 200
            }
        ]
    }
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfosByRange | Array[Object] | ユーザー情報 |
| userInfosByRange[].resultCode | int | ファクターのエラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfosByRange[].factor | int | ファクターID |
| userInfos[].resultCode | int | 該当ユーザーのコード。エラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| userInfos[].userId | String | ユーザーID |
| userInfos[].score | double | ユーザースコア |
| userInfos[].rank | int | 今回の周期の順位 |
| userInfos[].preRank | int | 以前の周期の順位 |
| userInfos[].extra | String | ユーザーと一緒に保存されるExtra Data(最大16バイト) |
| userInfos[].date | String | ユーザースコアがアップデートされた時間(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | ファクターに登録されたユーザー数 |

<br>

## Set API

### Set single user score

希望する1名のユーザースコアを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
```

**[Request Header]**

Common/HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey | String | Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
| factor | int | ファクターID |
| userId | String | ユーザーID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long | 必須 | トランザクションID |
|score|	double | 必須 | ユーザースコア |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
Content-Type: application/json

{
	"score": 10,
	"transactionId": 1234
}
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
  	},
  	"transactionId": 1234,
  	"resultInfo": {
		"resultCode": 0,
		"userId": "test1"
  	}
}
```

| Key | Type | Description |
| --- | --- | --- |
| resultInfo | Object | 結果情報 |
| resultInfo.resultCode | int | エラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| resultInfo.userId | String | 登録されたユーザーID |


### Set single user score with extra data

希望する1名のユーザースコアとExtra Dataを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey |	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
| factor | int | ファクターID |
| userId | String | ユーザーID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long |	mandatory | トランザクションID |
| score | double | mandatory | ユーザースコア |
| extra | String | optional | ユーザーと一緒に保存されるExtra Data(最大16バイト) |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
Content-Type: application/json

{
	"extra": "extraData",
	"score": 200,
	"transactionId": 1234
}
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 1234,
	"resultInfo": {
		"resultCode": 0,
		"userId": "test4"
	}
}
```

| Key | Type | Description |
| --- | --- | --- |
| resultInfo | Object | 結果情報 |
| resultInfo.resultCode | int | エラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| resultInfo.userId | String | 登録されたユーザーID |

### Set multiple user score

希望するユーザーのスコアを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | トランザクションID |
| userScoresWithFactor | Array[Object] | mandatory | ユーザースコアリストとFactorのリスト |
| userScoresWithFactor[].factor | int | mandatory | 登録を希望するFactor ID |
| userScoresWithFactor[].userScores | Array[Object] | mandatory | 登録を希望するユーザーIDとスコアリスト |
| userScores[].userId | String | mandatory | ユーザーID |
| userScores[].score | double | mandatory | ユーザースコア |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores

Content-Type: application/json
{
	"transactionId": 12345,
  	"userScoresWithFactor": [
		{
			"factor": 1,
			"userScores": [
			{
				"score": 1000,
				"userId": "user1"
			},
			{
				"score": 1100,
				"userId": "user2"
			}]
		},
		{
			"factor": 2,
			"userScores": [
				{
				"score": 1200,
				"userId": "user4"
				},
				{
				"score": 1300,
				"userId": "user5"
				}]
		}
	]
}
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 12345,
	"resultInfosWithFactor": [
	{
		"resultCode": 0,
		"factor": 1,
		"resultInfos": [
			{
				"resultCode": 0,
				"userId": "user1"
			},
			{
				"resultCode": 0,
				"userId": "user2"
			}
		]
	},
	{
		"resultCode": 0,
		"factor": 2,
		"resultInfos": [
			{
				"resultCode": 0,
				"userId": "user4"
			},
			{
				"resultCode": 0,
				"userId": "user5"
			}
		]
	}]
}
```

| Key | Type | Description |
| --- | --- | --- |
| resultInfosWithFactor | Array[Object] | 結果情報 |
| resultInfosWithFactor[].resultCode | int | ファクターのエラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | 登録されたユーザーの結果情報 |
| resultInfos.resultCode | int | ユーザーに対するエラーコード |
| resultInfos.userId | String | 登録されたユーザーID |

### Set multiple user score with extra data

希望するユーザースコアとExtra Dataを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores-with-extra
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | トランザクションID |
| userInfosWithFactor | Array[Object] | mandatory | ユーザースコアリストとFactorリスト |
| userInfosWithFactor[].factor | int | mandatory | 登録を希望するFactor ID |
| userInfosWithFactor[].userInfos | Array[Object] | mandatory | 登録を希望するユーザーIDとスコアリスト |
| userInfos[].userId | String | mandatory | ユーザーID |
| userInfos[].score | double | mandatory | ユーザースコア |
| userInfos[].extra | String | optional | ユーザーと一緒に保存されるExtra Data(最大16バイト) |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores-with-extra
Content-Type: application/json

{
	"transactionId": 12345,
  	"userInfosWithFactor": [
	{
		"factor": 1,
		"userInfos": [
		{
			"score": 1000,
			"userId": "user1",
			"extra": "extra Data1"
		},
		{
			"score": 1100,
			"userId": "user2",
			"extra": "extra Data2"
		}]
	},
	{
		"factor": 2,
		"userInfos": [
		{
			"score": 1200,
			"userId": "user4",
			"extra": "extra Data4"
		},
		{
			"score": 1300,
			"userId": "user5",
			"extra": "extra Data5"
		}]
	}]
}
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 12345,
	"resultInfosWithFactor": [
	{
		"resultCode": 0,
		"factor": 1,
		"resultInfos": [
			{
				"resultCode": 0,
				"userId": "user1"
			},
			{
				"resultCode": 0,
				"userId": "user2"
			}
		]
	},
	{
		"resultCode": 0,
		"factor": 2,
		"resultInfos": [
			{
				"resultCode": 0,
				"userId": "user4"
			},
			{
				"resultCode": 0,
				"userId": "user5"
			}
		]
	}]
}
```

| Key | Type | Description |
| --- | --- | --- |
| resultInfosWithFactor | Array[Object] | 結果情報 |
| resultInfosWithFactor[].resultCode | int | ファクターのエラーコード[\[LINK\]](/Game/Leaderboard/ja/error-code) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | 登録されたユーザーの結果情報 |
| resultInfos.resultCode | int | ユーザーに対するエラーコード |
| resultInfos.userId | String | 登録されたユーザーID |

<br>

## Delete API

### Delete single user info

希望するユーザー1名の情報を削除する方法です。該当ユーザーは完全に削除され、復旧できません。

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | ユーザーID |
| transactionId | long | optional | トランザクションID |
| isPast | bool | optional | trueまたはfalse(デフォルト値はfalse) <br> trueの場合、以前の周期のデータ削除 |

**[Request Sample]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userid}&transactionId=12345&isPast=false
```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 12345,
	"resultInfo": {
		"resultCode": 0,
		"userId": "test4"
	}
}
```
<br>

### Delete multiple user info

希望ユーザ複数の情報を削除する方法です。このユーザーは、完全に削除され、復元されません。

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 確認 [\[LINK\]](/Game/Leaderboard/ja/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | トランザクションID |
| userIds | Array[Object] | mandatory | ユーザーIDリスト。最大20個まで。 |
| isPast | bool | optional | trueまたはfalse(デフォルト値はfalse) <br> trueの場合、以前の周期のデータ削除 |


**[Request Sample]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users

{
    "transactionId": 1234,
    "isPast": false,
    "userIds": ["test18", "test11", "test14", "test16"]
    "isSort": false
}

```

**[Response]**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"header": {
		"resultCode": 0,
		"resultMessage": "LEADERBOARD_OK",
		"isSuccessful": true
	},
	"transactionId": 12345,
	"resultInfo": {
        "resultCode": 0,
        "factor": 1,
        "resultInfos": [
            {
                "resultCode": 0,
                "userId": "test18"
            },
            {
                "resultCode": 0,
                "userId": "test11"
            },
            {
                "resultCode": 0,
                "userId": "test14"
            },
            {
                "resultCode": 0,
                "userId": "test16"
            }
        ]
    }
}
```