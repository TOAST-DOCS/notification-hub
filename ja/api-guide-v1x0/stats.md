<!-- pre-align:aligned sig=ec416b7f4d48 -->

<!-- 新しいフォームのために追加されたスタイルです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォームのためにタイトルを<h1>に変更しました。 -->
<h1>統計</h1>

**Notification > Notification Hub > API v1.0 利用ガイド > 統計**



<span id="statsV1x0001ReadStats"></span>

## 統計照会

統計イベントを、イベントが発生した時刻を基準に照会します。<br>


**リクエスト**

```
GET /stats/v1.0/stats
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| eventCategory | Query | Enum | O | イベントカテゴリ |
| messageChannel | Query | Enum | X | メッセージチャンネルです。設定しない場合、すべてのメッセージチャンネルの統計データが照会され、イベントカテゴリはメッセージ送信(MESSAGE_SEND)のみ設定できます。<br> |
| statsKeyId | Query | String | X | 統計キーIDです。 |
| messageId | Query | String | X | メッセージIDです。 |
| templateId | Query | String | X | テンプレートIDです。 |
| eventDateTimeFrom | Query | DateTime | X | 統計イベント照会の開始日時(含む)です。年月日時分まで適用されます。秒とミリ秒は使用されません。<br> 例: \"2023-12-31T00:00:30.999+09:00\"は\"2023-12-31T00:00:00.000+09:00\"として処理されます。 |
| eventDateTimeTo | Query | DateTime | X | 統計イベント照会の終了日時(含まない)です。年月日時分まで適用されます。秒とミリ秒は使用されません。<br> 例: \"2024-01-01T00:00:30.999+09:00\"は\"2024-01-01T00:00:00.000+09:00\"として処理されます。 |
| statsType | Query | Enum | X | 統計タイプ<br> - MINUTELY: 0分〜59分のグルーピング<br> - HOURLY: 0時〜23時のグルーピング<br> - DAILY: 0日〜30日のグルーピング<br> - BY_DAY_OF_WEEK: 月・火・水・木・金・土・日のグルーピング<br> 例: statsTypeをBY_DAY_OF_WEEKに設定すると、30日分を照会しても曜日(月〜日)を基準にデータがグループ化されます。 |
| timeZone | Query | String | X | 統計照会のタイムゾーン(時間帯)です。例: Asia/Seoul、UTC、America/New_York<br> 統計照会時にデータを受け取る際、希望するタイムゾーンに設定して受け取ることができます。通常は照会するクライアント/ブラウザのタイムゾーンを設定します。<br> 例えば、曜日別にグルーピングされた統計データを韓国以外の場所から照会した場合、タイムゾーンが異なるため、希望するデータが照会されない場合があります。 |
| statsCriteria | Query | Array | X | 照会基準です。設定されたイベントカテゴリに応じて、設定できる照会基準が異なります。<br> |
| extra1 | Query | String | X | 追加収集されるデータです。 |
| extra2 | Query | String | X | 追加収集されるデータです。 |
| extra3 | Query | String | X | 追加収集されるデータです。 |

* メッセージチャンネルに応じて、設定できるイベントカテゴリが異なります。

  | メッセージチャンネル | イベントカテゴリ |
      | --- | --- |
  | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
  | ALIMTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* 照会開始日時は照会期間に含まれ、照会終了日時は照会期間に含まれません。
    * 例: 2025年1月1日1日分のデータを照会するには、eventDateTimeFromを2025-01-01T00:00:00.000+09:00に設定し、eventDateTimeToを2025-01-02T00:00:00.000+09:00に設定する必要があります。
* イベント以外に追加でデータを収集し、合計3つ(extra1、extra2、extra3)の追加フィールドを提供します。
  設定されたイベントカテゴリに応じて、追加収集されるデータの種類が異なります。

  | イベントカテゴリ | 追加データ1 | 追加データ2 | 追加データ3 |
      | --- | --- | --- | --- |
  | MESSAGE_SEND | 送信タイプ(SMS、LMS、MMSなど) | 送信目的(NORMAL、AUTH、AD) | 発信情報(発信番号、発信ドメインなど) |
  | INTERNATIONAL_MESSAGE_SEND | 送信タイプ(SMS、LMS、MMSなど) | 送信目的(NORMAL、AUTH、AD) | 発信情報(発信番号、発信ドメインなど) |


**リクエスト本文**

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| stats | Object | O |  |
| stats.columns | Array | O | イベントカテゴリに対するイベントがカラムとして返されます。<br>EVENT_DATE_TIMEカラムはイベント発生日時を示します。<br> |
| stats.rows | Array | O | EVENT_DATE_TIMEフィールドを除くその他のフィールドは、イベントカテゴリに応じて返されます。<br><br> |



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
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>