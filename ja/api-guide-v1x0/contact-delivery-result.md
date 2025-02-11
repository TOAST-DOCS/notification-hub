<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>連絡先別受信結果</h1>

**Notification > Notification Hub > API v1.0使用ガイド > 連絡先別受信結果**

<span id="read-contact-delivery-results"></span>

### 連絡先別受信結果リスト照会

送信リクエストされたメッセージの送信と受信結果を受信者の連絡先単位で照会します。

例えば、電子メールと電話番号を持つ受信者10人に電子メール、SMSテンプレートで構成された2つのフローメッセージを送信する場合、連絡先別受信結果リストを照会すると、40個の項目が照会されます。 (連絡先2個X受信者10人Xフローメッセージ2個=連絡先別受信結果40個)
様々な検索条件で連絡先別受信結果を照会できます。

<!-- !!! tip 「知っておくべきこと」-->
<!-- APIを使用する際、ユーザーが知っておくと良い注意事項や追加情報を提供する際に使用します。 -->

<!-- !!! warning 「注意」-->
<!--APIを使用する際、従わない場合、サービスの異常または非効率的な動作が発生する可能性がある注意事項を表記する際に使用します。 -->

**リクエスト**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- |----| --- |
| appKey | Header | String | Y  | アプリキー |
| accessToken | Header | String | Y  | 認証トークン |
| createdDateTimeFrom | Query | DateTime(ISO 8601) | Y  | 作成日時開始範囲 |
| createdDateTimeTo | Query | DateTime(ISO 8601) | Y  | 作成日時終了範囲 |
| messageId | Query | String | N  | メッセージID |
| templateId | Query | String | N  | テンプレートID |
| flowId | Query | String | N  | フローID |
| statsKeyId | Query | String | N  | 統計キーID |
| sender | Query | String | N  | 発信者 |
| contact | Query | String | N  | 連絡先 |
| messageChannel | Query | String | N  | メッセージチャンネル<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Query | String | N  | メッセージの目的 |
| status | Query | String | N  | 状態 |
| scheduled | Query | Boolean | N  | 予約送信かどうか |
| confirmBeforeSend | Query | Boolean | N  | 送信前に確認するかどうか |
| limit | Query | Integer | N  | 照会数 |
| offset | Query | Integer | N  | 照会開始位置 |

* **createdDateTimeFrom**と**createdDateTimeTo**の最大照会期間は7日です。

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

<!--リクエスト本文のフィールドを説明します。-->

**レスポンス本文**

<!--レスポンス本文を返さない場合は、「このAPIは応答本文を返しません」と入力します。 -->


```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "contactDeliveryResults": [
    {
      "messageId": "メッセージのID",
      "recipientIndex": 0,
      "contactIndex": 0,
      "contactType": "PHONE_NUMBER",
      "contact": "01012345678",
      "sender": {
        "senderKey": "発信_キー",
        "senderProfileId": "@nhnCloud",
        "senderProfileType": "GROUP",
        "senderPhoneNumber": "01012341234",
        "senderMailAddress": "abcde@nhn.com",
        "brandId": "AR.lj0eOjEI7Y",
        "chatbotId": "01012341234"
      },
      "templateId": "テンプレートのID",
      "flowId": "フローのID",
      "statsKeyId": "統計キーのID",
      "messageChannel": "SMS",
      "messagePurpose": "NORMAL",
      "confirmBeforeSend": false,
      "confirmedDateTime": "2023-01-01T00:00:00Z",
      "scheduled": false,
      "scheduledDateTime": "2024-10-26T07:52:12.728Z",
      "status": "REQUESTED",
      "resultCode": "5.0.0",
      "resultMessage": "Success",
      "templateParameters": {
        "key1": "value1",
        "key2": "value2"
      },
      "additionalProperty": {
        
      },
      "createdDateTime": "2023-01-01T00:00:00Z",
      "sentDateTime": "2023-01-01T00:00:00Z",
      "deliveredDateTime": "2023-01-01T00:00:00Z",
      "openedDateTime": "2023-01-01T00:00:00Z",
      "updatedDateTime": "2023-01-01T00:00:00Z"
    }
  ],
  "totalCount": 1
}
```



<!--レスポンス本文のフィールドを説明します。-->

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| header.isSuccessful | Boolean | APIリクエスト成否 |
| header.resultCode | Integer | 結果コード |
| header.resultMessage | String | 結果メッセージ |
| contactDeliveryResults | Object Array | 連絡先別の受信結果リスト |
| contactDeliveryResults[].messageId | String| メッセージのID |
| contactDeliveryResults[].recipientIndex | Number| 受信者インデックス|
| contactDeliveryResults[].contactIndex | Number| 連絡先インデックス|
| contactDeliveryResults[].contactType | String| 連絡先タイプ |
| contactDeliveryResults[].contact | String| 連絡先|
| contactDeliveryResults[].sender | Object| 発信者|
| contactDeliveryResults[].sender.senderKey | String| 発信プロフィール発信キー、お知らせトークとカカともへのメッセージのみ表示|
| contactDeliveryResults[].sender.senderProfileId | String| 発信プロフィールID、お知らせトークとカカともへのメッセージのみ表示 |
| contactDeliveryResults[].sender.senderProfileType | String| 発信プロフィールタイプ、お知らせトークとカカともへのメッセージのみ表示|
| contactDeliveryResults[].sender.senderPhoneNumber | String| 発信者電話番号、SMSのみ表示|
| contactDeliveryResults[].sender.senderMailAddress | String| 発信者メールアドレス、メールのみ表示|
| contactDeliveryResults[].sender.brandId | String| ブランドID, RCSのみ表示 |
| contactDeliveryResults[].sender.chatbotId | String| チャットルームID, RCSのみ表示 |
| contactDeliveryResults[].templateId | String| テンプレートのID、テンプレートメッセージのみ表示|
| contactDeliveryResults[].flowId | String| フローのID、テンプレートメッセージのみ表示|
| contactDeliveryResults[].statsKeyId | String| 統計キーのID|
| contactDeliveryResults[].messageChannel | String| メッセージチャンネル<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| contactDeliveryResults[].messagePurpose | String| メッセージの目的 |
| contactDeliveryResults[].confirmBeforeSend | Boolean | 承認後送信を使用するかどうか|
| contactDeliveryResults[].confirmedDateTime | DateTime(ISO 86091) | 承認日時(例：2024-10-29T06:09:00+09:00)|
| contactDeliveryResults[].scheduled | Boolean | 予約送信かどうか |
| contactDeliveryResults[].scheduledDateTime | DateTime(ISO 86091) | 予約送信日時 |
| contactDeliveryResults[].status | String| 状態 |
| contactDeliveryResults[].resultCode | String| 結果コード|
| contactDeliveryResults[].resultMessage | String| 結果メッセージ |
| contactDeliveryResults[].templateParameters | Object| テンプレートパラメータ |
| contactDeliveryResults[].additionalProperty | Object| 追加プロパティ、お知らせトーク、 RCSのみ提供|
| contactDeliveryResults[].createdDateTime | DateTime(ISO 86091) | 作成日時(例：2024-10-29T06:09:00+09:00)|
| contactDeliveryResults[].sentDateTime | DateTime(ISO 86091) | 送信日時、送信イベントが収集されるまで値はnull|
| contactDeliveryResults[].deliveredDateTime | DateTime(ISO 86091) | 受信日時、受信イベントが収集されるまで値はnull|
| contactDeliveryResults[].openedDateTime | DateTime(ISO 86091) | 閲覧日時、閲覧イベントが収集されるまで値はnull、プッシュとメールのみ提供 |
| contactDeliveryResults[].updatedDateTime | DateTime(ISO 86091) | 最終アップデート日時|
| totalCount | Number| 全体数|



**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 専門メッセージ送信
POST {{endpoint}}/message/v1.0/contact-delivery-results
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "confirmBeforeSend": false,
  "sender": {
    "senderPhoneNumber": "01012341234"
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "body": "こんにちは。 NHN Cloudの新規商品Notification Hubがリリースされました。"
  }
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X GET "${ENDPOINT}/message/v1.0/contact-delivery-results" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>
