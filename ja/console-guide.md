## Game > Leaderboard > コンソール使用ガイド

Leaderboardを使用するためには、サービス利用後、ランキングを登録する必要があります。
サービス利用後は、ゲーム指標の確認、ランキング情報の登録、初期化、削除およびプレイヤーのランキング情報の照会、修正、削除を行うことができます。

<br>

## Configuration

### Leaderboard Service Enable

Console上部の**(+)サービス選択**ボタンをクリックした後、サービスリストから**Leaderboard**サービスをクリックし、サービスを活性化できます。サービスが活性化すると、左側のタブに[Game] > [Leaderboard]メニューが表示されます。

![[図1 Leaderboard サービス活性化]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_1.PNG)


### API URL/AppKey

サービス活性化後、**URL&Appkey**をクリックし、API URLおよびAppkeyの値を確認できます。

![[図2 Leaderboard URL & AppKey 確認]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_2.PNG)

<br>

## Indicator Tab

### Target Date Indicator

特定日付の合計ユーザー数、Factor数、全体データの周期別占有率とFactor別占有率の現状を確認できます。今日の日付から6ヶ月前のデータのみ提供されます。

基本は、今日の日付が選択されリアルタイムデータが表示されますが、過去のデータを確認したい場合は、カレンダーで日付を選択すると、選択した日付の指標を直ちに照会できます。

![[図3 特定の日付の指標確認]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_3.PNG)

**[各項目別の説明]**
#### Data Total

- 選択した日付の合計データ件数

- Factorが三つで、各Factorにデータが100件、200件、300件保存されている場合、Data Total値は600と表示されます。

#### Factor Count

- 選択した日付に登録されているFactor数

- グラフには周期別に何件のFactorが登録されているかが表示されます。

#### データ占有率チャート

- 周期：全体のデータがどの周期に多く分布するかを表示します。
- ファクター：全体のデータがどのFactorに多く分布するかを表示します。


### Range Date Indicator

一定期間のデータの変動量を確認できます。照会可能範囲は、最大6ヶ月です。

最大10件まで特定のFactorを選択可能で、選択していない場合は、選択済みの周期を基準に上位10件のFactorのデータを照会します。

![[図4 一定期間の指標の確認]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_4.PNG)

<br>

## Data Tab

### Search User Info

**[ランキングデータの取得]**

Factor登録後ランキングデータタブに行けば登録したFactorが見えます。 Factorサイクル選択時に、そのサイクルのFactorが選別されます。

![[図5 ランキングデータの検索]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_5.PNG)

**[ユーザ情報検索]**

検索条件に合うランキングデータを照会できます。今後、検索されたユーザーをファイルでダウンロードできる機能を追加する予定です。

![[図6 ユーザ情報検索]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_6.PNG)

**[各項目別の説明]**

#### 周期選択
- 過去の周期：前の周期のランキング情報を基準に検索します。
- 現在の周期：現在の周期のランキング情報を基準に検索します。

#### 検索条件
- 順位別照会：最小値と最大値を入力し、照会するランキングの範囲を決めます。最大500件のデータのみ照会できます。
- ユーザーIDの照会：該当のFactor内に検索したいUser IDを入力します。存在しないUser IDを入力する場合は照会されません。

### Modify User Info

**[修正するユーザーデータの選択]**
照会したユーザーの登録済みのランキング情報を修正できます。

![[図7 修正するユーザーデータの選択]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_7.PNG)

**[ユーザーランキング修正ポップアップ]**
修正を希望するデータを選択し**修正**ボタンをクリックすると、ユーザーのスコア、その他の情報を修正できるポップアップが表示されます。**事由**には、ランキング変更事由を入力し、運営者が修正した履歴は、ランキングデータ画面の**変更履歴**ボタンをクリックすることで確認できます。<br/>
複数のデータを同じ値に修正した場合、修正画面でデータを選択し**選択ユーザー一括入力**ボタンをクリックすると、選択したデータを簡単に一括登録できます。

![[図8 ユーザーランキング修正ポップアップ]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_8.PNG)

### Delete User Info

**[削除するユーザーデータの選択]**
照会画面でデータを選択し**削除**ボタンをクリックすることで、データを削除できます。マルチ選択が可能で、同時に複数のデータを削除することもできます。

![[図9 削除するユーザーデータの選択]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_9.PNG)

**[ユーザーランキング削除ポップアップ]**
削除ボタンを押すと削除事由を入力するポップアップが表示されます。運営者が削除した履歴も修正履歴と同じく、ランキングデータ画面の**変更履歴**ボタンをクリックし確認できます。<br/>削除後は、復旧できないため、慎重に削除する必要があります。

![[図10 ユーザーランキング削除のポップアップ]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_10.PNG)

<br>

## Factor Configuration Tab

> **[重要]**<br>
> Factorの登録、初期化、削除は、プロジェクトのADMINとして登録されている使用者のみ行うことができます。 

### Add Factor

[Game] > [Leaderboard] > [ランキング設定] > [+追加]ボタンをクリックし、Factorを登録します。

> **[参考]**<br>
> Factorは[サイクル、アップデートの基準は、並べ替え基準]の束ねた単位です。<br>
> ハイスコ​​アランキングを毎日、毎週、毎月の使用したい場合はFactorを3つのことをする必要があります。

![[図11 Factor登録のための[+追加]クリック]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_11.PNG)

[+追加]ボタンをクリックすると、図3のようなポップアップが表示されます。

![[図12 Factor追加のポップアップ]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_12.PNG)

**[各項目別の説明]**

#### ファクター名

- ランキングを区分する名前であり、後でファクター検索に使われます。

#### 限界ユーザー数

- ファクターに登録可能な最大のユーザー数を意味します。
- 最大1000万人まで入力できます。

#### その他の情報

- ファクターの追加データで、必要な場合に入力します。

#### ファクターの周期

- ランキングの初期化期間を意味し、日間、週間、月間、全体があります。

#### ファクターリセット時間

- ファクターの初期化時間を設定します。
- 周期が全体である場合、初期化しないため設定はできず、日間、週間、月間のみ設定できます。

#### ファクターリセット日付

- 週間の場合は初期化する曜日を設定し、月間の場合は初期化する日付(1~28の中で選択可能)を設定します。
- 日間、全体周期の場合は、初期化日付設定はできません。

#### ソート基準

- Desc：スコアを降順にソートします。
- Asc：スコアを昇順にソートします。

#### ランキングのアップデート基準

- ランキングのデータを記録する基準を選択します。
- Best Score：ユーザーの最高スコアを記録します。
- Latest Score：ユーザーの最近のスコアを記録します。
- Accumulation Score：ユーザーの累計スコアを合算し記録します。

(例) データのソート基準が昇順で、以前登録されたデータが100、最近登録されたデータが10の場合のランキングデータ記録方法
- Best Score：最高記録の100
- Latest Score：最近の記録の10
- Accumulation Score：累計記録の110(100+10)

#### 同点者処理

- 同点者の順位処理方法を選択します。
- Priority First Ranking Get：先に登録されたユーザーが高いランキングとして記録されます。
- Priority Latest Ranking Get：後で登録されたユーザーが高いランキングとして記録されます。


> [参照]<br>
> FactorIDは、ファクター追加時に自動的に生成されるIDです。

### Search Factor

検索条件がファクター名である時、ファクター名に検索語が含まれたファクターを検索します。

![[図13 検索基準Factor名]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_13.PNG)

検索条件がFactorの周期である時、選択した周期(日間、週間、月間、全体)のファクターを検索します。

![[図14 検索基準Factor 周期]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_14.PNG)

### Init Factor

ファクターに保存されたデータを初期化したり、ファクターを削除できます。<br>
対象となるファクターを選択し、**初期化**ボタンをクリックします。

![[図15 ランキング設定での初期化するFactorの選択]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_15.PNG)

初期化ポップアップにてデータを初期化するファクター情報を確認し、**初期化**ボタンをクリックすると、すべてのデータが削除され、ファクターデータが初期化されます。

![[図16 Factor 初期化ポップアップ]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_16.PNG)

### Delete Factor

下部の「Factor登録情報も削除することを希望する場合はチェックを入れてください」という項目にチェックを入れた後、**初期化**ボタンをクリックすると、登録済みのファクター情報も削除されます。 

![[図17 Factor 削除]](http://static.toastoven.net/prod_leaderboardv2/renewal/console_guide_17.PNG)

※開発に関するapi情報は、[Developer's Guide](/Game/Leaderboard/ja/Developer%60s%20Guide/)をご参照ください。