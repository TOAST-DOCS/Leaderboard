## Game > Leaderboard > API 가이드

> **[유의 사항]**<br>
> 게임베이스를 통해 자동 활성화 된 리더보드는 아래의 이용 가이드를 참고해야 합니다.<br>
> [\[Gamebase api guide\]](/Game/Gamebase/ko/api-guide/#leaderboard)

Leaderboard API는 REST API 형태로, 다음과 같은 API를 제공합니다.

### HTTP API
- 유저 점수 등록(단일 / 다수)
- 유저 점수 획득(단일 / 다수 / 범위 / 특정유저 전후)
- 팩터에 있는 유저 수 검색
- 유저 점수 삭제(단일)

<br>

## 사전 준비
서버 API를 사용하기 위해서는 다음의 정보들을 알고 있어야 합니다.  

### Server Address
서버 API 호출 서버 주소는 다음과 같습니다. 해당 주소는 Leaderboard 콘솔에서도 확인할 수 있습니다.<br>

> https://api-leaderboard.cloud.toast.com

![그림 1 Server Address](http://static.toastoven.net/prod_leaderboardv2/renewal/api_guide_202106_1-1.PNG)

### AppKey
앱키는 게임 서버에서 요청을 보낼 때 꼭 필요한 고유 키로, 콘솔에서 확인할 수 있습니다.
> [주의] 앱키는 외부에 노출하면 안 되며, 변경할 수 없습니다.

![그림 2 AppKey](http://static.toastoven.net/prod_leaderboardv2/renewal/api_guide_202106_2-1.PNG)

### 주의 사항
모든 API를 사용하려면 **서비스 활성화 후 팩터를 등록**해야 합니다.  
Leaderboard API는 **클라이언트에서 호출 시 어뷰징 등의 위험이 있어 서버에서만 호출하는 것을 권장합니다.**

<br>

## 공통

### HTTP Header
API를 호출할 때 HTTP Header에 다음 항목을 설정해야 합니다.

| Name | Required |	Value |
|---|---|---|
| Content-Type | mandatory | application/json; charset=UTF-8 |

### API Response
모든 API 요청 응답으로 HTTP 200 OK를 전달합니다. API 요청 성공 유무는 Response Body의 header 항목을 참고하여 판단할 수 있습니다.

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
API를 호출하는 서버에서 내부적으로 API 요청을 관리할 수 있는 방안으로 TransactionId 기능을 제공합니다.
호출하는 서버에서 HTTP Body에 TransactionId를 설정하여 API를 호출하면, Leaderboard 서버는 응답 결과에 해당 TransactionId를 설정하여 결과를 전달합니다. TransactionId는 정수형 타입으로 받습니다.

### Time

유저의 업데이트 시간은 RFC 3339 정의를 따릅니다.

> https://tools.ietf.org/html/rfc3339

<br>

## Get API

### Get total factor count

팩터의 전체 수를 검색합니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factor-count
```

**[Request Header]**

Common/HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |

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

원하는 한 개의 팩터 정보를 검색합니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors
```

**[Request Header]**

Common/HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| factor | int | mandatory | 팩터 ID |

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

원하는 다수의 팩터 정보를 검색합니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors
```

**[Request Header]**

Common/HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| start | int | mandatory | 검색 시작 위치. 전체 팩터 수 보다 작아야함 |
| size | int | mandatory | 검색 크기. 최대 1,000까지 |

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

원하는 한 개의 팩터에 등록된 유저의 수를 검색합니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count
```

**[Request Header]**

Common/HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| isPast | bool | optional | true 또는 false(기본값은 false) <br> true이면 이전 주기의 데이터 검색 |

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
| resultInfo | Object | 결과 정보 |
| resultInfo.resultCode | int | 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| resultInfo.totalCount | int | 팩터에 등록된 유저 수 |

### Get single user info

원하는 한 명의 유저의 정보를 검색할 수 있습니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | 유저 ID |
| transactionId | long | optional | 트랜잭션 ID |
| isPast | bool | optional | true 또는 false(기본값은 false) <br> true이면 이전 주기의 데이터 조회 |

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
| userInfo | Object | 유저 정보 |
| userInfo.resultCode | int | 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfo.userId | String | 유저 ID |
| userInfo.score | Double | 유저 점수 |
| userInfo.rank | int | 이번 주기의 순위 |
| userInfo.preRank | int | 이전 주기의 순위 |
| userInfo.extra | String | 유저와 함께 저장되는 Extra Data(최대 16바이트) |
| userInfo.date | String | 유저 점수가 업데이트된 시간(RFC 3339) |
| userInfo.totalUserCountInFactor | int | 팩터에 등록된 유저 수 |

### Get multiple user info

원하는 다수의 유저 정보를 검색할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| isPast | bool | optional | true이면 이전 주기, false이면 현재 주기의 데이터 검색 |
| isSort | bool | optional | true이면 등수 기준 정렬, false이면 입력한 userId순으로 데이터 검색 |
| userIDsWithFactor | Array[[String, Array[String]]] | mandatory | 검색을 원하는 Factor와 유저 목록 묶음 |
| userIDsWithFactor[].factor |	int | mandatory | 조희를 원하는 Factor ID|
| userIDsWithFactor[].userIds |	Array[String] | mandatory | 검색을 원하는 유저 목록 |

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
| userInfosWithFactor | Array[Object] | 유저 정보 |
| userInfosWithFactor[].resultCode | int | 팩터의 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfosWithFactor[].factor | int | Factor ID |
| userInfosWithFactor[].userInfos | Array[Object] | 유저 점수 |
| userInfos[].resultCode | int | 해당 유저의 코드. 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfos[].userId | String | 유저 ID |
| userInfos[].score | double | 유저 점수 |
| userInfos[].rank | int | 이번 주기의 순위 |
| userInfos[].preRank | int | 이전 주기의 순위 |
| userInfos[].extra | String | 유저와  함께 저장되는 Extra Data(최대 16바이트) |
| userInfos[].date | String | 유저 점수가 업데이트된 시간(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | 팩터에 등록된 유저 수 |

### Get multiple user info by range

원하는 범위(등수)의 순위 정보를 검색할 수 있는 방법입니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| isPast | bool | optional | true 또는 false (기본값은 false) <br> true이면 이전 주기의 데이터 검색 |
| start | int | mandatory | 시작 순위|
| size | int | mandatory | 가져올 Leaderboard 정보의 개수|

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
| userInfosByRange | Array[Object] | 유저 정보 |
| userInfosByRange[].resultCode | int | 팩터의 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfosByRange[].factor | int | 팩터 ID |
| userInfos[].resultCode | int | 해당 유저의 코드. 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfos[].userId | String | 유저 ID |
| userInfos[].score | double | 유저 점수 |
| userInfos[].rank | int | 이번 주기의 순위 |
| userInfos[].preRank | int | 이전 주기의 순위 |
| userInfos[].extra | String | 유저와 함께 저장되는 Extra Data(최대 16바이트) |
| userInfos[].date | String | 유저 점수가 업데이트된 시간(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | 팩터에 등록된 유저 수 |

### Get multiple user info by pivot user

기준 유저의 순위 및 상위, 하위 유저들의 순위 정보를 검색할 수 있는 방법입니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| isPast | bool | optional | true 또는 false (기본값은 false) <br> true이면 이전 주기의 데이터 검색 |
| userId | String | mandatory | 기준 유저 ID|
| prevSize | int | mandatory | 기준 유저 순위에서 조회 할 상위 유저 크기 <br> 최대 500 |
| nextSize | int | mandatory | 기준 유저 순위에서 조회 할 하위 유저 크기 <br> 최대 500 |

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
| userInfosByRange | Array[Object] | 유저 정보 |
| userInfosByRange[].resultCode | int | 팩터의 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfosByRange[].factor | int | 팩터 ID |
| userInfos[].resultCode | int | 해당 유저의 코드. 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfos[].userId | String | 유저 ID |
| userInfos[].score | double | 유저 점수 |
| userInfos[].rank | int | 이번 주기의 순위 |
| userInfos[].preRank | int | 이전 주기의 순위 |
| userInfos[].extra | String | 유저와 함께 저장되는 Extra Data(최대 16바이트) |
| userInfos[].date | String | 유저 점수가 업데이트된 시간(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | 팩터에 등록된 유저 수 |

### Get selected rank user info

특정 순위의 유저들을 검색 할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | optional | 트랜잭션 ID |
| isPast | bool | optional | true 또는 false (기본값은 false) <br> true이면 이전 주기의 데이터 검색 |
| userRanks | Array[Integer] | mandatory | 유저 순위 목록. 최대 20개 까지. |
| isSort | bool | optional | true 또는 false (기본값은 false) <br> true이면 순위대로 정렬, false이면 순위 목록대로 유지 |

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
| userInfosByRange | Array[Object] | 유저 정보 |
| userInfosByRange[].resultCode | int | 팩터의 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfosByRange[].factor | int | 팩터 ID |
| userInfos[].resultCode | int | 해당 유저의 코드. 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| userInfos[].userId | String | 유저 ID |
| userInfos[].score | double | 유저 점수 |
| userInfos[].rank | int | 이번 주기의 순위 |
| userInfos[].preRank | int | 이전 주기의 순위 |
| userInfos[].extra | String | 유저와 함께 저장되는 Extra Data(최대 16바이트) |
| userInfos[].date | String | 유저 점수가 업데이트된 시간(RFC 3339) |
| userInfos[].totalUserCountInFactor | int | 팩터에 등록된 유저 수 |

<br>

## Set API

### Set single user score

원하는 한 명의 유저 점수를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
```

**[Request Header]**

Common/HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey | String | Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
| factor | int | 팩터 ID |
| userId | String | 유저 ID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long | 필수 | 트랜잭션 ID |
|score|	double | 필수 | 유저 점수 |

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
| resultInfo | Object | 결과 정보 |
| resultInfo.resultCode | int | 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| resultInfo.userId | String | 등록된 유저 ID |

### Set single user score with extra data

원하는 한 명의 유저 점수와 Extra Data를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
| appkey |	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
| factor | int | 팩터 ID |
| userId | String | 유저 ID |

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long |	mandatory | 트랜잭션 ID |
| score | double | mandatory | 유저 점수 |
| extra | String | optional | 유저와 함께 저장되는 Extra Data(최대 16바이트) |

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
| resultInfo | Object | 결과 정보 |
| resultInfo.resultCode | int | 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| resultInfo.userId | String | 등록된 유저 ID |

### Set multiple user score

원하는 유저들 점수를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | 트랜잭션 ID |
| userScoresWithFactor | Array[Object] | mandatory | 유저 점수 목록과 Factor의 목록 |
| userScoresWithFactor[].factor | int | mandatory | 등록을 원하는 Factor ID |
| userScoresWithFactor[].userScores | Array[Object] | mandatory | 등록을 원하는 유저 ID와 점수 목록 |
| userScores[].userId | String | mandatory | 유저 ID |
| userScores[].score | double | mandatory | 유저 점수 |

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
| resultInfosWithFactor | Array[Object] | 결과 정보 |
| resultInfosWithFactor[].resultCode | int | 팩터의 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | 등록된 유저의 결과 정보 |
| resultInfos.resultCode | int | 유저에 대한 오류 코드 |
| resultInfos.userId | String | 등록된 유저 ID |

### Set multiple user score with extra data

원하는 유저 점수와 Extra Data를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores-with-extra
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | 트랜잭션 ID |
| userInfosWithFactor | Array[Object] | mandatory | 유저 점수 목록과 Factor 목록 |
| userInfosWithFactor[].factor | int | mandatory | 등록을 원하는 Factor ID |
| userInfosWithFactor[].userInfos | Array[Object] | mandatory | 등록을 원하는 유저 ID와 점수 목록 |
| userInfos[].userId | String | mandatory | 유저 ID |
| userInfos[].score | double | mandatory | 유저 점수 |
| userInfos[].extra | String | optional | 유저와 함께 저장되는 Extra Data(최대 16바이트) |

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
| resultInfosWithFactor | Array[Object] | 결과 정보 |
| resultInfosWithFactor[].resultCode | int | 팩터의 오류 코드 [\[LINK\]](/Game/Leaderboard/ko/error-code) |
| resultInfosWithFactor[].factor | int | Factor ID |
| resultInfosWithFactor[].resultInfos | Array[Object] | 등록된 유저의 결과 정보 |
| resultInfos.resultCode | int | 유저에 대한 오류 코드 |
| resultInfos.userId | String | 등록된 유저 ID |

<br>

## Delete API

### Delete single user info

원하는 유저 한 명의 정보를 삭제하는 방법입니다. 해당 유저는 영구적으로 삭제되며, 복구되지 않습니다.

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| isPast | bool | optional | true 또는 false(기본값은 false) <br> true이면 이전 주기의 데이터 삭제 |

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

원하는 유저 여러 명의 정보를 삭제하는 방법입니다. 해당 유저는 영구적으로 삭제되며, 복구되지 않습니다.

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/api-guide/#http-header)

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/api-guide/#appkey)|
|factor|	int|	Factor ID|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId | long | mandatory | 트랜잭션 ID |
| userIds | Array[Object] | mandatory | 유저 ID 목록. 최대 20개까지. |
| isPast | bool | optional | true 또는 false(기본값은 false) <br> true이면 이전 주기의 데이터 삭제 |


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