## Game > Leaderboard > Overview

ゲームにおいて友だちとのランキング競争は今や欠かせない要素となっています。<br>
「Leaderboard」プラットフォームは、簡単な連動だけでランキングサービスを実装できるようサポートします。

<br>

## Merits

![[図0 Leaderboard Merits]](http://static.toastoven.net/prod_leaderboardv2/merits-jp.png)

<br>

## Main Function

以下のような機能を提供します。

### Web Console 

- 使用量の情報確認
- TPS(秒あたりのスループット)確認
- Factor登録 / 照会 / リセット
- ユーザースコア照会 / 変更 / 削除

### HTTP API

- ユーザースコア登録（単一 / 複数）
- ユーザースコア獲得（単一 / 複数 / 範囲）
- Factorに入っているユーザー数照会
- ユーザースコア削除（単一）

<br>

## Term

「Leaderboard」では、次の用語を使います。

| 用語 | 説明 |
| --- | --- |
| Leaderboard AppKey |	プロジェクト別に「Leaderboard AppKey」を発行 |
| Factor |	ランキングの目的を区分する単位。Factorには、周期、アップデート基準、ソート基準を設定 |
| 日間ランキング | 毎日決まった時間にリセットするランキング周期 |
| 週間ランキング | 一週間ごとに決まった曜日・時間にリセットするランキング周期 |
| 月間ランキング | 毎月決まった日付・時間にリセットするランキング周期 |
| 全体ランキング | リセットしないランキング周期 |

<br>

## Service Structure

### Physical Structure

「Leaderboard」プラットフォームの物理的構造は、以下の図の通りです。

![[図1 「Leaderboard」の物理的構造]](http://static.toastoven.net/prod_leaderboardv2/overview_1-jp.png)

- Game Server / Web Consoleは、api-leaderboard.cloud.toast.comでデータをやり取りします。
- Load Balancerは、複数で構成したLeaderboard APサーバーにリクエストを分散します。
- Leaderboard APサーバーは、Memory ServerとCassandraにデータを保存します。
- Leaderboard APサーバーは、Memory Serverからソート済みのデータを取得します。

### Logical Structure

「Leaderboard」プラットフォームの論理的構造は、以下の図の通りです。

![[図2 「Leaderboard」の論理的構造]](http://static.toastoven.net/prod_leaderboardv2/overview_2-jp.png)

- プロジェクト別にLeaderboard AppKeyが存在します。
- Leaderboard AppKey内に複数のFactorを登録できます。
- 1つのFactorに1つの周期を設定できます。

<br>

## Feature

設定はFactor単位で行うことができます。設定により、様々な特性のリーダーボードをご利用いただけます。

###  Sorting

スコアソート方式は、昇順/降順ソートで設定できます。

**[昇順ソート]**

昇順ソートは、低いスコアから高いスコアへソートします。

![[図3 昇順ソート]](http://static.toastoven.net/prod_leaderboardv2/overview_3-jp.png)

**[降順ソート]**

降順ソートは、高いスコアから低いスコアへソートします。

![[図4 降順ソート]](http://static.toastoven.net/prod_leaderboardv2/overview_4-jp.png)

### Score update

スコアのアップデート方式は、最高/最新/累計スコアで設定できます。

**[最高スコアのアップデート]**

新しく入ったスコアが前のスコアより高い場合は、アップデートを行います。

![[図5 最高スコアのアップデート]](http://static.toastoven.net/prod_leaderboardv2/overview_5-jp.png)

**[最新スコアのアップデート]**

既存のスコアとは関係なく、新しいスコアをアップデートします（常にアップデート）。

![[図6 最新スコアのアップデート]](ㅗttp://static.toastoven.net/prod_leaderboardv2/overview_6-jp.png)

**[累計スコアのアップデート]*

新しいスコアと既存のスコアの合計をアップデートします。

![[図7 累計スコアのアップデート]](http://static.toastoven.net/prod_leaderboardv2/overview_7-jp.png)

### Tie score

同点者のランキング決定方式は、Factor単位で最初/最新ランキング獲得者の優先順位で設定できます。

**[最初ランキング獲得者の優先順位]**

同点者が複数いる場合、先に登録されたユーザー方が高いランキングになります。

![[図8 最初ランキング獲得者の優先順位]](http://static.toastoven.net/prod_leaderboardv2/overview_8-jp.png)

**[最新ランキング獲得者の優先順位]**

同点者が複数いる場合、遅れて登録されたユーザーの方が高いランキングになります。

![[図9 最新ランキング獲得者の優先順位]](http://static.toastoven.net/prod_leaderboardv2/overview_9-jp.png)

### Reset time

該当Factorのリセット時間を設定できます。<br>
全体ランキングはリセットされません。

### Reset Date

週間ランキングはリセットの曜日を、月間ランキングはリセットの日付を指定できます。<br>
全体ランキングはリセットされません。

### Limit User

該当Factorに登録できる最大ユーザー数を意味します。最大1000万人まで入力できます。

