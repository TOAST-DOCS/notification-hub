<!-- pre-align:aligned sig=ff946ac84827 -->

<!-- 新しいフォーマットのために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォーマットのために見出しを<h1>に変更しました。 -->
# Kakao統計

**Notification > Notification Hub > API v1.0 使用ガイド > Kakao統計**

Kakao Biz Centerで提供する統計データを照会します。
統計データは送信元キーを基準として日別(DAILY)または月別(MONTHLY)で照会できます。
DAILY：直近90日以内のデータのみ照会可能であり、照会範囲は最大90日です。
MONTHLY：直近3か月以内のデータのみ照会可能であり、照会範囲は最大3か月です。

* リアルタイムの統計は提供しておらず、前日に収集したデータを毎日午前7時頃に提供します。
* お知らせトークの統計はD+1に初回提供し、D+2に確定します。
* 有効既読数は同じメッセージに対して重複集計しません。
* クリック数は同じメッセージに対して重複集計します。
* 送信成功件数が10件以下の場合は、有効既読数とクリック数を提供しません。

<a id="delivery-statistics"></a>
### 送信統計

送信元プロフィールを基準として、日別の送信数、有効既読数、クリック数を照会します。期間、送信識別子、メッセージタイプなどを設定して照会できます。

<a id="template-statistics"></a>
### テンプレート統計

テンプレート及びグループタグを基準として、日別の送信数、有効既読数、クリック数を照会します。期間、メッセージタイプなどを設定して照会できます。

* ブランドメッセージ(自由型)はグループタグを使用した場合にのみ提供します。



<a id="retrieve-alimtalk-delivery-statistics"></a>
## お知らせトーク送信統計の照会

お知らせトークの送信統計を照会します。
送信元プロフィールを基準として、日別の送信数、有効既読数、クリック数を照会します。期間、送信識別子、メッセージタイプなどを設定して照会できます。

照会期間(startDate ～ endDate)は最大3か月です。


**リクエスト**

```
GET /kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| senderKey | Query | String | O | 送信元キーです。 |
| periodType | Query | Enum | O | 照会期間の単位です。 |
| startDate | Query | String | O | 照会の開始日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) |
| endDate | Query | String | O | 照会の終了日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) startDate ～ endDateは最大3か月です。 |
| messageType | Query | Enum | X | メッセージのタイプです。 |
| receiveUserType | Query | Enum | X | 送信識別子です。 |
| limit | Query | Number | X | limitを設定しない場合のデフォルト値は500です。(最大1,000) |
| offset | Query | Number | X | offsetを設定しない場合のデフォルト値は0です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "alimtalkDeliveryStatistics" : [ {
    "date" : "2026-01-15",
    "messageType" : "AT",
    "receiveUserType" : "PhoneNumber",
    "totalSendRequestCount" : 1000,
    "validSendRequestCount" : 950,
    "validReadCount" : 800
  } ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| totalCount | Integer | O | 総件数 |
| alimtalkDeliveryStatistics | Array | O |  |
| alimtalkDeliveryStatistics[].date | String | O | 日付 (日別：YYYY-MM-DD、月別：YYYY-MM) |
| alimtalkDeliveryStatistics[].messageType | String | O | お知らせトークのメッセージタイプ<br>[AT(一般お知らせトーク)、AI(画像お知らせトーク)] |
| alimtalkDeliveryStatistics[].receiveUserType | String | O | 送信識別子<br>[PhoneNumber(電話番号)、AppUserId(アプリユーザーID)、UserKey(ユーザーキー)、None(受信者の識別子なし)] |
| alimtalkDeliveryStatistics[].totalSendRequestCount | Integer | O | 総送信リクエスト数 |
| alimtalkDeliveryStatistics[].validSendRequestCount | Integer | O | 有効送信リクエスト数 |
| alimtalkDeliveryStatistics[].validReadCount | Integer | O | 有効既読数 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトーク送信統計の照会

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/ALIMTALK?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="retrieve-alimtalk-template-statistics"></a>
## お知らせトークテンプレート統計の照会

お知らせトークテンプレートの統計を照会します。
テンプレート及びグループタグを基準として、日別の送信数、有効既読数、クリック数を照会します。期間、メッセージタイプなどを設定して照会できます。

照会期間(startDate ～ endDate)は最大3か月です。


**リクエスト**

```
GET /kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| senderKey | Query | String | O | 送信元キーです。 |
| periodType | Query | Enum | O | 照会期間の単位です。 |
| startDate | Query | String | O | 照会の開始日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) |
| endDate | Query | String | O | 照会の終了日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) startDate ～ endDateは最大3か月です。 |
| kakaoTemplateCode | Query | String | X | Kakaoのテンプレートコードです。 |
| messageType | Query | Enum | X | メッセージのタイプです。 |
| limit | Query | Number | X | limitを設定しない場合のデフォルト値は500です。(最大1,000) |
| offset | Query | Number | X | offsetを設定しない場合のデフォルト値は0です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "alimtalkTemplateStatistics" : [ {
    "date" : "2026-01-15",
    "messageType" : "AT",
    "templateCode" : "template_001",
    "totalSendSuccessCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
  } ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| totalCount | Integer | O | 総件数 |
| alimtalkTemplateStatistics | Array | O |  |
| alimtalkTemplateStatistics[].date | String | O | 日付 (日別：YYYY-MM-DD、月別：YYYY-MM) |
| alimtalkTemplateStatistics[].messageType | String | O | お知らせトークのメッセージタイプ<br>[AT(一般お知らせトーク)、AI(画像お知らせトーク)] |
| alimtalkTemplateStatistics[].templateCode | String | O | テンプレートコード |
| alimtalkTemplateStatistics[].totalSendSuccessCount | Integer | O | 総送信成功数 |
| alimtalkTemplateStatistics[].validReadCount | Integer | O | 有効既読数 |
| alimtalkTemplateStatistics[].totalClickCount | Integer | O | 総クリック数 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレート統計の照会

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/ALIMTALK?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="retrieve-brand-message-delivery-statistics"></a>
## ブランドメッセージ送信統計の照会

ブランドメッセージの送信統計を照会します。
送信元プロフィールを基準として、日別の送信数、有効既読数、クリック数を照会します。期間、送信識別子、メッセージタイプなどを設定して照会できます。

照会期間(startDate ～ endDate)は最大3か月です。


**リクエスト**

```
GET /kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| senderKey | Query | String | O | 送信元キーです。 |
| periodType | Query | Enum | O | 照会期間の単位です。 |
| startDate | Query | String | O | 照会の開始日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) |
| endDate | Query | String | O | 照会の終了日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) startDate ～ endDateは最大3か月です。 |
| messageSpec | Query | Enum | X | 送信タイプです。 |
| chatBubbleType | Query | Enum | X | メッセージのタイプです。 |
| targeting | Query | Enum | X | 送信ターゲティングの有無です。 |
| friendType | Query | Enum | X | 友だちのタイプです。 |
| receiveUserType | Query | Enum | X | 送信識別子です。 |
| limit | Query | Number | X | limitを設定しない場合のデフォルト値は500です。(最大1,000) |
| offset | Query | Number | X | offsetを設定しない場合のデフォルト値は0です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "brandmessageDeliveryStatistics" : [ {
    "date" : "2026-01-15",
    "receiveUserType" : "PhoneNumber",
    "messageSpec" : "BASIC",
    "chatBubbleType" : "TEXT",
    "friendType" : "F",
    "targeting" : "M",
    "totalSendRequestCount" : 1000,
    "validSendRequestCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
  } ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| totalCount | Integer | O | 総件数 |
| brandmessageDeliveryStatistics | Array | O |  |
| brandmessageDeliveryStatistics[].date | String | O | 日付 (日別：YYYY-MM-DD、月別：YYYY-MM) |
| brandmessageDeliveryStatistics[].receiveUserType | String | O | 送信識別子<br>[PhoneNumber(電話番号)、AppUserId(アプリユーザーID)、UserKey(ユーザーキー)、None(受信者の識別子なし)] |
| brandmessageDeliveryStatistics[].messageSpec | String | O | 送信タイプ<br>[BASIC(基本型)、FREESTYLE(自由型)] |
| brandmessageDeliveryStatistics[].chatBubbleType | String | O | メッセージのタイプ<br>[TEXT(テキスト型)、IMAGE(画像型)、WIDE(ワイド画像型)、WIDE_ITEM_LIST(ワイドアイテムリスト型)、CAROUSEL_FEED(カルーセルフィード型)、PREMIUM_VIDEO(プレミアム動画型)、COMMERCE(コマース型)、CAROUSEL_COMMERCE(カルーセルコマース型)] |
| brandmessageDeliveryStatistics[].friendType | String | O | 友だちのタイプ<br>[F(友だち)、N(非友だち)] |
| brandmessageDeliveryStatistics[].targeting | String | O | 送信ターゲティングの有無<br>[M(マーケティング受信同意ユーザー全体)、N(チャンネルフレンドを除く)、I(チャンネルフレンドのみ)、F(チャンネルフレンド全体)] |
| brandmessageDeliveryStatistics[].totalSendRequestCount | Integer | O | 総送信リクエスト数 |
| brandmessageDeliveryStatistics[].validSendRequestCount | Integer | O | 有効送信リクエスト数 |
| brandmessageDeliveryStatistics[].validReadCount | Integer | O | 有効既読数 |
| brandmessageDeliveryStatistics[].totalClickCount | Integer | O | 総クリック数 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ブランドメッセージ送信統計の照会

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/delivery-statistics/BRANDMESSAGE?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<a id="retrieve-brand-message-template-statistics"></a>
## ブランドメッセージテンプレート統計の照会

ブランドメッセージテンプレートの統計を照会します。
テンプレート及びグループタグを基準として、日別の送信数、有効既読数、クリック数を照会します。期間、メッセージタイプなどを設定して照会できます。

照会期間(startDate ～ endDate)は最大3か月です。


**リクエスト**

```
GET /kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| senderKey | Query | String | O | 送信元キーです。 |
| periodType | Query | Enum | O | 照会期間の単位です。 |
| startDate | Query | String | O | 照会の開始日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) |
| endDate | Query | String | O | 照会の終了日です。(DAILY：YYYY-MM-DD、MONTHLY：YYYY-MM) startDate ～ endDateは最大3か月です。 |
| kakaoTemplateCode | Query | String | X | Kakaoのテンプレートコードです。 |
| groupTagKey | Query | String | X | グループタグキーです。 |
| messageSpec | Query | Enum | X | 送信タイプです。 |
| chatBubbleType | Query | Enum | X | メッセージのタイプです。 |
| targeting | Query | Enum | X | 送信ターゲティングの有無です。 |
| friendType | Query | Enum | X | 友だちのタイプです。 |
| limit | Query | Number | X | limitを設定しない場合のデフォルト値は500です。(最大1,000) |
| offset | Query | Number | X | offsetを設定しない場合のデフォルト値は0です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は"このAPIはリクエスト本文を必要としません"と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は"このAPIはレスポンス本文を返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "totalCount" : 1,
  "brandmessageTemplateStatistics" : [ {
    "date" : "2026-01-15",
    "templateCode" : "template_001",
    "groupTagKey" : "group_tag_001",
    "messageSpec" : "BASIC",
    "chatBubbleType" : "TEXT",
    "friendType" : "F",
    "targeting" : "M",
    "totalSendSuccessCount" : 950,
    "validReadCount" : 800,
    "totalClickCount" : 500
  } ]
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| totalCount | Integer | O | 総件数 |
| brandmessageTemplateStatistics | Array | O |  |
| brandmessageTemplateStatistics[].date | String | O | 日付 (日別：YYYY-MM-DD、月別：YYYY-MM) |
| brandmessageTemplateStatistics[].templateCode | String | O | テンプレートコード |
| brandmessageTemplateStatistics[].groupTagKey | String | X | グループタグキー |
| brandmessageTemplateStatistics[].messageSpec | String | O | 送信タイプ<br>[BASIC(基本型)、FREESTYLE(自由型)] |
| brandmessageTemplateStatistics[].chatBubbleType | String | O | メッセージのタイプ<br>[TEXT(テキスト型)、IMAGE(画像型)、WIDE(ワイド画像型)、WIDE_ITEM_LIST(ワイドアイテムリスト型)、CAROUSEL_FEED(カルーセルフィード型)、PREMIUM_VIDEO(プレミアム動画型)、COMMERCE(コマース型)、CAROUSEL_COMMERCE(カルーセルコマース型)] |
| brandmessageTemplateStatistics[].friendType | String | O | 友だちのタイプ<br>[F(友だち)、N(非友だち)] |
| brandmessageTemplateStatistics[].targeting | String | O | 送信ターゲティングの有無<br>[M(マーケティング受信同意ユーザー全体)、N(チャンネルフレンドを除く)、I(チャンネルフレンドのみ)、F(チャンネルフレンド全体)] |
| brandmessageTemplateStatistics[].totalSendSuccessCount | Integer | O | 総送信成功数 |
| brandmessageTemplateStatistics[].validReadCount | Integer | O | 有効既読数 |
| brandmessageTemplateStatistics[].totalClickCount | Integer | O | 総クリック数 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ブランドメッセージテンプレート統計の照会

GET {{endpoint}}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE?senderKey={{senderKey}}&periodType={{periodType}}&startDate={{startDate}}&endDate={{endDate}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/kakaobizcenter/v1.0/kakao-statistics/template-statistics/BRANDMESSAGE?senderKey=${senderKey}&periodType=${periodType}&startDate=${startDate}&endDate=${endDate}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
