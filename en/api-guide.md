## Game > Leaderboard > API Guide 

> **[Caution]**<br>
> Leaderboards that are automatically activated through the gamebase should refer to the usage guide below.<br>
> [\[Gamebase api guide\]](/Game/Gamebase/en/api-guide/#leaderboard)

Leaderboard API provides the following APIs in the REST API format.  

### HTTP API
- Register user scores (single / multiple) 
- Win user scores (single / multiple / range / before and after a specific user) 
- Search the number of users at a factor 
- Delete user scores (single) 

<br>

## Prerequisites 
Information that follows must be available to use Server API. 

### Server Address
Server API can be called in the following address, which is also available from the Leaderboard console: <br>

> https://api-leaderboard.cloud.toast.com

![그림 1 Server Address](http://static.toastoven.net/prod_leaderboardv2/renewal/en/api_guide_202106_1-1.PNG)

### AppKey
Appkey is an original key required to send requests from a game server, and it is available in the console.  
> [Caution] Appkey must not be exposed and cannot be modified.  

![그림 2 AppKey](http://static.toastoven.net/prod_leaderboardv2/renewal/en/api_guide_202106_2-1.PNG)

### Caution 
To use all APIs, **service must be enabled first, to register factors**.  
Leaderboard API **is recommended to be called only from a server to avoid risks of abusive acts when it is called from Client.**

<br>

## Common 

### HTTP Header
Following item must be set at HTTP Header to call API: 

| Name | Required |	Value |
|---|---|---|
| Content-Type | mandatory | application/json; charset=UTF-8 |

### API Response
HTTP 200 OK is sent as response to all APIs. Success or failure of an API request can be decided upon the header of the Response Body. 

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
 TransactionId is provided as a means of management for API requests within servers sending API calls. With TransactionId set at the HTTP Body of a caller server to call API, the Leaderboard server sends results with the TransactionId set. TransactionId is received in the integer data type. 

### Time

User time is updated according to what is defined at RFC 3339. 

> https://tools.ietf.org/html/rfc3339

<br>

## Get API

### Get total factor count

Retrieves the total number of factors.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factor-count
```

**[Request Header]**

Common/HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |

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

Retrieve the desired one factor information.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors
```

**[Request Header]**

Common/HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
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

Retrieve the number of factor information you want.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors
```

**[Request Header]**

Common/HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
| start | int | mandatory | Where to start the search. Must be less than the total number of factors |
| size | int | mandatory | Search size. Up to 1,000 |

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

### Get User Counts in Factor

The number of registered users at a factor of choice can be searched. 

**[Method, URI]**

```
GET  https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count
```

**[Request Header]**

Check Common/HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | True or false (default is false) <br>For True, search data of a previous cycle |

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
| resultInfo | Object | Result information |
| resultInfo.resultCode | int | Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| resultInfo.totalCount | int | Number of registered users of a factor |

### Get Single User Information

Information of a single user of choice can be searched. 

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Leaderboard Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | User ID |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | True or false (default is false) <br>For True, query data of a previous cycle |

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
	    "totalUserCountInFactor": 200
	}
}
```

| Key | Type | Description |
| --- | --- | --- |
| userInfo | Object | User information |
| userInfo.resultCode | int | Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfo.userId | String | User ID |
| userInfo.score | Double | User scores |
| userInfo.rank | int | Ranking of the current cycle |
| userInfo.preRank | int | Ranking of the previous cycle |
| userInfo.extra | String | Extra data saved along with the user (up to 16 bytes) |
| userInfo.date | String | Updated time of user scores (RFC 3339) |
| userInfo.totalUserCountInFactor | int | Number of registered users of a factor |

### Get Multiple User Information

You can search information of multiple users as required.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | Search data of the previous cycle for True, or of the current cycle for False |
| isSort | bool | optional | Sort by ranks for True, or search data by userId for False |
| userIDsWithFactor | Array[[String, Array[String]]] | mandatory | List of factors and users combined to search |
| userIDsWithFactor[].factor |	int | mandatory | Factor ID to query |
| userIDsWithFactor[].userIds |	Array[String] | mandatory | List of users to search |

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
| userInfosWithFactor | Array[Object] | User information |
| userInfosWithFactor[].resultCode | int | Error code of a factor [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfosWithFactor[].factor | int | Factor ID |
| userInfosWithFactor[].userInfos | Array[Object] | User scores |
| userInfos[].resultCode | int | User code. Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User scores |
| userInfos[].rank | int | Ranking of the current cycle |
| userInfos[].preRank | int | Ranking of the previous cycle |
| userInfos[].extra | String | Extra data saved along with the user (up to 16 bytes) |
| userInfos[].date | String | Updated time of user scores (RFC 3339) |
| userInfos[].totalUserCountInFactor | int | Number of registered users of a factor |

### Get Multiple User Information by Range

You can search ranking information within the range (ranks) of choice.  

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | True or false (default is false) <br>Search data of the previous cycle, if it is True |
| start | int | mandatory | Ranking at start |
| size | int | mandatory | Number of Leaderboard information to import |

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
| userInfosByRange | Array[Object] | User information |
| userInfosByRange[].resultCode | int | Error code of a factor [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfosByRange[].factor | int | Factor ID |
| userInfos[].resultCode | int | User code. Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User scores |
| userInfos[].rank | int | Ranking of the current cycle |
| userInfos[].preRank | int | Ranking of the previous cycle |
| userInfos[].extra | String | Extra data saved along with the user (up to 16 bytes) |
| userInfos[].date | String | Updated time of user scores (RFC 3339) |
| userInfos[].totalUserCountInFactor | int | Number of registered users of a factor |

### Get multiple user info by pivot user

It is a method to retrieve ranking information of the base user and rank information of the upper and lower users.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | True or false (default is false) <br>Search data of the previous cycle, if it is True |
| userId | String | mandatory | Pivot User ID |
| prevSize | int | mandatory | The size of the parent user to view in the base user ranking <br> up to 500 |
| nextSize | int | mandatory | The size of the child user to view in the base user ranking <br> up to 500 |

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
| userInfosByRange | Array[Object] | User information |
| userInfosByRange[].resultCode | int | Error code of a factor [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfosByRange[].factor | int | Factor ID |
| userInfos[].resultCode | int | User code. Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User scores |
| userInfos[].rank | int | Ranking of the current cycle |
| userInfos[].preRank | int | Ranking of the previous cycle |
| userInfos[].extra | String | Extra data saved along with the user (up to 16 bytes) |
| userInfos[].date | String | Updated time of user scores (RFC 3339) |
| userInfos[].totalUserCountInFactor | int | Number of registered users of a factor |

### Get selected rank user info

This is a way to search for users with a specific rank.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | True or false (default is false) <br>Search data of the previous cycle, if it is True |
| userRanks | Array[Integer] | mandatory | User ranking list. Up to 20. |
| isSort | bool | optional | True or false (default is false) <br>Sort by ranks for True, or search data by rank list |

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
| userInfosByRange | Array[Object] | User information |
| userInfosByRange[].resultCode | int | Error code of a factor [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfosByRange[].factor | int | Factor ID |
| userInfos[].resultCode | int | User code. Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User scores |
| userInfos[].rank | int | Ranking of the current cycle |
| userInfos[].preRank | int | Ranking of the previous cycle |
| userInfos[].extra | String | Extra data saved along with the user (up to 16 bytes) |
| userInfos[].date | String | Updated time of user scores (RFC 3339) |
| userInfos[].totalUserCountInFactor | int | Number of registered users of a factor |

<br>

## Set API

### Set Single User Scores

You can register scores of a user of choice. 

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
```

**[Request Header]**

Common/HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey | String | Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
| factor | int | Factor ID |
| userId | String | User ID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long | Required | Transaction ID |
|score|	double | Required | User scores |

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
| resultInfo | Object | Result information |
| resultInfo.resultCode | int | Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| resultInfo.userId | String | Registered user ID |


### Set Single User Scores with Extra Data

You can register scores and extra data of a user of choice. 

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey |	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
| factor | int | Factor ID |
| userId | String | User ID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long |	mandatory | Transaction ID |
| score | double | mandatory | User scores |
| extra | String | optional | Extra data saved along with the user (up to 16 bytes) |

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
| resultInfo | Object | Result information |
| resultInfo.resultCode | int | Error code [\[LINK\]](/Game/Leaderboard/en/error-code) |
| resultInfo.userId | String | Registered user ID |

### Set Multiple User Scores

You can register scores of multiple users of choice. 

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | Transaction ID |
| userScoresWithFactor | Array[Object] | mandatory | List of user scores and factors |
| userScoresWithFactor[].factor | int | mandatory | Factor ID to register |
| userScoresWithFactor[].userScores | Array[Object] | mandatory | List of User IDs and scores to register |
| userScores[].userId | String | mandatory | User ID |
| userScores[].score | double | mandatory | User scores |

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
| resultInfosWithFactor | Array[Object] | Result information |
| resultInfosWithFactor[].resultCode | int | Error code of a factor [\[LINK\]](/Game/Leaderboard/en/error-code) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | Result information of a registered user |
| resultInfos.resultCode | int | Error code of a user |
| resultInfos.userId | String | Registered User ID |

### Set Multiple User Scores with Extra Data

User scores can be registered as required, along with extra data. 

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores-with-extra
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | Transaction ID |
| userInfosWithFactor | Array[Object] | mandatory | List of user scores and factors |
| userInfosWithFactor[].factor | int | mandatory | Factor ID to register ID |
| userInfosWithFactor[].userInfos | Array[Object] | mandatory | List of User IDs and scores to register |
| userInfos[].userId | String | mandatory | User ID |
| userInfos[].score | double | mandatory | User Scores |
| userInfos[].extra | String | optional | Extra data saved along with the user (up to 16 bytes) |

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
| resultInfosWithFactor | Array[Object] | Result information |
| resultInfosWithFactor[].resultCode | int | Error code of a factor [\[LINK\]](/Game/Leaderboard/en/error-code) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | Result information of a registered user |
| resultInfos.resultCode | int | Error code of a user |
| resultInfos.userId | String | Registered user ID |

<br>

## Delete API

### Delete Single User Information

Information of a user of choice can be deleted: the user information is permanently deleted and cannot be recovered. 

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Check Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | User ID |
| transactionId | long | optional | Transaction ID |
| isPast | bool | optional | True or false (default is false) <br>Delete data of the previous cycle, if it is true. |

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

### Delete multiple user info

Information of user list of choice can be deleted: user list information is permanently deleted and cannot be recovered.

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header [\[LINK\]](/Game/Leaderboard/en/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/en/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | Transaction ID |
| userIds | Array[Object] | mandatory | User ID List. Up to 20. |
| isPast | bool | optional | True or false (default is false) <br>Delete data of the previous cycle, if it is true. |


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