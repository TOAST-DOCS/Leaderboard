## Game > Leaderboard > 概要

ゲームでフレンドとの順位競争は、今では欠かすことのできない要素です。<br>
Leaderboardプラットフォームを使用すれば、簡単な連動だけでランキングサービスを実装できます。

<br>

## Merits

![[図0 Leaderboard Merits]](http://static.toastoven.net/prod_leaderboardv2/newMerits_jp_202203.png)

<br>

## 主な機能

次のような機能を提供します。

### ウェブコンソール

- 使用量情報確認
- TPS(1秒当たりの処理量)確認
- ファクター登録、検索、初期化
- ユーザースコア検索、変更、削除

### HTTP API

- ユーザースコア登録(単一、多数)
- ユーザースコア獲得(単一、多数、範囲)
- ファクターに含まれるユーザー数の検索
- ユーザースコア削除(単一)

<br>

## 用語

Leaderboardでは次の用語を使用します。

| 用語 | 説明 |
| --- | --- |
| Leaderboard AppKey |	プロジェクトにつき1つのLeaderboard AppKeyを発行する。 |
| ファクター |	ランキング目的を区分する単位。ファクターには周期、アップデート基準、ソート基準設定。 |
| デイリーランキング | 毎日決められた時間に初期化するランキング周期。 |
| 週間ランキング | 毎週決められた曜日、決められた時間に初期化するランキング周期。 |
| 月間ランキング | 毎月決められた日、決められた時間に初期化するランキング周期。 |
| 全体ランキング | 初期化しないランキング周期。 |

<br>

## サービス構造

### 物理的構造

Leaderboardプラットフォームの物理的構造は、下図のとおりです。

![[図1 Leaderboard物理的構造]](http://static.toastoven.net/prod_leaderboardv2/overview_1-jp.png)

- ゲームサーバー/NHN Cloud Consoleは、api-leaderboard.cloud.toast.comとデータを送受信します。
- Load Balancerは、複数台で構成したLeaderboard APサーバーに要請を分配します。
- Leaderboard APサーバーは、メモリサーバーとCassandraにデータを保存します。
- Leaderboard APサーバーは、メモリサーバーでソートされたデータを取得します。

### 論理的構造

Leaderboardプラットフォームの論理的構造は、下図のとおりです。

![[図2 Leaderboard論理的構造]](http://static.toastoven.net/prod_leaderboardv2/overview_2-jp.png)

- 1つのプロジェクトにつき1つのLeaderboard AppKeyがあります。
- Leaderboard AppKey内に複数個のファクターを登録できます。
- 1つのファクターに1つの周期を設定できます。

<br>

## 特徴

設定はファクター単位で可能です。設定によって複数の特性のLeaderboardを使用できます。

### ソート

スコアソート方式は、昇順、降順を設定できます。

**[昇順ソート]**

昇順ソートは、小さいスコアから大きいスコアにソートします。

![[図3昇順ソート]](http://static.toastoven.net/prod_leaderboardv2/overview_3-jp.png)

**[降順ソート]**

降順ソートは、大きいスコアから小さいスコアにソートします。

![[図4降順ソート]](http://static.toastoven.net/prod_leaderboardv2/overview_4-jp.png)

### スコアアップデート

スコアアップデート方式は、最高、最新、累積スコアに設定できます。

**[最高スコアアップデート]**

新しいスコアが以前のスコアより高いスコアの時にアップデートします。

![[図5最高スコアアップデート]](http://static.toastoven.net/prod_leaderboardv2/overview_5-jp.png)

**[最新スコアアップデート]**

既存スコアと関係なく新しいスコアをアップデートします(常にアップデート).

![[図6最新スコアアップデート]](http://static.toastoven.net/prod_leaderboardv2/overview_6-jp.png)

**[累積スコアアップデート]**

新しいスコアと既存スコアを合算してアップデートします。

![[図7累積スコアアップデート]](http://static.toastoven.net/prod_leaderboardv2/overview_7-jp.png)

### 同点者の処理

同点者の順位決定方式は、ファクター単位で最初、最新ランキング獲得者優先順位に設定できます。

**[最初ランキング獲得者優先順位]**

同点者が複数人いる場合、先に登録されたユーザーが高い順位になります。

![[図8：最初ランキング獲得者優先順位]](http://static.toastoven.net/prod_leaderboardv2/overview_8-jp.png)

**[最新ランキング獲得者優先順位]**

同点者が複数人の場合、後に登録されたユーザーが高い順位になります。

![[図9：最新ランキング獲得者優先順位]](http://static.toastoven.net/prod_leaderboardv2/overview_9-jp.png)

### 初期化時間

ファクターの初期化時間を設定できます。<br>
全体ランキングは初期化されません。

### 初期化日時

週間ランキングは初期化曜日を、月間ランキングは初期化日を指定できます。<br>
全体ランキングは初期化されません。

### 限界ユーザー数

ファクターに登録できる最大ユーザー数を意味します。最大1,000万人まで入力できます。
