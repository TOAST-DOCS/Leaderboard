## Game > Leaderboard > 오류 코드

## 오류 코드

아래 표의 오류 코드는 Response body의 header/body에 있는 resultCode와 resultMessage의 의미를 설명합니다.
header에 있는 resultCode에서 아래의 오류 코드가 아닌  HTTP 오류 코드가 보이면 아래 [참고] 링크를 참고해 주시기 바랍니다.

|Result Code| Result Code(Hex) | Result Message |설명|
|---|---|---|---|
|0|	0x00000000 |LEADERBOARD_SUCCESS | 요청 성공.|
|1|	0x00000001 |LEADERBOARD_SUCCESS_BUT_NOT_UPDATE | 요청은 성공했지만, 기존과 동일한 데이터가 들어와서 업데이트하지 않음. |
|459777|	0x00070401 |LEADERBOARD_ERROR_APPKEY_VERIFIER | AppKey 인증 실패. |
|462849|	0x00071001 |LEADERBOARD_AP_ERROR_INITIALIZE | 초기화 실패. |
|462850|	0x00071002 |LEADERBOARD_AP_ERROR_NOT_EXIST_USER | 등록되지 않은 User. |
|462851|	0x00071003 |LEADERBOARD_AP_ERROR_NOT_EXIST_FACTOR | 등록되지 않은 Factor.|
|462852|	0x00071004 |LEADERBOARD_AP_ERROR_NOT_EXIST_APPKEY | 등록되지 않은 AppKey. |
|462853|	0x00071005 |LEADERBOARD_AP_ERROR_TOO_BIG_EXTRA | Extra Data 제한 길이 초과. |
|462854|	0x00071006 |LEADERBOARD_AP_ERROR_WRONG_RANGE | 잘못된 범위. |
|462855|	0x00071007 |LEADERBOARD_AP_ERROR_WRONG_PARAM | 잘못된 파라미터. |
|462856|    0x00071008 |LEADERBOARD_AP_ERROR_WRONG_PATH | URI 입력 시 오탈자, 파라미터 누락. |
|462857|    0x00071009 |LEADERBOARD_AP_ERROR_TOO_BIG_SIZE | 요청 사이즈 초과. |
|463000|	0x00071098 |LEADERBOARD_AP_ERROR_SYSTEM | 시스템 오류. |
|463001|	0x00071099 |LEADERBOARD_AP_ERROR_UNKOWN | 미확인 오류. |

> [참고]
> 그 외 일반적인 오류 코드의 추가 정보는 다음 링크에서 확인하기 바랍니다.
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml