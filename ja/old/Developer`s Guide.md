## Game > Leaderboard > Developer's Guide

Leaderboard APIは、REST APIの形で以下のAPIを提供します。

### HTTP API
- ユーザースコア登録（単一 / 複数）
- ユーザースコア獲得（単一 / 複数 / 範囲）
- Factorに入っているユーザー数照会
- ユーザースコア削除（単一）

<br>

## Notice

### Caution
すべてのAPIを使用するためには、**商品をアクティブ化してから、Factorを登録**する必要があります。
Leaderboard APIは、**Serverから呼び出すことをお勧め**しており、**Clientからの呼び出しはお勧めしていません。**

### Server Address
サーバーAPIを呼び出すためのサーバーアドレスは、以下の通りです。このアドレスは「Leaderboard」のコンソール画面からも確認できます。<br>

> https://api-leaderboard.cloud.toast.com

![図 1 Server Address](http://static.toastoven.net/prod_leaderboardv2/developer_1-jp.png)

### AppKey
AppKeyは、ゲームサーバーにリクエストを送る際に必要な固有なキーで、 「Leaderboard」のコンソール画面からも確認できます。
> **注意事項** <br>
> AppKeyは、外部に露出されることがあってはなりません。なお、変更はできないので、ご注意ください。

![図 2 AppKey](http://static.toastoven.net/prod_leaderboardv2/developer_2-jp.png)

<br>

## Common

### HTTP Header
API呼び出し時にHTTP Headerに以下の項目を設定する必要があります。

| Name | Required | Value |
|---|---|---|
| Content-Type | mandatory | application/json; charset=UTF-8 |

### API Response
すべてのAPIリクエストに対するレスポンスとして、HTTP 200 OKを送ります。APIリクエストの成否は、Response Bodyのheader項目を参照し判断できます。

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
APIを呼び出すサーバーで内部的にAPIリクエストを管理できる方法として、TransactionId機能を提供します。
呼び出すサーバーのHTTP BodyにTransactionIdを設定しAPIを呼び出すと、「Leaderboard」サーバーは、レスポンスの結果に該当のTransactionIdを設定し、結果を送ります。TransactionIdは、定数型タイプです。

### Time

ユーザーのアップデート時間は、RFC 3339の定義に従います。

> https://tools.ietf.org/html/rfc3339

<br>

## Get API

### Get user count in factor

希望する1つのFactorに登録されているユーザー数を照会します。

**[Method, URI]**

```
GET  https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count?transactionid={transactionid}&ispast={ispast} 
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)


**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|
|factor|	int|	Leaderboard Factor|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionid | long | optional | トランザクションID |
| ispast | bool | optional | true or false（デフォルトはfalse） <br> trueの場合は、前回の周期のデータを照会 | 

**[Request Sample]**
```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count?transactionid=12345&ispast=false
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
| resultInfo.resultCode | int | エラーコード [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| resultInfo.totalCount | int | Factorに登録されているユーザー数 |

### Get single user info

希望する一人のユーザー情報を照会できます。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userId}&transactionid={transactionid}&ispast={ispast} 
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|
|factor|	int|	Leaderboard Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | User ID |
| transactionid | long | optional | トランザクションID |
| ispast | bool | optional | true or false（デフォルトはfalse) <br> trueの場合は、前回の周期のデータを照会 |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userId}&transactionid=12345&ispast=false
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
		"date": "2017-01-02T16:28:51+09:00"
	}
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfo | Object | ユーザー情報 |
| userInfo.resultCode | int | エラーコード [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| userInfo.userId | String | User ID |
| userInfo.score | Double | User Score |
| userInfo.rank | int | 今回の周期のランキング |
| userInfo.preRank | int | 前回の周期のランキング |
| userInfo.extra | String | ユーザーとともに保存されるExtra Data（最大16Byte） |
| userInfo.date | String | ユーザースコアがアップデートされた時間（RFC 3339） |

### Get multiple user info

希望する複数のユーザー情報を照会できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long |	mandatory | トランザクションID |
| isPast | bool | mandatory | true or false（デフォルトはfalse) <br> trueの場合は、前回の周期のデータを照会 |
| userIDsWithFactor | Array[[String, Array[String]]] | mandatory | 照会を希望するFactorとユーザーリストのまとめ |
| userIDsWithFactor[].factor |	int | mandatory | 照会を希望するFactor |
| userIDsWithFactor[].userIds |	Array[String] | mandatory | 照会を希望するユーザーリスト |

**[Request Sample]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
Content-Type: application/json

{
	"isPast": false,
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
			"date": "2017-01-02T16:42:31+09:00"
		},
		{
			"resultCode": 0,
			"userId": "user2",
			"score": 1100,
			"rank": 1,
			"preRank": 0,
			"extra": "extra Data2",
			"date": "2017-01-02T16:42:31+09:00"
		},
		{
			"resultCode": 462850,
			"userId": "user3",
			"score": 1100,
			"rank": 0,
			"preRank": 0,
			"extra": "",
			"date": "2017-01-02T16:42:31+09:00"
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
			"date": "2017-01-02T16:42:28+09:00"
		},
		{
			"resultCode": 0,
			"userId": "user5",
			"score": 1300,
			"rank": 2,
			"preRank": 0,
			"extra": "extra Data5",
			"date": "2017-01-02T16:42:28+09:00"
		},
		{
			"resultCode": 462850,
			"userId": "user6",
			"score": 1300,
			"rank": 0,
			"preRank": 0,
			"extra": "",
			"date": "2017-01-02T16:42:28+09:00"
		}]
	}]
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfosWithFactor | Array[Object] | ユーザー情報 |
| userInfosWithFactor[].resultCode | int | Factorに対するエラーコード[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| userInfosWithFactor[].factor | int | Factor ID |
| userInfosWithFactor[].userInfos | Array[Object] | User Score |
| userInfos[].resultCode | int | 該当ユーザーに対するコード。エラーコード [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User Score |
| userInfos[].rank | int | 今回の周期のランキング |
| userInfos[].preRank | int | 前回の周期のランキング |
| userInfos[].extra | String | ユーザーとともに保存されるExtra Data（最大16Byte) |
| userInfos[].date | String | ユーザースコアがアップデートされた時間（RFC 3339) |

### Get multiple user info by range

希望する範囲（順位）のランキング情報を照会できる方法です。

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?transactionid={transactionid}&ispast={ispast}&start={start}&size={size} 
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionid | long | optional | トランザクションID |
| ispast | bool | optional | true or false（デフォルトはfalse) <br> trueの場合は、前回の周期のデータを照会 |
| start | int | mandatory | 開始ランキング |
| size | int | mandatory | 取得するLeaderboardの情報数 |

**[Request Sample]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?transactionid=12345&ispast=false&start=1&size=3
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
			"date": "2017-01-02T16:42:28+09:00"
		},
		{
			"resultCode": 0,
			"userId": "user1",
			"score": 1000,
			"rank": 2,
			"preRank": 0,
			"extra": "extra Data1",
			"date": "2017-01-02T16:42:28+09:00"
		},
		{
			"resultCode": 0,
			"userId": "test4",
			"score": 200,
			"rank": 3,
			"preRank": 0,
			"extra": "extraData",
			"date": "2017-01-02T16:42:28+09:00"
		}]
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfosByRange | Array[Object] | ユーザー情報 |
| userInfosByRange[].resultCode | int | Factorに対するエラーコード[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| userInfosByRange[].factor | int | Factor ID |
| userInfos[].resultCode | int | 該当ユーザーに対するコード。エラーコード [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User Score |
| userInfos[].rank | int | 今回の周期のランキング |
| userInfos[].preRank | int | 前回の周期のランキング |
| userInfos[].extra | String | ユーザーとともに保存されるExtra Data（最大16Byte) |
| userInfos[].date | String | ユーザースコアがアップデートされた時間（RFC 3339) |

<br>

## Set API

### Set single user score

希望する一人のユーザーのスコアを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey | String | Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|
| factor | int | Factor ID |
| userId | String | User ID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long | mandatory | トランザクションID |
|score|	double | mandatory | ユーザースコア |

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
| resultInfo.resultCode | int | エラーコード [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| resultInfo.userId | String | 登録されたユーザーID  |


### Set single user score with extra data

希望する一人のユーザーのスコアとExtra Dataを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey |	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|
| factor | int | Factor ID |
| userId | String | User ID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long |	mandatory | トランザクションID |
| score | double | mandatory | ユーザースコア |
| extra | String | optional | ユーザーとともに保存されるExtra Data（最大16Byte) |

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
| resultInfo.resultCode | int | エラーコード [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| resultInfo.userId | String | 登録されたユーザーID  |

### Set multiple user score

希望するユーザースコアを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | トランザクションID |
| userScoresWithFactor | Array[Object] | mandatory | ユーザースコア・Factorのリスト |
| userScoresWithFactor[].factor | int | mandatory | 登録を希望するFactor |
| userScoresWithFactor[].userScores | Array[Object] | mandatory | 登録を希望するユーザーID/スコアのリスト |
| userScores[].userId | String | mandatory | User ID |
| userScores[].score | double | mandatory | User Score |

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
| resultInfosWithFactor[].resultCode | int | Factorに対するエラーコード[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | 登録されたユーザーの結果情報 |
| resultInfos.resultCode | int | User に対するエラーコード|
| resultInfos.userId | String | 登録されたユーザーID  |

### Set multiple user score with extra data

希望するユーザースコアとExtra Dataを登録できる方法です。

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores-with-extra
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | トランザクションID |
| userInfosWithFactor | Array[Object] | mandatory | ユーザースコア・Factorのリスト |
| userInfosWithFactor[].factor | int | mandatory | 登録を希望するFactor |
| userInfosWithFactor[].userInfos | Array[Object] | mandatory | 登録を希望するユーザーID/スコアのリスト |
| userInfos[].userId | String | mandatory | User ID |
| userInfos[].score | double | mandatory | User Score |
| userInfos[].extra | String | optional | ユーザーとともに保存されるExtra Data（最大16Byte) |

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
| resultInfosWithFactor[].resultCode | int | Factorに対するエラーコード[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#error-codes) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | 登録されたユーザーの結果情報 |
| resultInfos.resultCode | int | User に対するエラーコード|
| resultInfos.userId | String | 登録されたユーザーID |

<br>

## Delete API

### Delete single user info

希望する一人のユーザー情報を削除する方法です。該当ユーザーは永久的に削除され、復旧できません。

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?transactionid={transactionid}&ispast={ispast}
```

**[Request Header]**

Common / HTTP Headerの確認[\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ja/Developer%60s%20Guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| userId | String | mandatory | User ID |
| transactionid | long | optional | トランザクションID |
| ispast | bool | optional | true or false（デフォルトはfalse） <br> trueの場合は、前回の周期のデータを削除 |

**[Request Sample]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userid}?transactionid=12345&ispast=false
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

## Error Codes

以下の表のエラーコードは、Response bodyのheader/bodyにあるresultCodeとresultMessageの意味を説明したものです。
HeaderのresultCodeで以下のエラーコードではなく、HTTPのエラーコードが表示される場合は、以下の[参照]リンクをご参照ください。

|Result Code| Result Code(Hex) | Result Message |説明|
|---|---|---|---|
|0|	0x00000000 |LEADERBOARD_SUCCESS | リクエスト成功 |
|1|	0x00000001 |LEADERBOARD_SUCCESS_BUT_NOT_UPDATE | リクエストは成功したものの、既存と同じデータが入ったため、アップデートはしていない |
|459777|	0x00070401 |LEADERBOARD_ERROR_APPKEY_VERIFIER | アプリキー認証失敗 |
|462849|	0x00071001 |LEADERBOARD_AP_ERROR_INITIALTIZE | リセット失敗 |
|462850|	0x00071002 |LEADERBOARD_AP_ERROR_NOT_EXIST_USER | 未登録ユーザー |
|462851|	0x00071003 |LEADERBOARD_AP_ERROR_NOT_EXIST_FACTOR | 未登録Factor |
|462852|	0x00071004 |LEADERBOARD_AP_ERROR_NOT_EXIST_APPKEY | 未登録アプリキー |
|462853|	0x00071005 |LEADERBOARD_AP_ERROR_TOO_BIG_EXTRA | Extra Data 長さ制限超過 |
|462854|	0x00071006 |LEADERBOARD_AP_ERROR_WRONG_RANGE | 正しくない範囲 |
|462855|	0x00071007 |LEADERBOARD_AP_ERROR_WRONG_PARAM | 正しくないパラメーター |
|462856|    0x00071008 |LEADERBOARD_AP_ERROR_WRONG_PATH | URI入力時誤字、パラメータ不足 |
|463000|	0x00071098 |LEADERBOARD_AP_ERROR_SYSTEM | システムエラー |
|463001|	0x00071099 |LEADERBOARD_AP_ERROR_UNKOWN | 不明なエラー |

> [参照]  
> その他、一般的なエラーコードに対する追加情報は、以下のリンクよりご確認ください。 <br>
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml  

