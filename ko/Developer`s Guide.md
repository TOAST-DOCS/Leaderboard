## Game > Leaderboard > Developer's Guide

Leaderboard API 는 REST API 형태로 다음과 같은 API 를 제공합니다.

### HTTP API
- 유져 점수 등록 (단일 / 다수)
- 유져 점수 획득 (단일 / 다수 / 범위)
- 팩터에 들어있는 사용자 수 조회
- 유져 점수 삭제 (단일)

## Notice

### Caution
- 모든 API 사용을 하기 위해서는 **상품 활성화 후 팩터를 등록**해야 합니다.  
- Leaderboard API 는 **Server에서 호출 하는 것을 권장**하고, Client 에서의 호출은 권장하고 있지 않습니다.

### Server Address
서버 API 를 호출 하기 위한 서버 주소는 다음과 같습니다. 해당 주소는 Leaderboard 콘솔 화면에서도 확인 가능합니다.

![그림 1 Server Address](http://static.toastoven.net/prod_leaderboardv2/developer_1.jpg)

### AppKey
AppKey 는 게임 서버에서 요청을 보낼시 꼭 필요한 고유 키로, Leaderboard 콘솔 화면에서 확인 가능합니다.

![그림 2 AppKye](http://static.toastoven.net/prod_leaderboardv2/developer_2.jpg)

### TransactionId
API 를 호출하는 서버에서 내부적으로 API 요청을 관리할 수 있는 방안으로 TransactionId 기능을 제공합니다.
호출하는 서버에서 HTTP Body 에 TransactionId 를 설정하여 API 를 호출하면, Leaderboard 서버는 응답 결과에 해당 TransactionId 를 설정하여 결과를 전달합니다. TransactionId 는 정수형 타입으로 받습니다.

## Comon

### HTTP Header
API 호출 시 HTTP Header 에 다음 항목을 설정해야 합니다.
| Name | Required |	Value |
|---|---|---|
| Content-Type | mandatory | application/json; charset=UTF-8 |

### API Response
모든 API 요청에 대한 응답으로 HTTP 200 OK 를 전달합니다. API 요청 성공 유무는 Response Body 의 header 항목을 참고하여 판단할 수 있습니다.

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

## Get API

### Get user count in factor

원하는 한개의 Factor 에 등록된 사용자의 수 를 조회합니다.

**[Method, URI]**

```
GET  https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/user-count?transactionid={transactionid}&ispast={ispast} 
```

**[Request Header]**

Common / HTTP Header 확인 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#common)

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|
|factor|	Int|	Leaderboard 팩터|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| transactionid | long | optional | 트랜잭션 ID |
| ispast | bool | optional | true or false (기본값은 false) <br> 이전 주기 조회 여부 

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
| resultInfo | Object | 결과 정보 |
| resultInfo.resultCode | int | 에러코드 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#error%20codes) |
| resultInfo.totalCount | int | Factor 에 등록된 사용자 수 |

### Get single user info

원하는 한 명의 사용자의 정보를 조회할 수 있습니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userId}&transactionid={transactionid}&ispast={ispast} 
```

**[Path Variable]**

| Name | Type |	Value |
|---|---|---|
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|
|factor|	Int|	Leaderboard 팩터|

**[Request Parameter]**

| Name | Type | Required |  Value |
| --- | --- | --- | --- |
| userId | String |	mandatory | 사용자 ID |
| transactionid | long | optional | 트랜잭션 ID |
| ispast | bool | optional | true or false (기본값은 false) <br> 이전 주기 조회 여부 |

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
| userInfo | Object | 유져 정보 |
| userInfo.resultCode | int | 에러코드 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#error%20codes) |
| userInfo.userId | String | User ID |
| userInfo.score | Double | User Score |
| userInfo.rank | int | 이번 주기의 순위 |
| userInfo.preRank | int | 이전 주기의 순위 |
| userInfo.extra | String | User 와 함께 저장되는 Extra Data (최대 16Byte) |
| userInfo.date | String | User Score 가 업데이트 된 시간. (RFC 3339) |

### Get multiple user info

원하는 다수의 사용자 정보를 조회할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/get-users
```

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|

**[Request Body]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionId |	long |	mandatory | 트랜잭션 ID |
| isPast | bool | mandatory | 이전 Leaderboard 포함 여부 (입력하지 않을 시, 기본값은 False)|
| userIDsWithFactor | Array[[String, Array[String]]] | mandatory | 조회를 원하는 팩터와 User 리스트 묶음 |
| userIDsWithFactor[].factor |	int | mandatory | 조희를 원하는 팩터 |
| userIDsWithFactor[].userIds |	Array[String] | mandatory | 조회를 원하는 User 리스트 |

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
| userInfosWithFactor | Array[Object] | 유져들의 정보 |
| userInfosWithFactor[].resultCode | int | 팩터에 대한 에러코드 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#error%20codes) |
| userInfosWithFactor[].factor | int | 팩터 |
| userInfosWithFactor[].userInfos | Array[Object] | User Score |
| userInfos[].resultCode | int | 해당 User에 대한 코드. 에러코드 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#error%20codes) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User Score |
| userInfos[].rank | int | 이번 주기의 순위 |
| userInfos[].preRank | int | 이전 주기의 순위 |
| userInfos[].extra | String | User 와 함께 저장되는 Extra Data (최대 16Byte) |
| userInfos[].date | String | User Score 가 업데이트 된 시간. (RFC 3339) |

### Get multiple user info by range

원하는 범위(등수)의 순위 정보를 조회할 수 있는 방법입니다.

**[Method, URI]**

```
GET https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?transactionid={transactionid}&ispast={ispast}&start={start}&size={size} 
```

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|
|factor|	int|	팩터|

**[Request Parameter]**

| Name | Type | Required | Value |
| --- | --- | --- | --- |
| transactionid | long | optional | 트랜잭션 ID |
| ispast | bool | optional | true or false (기본값은 false) <br> 이전 주기 조회 여부 |
| start | int | mandatory | 시작 순위|
| size | int | mandatory | 가져올 Leaderboard 정보의 개수|

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
| userInfosByRange | Array[Object] | 유져들의 정보 |
| userInfosByRange[].resultCode | int | 팩터에 대한 에러코드 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#error%20codes) |
| userInfosByRange[].factor | int | 팩터 |
| userInfos[].resultCode | int | 해당 User에 대한 코드. 에러코드 [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#error%20codes) |
| userInfos[].userId | String | User ID |
| userInfos[].score | double | User Score |
| userInfos[].rank | int | 이번 주기의 순위 |
| userInfos[].preRank | int | 이전 주기의 순위 |
| userInfos[].extra | String | User 와 함께 저장되는 Extra Data (최대 16Byte) |
| userInfos[].date | String | User Score 가 업데이트 된 시간. (RFC 3339) |

## Set API

### Set single user score

원하는 한 명의 사용자 점수를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
```

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|
|factor|	Int|	팩터|
|userId|	String|	사용자 ID|

[표 7] 단일 사용자 점수 등록 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|score|	Int64|	사용자 점수|

[Example Request]

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score
Content-Type: application/json

{
	"score": 10,
	"transactionId": 1234
}
```

[Example Response]

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


### Set single user score with extra data

원하는 한 명의 사용자 점수와 Extra Data를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
```

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|
|factor|	Int|	팩터|
|userId|	String|	사용자 ID|

[표 7] 단일 사용자 점수 등록 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|score|	Double|	사용자 점수|
|extra|	String|	사용자 Extra Data (최대 16Byte)|

[Example Request]

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users/{userId}/score-with-extra
Content-Type: application/json

{
	"extra": "extraData",
	"score": 200,
	"transactionId": 1234
}
```

[Example Response]

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

### Set multiple user score

원하는 사용자들 점수를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores
```

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|

[표 8] 다수 사용자 Leaderboard 등록 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|userScoresWithFactor|	List|	사용자 점수 리스트와 팩터의 리스트|
|factor | Int| 등록을 원하는 팩터|
|userScores| List| 등록을 원하는 사용자 ID/점수의 리스트|
|userId | String | 사용자 ID |
|score | Double | 사용자 점수 |

[Example Request]

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

[Example Response]

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

### 다수 사용자 점수/ExtraData 등록

원하는 사용자들 점수와 Extra Data를 등록할 수 있는 방법입니다.

**[Method, URI]**

```
POST https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/scores-with-extra
```
**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|


[표 8] 다수 사용자 Leaderboard 등록 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|userScoresWithFactor|	List|	사용자 점수 리스트와 팩터의 리스트|
|factor | Int| 등록을 원하는 팩터|
|userScores| List| 등록을 원하는 사용자 ID/점수의 리스트|
|userId | String | 사용자 ID |
|score | Double | 사용자 점수 |
|extra | String | 사용자 Extra Data (최대 16Byte) |

[Example Request]

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

[Example Response]

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

## Leaderboard 삭제

### 단일 사용자 Leaderboard정보 삭제

원하는 한 명의 사용자 Leaderboard정보를 삭제하는 방법입니다. 입력한 사용자 Leaderboard 정보가 삭제됩니다. 

**[Method, URI]**

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users
```

**[Path Variable]**

| Name | Type | Value |
| --- | --- | --- |
|appkey|	String|	Leaderboard AppKey [\[LINK\]](/Game/Leaderboard/ko/Developer%60s%20Guide/#appkey)|
|Factor|	Int|	팩터|

[표 10] 다수 사용자 Leaderboard 삭제 Query 파라미터

|이름|	자료형|	설명|
|---|---|---|
|userid|	String|	사용자 ID|
|transactionid|	Int64|	트랜잭션 ID|
|ispast|	Bool|	이전 Leaderboard 포함 여부 (입력하지 않을 시, 기본값은 False)|

[Example Request]

```
DELETE https://api-leaderboard.cloud.toast.com/leaderboard/v2.0/appkeys/{appkey}/factors/{factor}/users?userId={userid}?transactionid=12345&ispast=false
```

[Example Response]

```
HTTP/1.1 200 OK
Content-Type: application/json

{
		"header": {
			"transactionId": 12345,
			"isSuccessful": true,
			"resultCode": 200,
			"resultMessage": "OK",
			"serviceCode": 1
		}
}
```

## Time

사용자의 업데이트 시간은 RFC 3339 정의를 따릅니다.

> https://tools.ietf.org/html/rfc3339

## Error Codes

[표 11]의 에러 코드는 Response body의 header/body에 있는 resultCode와 resultMessage의 의미를 설명합니다.  
header 에 있는 resultCode 에서 아래의 에러코드가 아닌  HTTP 에러 코드가 보이는 경우는 아래 [참고] 링크를 참고 부탁드립니다.

[표 11] 에러 코드  

|Result Code| Result Code(Hex) | Result Message |설명|
|---|---|---|---|
|0|	0x00000000 |LEADERBOARD_SUCCESS | 요청 성공.|
|1|	0x00000001 |LEADERBOARD_SUCCESS_BUT_NOT_UPDATE | 요청은 성공 했지만, 기존과 동일한 데이터가 들어와서 업데이트 하지 않음.|
|459777|	0x00070401 |LEADERBOARD_ERROR_APPKEY_VERIFIER | 앱키 인증 실패. |
|462849|	0x00071001 |LEADERBOARD_AP_ERROR_INITIALTIZE | 초기화 실패. |
|462850|	0x00071002 |LEADERBOARD_AP_ERROR_NOT_EXIST_USER | 등록되지 않은 사용자. |
|462851|	0x00071003 |LEADERBOARD_AP_ERROR_NOT_EXIST_FACTOR | 등록되지 않은 팩터.|
|462852|	0x00071004 |LEADERBOARD_AP_ERROR_NOT_EXIST_APPKEY | 등록되지 않은 앱키. |
|462853|	0x00071005 |LEADERBOARD_AP_ERROR_TOO_BIG_EXTRA | Extra Data 제한 길이 초과. |
|462854|	0x00071006 |LEADERBOARD_AP_ERROR_WRONG_RANGE | 잘못된 범위. |
|462855|	0x00071007 |LEADERBOARD_AP_ERROR_WRONG_PARAM | 잘못된 파라메터. |
|463000|	0x00071098 |LEADERBOARD_AP_ERROR_SYSTEM | 시스템 에러.|
|463001|	0x00071099 |LEADERBOARD_AP_ERROR_UNKOWN | 미확인 에러.|


> [참고]  
> 그 외 일반적인 에러 코드에 대한 추가 정보는 다음 링크에서 확인하기 바랍니다.   
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml  




