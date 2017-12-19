## Game > Leaderboard > Overview

게임에서 친구들과의 순위 경쟁은 이제 빠질 수 없는 요소 입니다.<br>
Leaderboard 플랫폼은 간단한 연동만으로 랭킹 서비스를 구현 할 수 있도록 지원 합니다.

<br>

## Merits

![[그림 0 Leaderboard Merits]](http://static.toastoven.net/prod_leaderboardv2/merits.png)

<br>

## Main Function

다음과 같은 기능을 제공합니다.

### Web Console 

- 사용량 정보 확인 
- TPS(초당 처리량) 확인
- Factor 등록 / 조회 / 초기화
- User 점수 조회 / 변경 / 삭제

### HTTP API

- User 점수 등록 (단일 / 다수)
- User 점수 획득 (단일 / 다수 / 범위)
- Factor에 들어있는 User 수 조회
- User 점수 삭제 (단일)

<br>

## Term

Leaderboard 에서는 다음 용어를 사용합니다.

| 용어 | 설명 |
| --- | --- |
| Leaderboard AppKey |	프로젝트당 하나의 Leaderboard AppKey를 발급함. |
| Factor |	랭킹 목적을 구분하는 단위. Factor에는 주기, 업데이트 기준, 정렬기준 설정. |
| 일간랭킹 | 하루마다 정해진 시간에 초기화하는 랭킹 주기. |
| 주간랭킹 | 일주일마다 정해진 요일, 정해진 시간에 초기화하는 랭킹 주기. |
| 월간랭킹 | 달마다 정해진 날, 정해진 시간에 초기화하는 랭킹 주기. |
| 전체랭킹 | 초기화하지 않는 랭킹 주기. |

<br>

## Service Structure

### Physical Structure

Leaderboard 플랫폼의 물리적 구성은 아래 그림과 같습니다.

![[그림 1 Leaderboard 물리적 구조]](http://static.toastoven.net/prod_leaderboardv2/overview_1.png)

- Game Server / Web Console은 api-leaderboard.cloud.toast.com으로 데이터를 주고 받습니다.
- Load Balancer는 여러 대로 구성한 Leaderboard AP 서버로 요청을 분배시킵니다.
- Leaderboard AP 서버는 Memory Server 와 Cassandra 에 데이터를 저장합니다.
- Leaderboard AP 서버는 Memory Server 에서 정렬된 데이터를 가져옵니다.

### Logical Structure

Leaderboard 플랫폼의 논리적 구조는 아래 그림과 같습니다.

![[그림 2 Leaderboard 논리적 구조]](http://static.toastoven.net/prod_leaderboardv2/overview_2.png)

- 한 개의 프로젝트 당 하나의 Leaderboard AppKey가 존재합니다.
- Leaderboard AppKey내에 여러 개의 Factor를 등록할 수 있습니다.
- 한 개의 Factor에 한 개의 주기를 설정할 수 있습니다.

<br>

## Feature

설정은 Factor 단위로 할 수 있습니다. 설정에 따라서 여러 특성의 리더보드를 사용하실 수 있습니다.

###  Sorting

점수 정렬 방식은 오름차순/내림차순 정렬로 설정할 수 있습니다. 

**[오름차순 정렬]**

오름차순 정렬은 작은 점수부터 큰 점수로 정렬합니다.

![[그림 3 오름차순 정렬]](http://static.toastoven.net/prod_leaderboardv2/overview_3.png)

**[내림차순 정렬]**

내림차순 정렬은 큰 점수부터 작은 점수로 정렬합니다.

![[그림 4 내림차순 정렬]](http://static.toastoven.net/prod_leaderboardv2/overview_4.png)

### Score update

점수 업데이트 방식은 최고/최근/누적 점수로 설정할 수 있습니다. 

**[최고 점수 업데이트]**

새로 들어온 점수가 이전 점수보다 높은 점수인 경우 업데이트 합니다.

![[그림 5 최고 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_5.png)

**[최근 점수 업데이트]**

기존 점수와 상관 없이 새로 들어온 점수를 업데이트 합니다. (항상 업데이트)

![[그림 6 최근 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_6.png)

**[누적 점수 업데이트]**

새로 들어온 점수와 기존 점수의 합해서 업데이트 합니다.

![[그림 7 누적 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_7.png)

### Tie score

동점자 순위 결정 방식은 Factor 단위로 최초/최근 랭킹 획득자 우선순위로 설정할 수 있습니다.

**[최초 랭킹 획득자 우선 순위]**

동점자가 여러명일 경우 가장 먼저 등록된 User가 더 높은 순위를 가집니다.

![[그림 8 최초 랭킹 획득자 우선 순위]](http://static.toastoven.net/prod_leaderboardv2/overview_8.png)

**[최근 랭킹 획득자 우선 순위]**

동점자가 여러명일 경우 가장 나중에 등록된 User가 더 높은 순위를 가집니다.

![[그림 9 최근 랭킹 획득자 우선 순위]](http://static.toastoven.net/prod_leaderboardv2/overview_9.png)

### Reset time

해당 Factor의 초기화 시간을 설정 할 수 있습니다.<br>
전체 랭킹의 경우는 초기화되지 않습니다.

### Reset Date

주간랭킹의 경우 초기화 요일을, 월간랭킹의 경우 초기화 날을 지정할 수 있습니다.<br>
전체 랭킹의 경우는 초기화되지 않습니다.

### Limit User

해당 Factor에 등록될 수 있는 최대 유저 수를 뜻합니다. 최대 1000만 명까지 입력할 수 있습니다.
