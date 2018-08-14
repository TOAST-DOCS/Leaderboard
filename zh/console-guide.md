## Game > Leaderboard > Console Guide

Leaderboard 사용을 위해선 상품 이용 후 랭킹을 등록해야 합니다.
상품 이용 후에는 게임의 지표 확인, 랭킹정보 등록, 초기화, 삭제 및 플레이어의 랭킹 정보 조회, 수정, 삭제를 할 수 있습니다.

<br>

## Configuration

### Leaderboard Service Enable

Console에서 [서비스 선택] > [Leaderboard]를 클릭하면 서비스가 활성화 되고 좌측 탭에 [Game] > [Leaderboard] 메뉴가 나타납니다.

![[그림 1 Leaderboard 서비스 활성화]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_1-1.PNG)


### API URL/AppKey

서비스 활성화 후 접속 시 API URL 및 Appkey 값을 확인할 수 있습니다.

![[그림 2 Leaderboard URL & AppKey 확인]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_2-1.PNG)

<br>

## Indicator Tab

### Target Date Indicator

특정 일자의 총 유저 수, Factor 수, 주기 및 Factor별 점유율 현황을 확인 할 수 있습니다. 오늘 날짜로 부터 6개월 전 까지의 데이터만 제공됩니다.

달력에서 날짜 선택 시 그 날의 지표가 바로 조회됩니다.

![[그림 3 특정 일자의 지표 확인]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_3-1.PNG)

**[각 항목별 설명]**
#### Data Total

- 그 날짜의 총 유저 수.

#### Factor Count

- 그 날짜의 Factor 수. 그래프에는 주기 별로 Factor가 얼마나 있는지 표시됩니다.

#### Data 점유율 차트

- 주기 : 주기를 기준으로 유저 수를 표시합니다.
- 팩터 : Factor를 기준으로 유저 수를 표시합니다.


### Range Date Indicator

일정 기간 동안의 데이터 변동 량을 확인 할 수 있습니다. 조회 가능 범위는 최대 6개월 입니다.

최대 10개 까지 특정 Factor를 선택 할 수 있으며, 미 선택 시 선택 된 주기를 기준으로 상위 10개 Factor의 데이터를 조회합니다.  

![[그림 4 일정 기간의 지표 확인]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_4.PNG)

<br>

## Data Tab

### Search User Info

**[랭킹 데이터 검색]**

Factor 등록 후 랭킹 데이터 탭으로 가면 등록한 Factor들이 보입니다. Factor 주기 선택 시 해당 주기의 Factor들이 선별됩니다.

![[그림 5 랭킹 데이터 검색]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_5-2.PNG)

**[유저 정보 검색]**

검색 기준을 선택해 유저 정보를 검색합니다.

![[그림 6 유저 정보 검색]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_6-2.PNG)

**[각 항목별 설명]**

#### 주기 선택
- 지난 주기 : 이전 주기의 랭킹 정보를 기준으로 검색합니다.
- 현재 주기 : 현재 주기의 랭킹 정보를 기준으로 검색합니다.

#### 검색 조건
- 순위별 조회 : 조회할 유저의 랭킹 범위를 정합니다. 조회 시 500명 까지 범위가 제한됩니다.
- 사용자 ID 조회 : 해당 Factor 내에 검색하고자 하는 User ID를 입력합니다. User가 없는 경우 조회되지 않습니다.

### Modify User Info

**[수정할 유저 데이터 선택]**
조회 후 수정할 유저를 선택합니다.

![[그림 7 수정할 유저 데이터 선택]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_7-1.PNG)

**[유저 랭킹 수정 팝업]**
수정 버튼을 누르면 수정 할 데이터를 입력하는 팝업이 뜹니다. 점수, 기타 정보를 수정 할 수 있으며 변경 점수 및 사유는 필수 입력 입니다.

![[그림 8 유저 랭킹 수정 팝업]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_8.PNG)

### Delete User Info

**[삭제할 유저 데이터 선택]**
조회 후 삭제할 유저를 선택합니다.

![[그림 9 삭제할 유저 데이터 선택]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_9-1.PNG)

**[유저 랭킹 삭제 팝업]**
삭제 버튼을 누르면 삭제 여부를 묻는 팝업이 뜹니다. 사유는 필수 입력이며 삭제 후 복구가 불가능하니 신중히 삭제해야 합니다.

![[그림 10 유저 랭킹 삭제 팝업]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_10.PNG)

### Download User Data

**[데이터 저장 버튼 클릭]**
현재 조회한 유저 정보들을 저장하려면 데이터 저장 버튼을 누릅니다.

![[그림 18 데이터 저장 버튼 클릭]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_18.PNG)

**[데이터 저장 팝업]**
데이터는 1회 최대 10만 건까지 저장 가능하며, 허용량 초과 시 조회 시작 순위 포함 10만 명 까지만 다운로드 됩니다.

![[그림 19 데이터 저장 팝업]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_19.PNG)

<br>

## Setting Tab

> **[유의 사항]**<br>
> Factor의 등록, 초기화, 삭제는 프로젝트의 ADMIN으로 등록된 사용자만 수행 할 수 있습니다. 

### Add Factor

서비스 활성화 후 Factor 정보를 추가해야 합니다. [Game] > [Leaderboard] > [랭킹 설정] > [+추가] 버튼을 클릭해 Factor를 등록합니다.

> **[참고]**<br>
> Factor는 [주기, 업데이트 기준, 정렬기준]의 묶은 단위입니다.<br>
> 최고점수 랭킹을 일간, 주간, 월간으로 사용하고 싶다면 Factor를 3가지를 만들어야 합니다.

![[그림 11 Factor 등록을 위하여 [+추가] 클릭]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_11-1.PNG)

[+추가] 버튼을 클릭하면 아래와 같은 팝업이 열립니다.

![[그림 12 Factor 추가 팝업]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_12-3.PNG)

**[각 항목별 설명]**
#### Factor ID

- Factor의 고유한 숫자 ID로 팝업 오픈 시 자동으로 지정되나 사용자 임의로 변경 할 수 있습니다. 다른 Factor ID와 중복 불가입니다.

#### Factor 이름

- 랭킹을 구분할 이름이며 차후 Factor 검색에 사용될 수 있습니다. Factor 이름은 등록 후 수정이 가능합니다.

#### 한계 유저 수

- 해당 Factor에 등록될 수 있는 최대 유저 수를 뜻합니다. 최대 1000만 명까지 입력할 수 있습니다.

#### 기타정보

- Factor의 extra 데이터로 필요 시 입력합니다. 기타 정보는 등록 후 수정이 가능합니다.

#### Factor 주기

- 랭킹의 초기화 기간을 의미하며 일간, 주간, 월간, 전체가 있습니다. 주기 또한 Factor 검색에 사용될 수 있으며 각 주기를 기준으로 유저들을 분류합니다.

#### 기준 시간 선택

- Factor의 기준이 되는 UTC 시간을 의미합니다. Factor 내 유저 조회 시 최근 업데이트 시간은 이 값을 기준으로 표시됩니다. 

#### Factor 리셋 시간

- Factor 별 초기화 시간을 의미합니다. 기준 UTC 시간을 토대로 계산됩니다. 주기가 전체인 경우 활성화 되지 않습니다.

#### Factor 리셋 간격

- Factor 주기의 초기화 간격을 의미합니다. 3으로 설정 시 일간 - 3일, 주간 - 3주, 월간 - 3개월에 1번 초기화 됩니다.

#### Factor 리셋 일자

- 주간, 월간의 경우 초기화 될 요일, 일자를 선택해야합니다.

#### 정렬 기준

- Desc : 점수를 내림차순으로 정렬합니다.
- Asc : 점수를 오름차순으로 정렬합니다.

#### 랭킹 업데이트 기준

- Best Score : 최고 점수 등록. User의 베스트 점수를 기록합니다.
- Latest Score : 최신 점수 등록. User의 가장 최근 점수를 기록합니다.
- Accumulation Score : 누적 점수 등록. User의 점수를 누적 합산해 등록합니다.

#### 동점자 처리

- Priority First Ranking Get : 최초 랭킹 획득 우선. 동점인 경우 먼저 등록된 유저가 높은 등수로 기록됩니다.
- Priority Latest Ranking Get : 최근 랭킹 획득 우선. 동점인 경우 나중에 등록된 유저가 높은 등수로 기록됩니다.

> FactorID는 Factor 추가 시 자동으로 지정됩니다.

### Search Factor

검색 조건이 Factor 이름일 시 이름에 검색어가 포함된 Factor를 검색합니다.

![[그림 13 검색 기준 Factor 이름]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_13.PNG)

검색 조건이 Factor 주기일 시 선택 목록에 있는 주기로 검색합니다.

![[그림 14 검색 기준 Factor 주기]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_14.PNG)

### Init Factor

초기화 할 Factor들을 선택합니다.

![[그림 15 랭킹 설정에서 초기화 할 Factor 선택]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_15-1.PNG)

초기화 버튼을 클릭 시 초기화 팝업이 나타납니다. 초기화 후엔 Factor의 유저 데이터가 전부 사라지고 복구가 불가능 하니 신중하게 수행합니다.

![[그림 16 Factor 초기화 팝업]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_16.PNG)

### Delete Factor

초기화 팝업에서 하단 항목 체크 시 Factor까지 삭제됩니다. 데이터 복구가 불가능하니 신중하게 수행합니다. 

![[그림 17 Factor 삭제]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_17.PNG)

※ 개발과 관련된 api 정보는 [API Guide](/Game/Leaderboard/zh/api-guide/) 를 참조해주세요.