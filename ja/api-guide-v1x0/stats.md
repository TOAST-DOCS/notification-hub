<!-- 新しい書式のために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しい書式のために見出しを<h1>に変更しました。 -->
<h1>統計</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > 統計**



<span id="statsV1x0001ReadStats"></span>

## 統計照会

統計イベントをイベント発生時間基準で照会します。<br>


**リクエスト**

```
GET /stats/v1.0/stats
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | Y | Appkey |
| X-NHN-Authorization | Header | String | Y | アクセストークン |
| eventCategory | Query | V1x0EventCategory | Y | イベントカテゴリー |
| messageChannel | Query | V1x0MessageChannel | N | メッセージチャネルです。設定しない場合、メッセージチャネル全体に対する統計データが照会され、イベントカテゴリーはメッセージ送信(MESSAGE_SEND)のみ設定できます。<br> |
| statsKeyId | Query | String | N | 統計キーIDです。 |
| messageId | Query | String | N | メッセージIDです。 |
| templateId | Query | String | N | テンプレートIDです。 |
| eventDateTimeFrom | Query | Date | N | 統計イベントの照会開始日時(含む)です。年月日時分まで適用されます。秒とミリ秒は使用されません。<br> 例として、\"2023-12-31T00:00:30.999+09:00\"は\"2023-12-31T00:00:00.000+09:00\"として処理されます。 |
| eventDateTimeTo | Query | Date | N | 統計イベントの照会終了日時(含まない)です。年月日時分まで適用されます。秒とミリ秒は使用されません。<br> 例として、\"2024-01-01T00:00:30.999+09:00\"は\"2024-01-01T00:00:00.000+09:00\"として処理されます。 |
| statsType | Query | V1x0StatsType | N | 統計タイプ<br> - MINUTELY：0分～59分の間でグルーピング<br> - HOURLY：0時～23時の間でグルーピング<br> - DAILY：0日～30日の間でグルーピング<br> - BY_DAY_OF_WEEK：月火水木金土日でグルーピング<br> 例：timeGroupingをBY_DAY_OF_WEEKに設定すると、30日分を照会しても曜日(月～日)基準でデータがグループ化されます。 |
| timeZone | Query | String | N | 統計照会のタイムゾーンです。例：Asia/Seoul、UTC、America/New_York <br> 統計照会時、データを受け取る際に任意のタイムゾーンに設定して受け取ることができます。一般的に、照会するクライアント/ブラウザーのタイムゾーンを設定します。<br> 例えば、曜日別にグルーピングされた統計データを韓国以外の場所で照会した場合、タイムゾーンが異なるため、目的のデータが照会されない場合があります。 |
| statsCriteria | Query | List | N | 照会基準です。設定されたイベントカテゴリーに応じて、設定できる照会基準が変わります。<br> |
| extra1 | Query | String | N | 追加収集されるデータです。 |
| extra2 | Query | String | N | 追加収集されるデータです。 |
| extra3 | Query | String | N | 追加収集されるデータです。 |

* メッセージチャネルに応じて、設定できるイベントカテゴリーが変わります。

    | メッセージチャネル | イベントカテゴリー |
    | --- | --- |
    | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
    | ALIMTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* 照会開始日時は照会期間に含まれ、照会終了日時は照会期間に含まれません。
    * 例：2025年1月1日の1日分のデータを照会するためには、eventDateTimeFromを2025-01-01T00:00:00.000+09:00に設定し、eventDateTimeToを2025-01-02T00:00:00.000+09:00に設定する必要があります。
* イベント以外に追加でデータを収集し、計3つ(extra1、extra2、extra3)の追加フィールドを提供します。
設定されたイベントカテゴリーに応じて、追加収集されるデータの種類が異なります。

    | イベントカテゴリー | 追加データ 1 | 追加データ 2 | 追加データ 3 |
    | --- | --- | --- | --- |
    | MESSAGE_SEND | 送信タイプ(SMS、LMS、MMSなど) | 送信目的(NORMAL、AUTH、AD) | 送信元情報(送信元番号、送信元ドメインなど) |
    | INTERNATIONAL_MESSAGE_SEND | 送信タイプ(SMS、LMS、MMSなど) | 送信目的(NORMAL、AUTH、AD) | 送信元情報(送信元番号、送信元ドメインなど) |


**リクエスト本文**

<!-- リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!-- レスポンス本文を返却しない場合は「このAPIはレスポンス本文を返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "stats" : {
    "columns" : [ {
      "name" : "EVENT_DATE_TIME"
    }, {
      "name" : "REQUESTED"
    }, {
      "name" : "SENT"
    }, {
      "name" : "SEND_FAILED"
    }, {
      "name" : "DELIVERED"
    }, {
      "name" : "DELIVERY_FAILED"
    }, {
      "name" : "OPENED"
    } ],
    "rows" : [ {
      "EVENT_DATE_TIME" : "2023-12-31T00:00:00.000+09:00",
      "REQUESTED" : 10,
      "SENT" : 10,
      "SEND_FAILED" : 1,
      "DELIVERED" : 7,
      "DELIVERY_FAILED" : 1,
      "OPENED" : 1
    } ]
  }
}
```

<!-- レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業の成否を示します。<br>デフォルト値：true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| stats | Object |  |
| stats.columns | Array | イベントカテゴリーに対するイベントがカラムとしてレスポンスされます。<br>EVENT_DATE_TIMEカラムはイベント発生日時を示します。<br> |
| stats.rows | Array | EVENT_DATE_TIMEフィールドを除く残りのフィールドは、イベントカテゴリーに応じてレスポンスされます。<br><br> |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 統計照会

GET {{endpoint}}/stats/v1.0/stats?eventCategory={{eventCategory}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/stats/v1.0/stats?eventCategory=${eventCategory}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
