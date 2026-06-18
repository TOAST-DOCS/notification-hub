<!-- pre-align:aligned sig=5e0edaf20f7a -->

<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>連絡先別受信結果</h1>

**Notification > Notification Hub > API v1.0使用ガイド > 連絡先別受信結果**

<span id="read-contact-delivery-results"></span>

## 連絡先別受信結果一覧照会

送信リクエストされたメッセージの送信および受信結果を、受信者の連絡先単位で照会します。

たとえば、メールアドレスと電話番号を持つ受信者10名に、メール・SMSテンプレートで構成されたフローメッセージを2件送信する場合、連絡先別受信結果一覧を照会すると40件の項目が照会されます。(連絡先2個 × 受信者10名 × フローメッセージ2件 = 連絡先別受信結果40件)
さまざまな検索条件で連絡先別受信結果を照会できます。


**リクエスト**

```
GET /message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリケーションキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageId | Query | String | X | メッセージIDです。メッセージ送信リクエストを受信すると生成される値です。 |
| templateId | Query | String | X | テンプレートIDです。 |
| flowId | Query | String | X | フローIDです。 |
| statsKeyId | Query | String | X | 統計キーIDです。 |
| sender | Query | String | X | 送信者情報です。 |
| contact | Query | String | X | 連絡先です。 |
| messageChannel | Query | Enum | X | メッセージチャンネルです。 |
| messagePurpose | Query | Enum | X | メッセージ目的です。 |
| statuses | Query | Enum | X | メッセージステータスです。送信結果として確認できます。<br>メッセージ送信リクエストを受信すると、メッセージステータスがREQUESTEDに設定されます。<br> |
| scheduled | Query | Boolean | X | 予約送信の有無です。 |
| confirmBeforeSend | Query | Boolean | X | 承認後送信の有無です。 |
| createdDateTimeFrom | Query | DateTime | X | リクエスト開始日時です。デフォルト値は7日前です。 |
| createdDateTimeTo | Query | DateTime | X | リクエスト終了日時です。デフォルト値は現在日時です。 |
| limit | Query | Number | X | 照会するメッセージ数です。デフォルト値は10です。 |
| offset | Query | Number | X | 照会するメッセージの開始位置です。デフォルト値は0です。 |

* **createdDateTimeFrom** と **createdDateTimeTo** の最大照会期間は7日です。


**リクエスト本文**

<!--リクエスト本文が不要な場合は、「このAPIはリクエスト本文を必要としません」と入力します。-->

このAPIはリクエスト本文を必要としません。



**レスポンス本文**

<!--レスポンス本文を返さない場合は、「このAPIはレスポンス本文を返しません」と入力します。-->

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

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| contactDeliveryResults | Array | O | メッセージ送信結果です。 |
| contactDeliveryResults[].messageId | String | O | メッセージID |
| contactDeliveryResults[].recipientIndex | Integer | O | 受信者インデックスです。 |
| contactDeliveryResults[].contactIndex | Integer | O | 連絡先インデックスです。 |
| contactDeliveryResults[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER(電話番号), EMAIL_ADDRESS(メールアドレス), TOKEN_ADM(Amazon Device Messagingトークン), TOKEN_FCM(Firebase Cloud Messagingトークン), TOKEN_APNS(Apple Push Notificationサービストークン), TOKEN_APNS_SANDBOX(APNSサンドボックストークン), TOKEN_APNS_SANDBOX_VOIP(APNSサンドボックスVoIPトークン), TOKEN_APNS_VOIP(APNS VoIPトークン)] |
| contactDeliveryResults[].contact | String | O | 連絡先です。 |
| contactDeliveryResults[].sender | Object | X |  |
| contactDeliveryResults[].sender.senderKey | String | X | 送信プロファイル送信キー |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalkチャンネル名 |
| contactDeliveryResults[].sender.senderProfileType | String | X | 送信プロファイルタイプ<br>[GROUP(グループ送信プロファイル), NORMAL(通常送信プロファイル)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | 送信番号 |
| contactDeliveryResults[].sender.senderMailAddress | String | X | 送信メールアドレス |
| contactDeliveryResults[].sender.brandId | String | X | ブランドID |
| contactDeliveryResults[].sender.chatbotId | String | X | チャット(チャットボット)ID |
| contactDeliveryResults[].templateId | String | X | テンプレートID |
| contactDeliveryResults[].flowId | String | X | フローID |
| contactDeliveryResults[].statsKeyId | String | X | 統計キーID |
| contactDeliveryResults[].clientReference | String | X | ユーザー定義フィールド |
| contactDeliveryResults[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| contactDeliveryResults[].messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(通常), AD(広告), AUTH(認証)] |
| contactDeliveryResults[].options | Object | X |  |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) 通信事業者からデバイスへの送信を試みる時間(1: 1日、2: 40秒、3: 3分、4: 1時間)<br>デフォルト値: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) RCS Biz Center 統計連携のためのグループID [ガイド](../console-guide/send-a-message/#RCS)（最大20バイト） |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | 確認後送信の有無です。 |
| contactDeliveryResults[].confirmedDateTime | String | X | メッセージ送信確認日時です。 |
| contactDeliveryResults[].scheduled | Boolean | O | 予約送信の有無です。 |
| contactDeliveryResults[].scheduledDateTime | String | X | 予約送信日時です。 |
| contactDeliveryResults[].status | String | O | 送信/受信ステータス<br>[REQUESTED(リクエスト済み), CONFIRM_WAITED(確認待機中), WAITED(待機中), SCHEDULED(スケジュール済み), IN_PROGRESS(送信中), SENT(送信済み), SEND_FAILED(送信失敗), DELIVERED(受信済み), DELIVERY_FAILED(受信失敗), CANCELED(キャンセル済み)] |
| contactDeliveryResults[].resultCode | String | X | 送信結果コードです。メッセージチャンネルによって値が異なります。 |
| contactDeliveryResults[].resultMessage | String | X | 送信結果メッセージです。 |
| contactDeliveryResults[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| contactDeliveryResults[].additionalProperty | Object | X |  |
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
### 連絡先別受信結果一覧照会

GET {{endpoint}}/message/v1.0/contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="contactDeliveryResultV1x0002ReadFinalContactDeliveryResults"></span>

<a id="retrieve-a-list-of-the-final-send-status-messages"></a>

## 最終送信ステータスメッセージ一覧照会

送信過程が完了したメッセージの結果一覧を照会します。<br>
最終送信ステータスには「SEND_FAILED(送信失敗)」「DELIVERED(受信成功)」「DELIVERY_FAILED(受信失敗)」「CANCELED(キャンセル)」があります。


**リクエスト**

```
GET /message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリケーションキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageId | Query | String | X | メッセージIDです。メッセージ送信リクエストを受け取ると生成される値です。 |
| templateId | Query | String | X | テンプレートIDです。 |
| flowId | Query | String | X | フローIDです。 |
| statsKeyId | Query | String | X | 統計キーIDです。 |
| sender | Query | String | X | 送信者情報です。 |
| contact | Query | String | X | 連絡先です。 |
| messageChannel | Query | Enum | X | メッセージチャンネルです。 |
| messagePurpose | Query | Enum | X | メッセージ目的です。 |
| scheduled | Query | Boolean | X | スケジュール送信の有無です。 |
| confirmBeforeSend | Query | Boolean | X | 承認後送信の有無です。 |
| updatedDateTimeFrom | Query | DateTime | X | 送信ステータス更新開始日時です。デフォルト値は7日前です。 |
| updatedDateTimeTo | Query | DateTime | X | 送信ステータス更新終了日時です。デフォルト値は現在の日時です。 |
| limit | Query | Number | X | 照会するメッセージ数です。デフォルト値は10です。 |
| offset | Query | Number | X | 照会するメッセージの開始位置です。デフォルト値は0です。 |



**リクエスト本文**

<!--リクエスト本文が不要な場合は「このAPIはリクエスト本文を必要としません」と入力します。-->

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

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| contactDeliveryResults | Array | O | メッセージ送信結果です。 |
| contactDeliveryResults[].messageId | String | O | メッセージID |
| contactDeliveryResults[].recipientIndex | Integer | O | 受信者インデックスです。 |
| contactDeliveryResults[].contactIndex | Integer | O | 連絡先インデックスです。 |
| contactDeliveryResults[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER(電話番号), EMAIL_ADDRESS(メールアドレス), TOKEN_ADM(Amazon Device Messagingトークン), TOKEN_FCM(Firebase Cloud Messagingトークン), TOKEN_APNS(Apple Push Notificationサービストークン), TOKEN_APNS_SANDBOX(APNSサンドボックストークン), TOKEN_APNS_SANDBOX_VOIP(APNSサンドボックスVoIPトークン), TOKEN_APNS_VOIP(APNS VoIPトークン)] |
| contactDeliveryResults[].contact | String | O | 連絡先です。 |
| contactDeliveryResults[].sender | Object | X |  |
| contactDeliveryResults[].sender.senderKey | String | X | 送信プロファイル送信キー |
| contactDeliveryResults[].sender.senderProfileId | String | X | KakaoTalkチャンネル名 |
| contactDeliveryResults[].sender.senderProfileType | String | X | 送信プロファイルタイプ<br>[GROUP(グループ送信プロファイル), NORMAL(一般送信プロファイル)] |
| contactDeliveryResults[].sender.senderPhoneNumber | String | X | 送信番号 |
| contactDeliveryResults[].sender.senderMailAddress | String | X | 送信メールアドレス |
| contactDeliveryResults[].sender.brandId | String | X | ブランドID |
| contactDeliveryResults[].sender.chatbotId | String | X | チャットルーム（チャットボット）ID |
| contactDeliveryResults[].templateId | String | X | テンプレートID |
| contactDeliveryResults[].flowId | String | X | フローID |
| contactDeliveryResults[].statsKeyId | String | X | 統計キーID |
| contactDeliveryResults[].clientReference | String | X | ユーザー定義フィールド |
| contactDeliveryResults[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| contactDeliveryResults[].messagePurpose | String | O | 送信内容タイプ<br>デフォルト値: NORMAL<br>[NORMAL(一般), AD(広告), AUTH(認証)] |
| contactDeliveryResults[].options | Object | X |  |
| contactDeliveryResults[].options.expiryOption | Integer | X | (RCS) 通信会社からデバイスへの送信試行時間（1: 1日、2: 40秒、3: 3分、4: 1時間）<br>デフォルト値: 1 |
| contactDeliveryResults[].options.groupId | String | X | (RCS) RCS Biz Center 統計連携用の group ID [ガイド](../console-guide/send-a-message/#RCS)（最大 20 Byte） |
| contactDeliveryResults[].confirmBeforeSend | Boolean | O | 確認後送信の有無です。 |
| contactDeliveryResults[].confirmedDateTime | String | X | メッセージ送信確認日時です。 |
| contactDeliveryResults[].scheduled | Boolean | O | スケジュール送信の有無です。 |
| contactDeliveryResults[].scheduledDateTime | String | X | スケジュール送信日時です。 |
| contactDeliveryResults[].status | String | O | 送信/受信ステータス<br>[REQUESTED(リクエスト済み), CONFIRM_WAITED(確認待機中), WAITED(待機中), SCHEDULED(スケジュール済み), IN_PROGRESS(進行中), SENT(送信済み), SEND_FAILED(送信失敗), DELIVERED(受信済み), DELIVERY_FAILED(受信失敗), CANCELED(キャンセル済み)] |
| contactDeliveryResults[].resultCode | String | X | 送信結果コードです。メッセージチャンネルによって値が異なります。 |
| contactDeliveryResults[].resultMessage | String | X | 送信結果メッセージです。 |
| contactDeliveryResults[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| contactDeliveryResults[].additionalProperty | Object | X |  |
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
### 最終送信ステータスメッセージ一覧照会

GET {{endpoint}}/message/v1.0/final-contact-delivery-results
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X GET "${endpoint}/message/v1.0/final-contact-delivery-results" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
