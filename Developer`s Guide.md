## Game > LeaderBoard > Developer's Guide

Leaderboard API 는 REST API 형태로 다음 3가지 종류를 제공합니다.

#### Leaderboard 조회

- 단일/다수 사용자 점수, 순위 조회
- 일정 범위의 전체 점수, 순위 조회

#### Leaderboard 등록

- 단일/다수 사용자 점수 등록

#### Leaderboard 삭제

- 단일/모든 사용자 Leaderboard 정보 삭제

> [주의]  
> API 사용을 하기 위해서는 팩터를 등록해야 합니다.  

## Leaderboard 조회

### 단일 사용자 점수/순위 조회

원하는 한 명의 사용자의 Leaderboard 정보를 조회할 수 있는 방법입니다.

[URL]

```
GET https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userId}/rank-info
```

[표 1] 단일 사용자 점수/순위 조회 URL 파라미터

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	Leaderboard AppKey|
|factor|	Int|	Leaderboard 팩터|
|userid|	String|	사용자 ID|

[표 2] 단일 사용자 점수/순위 조회 Query 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionid|	Int64|	트랜잭션 ID|
|ispast|	Bool|	이전 Leaderboard 포함 여부 (입력하지 않을 시, 기본값은 False)|

[Example Request]

```
GET https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}/rank-info?transactionid=12345&ispast=false
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
		},

		"factor": 1,
		"userId": "user1234",
		"score": 1000,
		"rank": 2,
		"rankChange": 0,
		"lastUpdate": 1408599041
}
```

### 다수 사용자 점수/순위 조회

여러 사용자 Leaderboard 정보를 조회할 수 있는 방법입니다.

[URL]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/${appkey}/rank-infos/get
```

[표 3] 다수 사용자 점수/순위 조회 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|isPast|	Bool|	이전 Leaderboard 포함 여부 (입력하지 않을 시, 기본값은 False)|
|userlist|	Vector|	조회를 원하는 유저 리스트|

[Example Request]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/${appkey}/rank-infos/get
Content-Type: application/json
{
        "transactionId": 12345,
        "isPast": false,
        "users": [
            {
                "factor": 1,
                   "userIDList" : ["user1000", "user1001", "user1002"]            
            },
            {
                "factor": 2,
                   "userIDList" : ["user2000", "user2001", "user2002"]            
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
			"transactionId": 12345,
			"isSuccessful": true,
			"resultCode": 200,
			"resultMessage": "OK",
			"serviceCode": 1
		},
		"rankInfos": [
			{
			"factor": 1,
				"totalSize" : 2,
   				"userRankInfoList" : [
    					{
     						"userId" : "user1000",
     						"score" : 1200,
    						"rank" : 1,
     						"rankChange" : 0,
     						"lastUpdate" : 1408599041
   					},
    					{
     						"userId" : "user1001",
     						"score" : 1100,
    						"rank" : 2,
     						"rankChange" : 0,
     						"lastUpdate" : 1408599042
   					}
				]			
			},
			{
			"factor": 2,
				"totalSize" : 1,
   				"userRankInfoList" : [
    					{
     						"userId" : "user2000",
     						"score" : 2200,
    						"rank" : 1,
     						"rankChange" : 0,
     						"lastUpdate" : 1408599041
   					}					
				]			
			}
		]
}
```

### 일정 범위의 전체 점수/순위 조회

전체 순위 중에서 원하는 범위의 순위 정보를 조회할 수 있는 방법입니다.

[URL]

```
GET https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/rank-infos
```

[표 4] 일정 범위의 전체 점수/순위 조회 URL 파라미터

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	Leaderboard AppKey|
|factor|	Int|	팩터|

[표 5] 일정 범위의 전체 점수/순위 조회 Query 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionid|	Int64|	트랜잭션 ID|
|ispast|	Bool|	이전 Leaderboard 포함 여부 (입력하지 않을 시, 기본값은 False)|
|start|	Int|	시작 순위|
|size|	Int|	가져올 Leaderboard 정보의 개수|

[Example Request]

```
GET https://api-ranking.cloud.toast.com/ranking/v3/api/ appkey/{appkey}/factors/{factor}/rank-infos?transactionid=12345&ispast=false&start=1&size=3
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
	},
	"userRankInfoList": [
			{

				   "factor": 1,
				   "userId": "user0000",
				   "score": 1100,
				   "rank": 1,
				   "rankChange": 0,
				   "lastUpdate": 1408599990
			},
			{

				   "factor": 1,
				   "userId": "user1234",
				   "score": 1000,
				   "rank": 2,
				   "rankChange": 0,
				   "lastUpdate": 1408599041
			},
			{

				   "factor": 1,
				   "userId": "user0001",
				   "score": 900,
				   "rank": 3,
				   "rankChange": 0,
				   "lastUpdate": 1408589468
			}
	],
	"totalSize": 1000
}
```

## Leaderboard 등록

### 단일 사용자 점수 등록

원하는 한 명의 사용자 점수를 등록할 수 있는 방법입니다.

[URL]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}/score
```

[표 6] 단일 사용자 점수 등록 URL 파라미터

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	Leaderboard AppKey|
|factor|	Int|	팩터|
|userid|	String|	사용자 ID|

[표 7] 단일 사용자 점수 등록 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|score|	Int64|	사용자 점수|

[Example Request]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}/score
Content-Type: application/json

{
		"transactionId": 12345,
		"score": 1005
}
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

### 다수 사용자 Leaderboard 등록

원하는 사용자들 점수를 등록할 수 있는 방법입니다.

[URL]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/${appkey}/scores
```

[표 8] 다수 사용자 Leaderboard 등록 Body 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionId|	Int64|	트랜잭션 ID|
|scores|	Vector|	사용자 점수 리스트|

[Example Request]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/${appkey}/scores

Content-Type: application/json
{
    "transactionId": 12345,
    "scores": [
    {
        "factor": 1,
        "userScoreList" : [
        {
            "userId": "user1000",
            "score": 1200
        },
        {
            "userId": "user1001",
            "score": 1100
        }
        ]
    },
    {
        "factor": 1,
        "userScoreList" : [
        {
            "userId": "user1000",
            "score": 1200
        }
        ]
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
				"transactionId": 12345,
				"isSuccessful": true,
				"resultCode": 200,
				"resultMessage": "OK",
				"serviceCode": 1
		}
}
```

## Leaderboard 삭제

### 단일 사용자 Leaderboard정보 삭제

원하는 한 명의 사용자 Leaderboard정보를 삭제하는 방법입니다. 입력한 사용자 Leaderboard 정보가 삭제됩니다. 모든 팩터 삭제를 원하는 경우, factor 값에 -1을 입력해서 요청합니다.

[URL]

```
DELETE https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}
```

[표 9] 다수 사용자 Leaderboard 삭제 URL 파라미터

|이름|	자료형|	설명|
|---|---|---|
|appkey|	String|	Leaderboard Service AppKey|
|Factor|	Int|	팩터|
|userid|	String|	사용자 ID|

[표 10] 다수 사용자 Leaderboard 삭제 Query 파라미터

|이름|	자료형|	설명|
|---|---|---|
|transactionid|	Int64|	트랜잭션 ID|
|ispast|	Bool|	이전 Leaderboard 포함 여부 (입력하지 않을 시, 기본값은 False)|

[Example Request]

```
DELETE https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}?transactionid=12345&ispast=false
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

## 에러 코드

[표 11]의 에러 코드는 Response body의 header에 있는 resultCode와 resultMessage의 의미를 설명합니다.  

[표 11] 에러 코드  

|Result Code|	설명|
|---|---|
|200|	OK : 요청 성공|
|400|	Bad Request : 잘못된 요청일 경우|
|401|	Unauthorized : 유효하지 않은 Leaderboard AppKey일 경우|
|404|	Not Found : 요청한 리소스를 찾을 수 없을 경우|
|501|	Not Implemented : 데이터가 존재하지 않을 경우|

> [참고]  
> HTTP 상태 코드가 400일 경우, API 형식에 맞지 않을 때 발생합니다.   
> HTTP 상태 코드는 200이고 결과 코드가 400일 경우, 요청이 API 형식에는 맞으나 값이 잘못되었을 때 발생합니다.  
> 그 외 일반적인 에러 코드에 대한 추가 정보는 다음 링크에서 확인하기 바랍니다.   
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml  
