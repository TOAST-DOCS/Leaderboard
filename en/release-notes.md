## Game > Leaderboard > Release Notes

### August 09, 2022
#### Feature Updates
* [API] Add the result value of the total number of users in the factor to the user lookup api.

### October 12, 2021
#### Feature Updates
* [Console] Ranking Indicator, Ranking Data, Ranking Setting
    * Changed the file download format to CSV. 

#### Bug Fixes
* [Console] Fixed an issue where the contents are omitted when downloading files from the results searched by factor cycle in Ranking Setting

### August 24, 2021

#### Feature Updates
* [API] Applied the request size limit (maximum 500) for user ranking lookup and registration API.

#### Bug Fixes
* [Console] Fixed an issue where, when you add ranking factors with files, registration fails unless you input additional information.

### Mar. 23, 2021

#### Feature Updates
* [API] Add multiple user delete api
* [API] Add factor count, single factor, multiple factor lookup api

### Feb. 23, 2021

#### Feature Updates
* [API] Add api to search users of specific rank

### Sep. 22, 2020

#### Feature Updates
* [Document] Added explanation on how to use the game base due to automatic activation

#### Bug Fixes
* [Console] Fixed an error when searching users with a certain score or higher
* [API] Fixed an error when searching a user of a factor that did not exist

### Jan. 21, 2020

#### Feature Updates
* [Common] Added automatic activation of leaderboard upon gamebase activation

### Apr. 23, 2019

#### Feature Updates
* [API] Add pre- and post-ranking query APIs with specific users

### Mar. 26, 2019

#### Feature Updates
* [API] Uniform parameter case with camel case. You can use the parameters that are guided by the existing lower case 

### Feb. 26, 2019

#### Feature Updates
* [Console] Updated Korean, Japanese, and English Contents

* [Console] Applied multilingual Datepicker

* [Document] Updated Korean, Japanese, and English Guide

### Oct. 23, 2018

#### Feature Updates 
* [Console] Expanded UTC time range for factor registration 

* [API] Added the sorting feature for Get Multiple User Info API

* [Document] Added description on improved Get Multiple User Info API

### August 28, 2018

#### Feature Updates 
* [Console] Added UTC configuration with factor registration 

* [Console] Shows recent updated time based on UTC time to query user data 

* [Console] Added a feature of modifying name and extra data after factor is registered 

* [Document] Added description regarding improved UTC configuration or modifying factors 

### July 24, 2018 

#### Feature Updates 
* [Console] Changed the order of user data on the Ranking Data tab, to show the ranking first 

#### Bug Fixes 
* [Console] Fixed the failure of paging, when querying users in particular ranges on the Ranking Data tab 

* [Console] Fixed the unavailability of finding data when downloading users in particular ranges 

### June 26, 2018

#### Bug Fixes 
* [Console] Fixed partial missing of indicator information 

### May 29, 2018

#### Feature Updates 
* [Console] Released the limit of 500 users, for the query of user data 

* [Console] Added a feature of downloading queried user data, for up to 100 million at a time.

* [Console] Allowed to specify Factor ID when a factor is registered.  

* [Document] Added a feature of describing new or improved console features. 

### March 22, 2018

#### Feature Updates 
* [Console] Improved to configure by N cycle when a factor is registered. 

* [Document] Added description regarding the configuration of improved N cycle 

### Feb. 22, 2018

#### Feature Updates 
* [Console] Updated UI of the console 

* [Console] Added tabs for ranking indicators: available to check by daily indicators  

* [Console] Added a feature of modifying user information. Added a feature of finding change history of user information.  

* [Console] Added a feature of initializing a factor 

* [Console] Changed to allow only project ADMINs to add or initialize factors  

* [Document] Added a feature of describing new console features 

### Oct. 26, 2017

#### Feature Updates 
* [Document] Added description for error codes regarding WRONG_PATH 
* [Document] Supported guides in Japanese 

#### Bug Fixes 
* [Console] Fixed the error of check boxes for all user information remaining selected even after deleted or re-searched. 

### August 24, 2017

#### Feature Updates 
* [Document] Inserted words regarding API call policy 
* [Console] Changed terms and description for factor registration 

#### Bug Fixes 
* [Console] Fixed the issue of users of previous cycles remaining undeleted  

* [Server] Modified the issue of integrity for data inputs during initialization 

* [API] Fixed the issue of Infinity when a too big or small number is entered for a score 

* [API] Modified to prevent using "" for a UserID  

### June 22, 2017

#### Bug Fixes 
* [Console] Fixed the issue of ranking name cuts when they are registered in Korean on the Internet Explorer 

* [Console] Fixed the issue of user range inquiries within a ranking, which do not match UI

### April 20, 2017

#### Feature Updates 
* [Console] Added a feature of searching factors on the Ranking Setting tab: search is available by factor name or factor cycle. 
* [Console] Simplified the search window on the Ranking Data tab: registered factors are classified by factor cycle, when searched. 

#### Bug Fixes 
* [API] Returns HTTP Status Code to 200, when the server receives a request, even if it is abnormal.  

### Feb. 23, 2017

#### Feature Updates 
* [Console] Changed not to show factor initialization time, for 'All' cycles, when a factor is added. 
* [Console] Added a feature of allowing searches of past cycles when querying the ranking of each user ID  

#### Bug Fixes 
* [Console] Fixed the error of web page suspension, when it is requested to remove multiple ranking data  

### Jan. 19, 2017

#### Upgrade Guide for LeaderBoard v2 

* Change in Internal Structure 
    * Data Scalability 
        * Changed the structure for flexible data scalability 
    * Performance
        * Improved performance as compared a previous version

* Improved REST API Interface 
    * Updated with more consistent and precise REST API interface

<a href="https://toast.com/support/notice/detail/1453435858K00349" target="_blank">[Notice] Upgrade Guide for TOAST Cloud LeaderBoard v2 </a><br>
