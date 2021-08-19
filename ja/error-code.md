## Game > Leaderboard > エラーコード

## エラーコード

下記表のエラーコードはResponse bodyのheader/bodyにあるresultCodeとresultMessageの意味を説明します。
headerにあるresultCodeで下記のエラーコードではなくHTTPエラーコードが表示された場合、下記[参考]リンクを参照してください。

|Result Code| Result Code(Hex) | Result Message |説明|
|---|---|---|---|
|0|	0x00000000 |LEADERBOARD_SUCCESS | 要請成功。|
|1|	0x00000001 |LEADERBOARD_SUCCESS_BUT_NOT_UPDATE | 要請は成功しましたが、既存と同じデータが入ってアップデートしない。 |
|459777|	0x00070401 |LEADERBOARD_ERROR_APPKEY_VERIFIER | AppKey認証失敗。 |
|462849|	0x00071001 |LEADERBOARD_AP_ERROR_INITIALIZE | 初期化失敗。 |
|462850|	0x00071002 |LEADERBOARD_AP_ERROR_NOT_EXIST_USER | 登録されていないUser。 |
|462851|	0x00071003 |LEADERBOARD_AP_ERROR_NOT_EXIST_FACTOR | 登録されていないFactor。|
|462852|	0x00071004 |LEADERBOARD_AP_ERROR_NOT_EXIST_APPKEY | 登録されていないAppKey。 |
|462853|	0x00071005 |LEADERBOARD_AP_ERROR_TOO_BIG_EXTRA | Extra Data制限の長さを超過。 |
|462854|	0x00071006 |LEADERBOARD_AP_ERROR_WRONG_RANGE | 無効な範囲。 |
|462855|	0x00071007 |LEADERBOARD_AP_ERROR_WRONG_PARAM | 無効なパラメータ。 |
|462856|    0x00071008 |LEADERBOARD_AP_ERROR_WRONG_PATH | URI入力時の誤字・脱字、パラメータ漏れ。 |
|462857|    0x00071009 |LEADERBOARD_AP_ERROR_TOO_BIG_SIZE | リクエストサイズを超え。 |
|463000|	0x00071098 |LEADERBOARD_AP_ERROR_SYSTEM | システムエラー。 |
|463001|	0x00071099 |LEADERBOARD_AP_ERROR_UNKOWN | 未確認エラー。 |

> [参考]
> その他一般的なエラーコードの追加情報は次のリンクからご確認ください。
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml
