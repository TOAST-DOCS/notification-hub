<!-- pre-align:aligned sig=8c77b572b6aa -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>連絡先別受信結果</h1>

**Notification > Notification Hub > API v1.0使用ガイド > 連絡先別受信結果**

<a id="retrieve-a-list-of-received-results-by-contacts"></a>
## 連絡先別受信結果リスト照会 { #retrieve-a-list-of-received-results-by-contacts }

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
| messageChannel | Query | Enum | X | メッセージチャンネルです。<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), RCS(RCS), EMAIL(Email), PUSH(Push)] |
| messagePurpose | Query | Enum | X | メッセージ目的です。<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| statuses | Query | Enum | X | メッセージのステータスです。送信結果として確認できます。<br> メッセージ送信リクエストを受信すると、メッセージステータスがREQUESTEDに設定されます。<br> <br>[REQUESTED(リクエスト済み), SCHEDULED(スケジュール済み), READY(準備完了), CONFIRM_WAITED(確認待機中), WAITED(待機中), IN_PROGRESS(送信中), SENT(送信済み), SEND_FAILED(送信失敗), DELIVERED(受信済み), DELIVERY_FAILED(受信失敗), CANCELED(キャンセル済み)] |
| messagePurpose | Query | String | N  | メッセージの目的 |
| status | Query | String | N  | 状態 |
| scheduled | Query | Boolean | N  | 予約送信かどうか |
| confirmBeforeSend | Query | Boolean | N  | 送信前に確認するかどうか |
| limit | Query | Integer | N  | 照会数 |
| offset | Query | Integer | N  | 照会開始位置 |

**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

<!--リクエスト本文のフィールドを説明します。-->

**レスポンス本文**

<!--レスポンス本文を返さない場合は、「このAPIは応答本文を返しません」と入力します。 -->


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
    "templateId" : "Tj3nE8dq",
    "flowId" : "R2m9Kv0x",
    "statsKeyId" : "aA123456",
    "clientReference" : "ユーザー定義フィールド",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "options" : {
      "expiryOption" : 1,
      "groupId" : "20240814125609swLmoZTsGr0"
    },
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
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://example.com/thumbnail.jpg"
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

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| contactDeliveryResults | Array | O | メッセージ送信結果です。 |
| contactDeliveryResults[].messageId | String | O | メッセージID |
| contactDeliveryResults[].recipientIndex | Integer | O | 受信者インデックスです。 |
| contactDeliveryResults[].contactIndex | Integer | O | 連絡先インデックスです。 |
| contactDeliveryResults[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER(電話番号)、EMAIL_ADDRESS(メールアドレス)、TOKEN_ADM(Amazon Device Messagingトークン)、TOKEN_FCM(Firebase Cloud Messagingトークン)、TOKEN_APNS(Apple Push Notificationサービストークン)、TOKEN_APNS_SANDBOX(APNSサンドボックストークン)、TOKEN_APNS_SANDBOX_VOIP(APNSサンドボックスVoIPトークン)、TOKEN_APNS_VOIP(APNS VoIPトークン)] |
| contactDeliveryResults[].contact | String | O | 連絡先です。 |
| contactDeliveryResults[].sender | Object | X | チャンネル別の送信者情報です。<br>- ALIMTALK : senderKey, senderProfileId, senderProfileType<br>- SMS : senderPhoneNumber<br>- EMAIL : senderMailAddress<br>- RCS : brandId, chatbotId<br> |
| contactDeliveryResults[].sender.senderKey | String | X | 発信プロフィール発信キー |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalkチャンネル名 |
| contactDeliveryResults[].sender.senderProfileType | String | X | 発信プロフィールタイプ<br>[GROUP(グループ発信プロフィール)、NORMAL(一般発信プロフィール)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | 発信番号 |
| contactDeliveryResults[].sender.senderMailAddress | String | X | 発信メールアドレス |
| contactDeliveryResults[].sender.brandId | String | X | ブランドID |
| contactDeliveryResults[].sender.chatbotId | String | X | チャットルーム(チャットボット)ID |
| contactDeliveryResults[].templateId | String | X | テンプレートID |
| contactDeliveryResults[].flowId | String | X | フローID |
| contactDeliveryResults[].statsKeyId | String | X | 統計キーID |
| contactDeliveryResults[].clientReference | String | X | ユーザー定義フィールド |
| contactDeliveryResults[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| contactDeliveryResults[].messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般)、AD(広告)、AUTH(認証)] |
| contactDeliveryResults[].options | Object | X | チャンネル別オプションです。 |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) キャリアからデバイスへの送信試行時間(1: 1日、2: 40秒、3: 3分、4: 1時間)<br>デフォルト値: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) RCS Biz Center統計連動のためのgroup ID [ガイド](../console-guide/send-a-message/#RCS) (最大20 Byte) |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | 確認後送信かどうかです。 |
| contactDeliveryResults[].confirmedDateTime | String | X | メッセージ送信確認日時です。 |
| contactDeliveryResults[].scheduled | Boolean | O | 予約送信かどうかです。 |
| contactDeliveryResults[].scheduledDateTime | String | X | 予約送信日時です。 |
| contactDeliveryResults[].status | String | O | 送信/受信ステータス<br>[REQUESTED(リクエスト済み)、CONFIRM_WAITED(確認待ち)、WAITED(待機中)、SCHEDULED(スケジュール済み)、IN_PROGRESS(送信中)、SENT(送信済み)、SEND_FAILED(送信失敗)、DELIVERED(受信済み)、DELIVERY_FAILED(受信失敗)、CANCELED(キャンセル済み)] |
| contactDeliveryResults[].resultCode | String | X | 送信結果コードです。メッセージチャンネルによって値が異なります。 |
| contactDeliveryResults[].resultMessage | String | X | 送信結果メッセージです。 |
| contactDeliveryResults[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| contactDeliveryResults[].imageParameters | Array | X | 受信者別の画像パラメーターです。ブランドメッセージでのみ使用されます。 |
| contactDeliveryResults[].imageParameters[].attachmentId | String | X | 添付ファイルID |
| contactDeliveryResults[].imageParameters[].imageUrl | String | X | 画像URL |
| contactDeliveryResults[].imageParameters[].imageLink | String | X | 画像クリック時に移動するURL |
| contactDeliveryResults[].videoParameter | Object | X | 受信者別のビデオパラメーターです。ブランドメッセージでのみ使用されます。 |
| contactDeliveryResults[].videoParameter.videoUrl | String | X | カカオTV動画URL |
| contactDeliveryResults[].videoParameter.thumbnailAttachmentId | String | X | サムネイル画像添付ファイルID |
| contactDeliveryResults[].videoParameter.thumbnailUrl | String | X | 動画サムネイルイメージURL |
| contactDeliveryResults[].additionalProperty | Object | X | メッセージチャンネルの追加プロパティです。 |
| contactDeliveryResults[].createdDateTime | String | O | メッセージが作成された日時です。 |
| contactDeliveryResults[].sentDateTime | String | X | メッセージが送信された日時です。 |
| contactDeliveryResults[].deliveredDateTime | String | X | メッセージが受信された日時です。 |
| contactDeliveryResults[].openedDateTime | String | X | メッセージが開封された日時です。 |
| contactDeliveryResults[].updatedDateTime | String | X | メッセージが更新された日時です。 |
| totalCount | Integer | O | 照会されたメッセージ送信結果の総件数です。 |



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

```curl
curl -X GET "${ENDPOINT}/message/v1.0/contact-delivery-results" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>

</details>

<a id="retrieve-a-list-of-the-final-send-status-messages"></a>
## 最終送信ステータスメッセージリスト照会 { #retrieve-a-list-of-the-final-send-status-messages }

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
| messageChannel | Query | Enum | X | メッセージチャンネルです。<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), RCS(RCS), EMAIL(Email), PUSH(Push)] |
| messagePurpose | Query | Enum | X | メッセージ目的です。<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
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
    "templateId" : "Tj3nE8dq",
    "flowId" : "R2m9Kv0x",
    "statsKeyId" : "aA123456",
    "clientReference" : "ユーザー定義フィールド",
    "messageChannel" : "SMS",
    "messagePurpose" : "NORMAL",
    "options" : {
      "expiryOption" : 1,
      "groupId" : "20240814125609swLmoZTsGr0"
    },
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
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://example.com/thumbnail.jpg"
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
| contactDeliveryResults[].sender | Object | X | チャンネル別の送信者情報です。<br>- ALIMTALK : senderKey, senderProfileId, senderProfileType<br>- SMS : senderPhoneNumber<br>- EMAIL : senderMailAddress<br>- RCS : brandId, chatbotId<br> |
| contactDeliveryResults[].sender.senderKey | String | 発信プロフィール発信キー |
| contactDeliveryResults[].sender.senderProfileId | String | カカオトークチャンネル名 |
| contactDeliveryResults[].sender.senderProfileType | String | 送信元プロフィールタイプ<br>[GROUP(グループ送信元プロフィール)、NORMAL(一般送信元プロフィール)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | 発信番号 |
| contactDeliveryResults[].sender.senderMailAddress | String | 発信メールアドレス |
| contactDeliveryResults[].sender.brandId | String | ブランドID |
| contactDeliveryResults[].sender.chatbotId | String | チャットルーム(チャットボット) ID |
| contactDeliveryResults[].templateId | String | テンプレートID |
| contactDeliveryResults[].flowId | String | フローID |
| contactDeliveryResults[].statsKeyId | String | 統計キーID |
| contactDeliveryResults[].clientReference | String | ユーザー指定フィールド |
| contactDeliveryResults[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), BRANDMESSAGE(ブランドメッセージ), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| contactDeliveryResults[].options.expiryOption | Integer | (RCS) RCSメッセージ受信待機有効期限設定値(1: 1日、 2: 40秒、 3: 3分、 4: 1時間) |
| contactDeliveryResults[].options | Object | X | チャンネル別オプションです。 |
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
| contactDeliveryResults[].imageParameters | Array | X | 受信者別のイメージパラメーターです。ブランドメッセージでのみ使用されます。 |
| contactDeliveryResults[].imageParameters[].attachmentId | String | X | 添付ファイルID |
| contactDeliveryResults[].imageParameters[].imageUrl | String | X | 画像URL |
| contactDeliveryResults[].imageParameters[].imageLink | String | X | 画像クリック時に移動する URL |
| contactDeliveryResults[].videoParameter | Object | X | 受信者別のビデオパラメーターです。ブランドメッセージでのみ使用されます。 |
| contactDeliveryResults[].videoParameter.videoUrl | String | X | カカオTV動画URL |
| contactDeliveryResults[].videoParameter.thumbnailAttachmentId | String | X | サムネイル画像添付ファイルID |
| contactDeliveryResults[].videoParameter.thumbnailUrl | String | X | 動画サムネイル画像 URL |
| contactDeliveryResults[].additionalProperty | Object | X | メッセージチャンネルの追加プロパティです。 |
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

```http
curl -X GET "${endpoint}/message/v1.0/final-contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
