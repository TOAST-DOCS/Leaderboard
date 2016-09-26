## Game > LeaderBoard > Getting Started

Leaderboard 를 사용하기 위해서는 상품 구매 후 팩터를 등록해야 합니다.
상품 구매 후에는 플레이어의 랭킹 정보에 대한 등록, 조회, 삭제를 할 수 있습니다.

## 사용 설정

### Leaderboard 서비스 활성화

Console에서 [Game] > [Leaderboard]를 선택한 후 [상품이용] 버튼을 클릭하면 서비스가 활성화되어 상품소개에서 관리화면으로 전환됩니다.

![[그림 1 Leaderboard 서비스 활성화]](http://static.toastoven.net/prod_leaderboard/rank_8.jpg)
<center>[그림 1 Leaderboard 서비스 활성화]</center>

### 팩터 추가

서비스 활성화 후에는 팩터 정보를 추가해야 합니다. [Game] > [Leaderboard] > [랭킹 설정] > [+추가] 버튼을 클릭하여 팩터를 등록합니다.

> [참고]  
> 팩터(Factor)는 [주기,업데이트 기준 ,정렬기준]의 묶은 단위입니다. 예를 들어 최고점수 랭킹을 일간, 주간, 월간으로 사용하고 싶다면 팩터를 3가지를 만들어야 합니다.

![[그림 2 팩터 등록을 위하여 [+추가] 클릭]](http://static.toastoven.net/prod_leaderboard/rank_9.jpg)
<center>[그림 2 팩터 등록을 위하여 [+추가] 클릭]</center>

[+추가] 버튼을 클릭하면 그림 3과 같은 <팩터 추가> 대화창이 팝업 됩니다.

![[그림 3 팩터 추가]](http://static.toastoven.net/prod_leaderboard/rank_10.jpg)
<center>[그림 3 팩터 추가]</center>

팩터 등록 예로 주간최고 점수를 등록해 보겠습니다.

#### 랭킹 업데이트 기준

- 높은 점수를 업데이트 하도록 [Higher Score Only]를 선택합니다.

#### 정렬 기준

- 점수가 높을 수록 순위가 올라가야 하므로 내림차순인 [Desc]를 선택합니다.

#### 팩터 주기

- [Weekly]를 선택합니다.

#### 팩터 주간 리셋 시간

- 매주 월요일에 리셋하도록 [월요일]을 선택합니다.

#### 설명

- “주간최고점수”로 입력한 후 [팩터 추가] 버튼을 클릭합니다.

## 서비스 이용

서비스 활성화 단계를 거친 후에는 플레이어의 랭킹 정보를 등록, 조회, 삭제 등을 할 수 있습니다. 랭킹 정보 액세스 API에서 사용하는 주요 파라미터는 표 1과 같습니다.

[표 1 Leaderboard API 주요 파라미터]

|이름|	설명|
|---|---|
|appkey|	Leaderboard AppKey|
|factor|	팩터ID|

### Endpoint URL/AppKey

서비스 활성화 후 접속할 URL & Appkey 값을 확인합니다. URL & Appkey 값은 그림 4에서와 같이 화면 상단에서 확인 할 수 있습니다.

![[그림 4 Leaderboard URL & AppKey 확인]](http://static.toastoven.net/prod_leaderboard/rank_11.jpg)
<center>[그림 4 Leaderboard URL & AppKey 확인]</center>

> [주의]  
> AppKey값은 프로젝트에서 활성화하는 상품마다 각각 별도로 생성됩니다.  
> 다른 상품의 AppKey를 사용하지 않도록 주의해 주십시오.  

### 팩터 ID

팩터ID는 팩터 추가 후 [Game] > [Leaderboard] > [랭킹 설정]에서 테이블 정보로 확인 가능합니다. 그림 5에서 주간 점수의 팩터ID값은 1입니다.

![[그림 5 랭킹 설정에서 팩터ID 확인]](http://static.toastoven.net/prod_leaderboard/rank_12.jpg)
<center>[그림 5 랭킹 설정에서 팩터ID 확인]</center>

### 주기

주기(period) 파라미터 값은 표 2를 참고해 주십시오.

[표 2 랭킹 주기 값]

|주기 값|	설명|
|---|---|
|M|	월간(Monthly) 주기|
|W|	주간(Weekly) 주기|
|D|	일간(Daily) 주기|
|T|	전체(Total) 주기|

### 랭킹 등록

랭킹 점수는 단일 사용자 혹은 다수 사용자 점수 등록을 할 수 있습니다.

[단일 사용자 점수 등록 Request]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}/score
Content-Type: application/json

{
	"transactionId": {transactionId},
	"score": {score}
}
```

위 예에서는 Leaderboard AppKey(appkey), 등록한 팩터ID(factor), 사용자ID(userid,) 점수(score)를 파라미터로 전송했습니다. 해당 Factor에 점수 등록을 마쳤다는 응답을 받습니다.

[성공 시 Response]

```
HTTP/1.1 200 OK
Content-Type: application/json

{
		"header": {
			"isSuccessful": true,
			"resultCode": 200,
			"resultMessage": "OK",
			"serviceCode": 1,
			"transactionId": {transactionId}
		}
}
```

[다수 사용자 점수 등록 Request]

```
POST https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/scores

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

Leaderboard AppKey(appkey)와 등록하고자 하는 팩터ID(factor), 사용자ID(userid), 점수(score)를 입력한 후 요청합니다. 요청 성공 시 다음과 같은 응답을 받을 수 있습니다.

[성공 시 Response]

```
HTTP/1.1 200 OK
Content-Type: application/json

{
		"header": {
			"isSuccessful": true,
			"resultCode": 200,
			"resultMessage": "OK",
			"serviceCode": 1,
			"transactionId": {transactionId}
		}
}
```

### 랭킹 조회

단일 사용자, 다수 사용자 랭킹 조회, 범위 랭킹 조회 등을 할 수 있습니다. 여기서는 단일 사용자 조회, 범위 조회에 대해서 알아봅니다.

[단일 사용자 랭킹 정보 조회]

```
GET https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userId}/rank-info?transactionid={transactionId}&ispast={isPast}
```

AppKey(appkey)와 조회하고자 하는 팩터 정보 를 입력합니다. 단일 조회 시에는 사용자 ID(userId)를 입력하고, 범위 조회 시에는 시작 순위(start)와 크기(size)를 입력합니다. 이전 점수를 조회하고 싶다면 ispast 파라미터를 true로 입력합니다 (ispast 항목을 입력하지 않을 시, 현재 시점의 점수를 조회). 요청 성공 시 아래와 같은 응답을 받을 수 있습니다.

[단일 사용자 랭킹 정보 조회 성공 Response]

```
HTTP/1.1 200 OK
Content-Type: application/json

{
		"header": {

			"isSuccessful": true,
			"resultCode": 200,
			"resultMessage": "OK",
			"serviceCode": 1,
			"transactionId": {transactionid}
		},
		"rankInfoList": [
			{
				"factor": {factor},
				"lastUpdate": {lastUpdate},
				"rank": {rank},
				"rankChange": {rankChange},
				"score": {score},
				"userId": {userid},
			},...
		]
}
```

[일정 범위의 랭킹 정보 조회]

```
GET https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/rank-infos?transactionid={transactionId}&ispast={isPast}&start={start}&size={size}
```

[일정 범위의 랭킹 정보 조회 성공 Response]

```
HTTP/1.1 200 OK
Content-Type: application/json

{
		"header": {
			"isSuccessful": true,
			"resultCode": 200,
			"resultMessage": "OK",
			"serviceCode": 1,
			"transactionId": {transactionid}
		},
		"totalSize": {totalSize},
		"userRankInfoList": [
			{
				"factor": {factor},
				"lastUpdate": {lastUpdate},
				"rank": {rank},
				"rankChange": {rankChange},
				"score": {score},
				"userId": {userid}
			}, ...
		]
}
```

### 랭킹 삭제
단일 사용자 랭킹 정보 및 모든 사용자 랭킹 정보 삭제를 할 수 있습니다. 모든 팩터에 대해서 삭제를 원할 경우, 팩터 값에 -1을 입력한 후 요청합니다.

[단일 사용자 랭킹정보 삭제 Request]

```
DELETE https://api-ranking.cloud.toast.com/ranking/v3/api/appkey/{appkey}/factors/{factor}/users/{userid}?transactionid={transactionid}
```

[단일 사용자 랭킹정보 삭제 Response]

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
}]
```

## 데이터 관리

전체 랭킹 데이터는 Console에서 확인 가능합니다. [Game] > [Leaderboard] > [랭킹 데이터] 탭을 선택하면 데이터 검색이 가능합니다.

![[그림 6 랭킹 데이터 검색]](http://static.toastoven.net/prod_leaderboard/rank_13.jpg)
<center>[그림 6 랭킹 데이터 검색]</center>
