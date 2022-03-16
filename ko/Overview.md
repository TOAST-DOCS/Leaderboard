## Game > Leaderboard > 개요

게임에서 친구들과의 순위 경쟁은 이제 빠질 수 없는 요소입니다.<br>
Leaderboard 플랫폼을 사용하면 간단한 연동만으로 랭킹 서비스를 구현할 수 있습니다.

<br>

## Merits

![[그림 0 Leaderboard Merits]](http://static.toastoven.net/prod_leaderboardv2/newMerits_kr_202203.png)

<br>

## 주요 기능

다음과 같은 기능을 제공합니다.

### Web Console

- 사용량 정보 확인
- TPS(초당 처리량) 확인
- 팩터 등록, 검색, 초기화
- 유저 점수 검색, 변경, 삭제

### HTTP API

- 유저 점수 등록(단일, 다수)
- 유저 점수 획득(단일, 다수, 범위)
- 팩터에 들어 있는 유저 수 검색
- 유저 점수 삭제(단일)

<br>

## 용어

Leaderboard에서는 다음 용어를 사용합니다.

| 용어 | 설명 |
| --- | --- |
| Leaderboard AppKey |	프로젝트당 하나의 Leaderboard AppKey를 발급함. |
| 팩터 |	랭킹 목적을 구분하는 단위. 팩터에는 주기, 업데이트 기준, 정렬 기준 설정. |
| 일간 랭킹 | 매일 정해진 시간에 초기화하는 랭킹 주기. |
| 주간 랭킹 | 매주 정해진 요일, 정해진 시간에 초기화하는 랭킹 주기. |
| 월간 랭킹 | 매달 정해진 날, 정해진 시간에 초기화하는 랭킹 주기. |
| 전체 랭킹 | 초기화하지 않는 랭킹 주기. |

<br>

## 서비스 구조

### 물리적 구조

Leaderboard 플랫폼의 물리적 구조는 아래 그림과 같습니다.

![[그림 1 Leaderboard 물리적 구조]](http://static.toastoven.net/prod_leaderboardv2/overview_1.png)

- 게임 서버/NHN Cloud Console은 api-leaderboard.cloud.toast.com으로 데이터를 주고받습니다.
- Load Balancer는 여러 대로 구성한 Leaderboard AP 서버로 요청을 분배합니다.
- Leaderboard AP 서버는 메모리 서버와 Cassandra에 데이터를 저장합니다.
- Leaderboard AP 서버는 메모리 서버에서 정렬된 데이터를 가져옵니다.

### 논리적 구조

Leaderboard 플랫폼의 논리적 구조는 아래 그림과 같습니다.

![[그림 2 Leaderboard 논리적 구조]](http://static.toastoven.net/prod_leaderboardv2/overview_2.png)

- 한 개의 프로젝트당 하나의 Leaderboard AppKey가 있습니다.
- Leaderboard AppKey 내에 여러 개의 팩터를 등록할 수 있습니다.
- 한 개의 팩터에 한 개의 주기를 설정할 수 있습니다.

<br>

## 특징

설정은 팩터 단위로 할 수 있습니다. 설정에 따라서 여러 특성의 Leaderboard를 사용할 수 있습니다.

###  정렬

점수 정렬 방식은 오름차순, 내림차순 정렬로 설정할 수 있습니다.

**[오름차순 정렬]**

오름차순 정렬은 작은 점수부터 큰 점수로 정렬합니다.

![[그림 3 오름차순 정렬]](http://static.toastoven.net/prod_leaderboardv2/overview_3.png)

**[내림차순 정렬]**

내림차순 정렬은 큰 점수부터 작은 점수로 정렬합니다.

![[그림 4 내림차순 정렬]](http://static.toastoven.net/prod_leaderboardv2/overview_4.png)

### 점수 업데이트

점수 업데이트 방식은 최고, 최근, 누적 점수로 설정할 수 있습니다.

**[최고 점수 업데이트]**

새로 들어온 점수가 이전 점수보다 높은 점수일 때 업데이트합니다.

![[그림 5 최고 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_5.png)

**[최근 점수 업데이트]**

기존 점수와 상관없이 새로 들어온 점수를 업데이트합니다(항상 업데이트).

![[그림 6 최근 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_6.png)

**[누적 점수 업데이트]**

새로 들어온 점수와 기존 점수를 합해서 업데이트합니다.

![[그림 7 누적 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_7.png)

### 동점자 처리

동점자 순위 결정 방식은 팩터 단위로 최초, 최근 랭킹 획득자 우선순위로 설정할 수 있습니다.

**[최초 랭킹 획득자 우선순위]**

동점자가 여러 명이면 가장 먼저 등록된 유저가 더 높은 순위가 됩니다.

![[그림 8 최초 랭킹 획득자 우선순위]](http://static.toastoven.net/prod_leaderboardv2/overview_8.png)

**[최근 랭킹 획득자 우선순위]**

동점자가 여러 명이면 가장 나중에 등록된 유저가 더 높은 순위가 됩니다.

![[그림 9 최근 랭킹 획득자 우선순위]](http://static.toastoven.net/prod_leaderboardv2/overview_9.png)

### 초기화 시간

해당 팩터의 초기화 시간을 설정할 수 있습니다.<br>
전체 랭킹은 초기화되지 않습니다.

### 초기화 일자

주간 랭킹은 초기화 요일을, 월간 랭킹은 초기화 날을 지정할 수 있습니다.<br>
전체 랭킹은 초기화되지 않습니다.

### 한계 유저 수

해당 팩터에 등록할 수 있는 최대 유저 수를 뜻합니다. 최대 1,000만 명까지 입력할 수 있습니다.