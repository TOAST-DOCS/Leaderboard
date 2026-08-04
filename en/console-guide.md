<!-- pre-align:aligned sig=5dbe7787c4ab -->

<a id="game-leaderboard-console-user-guide"></a>
## Game > Leaderboard > Console User Guide { #game-leaderboard-console-user-guide }

Leaderboard must be enabled first to use the service, before registering factors.   
Following features are available: 
* Check ranking indicators of a game  
* Register, initialize, and delete factors 
* Search, modify, and delete user's ranking information 

<a id="ranking-indicators"></a>
## Ranking Indicators { #ranking-indicators }
![leaderboard_01_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_01_202106.png)

<a id="indicators-of-particular-dates"></a>
### 1. Indicators of Particular Dates { #indicators-of-particular-dates }

You can check the total number of users, number of factors, cycle and occupancy rate of each factor, on a particular date: data are available on a date between today and 6 months before. 

Select a date on a calendar to find its indicators. 

**[Description of Each Item ]**

<a id="indicators-of-particular-dates-entire-data"></a>
#### Entire Data 

- The day's total number of users

<a id="indicators-of-particular-dates-number-of-factors"></a>
#### Number of Factors 

- The day's number of factors: displayed on a graph by each cycle. 

<a id="indicators-of-particular-dates-chart-of-data-occupancy-rate"></a>
#### Chart of Data Occupancy Rate 

- Cycle: Shows the number of users by the cycle.  
- Factor: Shows the number of users by the factor. 


<a id="data-indicators-during-search-period"></a>
### 2. Data Indicators during Search Period { #data-indicators-during-search-period }

Data fluctuation can be traced during a particular search period, which cannot exceed 6 months. 

Up to 10 factors can be selected; if no factor is selected, top 10 factor data are searched, as of a selected cycle.   

<a id="ranking-data"></a>
## Ranking Data { #ranking-data }

<a id="search-of-ranking-data"></a>
### Search of Ranking Data { #search-of-ranking-data }

![leaderboard_02_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_02_202106.png)

**[Search of Ranking Data]**

Registered factors can be found on the **Ranking Data** tab. Select a factor cycle to see factors of the cycle only. 
Select a search criteria to search for user information. 

**[Description of Each Item]**

<a id="search-of-ranking-data-select-cycle"></a>
#### Select Cycle
- Previous Cycle: Search ranking information of the previous cycle.
- Current Cycle: Search ranking information of the current cycle. 

<a id="search-of-ranking-data-search-conditions"></a>
#### Search Conditions 
- Search by Ranking: Specify the range of ranking for the users to search for. The range is limited to 500 for a search. 
- Search by User ID: Enter user ID to search for a factor. Cannot search when user is not available. 


<a id="user-information"></a>
### User Information { #user-information }

![leaderboard_03_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_03_202106.png)

<a id="user-information-modify-user-information"></a>
#### 1. Modify User Information 

Select a user to modify after search. 

**[Window for Modifying User Ranking]**
Click **Modify** and a window shows up to enter data. Scores and other data can be modified, while updated scores are required, along with reasons of change.

![leaderboard_04_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_04_202106.png)

<a id="user-information-delete-user-information"></a>
#### 2. Delete User Information 

Select a user to delete after search. 

**[Window for Deleting User Ranking]**

Click **Delete** and a window shows up asking whether to delete. Reasons are required, and you must be cautious since data cannot be recovered once deleted. 

![leaderboard_05_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_05_202106.png)

<a id="user-information-save-user-data"></a>
#### 3. Save User Data 

To save currently-searched user information, click **Save Data**.

**[Window for Saving Data]**
Data can be saved for up to 100 thousand cases at a time, and if it exceeds the limit, only up to 100 thousand, including ranks after search started, can be downloaded. 

![leaderboard_06_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_06_202106.png)

<a id="ranking-setting"></a>
## Ranking Setting { #ranking-setting }

![leaderboard_07_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_07_202106.png)

> **[Note]**<br>
> Registering, initializing, and deleting factors are executable only by those users who are registered as ADMIN.  

<a id="register-factors"></a>
### Register Factors { #register-factors }

<a id="register-factors-direct-input"></a>
#### Direct Input

After service is enabled, factor information must be added. Go to **Game > Leaderboard > Ranking Setting > +Add > Direct Input** to register factors.

> **[Note]**<br>
> A factor refers to the combination of [Cycle, Update Standard, and Alignment Standard].<br>
> To apply ranking of the highest scores on a daily, weekly, and monthly basis, three factors must be created.  

Click **[+Add]** and a window pops up as below.

![leaderboard_08_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_08_202106.png)

**[Description of Each Item]**

##### Factor ID

- The ID composed of original numbers of a factor; can be automatically saved when the window opens but cannot be randomly changed by user. It cannot be redundantly used. 

##### Factor Name

- The name classifying ranks, available for the search of factors. Factor names can be modified after registered. 

##### Limited Number of Users 

- The maximum number of users to be registered for a factor: no more than 10 million. 

##### Extra Data

- Other data of a factor, which can be entered only when it is required; modifiable after registered. 

##### Factor Cycle 

- The initialization period of a ranking, available by day, week, month, or all. Cycle is also available for the search of factors, and users are classified by each cycle.  

##### Select Time Criteria 

- UTC time which serves as criteria of a factor. For the search of users within a factor, the latest updated time is displayed based on this value.  

##### Factor Initialization Time 

- Time of initialization for each factor, to be calculated by standard UTC time. Cannot be enabled, if the cycle is 'all. ' 

##### Factor Initialization Interval 

- Refers to the interval of initialization for a factor cycle. If it is set at 3, initialization is executed at every 3 days, 3 weeks, or 3 months, each on daily, weekly, or monthly basis.   

##### Factor Initialization Date 

- Select a day and date to initialize, for the weekly or monthly data.  

##### Sorting Criteria 

- Descending Order: Sort scores in the descending order. 
- Ascending Order: Sort scores in the ascending order. 

##### Criteria of Ranking Updates

- By Best Scores: Records the highest scores of the user.
- By Latest Scores: Records the latest scores of the user. 
- By Accumulated Scores: Registers the accumulated scores of the user. 

##### Tie-Breaking 

- Priority for First Ranks: Records the earlier-registered same-score user at a higher rank.
- Priority for Recent Ranks: Records the later-registered same-score user at a higher rank.

> [Note] Factor ID is automatically specified when a factor is added. 

<a id="register-factors-upload-files"></a>
#### Upload Files

If you want to add multiple factors at once, click **Game > Leaderboard > Ranking Setting > +Add > Upload Files** to upload the file to register the factors.

**[Guide]**

Download the template, fill out the factor information, and upload the excel file.

Press the Add Factor button to add factors.

<a id="search-factors"></a>
### Search Factors { #search-factors }

![leaderboard_09_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_09_201902.png)

When a search condition is the factor name, search factors by the name containing search words. 

When a search condition is the factor cycle, search factors by the cycle on the selection list. 

<a id="initialize-factors"></a>
### Initialize Factors { #initialize-factors }

![leaderboard_10_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_10_202106.png)

Select a factor to initialize. 

Click **Initialize** and a window pops up. Once a factor is initialized, all its user data is deleted and cannot be recovered, so make a cautious decision.  

If the bottom is checked on the pop-up page, even the factor shall be deleted. Take it cautiously since data cannot be recovered once it is deleted.  


<a id="modify-factors"></a>
### Modify Factors { #modify-factors }

Select a factor name to modify from the list. 

Then a window pops up to **Modify Factors**. Only factor name and other information can be modified. 

![leaderboard_11_201902](https://static.toastoven.net/prod_leaderboardv2/en/leaderboard_11_202106.png)

※ See [API Guide](/Game/Leaderboard/en/api-guide/) for API information. 
