## Game > Leaderboard > 콘솔 사용 가이드

Leaderboard 사용을 위해서 서비스 활성화 후 팩터를 등록해야 합니다.  
서비스를 이용하면 아래 목록의 기능을 사용할 수 있습니다.

- 게임의 랭킹 지표 확인
- 팩터의 등록, 초기화, 삭제
- 유저의 랭킹 정보 검색, 수정, 삭제

## 랭킹 지표
![leaderboard_01_201901-1](https://static.toastoven.net/prod_leaderboardv2/leaderboard_01_202106-1.png)

### 1. 특정 일자 지표

특정 일자의 총 유저 수, 팩터 수, 주기 및 팩터별 점유율 현황을 확인할 수 있습니다. 오늘 날짜에서 6개월 전까지의 데이터만 확인할 수 있습니다.

달력에서 날짜를 선택하면 그날의 지표를 바로 확인할 수 있습니다.

**[항목별 설명]**

#### 전체 데이터

- 그날의 총 유저 수.

#### 팩터 수

- 그날의 팩터 수. 그래프에는 주기별로 팩터가 얼마나 있는지 표시됩니다.

#### 데이터 점유율 차트

- 주기: 주기를 기준으로 유저 수를 표시합니다.
- 팩터: 팩터를 기준으로 유저 수를 표시합니다.


### 2. 검색 기간 동안의 데이터 지표

일정 기간의 데이터 변동량을 확인할 수 있습니다. 검색 가능 범위는 최대 6개월입니다.

최대 10개까지 특정 팩터를 선택할 수 있으며, 선택하지 않으면 선택된 주기를 기준으로 상위 10개 팩터의 데이터를 검색합니다.  

## 랭킹 데이터

### 랭킹 데이터 검색

![leaderboard_02_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_02_202106.png)

**[랭킹 데이터 검색]**

팩터를 등록하면 **랭킹 데이터** 탭에서 등록한 팩터를 확인할 수 있습니다. 팩터 주기를 선택하면 해당 주기의 팩터만 볼 수 있습니다.
검색 기준을 선택해 유저 정보를 검색합니다.

**[항목별 설명]**

#### 주기 선택
- 지난 주기: 이전 주기의 랭킹 정보를 기준으로 검색합니다.
- 현재 주기: 현재 주기의 랭킹 정보를 기준으로 검색합니다.

#### 검색 조건
- 순위별 검색: 검색할 유저의 랭킹 범위를 정합니다. 검색 시 500명까지 범위가 제한됩니다.
- 유저 ID 검색: 해당 팩터 내에 검색하고자 하는 유저 ID를 입력합니다. 유저가 없으면 검색되지 않습니다.


### 유저 정보

![leaderboard_03_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_03_202106.png)

#### 1. 유저 정보 수정

검색 후 수정할 유저를 선택합니다.

**[유저 랭킹 수정 창]**
**수정** 버튼을 클릭하면 수정할 데이터를 입력하는 창이 나타납니다. 점수, 기타 정보를 수정할 수 있으며 변경 점수와 사유는 필수로 입력해야 합니다.

![leaderboard_04_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_04_202106.png)

#### 2. 유저 정보 삭제

검색 후 삭제할 유저를 선택합니다.

**[유저 랭킹 삭제 창]**
**삭제** 버튼을 클릭하면 삭제 여부를 묻는 창이 나타납니다. 사유는 필수로 입력해야 하며 삭제 후 복구할 수 없으므로 신중히 삭제해야 합니다.

![leaderboard_05_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_05_202106.png)

#### 3. 유저 데이터 저장

현재 검색한 유저 정보를 저장하려면 **데이터 저장** 버튼을 클릭합니다.

**[데이터 저장 창]**
데이터는 1회 최대 10만 건까지 저장할 수 있으며, 허용량을 초과하면 검색 시작 순위 포함 10만 명까지만 다운로드됩니다.

![leaderboard_06_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_06_202106.png)

## 랭킹 설정

![leaderboard_07_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_07_202106.png)

> **[유의 사항]**<br>
> 팩터의 등록, 초기화, 삭제는 프로젝트의 ADMIN으로 등록된 사용자만 수행할 수 있습니다. 

### 팩터 등록

#### 직접 입력

서비스를 활성화한 후 팩터 정보를 추가해야 합니다. **Game > Leaderboard > 랭킹 설정 > +추가 > 직접 입력** 버튼을 클릭해 팩터를 등록합니다.

> **[참고]**<br>
> 팩터는 [주기, 업데이트 기준, 정렬기준]의 묶은 단위입니다.<br>
> 최고 점수 랭킹을 일간, 주간, 월간으로 사용하고 싶다면 팩터를 3개 만들어야 합니다.

**[+추가]** 버튼을 클릭하면 아래와 같은 창이 열립니다.

![leaderboard_08_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_08_202106.png)

**[항목별 설명]**

##### 팩터 ID

- 팩터의 고유한 숫자 ID로 창을 열면 자동으로 지정되나 사용자 임의로 변경할 수 있습니다. 팩터 ID는 중복해서 사용할 수 없습니다.

##### 팩터 이름

- 랭킹을 구분하는 이름이며 차후 팩터 검색에 사용할 수 있습니다. 팩터 이름은 등록 이후에 수정할 수 있습니다.

##### 한계 유저 수

- 해당 팩터에 등록할 수 있는 최대 유저 수입니다. 최대 1,000만 명까지 입력할 수 있습니다.

##### 기타 정보

- 팩터의 기타 정보로, 필요할 때만 입력하면 됩니다. 기타 정보는 등록한 후 수정할 수 있습니다.

##### 팩터 주기

- 랭킹의 초기화 기간을 의미하며 일간, 주간, 월간, 전체가 있습니다. 주기 또한 팩터 검색에 사용할 수 있으며 각 주기를 기준으로 유저를 분류합니다.

##### 기준 시간 선택

- 팩터의 기준이 되는 UTC 시간입니다. 팩터 내 유저를 검색할 때 최근 업데이트 시간은 이 값을 기준으로 표시됩니다. 

##### 팩터 초기화 시간

- 팩터별 초기화 시간입니다. 기준 UTC 시간을 토대로 계산됩니다. 주기가 '전체'인 경우 활성화되지 않습니다.

##### 팩터 초기화 간격

- 팩터 주기의 초기화 간격을 의미합니다. 3으로 설정하면 일간일 때는 3일, 주간일 때는 3주, 월간일 때는 3개월에 한 번 초기화됩니다.

##### 팩터 초기화 일자

- 주간, 월간의 경우 초기화할 요일, 일자를 선택해야 합니다.

##### 정렬 기준

- 내림차순: 점수를 내림차순으로 정렬합니다.
- 오름차순: 점수를 오름차순으로 정렬합니다.

##### 랭킹 업데이트 기준

- 베스트 점수 등록: 유저의 최고 점수를 기록합니다.
- 최신 점수 등록: 유저의 가장 최근 점수를 기록합니다.
- 누적 점수 등록: 유저의 점수를 누적 합산해 등록합니다.

##### 동점자 처리

- 최초 랭킹 획득 우선: 동점이면 먼저 등록된 유저가 높은 등수로 기록됩니다.
- 최근 랭킹 획득 우선: 동점이면 나중에 등록된 유저가 높은 등수로 기록됩니다.

> [참고] 팩터 ID는 팩터 추가 시 자동으로 지정됩니다.

#### 파일 업로드

여러 팩터를 한 번에 추가하고 싶으신 경우에 **Game > Leaderboard > 랭킹 설정 > +추가 > 파일 업로드** 버튼을 클릭해 파일을 업로드하여 팩터를 등록할 수 있습니다.

**[가이드]**

템플릿을 다운받고 팩터 정보를 기입한 후 해당 엑셀 파일을 업로드 합니다. 

팩터 추가 버튼을 눌러 팩터를 추가합니다.

### 팩터 검색

![leaderboard_09_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_09_201812.png)

검색 조건이 팩터 이름이면 이름에 검색어가 포함된 팩터를 검색합니다.

검색 조건이 팩터 주기이면 선택 목록에 있는 주기로 검색합니다.

### 팩터 초기화

![leaderboard_10_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_10_202106.png)

초기화할 팩터를 선택합니다.

**초기화** 버튼을 클릭하면 초기화 창이 나타납니다. 초기화하면 팩터의 유저 데이터가 전부 사라지며 복구할 수 없으니 신중하게 수행해야 합니다.

초기화 창에서 하단 항목을 선택하면 팩터까지 삭제됩니다. 데이터를 복구할 수 없으니 신중하게 수행해야 합니다. 


### 팩터 수정

팩터 목록에서 수정할 팩터의 이름을 선택합니다.

선택하면 **팩터 수정** 창이 나타납니다. 팩터 이름, 기타 정보만 수정할 수 있습니다.

![leaderboard_11_201812](https://static.toastoven.net/prod_leaderboardv2/leaderboard_11_202106.png)

※ API 정보는 [API Guide](/Game/Leaderboard/ko/api-guide/)를 참고해 주세요.
