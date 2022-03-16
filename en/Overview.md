## Game > Leaderboard > Overview

Competing for a higher rank is essential for a game play. <br>
With Leaderboard, it only takes a simple integration to implement a ranking service.  

<br>

## Merits

![[그림 0 Leaderboard Merits]](http://static.toastoven.net/prod_leaderboardv2/newMerits_en_202203.png)

<br>

## Main Features

Following features are provided: 

### Web Console

- Check usage volume information 
- Check Transactions Per Second (TPS) 
- Register, search, or initialize factors 
- Search, change, or delete user scores 

### HTTP API

- Register user scores (by single or multiple) 
- Win user scores (by single, multiple, or range)
- Search the number of users in a factor 
- Delete user scores (single) 

<br>

## Glossary

Following terms are used for Leaderboard.

| Term | Description |
| --- | --- |
| Leaderboard AppKey |	One Leaderboard Appkey is issued for each project. |
| Factor |	The unit of ranking purpose. Each factor is configured by cycle, update, or sorting. |
| Daily Ranking | Ranking cycle which is initialized at every specific time of the day. |
| Weekly Ranking | Ranking cycle which is initialized at every specific day and time of the week. |
| Monthly Ranking | Ranking cycle which is initialized at every specific day and time of the month. |
| Total Ranking | Ranking cycle which is not initialized. |

<br>

## Service Structure 

### Physical Structure

The Leadboard platform is physically structured as below: 

![[그림 1 Leaderboard 물리적 구조]](http://static.toastoven.net/prod_leaderboardv2/overview_1.png)

- Game server/NHN Cloud Console exchanges data at api-leaderboard.cloud.toast.com.
- Load Balancer distributes requests to many Leaderboard AP servers.
- Leaderboard AP server saves data in the memory server and Cassandra.
- Leaderboard AP server imports sorted data from the memory server. 

### Logical Structure

The Leaderboard platform is logically structured as below: 

![[그림 2 Leaderboard 논리적 구조]](http://static.toastoven.net/prod_leaderboardv2/overview_2.png)

- Each project owns one Leaderboard AppKey.
- Many factors can be registered within a Leaderboard AppKey.
- One factor can be assigned with a cycle. 

<br>

## Features 

Leaderboard is configured by factor. Depending on the setting, it can be differently applied. 

###  Sorting

Scores can be sorted in the ascending or descending order. 

**[Sort by Ascending Order]**

The ascending order sorts scores from the lowest to the highest.

![[그림 3 오름차순 정렬]](http://static.toastoven.net/prod_leaderboardv2/overview_3.png)

**[Sort by Descending Order]**

The descending order sorts scores from the highest to the lowest. 

![[그림 4 내림차순 정렬]](http://static.toastoven.net/prod_leaderboardv2/overview_4.png)

### Updating Scores 

Scores can be updated by the highest, the latest, or the accumulated. 

**[Updating with the Highest Scores]**

Updated when a newer score is higher than a previous one. 

![[그림 5 최고 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_5.png)

**[Updating with the Latest Scores]**

Updated with new scores, regardless of existing scores (updated at all times).

![[그림 6 최근 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_6.png)

**[Updating with the Accumulated Scores]**

Updated with the combination of a new score and an existing one.

![[그림 7 누적 점수 업데이트]](http://static.toastoven.net/prod_leaderboardv2/overview_7.png)

### Tie-Breaking  

The tie-breaking method may be set to prioritize the first or the latest-ranks by factor.

**[Set Priorities for First Ranks ]**

When there are a multiple number of ties, the first-registered user ranks the highest. 

![[그림 8 최초 랭킹 획득자 우선순위]](http://static.toastoven.net/prod_leaderboardv2/overview_8.png)

**[Set Priorities for Latest Ranks]**

When there are a multiple number of ties, the latest-registered user ranks the highest. 

![[그림 9 최근 랭킹 획득자 우선순위]](http://static.toastoven.net/prod_leaderboardv2/overview_9.png)

### Initialization Time 

Initialization time of a factor can be configured. <br>
The entire ranking is not initialized. 

### Initialization Date and Time

For the weekly ranking, specify a date of initialization; for the monthly ranking, specify a day of initialization.  <br>
The entire ranking is not initialized. 

### Limited Number of Users

The maximum number of users to be registered for a factor: no more than 10 million.  