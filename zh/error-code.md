## Game > Leaderboard > Error Codes

## Error Codes 

Below table describes resultCode and resultMessage at the header/body in the Response body. 
If resultCode at the header displays HTTP error codes, not like below, see the [Note] link at the bottom. 

|Result Code| Result Code(Hex) | Result Message |Description|
|---|---|---|---|
|0|	0x00000000 |LEADERBOARD_SUCCESS | Successfully requested. |
|1|	0x00000001 |LEADERBOARD_SUCCESS_BUT_NOT_UPDATE | Requested successfully, but not updated since data is same as before. |
|459777|	0x00070401 |LEADERBOARD_ERROR_APPKEY_VERIFIER | AppKey authentication failed. |
|462849|	0x00071001 |LEADERBOARD_AP_ERROR_INITIALIZE | Initialization failed. |
|462850|	0x00071002 |LEADERBOARD_AP_ERROR_NOT_EXIST_USER | Unregistered user. |
|462851|	0x00071003 |LEADERBOARD_AP_ERROR_NOT_EXIST_FACTOR | Unregistered factor. |
|462852|	0x00071004 |LEADERBOARD_AP_ERROR_NOT_EXIST_APPKEY | Unregistered Appkey. |
|462853|	0x00071005 |LEADERBOARD_AP_ERROR_TOO_BIG_EXTRA | Limit in the length of extra data exceeded. |
|462854|	0x00071006 |LEADERBOARD_AP_ERROR_WRONG_RANGE | Invalid range. |
|462855|	0x00071007 |LEADERBOARD_AP_ERROR_WRONG_PARAM | Invalid parameter. |
|462856|    0x00071008 |LEADERBOARD_AP_ERROR_WRONG_PATH | Character missing in the URI; parameter missing. |
|462857|    0x00071009 |LEADERBOARD_AP_ERROR_TOO_BIG_SIZE | Exceeded request size. |
|463000|	0x00071098 |LEADERBOARD_AP_ERROR_SYSTEM | Error in system. |
|463001|	0x00071099 |LEADERBOARD_AP_ERROR_UNKOWN | Unidentified error. |

> [Note]
> For more information on other general error codes, see the link:  
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml