## Game > Leaderboard > Error Code

## Error Codes

以下の表のエラーコードは、Response bodyのheader/bodyにあるresultCodeとresultMessageの意味を説明したものです。
HeaderのresultCodeで以下のエラーコードではなく、HTTPのエラーコードが表示される場合は、以下の[参照]リンクをご参照ください。

|Result Code| Result Code(Hex) | Result Message |説明|
|---|---|---|---|
|0|	0x00000000 |LEADERBOARD_SUCCESS | リクエスト成功 |
|1|	0x00000001 |LEADERBOARD_SUCCESS_BUT_NOT_UPDATE | リクエストは成功したものの、既存と同じデータが入ったため、アップデートはしていない |
|459777|	0x00070401 |LEADERBOARD_ERROR_APPKEY_VERIFIER | アプリキー認証失敗 |
|462849|	0x00071001 |LEADERBOARD_AP_ERROR_INITIALTIZE | リセット失敗 |
|462850|	0x00071002 |LEADERBOARD_AP_ERROR_NOT_EXIST_USER | 未登録ユーザー |
|462851|	0x00071003 |LEADERBOARD_AP_ERROR_NOT_EXIST_FACTOR | 未登録Factor |
|462852|	0x00071004 |LEADERBOARD_AP_ERROR_NOT_EXIST_APPKEY | 未登録アプリキー |
|462853|	0x00071005 |LEADERBOARD_AP_ERROR_TOO_BIG_EXTRA | Extra Data 長さ制限超過 |
|462854|	0x00071006 |LEADERBOARD_AP_ERROR_WRONG_RANGE | 正しくない範囲 |
|462855|	0x00071007 |LEADERBOARD_AP_ERROR_WRONG_PARAM | 正しくないパラメーター |
|462856|    0x00071008 |LEADERBOARD_AP_ERROR_WRONG_PATH | URI入力時誤字、パラメータ不足 |
|463000|	0x00071098 |LEADERBOARD_AP_ERROR_SYSTEM | システムエラー |
|463001|	0x00071099 |LEADERBOARD_AP_ERROR_UNKOWN | 不明なエラー |

> [参照]  
> その他、一般的なエラーコードに対する追加情報は、以下のリンクよりご確認ください。 <br>
> http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml  