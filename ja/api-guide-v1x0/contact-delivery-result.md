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
| messageChannel | Query | String | N  | メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |
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
    "options" : {
      "expiryOption" : 1,
      "groupId" : "groupId"
    },      
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
| contactDeliveryResults[].sender.senderPhoneNumber | String| 発信者電話番号、SMSのみ表示|
| contactDeliveryResults[].sender.senderMailAddress | String| 発信者メールアドレス、メールのみ表示|
| contactDeliveryResults[].sender.brandId | String| ブランドID, RCSのみ表示 |
| contactDeliveryResults[].sender.chatbotId | String| チャットルームID, RCSのみ表示 |
| contactDeliveryResults[].templateId | String| テンプレートのID、テンプレートメッセージのみ表示|
| contactDeliveryResults[].flowId | String| フローのID、テンプレートメッセージのみ表示|
| contactDeliveryResults[].statsKeyId | String| 統計キーのID|
| contactDeliveryResults[].options | Object | 送信オプション |
| contactDeliveryResults[].options.expiryOption | Integer | RCSメッセージ受信待機有効期限設定値(1: 1日、 2: 40秒、 3: 3分、 4: 1時間) |
| contactDeliveryResults[].options.groupId | String | RCS BizCenter統計連動のためのグループID |
| contactDeliveryResults[].messageChannel | String| メッセージチャンネル<br>SMS, RCS, ALIMTALK, EMAIL, PUSH |
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
<span id="contactDeliveryResultV1x0002ReadFinalContactDeliveryResults"></span>

## 最終送信ステータスメッセージリスト照会

送信プロセスが終了したメッセージ結果リストを照会します。<br>
最終送信ステータスには「SEND_FAILED(送信失敗)」、「DELIVERED(受信成功)」、「DELIVERY_FAILED(受信失敗)」、「CANCELED(キャンセル)」があります。


**リクエスト**

```
GET /message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | アプリキー |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messageId | Query  | String | N | メッセージIDです。メッセージ送信リクエストを受信すると作成される値です。
| templateId | Query  | String | N | テンプレートIDです。 |
| flowId | Query  | String | N | フローIDです。 |
| statsKeyId | Query  | String | N | 統計キーIDです。 |
| sender | Query  | String | N | 発信者情報です。 |
| contact | Query  | String | N | 連絡先です。 |
| messageChannel | Query  | String | N | メッセージチャンネルです。 |
| messagePurpose | Query  | String | N | メッセージの目的です。 |
| scheduled | Query  | Boolean | N | 予約送信なのかどうかを示します。 |
| confirmBeforeSend | Query  | Boolean | N | 承認後に送信するかどうかを示します。 |
| updatedDateTimeFrom | Query  | Date | N | 送信ステータスアップデート開始日時です。デフォルト値は7日前です。 |
| updatedDateTimeTo | Query  | Date | N | 送信ステータスアップデート終了日時です。デフォルト値は現在日時です。 |
| limit | Query  | Integer | N | 照会するメッセージの数です。デフォルト値は10です。 |
| offset | Query  | Integer | N | 照会するメッセージの開始位置です。デフォルト値は0です。 |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は、「このAPIはレスポンス本文を返しません」と入力します。 -->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "contactDeliveryResults" : [ {
    "messageId" : "メッセージのID",
    "recipientIndex" : 0,
    "contactIndex" : 0,
    "contactType" : "PHONE_NUMBER",
    "contact" : "01012345678",
    "sender" : {
      "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c",
      "senderProfileId" : "@nhnCloud",
      "senderProfileType" : "GROUP",
      "senderPhoneNumber" : "01012341234",
      "senderMailAddress" : "abcde@nhn.com",
      "brandId" : "AR.lj0eOjEI7Y",
      "chatbotId" : "01012341234"
    },
    "templateId" : "テンプレートのID",
    "flowId" : "フローのID",
    "statsKeyId" : "統計キーのID",
    "clientReference" : "ユーザー指定フィールド",
    "options" : {
      "expiryOption" : 1,
      "groupId" : "groupId"
    },
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "confirmBeforeSend" : false,
    "confirmedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "scheduled" : false,
    "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
    "status" : "REQUESTED",
    "resultCode" : "5.0.0",
    "resultMessage" : "Success",
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    },
    "additionalProperty" : { },
    "createdDateTime" : "2024-10-29T06:00:01.000+09:00",
    "sentDateTime" : "2024-10-29T06:00:01.000+09:00",
    "deliveredDateTime" : "2024-10-29T06:00:01.000+09:00",
    "openedDateTime" : "2024-10-29T06:00:01.000+09:00",
    "updatedDateTime" : "2024-10-29T06:00:01.000+09:00"
  } ],
  "totalCount" : 1
}
```

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | 作業が成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| contactDeliveryResults | Array | メッセージ送信結果です。 |
| contactDeliveryResults[].messageId | String | メッセージID |
| contactDeliveryResults[].recipientIndex | Integer | 受信者インデックスです。 |
| contactDeliveryResults[].contactIndex | Integer | 連絡先インデックスです。 |
| contactDeliveryResults[].contactType | Object | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| contactDeliveryResults[].contact | String | 連絡先です。 |
| contactDeliveryResults[].sender | Object |  |
| contactDeliveryResults[].sender.senderKey | String | 発信プロフィール発信キー |
| contactDeliveryResults[].sender.senderProfileId | String | カカオトークチャンネル名 |
| contactDeliveryResults[].sender.senderProfileType | String | 発信プロフィールタイプ<br>[GROUP, NORMAL] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | 発信番号 |
| contactDeliveryResults[].sender.senderMailAddress | String | 発信メールアドレス |
| contactDeliveryResults[].sender.brandId | String | ブランドID |
| contactDeliveryResults[].sender.chatbotId | String | チャットルーム(チャットボット) ID |
| contactDeliveryResults[].templateId | String | テンプレートID |
| contactDeliveryResults[].flowId | String | フローID |
| contactDeliveryResults[].statsKeyId | String | 統計キーID |
| contactDeliveryResults[].clientReference | String | ユーザー指定フィールド |
| contactDeliveryResults[].options | Object | 送信オプション |
| contactDeliveryResults[].options.expiryOption | Integer | RCSメッセージ受信待機有効期限設定値(1: 1日、 2: 40秒、 3: 3分、 4: 1時間) |
| contactDeliveryResults[].options.groupId | String | RCS BizCenter統計連動のためのグループID |
| contactDeliveryResults[].messageChannel | Object | メッセージチャンネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| contactDeliveryResults[].messagePurpose | Object | 送信内容タイプ(NORMAL:一般、 AD:広告、 AUTH:認証、 default: NORMAL)<br>[NORMAL, AD, AUTH] |
| contactDeliveryResults[].confirmBeforeSend | Boolean | 確認後に送信するかどうかを示します。 |
| contactDeliveryResults[].confirmedDateTime | String | メッセージ送信確認時刻です。 |
| contactDeliveryResults[].scheduled | Boolean | 予約送信するかどうかを示します。 |
| contactDeliveryResults[].scheduledDateTime | String | 予約送信時刻です。 |
| contactDeliveryResults[].status | Object | 送信/受信状態です。<br>[REQUESTED, CONFIRM_WAITED, WAITED, SCHEDULED, IN_PROGRESS, SENT, SEND_FAILED, DELIVERED, OPENED, DELIVERY_FAILED, CANCELED] |
| contactDeliveryResults[].resultCode | String | 送信結果コードです。メッセージチャンネルによって値が異なります。 |
| contactDeliveryResults[].resultMessage | String | 送信結果メッセージです。 |
| contactDeliveryResults[].templateParameters | Object | テンプレートパラメータです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータはメッセージテンプレートパラメータより優先されます。<br><br> |
| contactDeliveryResults[].additionalProperty | Object |  |
| contactDeliveryResults[].createdDateTime | String | メッセージが作成された時刻です。 |
| contactDeliveryResults[].sentDateTime | String | メッセージが送信された時刻です。 |
| contactDeliveryResults[].deliveredDateTime | String | メッセージを受信した時刻です。 |
| contactDeliveryResults[].openedDateTime | String | メッセージが閲覧された時刻です。 |
| contactDeliveryResults[].updatedDateTime | String | メッセージが修正された時刻です。 |
| totalCount | Integer | 照会されたメッセージ送信結果の総数です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 最終送信ステータスメッセージリスト照会

GET {{endpoint}}/message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/final-contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
