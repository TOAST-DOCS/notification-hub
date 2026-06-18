<!-- pre-align:aligned sig=ec416b7f4d48 -->

<!-- 新しい様式のために追加された style です。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しい様式のためにタイトルを <h1> に変更しました。 -->
<h1>統計</h1>

**Notification > Notification Hub > API v1.0 사용 가이드 > 통계**



<span id="statsV1x0001ReadStats"></span>

## 統計照会

統計イベントを、イベントが発生した時間基準で照会します。<br>


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
| eventCategory | Query | Enum | O | イベントカテゴリー |
| messageChannel | Query | Enum | X | メッセージチャンネルです。設定しない場合、全メッセージチャンネルの統計データが照会され、イベントカテゴリーはメッセージ送信（MESSAGE_SEND）のみ設定できます。<br> |
| statsKeyId | Query | String | X | 統計キー ID です。 |
| messageId | Query | String | X | メッセージ ID です。 |
| templateId | Query | String | X | テンプレート ID です。 |
| eventDateTimeFrom | Query | DateTime | X | 統計イベント照会開始日時（含む）です。年月日時分まで適用されます。秒とミリ秒は使用されません。<br> 例: \"2023-12-31T00:00:30.999+09:00\" は \"2023-12-31T00:00:00.000+09:00\" として処理されます。 |
| eventDateTimeTo | Query | DateTime | X | 統計イベント照会終了日時（含まない）です。年月日時分まで適用されます。秒とミリ秒は使用されません。<br> 例: \"2024-01-01T00:00:30.999+09:00\" は \"2024-01-01T00:00:00.000+09:00\" として処理されます。 |
| statsType | Query | Enum | X | 統計タイプ<br> - MINUTELY: 0分〜59分でグループ化<br> - HOURLY: 0時〜23時でグループ化<br> - DAILY: 0日〜30日でグループ化<br> - BY_DAY_OF_WEEK: 月火水木金土日でグループ化<br> 例: statsType を BY_DAY_OF_WEEK に設定すると、30日分を照会しても曜日（月〜日）基準でデータがグループ化されます。 |
| timeZone | Query | String | X | 統計照会タイムゾーン（時間帯）です。例: Asia/Seoul, UTC, America/New_York <br> 統計照会時に、希望するタイムゾーンでデータを受け取ることができます。一般的には、照会するクライアント/ブラウザのタイムゾーンを設定します。<br> 例えば、曜日別にグループ化された統計データを韓国以外の場所から照会した場合、タイムゾーンが異なるため、希望するデータが照会されない場合があります。 |
| statsCriteria | Query | Array | X | 照会基準です。設定されたイベントカテゴリーに応じて、設定できる照会基準が異なります。<br> |
| extra1 | Query | String | X | 追加収集されるデータです。 |
| extra2 | Query | String | X | 追加収集されるデータです。 |
| extra3 | Query | String | X | 追加収集されるデータです。 |

* メッセージチャンネルに応じて、設定できるイベントカテゴリーが異なります。

  | メッセージチャンネル | イベントカテゴリー |
      | --- | --- |
  | SMS | MESSAGE_SEND, INTERNATIONAL_MESSAGE_SEND |
  | ALIMTALK, RCS, EMAIL, PUSH | MESSAGE_SEND |
* 照会開始日時は照会期間に含まれ、照会終了日時は照会期間に含まれません。
    * 例: 2025年1月1日の1日分のデータを照会するには、eventDateTimeFrom を 2025-01-01T00:00:00.000+09:00 に設定し、eventDateTimeTo を 2025-01-02T00:00:00.000+09:00 に設定する必要があります。
* イベント以外に追加でデータを収集し、合計3つ（extra1、extra2、extra3）の追加フィールドを提供します。
  設定されたイベントカテゴリーに応じて、追加収集されるデータの種類が異なります。

  | イベントカテゴリー | 追加データ 1 | 追加データ 2 | 追加データ 3 |
      | --- | --- | --- | --- |
  | MESSAGE_SEND | 送信タイプ（SMS、LMS、MMS など） | 送信目的（NORMAL、AUTH、AD） | 発信情報（発信番号、発信ドメインなど） |
  | INTERNATIONAL_MESSAGE_SEND | 送信タイプ（SMS、LMS、MMS など） | 送信目的（NORMAL、AUTH、AD） | 発信情報（発信番号、発信ドメインなど） |


**リクエスト本文**

<!--リクエスト本文を要求しない場合は「この API はリクエスト本文を要求しません」と入力します。-->

この API はリクエスト本文を要求しません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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
| header | Object | O | |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| stats | Object | O | |
| stats.columns | Array | O | イベントカテゴリーに対するイベントがカラムとしてレスポンスされます。<br>EVENT_DATE_TIME カラムはイベント発生日時を示します。<br> |
| stats.rows | Array | O | EVENT_DATE_TIME フィールドを除くその他のフィールドは、イベントカテゴリーに応じてレスポンスされます。<br><br> |



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