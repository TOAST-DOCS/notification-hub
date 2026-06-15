<!-- pre-align:aligned sig=65b610526e63 -->

<!-- 新しいフォーマットのために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォーマットのために見出しを<h1>に変更しました。 -->
<h1>メッセージ</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > メッセージ**



<span id="messageV1x0001SmsFreeFormMessages"></span>

## 自由形式メッセージの送信リクエスト - SMS

SMSに対する自由形式メッセージの送信をリクエストします。メッセージ内容をリクエスト本文に入力した後、送信をリクエストします。

各メッセージチャンネルへメッセージを送信するには、各メッセージチャンネルの送信元情報が登録されている必要があります。送信元情報の登録は、**Notification Hubコンソール** > **送信元情報タブ**で行えます。メッセージチャンネルの送信元情報に関する詳細な説明は、**Notification** > **Notification Hub** > **利用ポリシーおよび事前設定のご案内**で確認できます。


**リクエスト**

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | 送信元番号 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |
| content | Object | X |  |
| content.messageType | String | O | 送信メッセージのタイプ(SMS、LMS、MMS)<br>[SMS(ショートメッセージ)、LMS(ロングメッセージ)、MMS(マルチメディアメッセージ)] |
| content.title | String | X | メッセージのタイトル |
| content.body | String | O | メッセージの本文 |
| content.attachmentIds | Array | X | 添付ファイルID(最大3つ) |

* メッセージチャンネルにより、**sender**、**content**フィールドは異なる形式を持ちます。
* メッセージチャンネルにより、**recipients[].contact.contactType**、**recipients[].contact.contact**フィールドに入力できる値が異なります。
* 予約送信の場合は**scheduledDateTime**を設定します。送信が開始される前の予約送信は、リクエストのキャンセルが可能です。リクエストキャンセルAPIを呼び出すか、**Notification Hubコンソール** > **送信照会**からキャンセルできます。
* 確認後送信の場合は、**confirmBeforeSend**を**true**に設定します。確認後送信のメッセージは、**Notification Hubコンソール** > **送信照会**で承認を行うと送信が進行します。
* 予約送信と確認後送信は同時に設定できません。

<a id="sender-fields-by-message-channel"></a>

### メッセージチャンネル別のsenderフィールド

| メッセージチャンネル | フィールド | 説明 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 送信元番号 |
| RCS | sender.brandId | ブランドID |
| RCS | sender.chatbotId | トークルームID |
| EMAIL | sender.senderMailAddress | 送信元メールアドレス |
| ALIMTALK | sender.senderKey | 送信元キー |
| ALIMTALK | sender.senderProfileType | 送信元プロフィールタイプ<br>GROUP、NORMAL |

* お知らせトーク(ALIMTALK)は、送信元キー(senderKey)と送信元プロフィールタイプ(senderProfileType)を必須で入力する必要があります。
* お知らせトーク(ALIMTALK)は、送信時にテンプレートが必ず必要です。自由形式メッセージの送信をサポートしていません。
* 送信元プロフィールタイプには**GROUP(グループ)**と**NORMAL(一般)**があります。**GROUP**はグループ送信元プロフィール、**NORMAL**は一般送信元プロフィールです。


**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージの送信リクエスト - SMS

POST {{endpoint}}/message/v1.0/SMS/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/SMS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderPhoneNumber" : "01012341234"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0003EmailFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---email"></a>

## 自由形式メッセージの送信リクエスト - EMAIL

EMAILに対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "EMAIL_ADDRESS",
      "contact" : "recipient@example.com",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリングアラート",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| sender | Object | X |  |
| sender.senderMailAddress | String | O | 送信元メールアドレス |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |
| content | Object | X |  |
| content.title | String | O | テンプレートメールのタイトル |
| content.body | String | O | テンプレートメールの本文 |
| content.attachmentIds | Array | X | テンプレートの添付ファイルID |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージの送信リクエスト - EMAIL

POST {{endpoint}}/message/v1.0/EMAIL/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "EMAIL_ADDRESS",
      "contact" : "recipient@example.com",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリングアラート",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/EMAIL/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "senderMailAddress" : "abcde@nhn.com"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "EMAIL_ADDRESS",
      "contact" : "recipient@example.com",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "title" : "[NHN Cloud Email][##env##] モニタリングアラート",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0004RcsFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---rcs"></a>

## 自由形式メッセージの送信リクエスト - RCS

RCSに対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定のタイトル",
              "description" : "予定の説明"
            }
          }
        }
      }
    } ]
  },
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| sender | Object | O |  |
| sender.brandId | String | O | ブランドID |
| sender.chatbotId | String | O | トークルーム(チャットボット)ID |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |
| content | Object | X |  |
| content.messageType | String | X | RCS送信メッセージのタイプ<br>[SMS(ショートメッセージ)、LMS(ロングメッセージ)、MMS(マルチメディアメッセージ)、RBC_TEMPLATE(RCS Biz Centerテンプレート)] |
| content.title | String | X | (Deprecated、content.cards[].titleを使用) メッセージのタイトル |
| content.body | String | X | (Deprecated、content.cards[].descriptionを使用) メッセージの本文 |
| content.smsType | String | X | SMSのタイプ<br>[STANDALONE(スタンドアロン型)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| content.lmsType | String | X | LMSのタイプ<br>[STANDALONE(スタンドアロン型)、FORMAT_BASIC(基本形式)、FORMAT_TITLE_HIGHLIGHT(タイトル強調形式)、FORMAT_PARAGRAPH(段落形式)、UNIFIED_STANDALONE(統合スタンドアロン型)] |
| content.mmsType | String | X | MMSのタイプ(MMS送信の場合は必須)<br>[HORIZONTAL(横型)、VERTICAL(縦型)、CAROUSEL_MEDIUM(カルーセル中型)、CAROUSEL_SMALL(カルーセル小型)、UNIFIED_HORIZONTAL(統合横型)、UNIFIED_VERTICAL(統合縦型)] |
| content.messagebaseId | String | X | RCS Biz CenterテンプレートID |
| content.unsubscribePhoneNumber | String | X | 受信拒否番号(広告送信の場合は必須) |
| content.cards | Array | X | RCSカード |
| content.cards[].title | String | X | タイトル |
| content.cards[].description | String | X | 本文 |
| content.cards[].attachmentId | String | X | 添付ファイルID<br>※ 統合MMSカードでGIF画像を添付すると、iOSデバイスでは受信できません。 |
| content.cards[].mTitle | String | X | メインタイトル |
| content.cards[].mTitleMedia | String | X | メインタイトルロゴファイルID |
| content.cards[].title1 | String | X | タイトル 1 |
| content.cards[].title2 | String | X | タイトル 2 |
| content.cards[].title3 | String | X | タイトル 3 |
| content.cards[].description1 | String | X | 本文 1 |
| content.cards[].description2 | String | X | 本文 2 |
| content.cards[].description3 | String | X | 本文 3 |
| content.cards[].buttons | Array | X | RCSボタンリスト |
| content.cards[].buttons[].buttonType | String | X | COMPOSE(トークルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(地図を表示する)、MAP_QUERY(地図を検索する)、MAP_SHARE(現在地を共有する)、URL(URLに接続する)、CALENDAR(予定を登録する)<br>※ 統合メッセージタイプにCLIPBOARD(コピーする)ボタンを使用すると、iOSデバイスでは受信できません。<br><br>[COMPOSE、CLIPBOARD、DIALER、MAP_SHOW、MAP_QUERY、MAP_SHARE、URL、CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | ボタンアクション |
| content.buttons | Array | X | (Deprecated、content.cards[].buttonsを使用) RCSボタンリスト |
| content.buttons[].buttonType | String | X | COMPOSE(トークルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(地図を表示する)、MAP_QUERY(地図を検索する)、MAP_SHARE(現在地を共有する)、URL(URLに接続する)、CALENDAR(予定を登録する)<br>※ 統合メッセージタイプにCLIPBOARD(コピーする)ボタンを使用すると、iOSデバイスでは受信できません。<br><br>[COMPOSE、CLIPBOARD、DIALER、MAP_SHOW、MAP_QUERY、MAP_SHARE、URL、CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | ボタンアクション |
| options | Object | X |  |
| options.expiryOption | Integer | X | 通信キャリアからデバイスへの送信を試みる時間(1：1日、2：40秒、3：3分、4：1時間)<br>デフォルト値：1 |
| options.groupId | String | X | RCS Biz Center統計連動のためのグループID [ガイド](../console-guide/send-a-message/#RCS) (最大20 Byte) |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージの送信リクエスト - RCS

POST {{endpoint}}/message/v1.0/RCS/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定のタイトル",
              "description" : "予定の説明"
            }
          }
        }
      }
    } ]
  },
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/RCS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "sender" : {
    "brandId" : "AR.lj0eOjEI7Y",
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "content" : {
    "messageType" : "SMS",
    "title" : "祝日の営業時間のお知らせ",
    "body" : "こんにちは。本日お客様の商品が入荷いたしました。ご来店ください^^",
    "smsType" : "STANDALONE",
    "lmsType" : "HORIZONTAL",
    "mmsType" : "HORIZONTAL",
    "messagebaseId" : "44o4SUjpqnjDuUcH+uHvPg==",
    "unsubscribePhoneNumber" : "08012341234",
    "cards" : [ {
      "title" : "タイトル",
      "description" : "本文",
      "attachmentId" : "20240814125609swLmoZTsGr0",
      "mTitle" : "メインタイトル",
      "mTitleMedia" : "LT-messagebase.common-2k8ydI",
      "title1" : "タイトル 1",
      "title2" : "タイトル 2",
      "title3" : "タイトル 3",
      "description1" : "本文 1",
      "description2" : "本文 2",
      "description3" : "本文 3",
      "buttons" : [ {
        "buttonType" : "CALENDAR",
        "buttonJson" : {
          "action" : {
            "displayText" : "予定を登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "予定のタイトル",
                "description" : "予定の説明"
              }
            }
          }
        }
      } ]
    } ],
    "buttons" : [ {
      "buttonType" : "CALENDAR",
      "buttonJson" : {
        "action" : {
          "displayText" : "予定を登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "予定のタイトル",
              "description" : "予定の説明"
            }
          }
        }
      }
    } ]
  },
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  }
}'
```

</details>

<span id="messageV1x0005PushFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---push"></a>

## 自由形式メッセージの送信リクエスト - PUSH

PUSHに対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "TOKEN_FCM",
      "contact" : "TOKEN_FCM",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに対するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに対する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |
| content | Object | X | プッシュメッセージの内容 |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージの送信リクエスト - PUSH

POST {{endpoint}}/message/v1.0/PUSH/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "TOKEN_FCM",
      "contact" : "TOKEN_FCM",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに対するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに対する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/PUSH/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "TOKEN_FCM",
      "contact" : "TOKEN_FCM",
      "clientReference" : "1234:abcd:011-asd"
    } ]
  } ],
  "id" : "alpha123",
  "content" : {
    "unsubscribePhoneNumber" : "代表番号",
    "unsubscribeGuide" : "メニュー > 設定",
    "title" : "タイトル",
    "body" : "内容",
    "richMessage" : {
      "buttons" : [ {
        "name" : "ボタン名",
        "submitName" : "送信ボタン名",
        "buttonType" : "ボタンタイプ、REPLY、DEEP_LINK、OPEN_APP、OPEN_URL、DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに対するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ、IMAGE、GIF、VIDEO、AUDIO。AndroidではIMAGEのみサポート",
        "extension" : "メディアファイルの拡張子、jpg、png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きなアイコンの位置、REMOTE、LOCAL",
        "source" : "メディアが位置する場所のアドレス、URL、LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
        "description" : "グループに対する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}'
```

</details>

<span id="messageV1x0006TemplateMessages"></span>

<a id="request-template-message-sending"></a>

## テンプレートメッセージの送信リクエスト

登録したテンプレートを利用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単一受信者、一括受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単一受信者(recipient)<br>
* 一括/グループ受信者(id)<br>
  <br>
  予約送信の場合は'scheduledDateTime'を設定します。<br>
  確認後送信の場合は'confirmBeforeSend'をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageChannel | Path | Enum | O | メッセージのチャンネルです。 |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| templateId | String | X | テンプレートID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートメッセージの送信リクエスト

POST {{endpoint}}/message/v1.0/{{messageChannel}}/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/${messageChannel}/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0007AlimtalkTemplateMessages"></span>

<a id="send-alimtalk-template-message"></a>

## お知らせトークテンプレートメッセージの送信

登録したテンプレートを利用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単一受信者、一括受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単一受信者(recipient)<br>
* 一括/グループ受信者(id)<br>
  <br>
  予約送信の場合は'scheduledDateTime'を設定します。<br>
  確認後送信の場合は'confirmBeforeSend'をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/ALIMTALK/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| sender | Object | X |  |
| sender.senderKey | String | O | 送信元プロフィール送信元キー |
| templateId | String | O | テンプレートID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートメッセージの送信

POST {{endpoint}}/message/v1.0/ALIMTALK/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/ALIMTALK/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0008EmailTemplateMessages"></span>

<a id="send-email-template-message"></a>

## EMAILテンプレートメッセージの送信

登録したテンプレートを利用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単一受信者、一括受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単一受信者(recipient)<br>
* 一括/グループ受信者(id)<br>
  <br>
  予約送信の場合は'scheduledDateTime'を設定します。<br>
  確認後送信の場合は'confirmBeforeSend'をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/EMAIL/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| templateId | String | X | テンプレートID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### EMAILテンプレートメッセージの送信

POST {{endpoint}}/message/v1.0/EMAIL/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/EMAIL/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0008RcsTemplateMessages"></span>

<a id="send-rcs-template-message"></a>

## RCSテンプレートメッセージの送信

登録したテンプレートを利用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単一受信者、一括受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単一受信者(recipient)<br>
* 一括/グループ受信者(id)<br>
  <br>
  予約送信の場合は'scheduledDateTime'を設定します。<br>
  確認後送信の場合は'confirmBeforeSend'をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "unsubscribePhoneNumber" : "08012341234"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| sender | Object | X |  |
| sender.chatbotId | String | X | トークルーム(チャットボット)ID |
| content | Object | X |  |
| content.unsubscribePhoneNumber | String | X | 受信拒否電話番号 |
| templateId | String | X | テンプレートID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |
| options | Object | X |  |
| options.expiryOption | Integer | X | 通信キャリアからデバイスへの送信を試みる時間(1：1日、2：40秒、3：3分、4：1時間)<br>デフォルト値：1 |
| options.groupId | String | X | RCS Biz Center統計連動のためのグループID [ガイド](../console-guide/send-a-message/#RCS) (最大20 Byte) |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレートメッセージの送信

POST {{endpoint}}/message/v1.0/RCS/template-messages/{{messagePurpose}}
{
  "statsKeyId" : "aA123456",
  "sender" : {
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "unsubscribePhoneNumber" : "08012341234"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/RCS/template-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "sender" : {
    "chatbotId" : "44o4SUjpqnjDuUcH+uHvPg=="
  },
  "content" : {
    "unsubscribePhoneNumber" : "08012341234"
  },
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "options" : {
    "expiryOption" : 1,
    "groupId" : "20240814125609swLmoZTsGr0"
  }
}'
```

</details>

<span id="messageV1x0008SmsTemplateMessages"></span>

<a id="send-sms-template-message"></a>

## SMSテンプレートメッセージの送信

登録したテンプレートを利用してメッセージを送信します。
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。

受信対象の設定は、単一受信者、一括受信者、グループクエリのいずれかを選択して設定する必要があります。
* 単一受信者(recipient)
* 一括/グループ受信者(id)

予約送信の場合は'scheduledDateTime'を設定します。
確認後送信の場合は'confirmBeforeSend'をtrueに設定します。

画像レイアウトが連動したMMSテンプレートの送信時、次の事項に留意する必要があります。
* **必須のテンプレートパラメーター**：cardNumber、scratchNumberを必ず含める必要があります。
  * cardNumber：バーコードの作成に使用され、必ず16桁の数字で構成されている必要があります。
  * scratchNumber：別途の制約条件はありません。
* **画像レイアウトのOverride**：リクエスト本文にcontent.imageLayoutIdまたはcontent.imageLayoutNameを含めて、テンプレートに設定された画像レイアウトを変更できます。
  * content.imageLayoutIdとcontent.imageLayoutNameのどちらか一方のみ使用する必要があります。
  * 両方のフィールドとも含まれていない場合は、テンプレート作成時に連動したデフォルトの画像レイアウトが使用されます。


**リクエスト**

```
POST /message/v1.0/SMS/template-messages/{messagePurpose}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "content" : {
    "imageLayoutId" : "aA123456",
    "imageLayoutName" : "2025-プロモーション-レイアウト"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| templateId | String | X | テンプレートID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| content | Object | X |  |
| content.imageLayoutId | String | X | 画像レイアウトID |
| content.imageLayoutName | String | X | 画像レイアウト名 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレートメッセージの送信

POST {{endpoint}}/message/v1.0/SMS/template-messages/{{messagePurpose}}
{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "content" : {
    "imageLayoutId" : "aA123456",
    "imageLayoutName" : "2025-プロモーション-レイアウト"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/SMS/template-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "templateId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "content" : {
    "imageLayoutId" : "aA123456",
    "imageLayoutName" : "2025-プロモーション-レイアウト"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123"
}'
```

</details>

<span id="messageV1x0009FlowMessages"></span>

<a id="send-flow-message"></a>

## フローメッセージの送信

登録したフローを利用してメッセージを送信します。<br>
フローを登録していない場合は、フローを登録して送信する必要があります。<br>
<br>
受信対象の設定は、単一受信者、一括受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単一受信者(recipient)<br>
* 一括/グループ受信者(id)<br>
  <br>
  予約送信の場合は'scheduledDateTime'を設定します。<br>
  確認後送信の場合は'confirmBeforeSend'をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "flow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "タイトル",
        "body" : "本文"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "nextSteps" : [ {
        "messageChannel" : "RCS"
      } ]
    } ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| flowId | String | X | フローID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 一括受信者の一覧およびファイルのアップロード成功時に作成されるID |
| flow | Object | X |  |
| flow.steps | Array | O |  |
| flow.steps[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS)、ALIMTALK(お知らせトーク)、EMAIL(メール)、RCS(RCS)、PUSH(プッシュ)] |
| flow.steps[].sender | Object | X | 送信元情報です。送信元情報はメッセージのチャンネルにより異なる構成になる場合があります。<br> |
| flow.steps[].content | Object | X | メッセージの内容です。メッセージの内容はメッセージのチャンネルにより異なる構成になる場合があります。<br> |
| flow.steps[].options | Object | X | 送信オプションです。送信オプションはメッセージのチャンネルにより異なる構成になる場合があります。<br> |
| flow.steps[].nextSteps | Array | X | 次の段階です。次の段階がない場合、メッセージの送信が終了します。<br> |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローメッセージの送信

POST {{endpoint}}/message/v1.0/flow-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "flow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "タイトル",
        "body" : "本文"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "nextSteps" : [ {
        "messageChannel" : "RCS"
      } ]
    } ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/flow-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "statsKeyId" : "aA123456",
  "flowId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "id" : "alpha123",
  "flow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "タイトル",
        "body" : "本文"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "nextSteps" : [ {
        "messageChannel" : "RCS"
      } ]
    } ]
  }
}'
```

</details>

<span id="messageV1x0010InstantFlowMessages"></span>

<a id="send-an-instant-flow-message"></a>

## インスタントフローメッセージの送信

メッセージ送信リクエスト時にフローを定義してメッセージの送信をリクエストします。<br>
<br>
インスタントフロー入力時にテンプレートを利用して送信をリクエストしたり、直接送信元情報や内容を入力して送信をリクエストしたりできます。


**リクエスト**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | メッセージの目的です。 |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->


```
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "instantFlow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "タイトル",
        "body" : "本文"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}
```

<!--リクエストボディのフィールドを説明します。-->

| パス | 型 | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| scheduledDateTime | String | X | 予約送信時間 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | O |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER、EMAIL_ADDRESS、TOKEN_ADM、TOKEN_FCM、TOKEN_APNS、TOKEN_APNS_SANDBOX、TOKEN_APNS_SANDBOX_VOIP、TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるカスタムフィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| instantFlow | Object | O |  |
| instantFlow.steps | Array | O |  |
| instantFlow.steps[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS)、ALIMTALK(お知らせトーク)、EMAIL(メール)、RCS(RCS)、PUSH(プッシュ)] |
| instantFlow.steps[].sender | Object | X | 送信元情報です。送信元情報はメッセージのチャンネルにより異なる構成になる場合があります。<br> |
| instantFlow.steps[].content | Object | X | メッセージの内容です。メッセージの内容はメッセージのチャンネルにより異なる構成になる場合があります。<br> |
| instantFlow.steps[].options | Object | X | 送信オプションです。送信オプションはメッセージのチャンネルにより異なる構成になる場合があります。<br> |
| instantFlow.steps[].templateId | String | X | テンプレートIDです。テンプレートIDを設定した場合、リクエスト時に送信元情報(sender)とメッセージの内容(content)は適用されません。<br>インスタントフローメッセージでテンプレートIDを設定しない場合は、送信元情報(sender)とメッセージの内容(content)が必ず必要です。<br> |
| instantFlow.steps[].nextSteps | Array | X | 次の段階です。次の段階がない場合、メッセージの送信が終了します。<br> |



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  },
  "messageId" : "aA123456"
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### インスタントフローメッセージの送信

POST {{endpoint}}/message/v1.0/instant-flow-messages/{{messagePurpose}}
{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "instantFlow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "タイトル",
        "body" : "本文"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/instant-flow-messages/${messagePurpose}" \
-d '{
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false,
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "recipients" : [ {
    "contacts" : [ {
      "contactType" : "PHONE_NUMBER",
      "contact" : "01012345678",
      "clientReference" : "1234:abcd:011-asd"
    } ],
    "templateParameters" : {
      "key1" : "value1",
      "key2" : "value2"
    }
  } ],
  "instantFlow" : {
    "steps" : [ {
      "messageChannel" : "SMS",
      "sender" : {
        "senderPhoneNumber" : "0123456789"
      },
      "content" : {
        "title" : "タイトル",
        "body" : "本文"
      },
      "options" : {
        "expiryOption:" : 1,
        "groupId\"" : "groupId"
      },
      "templateId" : "Tj3nE8dq",
      "nextSteps" : [ ]
    } ]
  }
}'
```

</details>

<span id="messageV1x0100MessageIdDoCancel"></span>

<a id="cancel-sending-message"></a>

## メッセージの送信キャンセル

送信をキャンセルするメッセージIDを入力して送信をキャンセルします。<br>
メッセージ送信時にレスポンスとして受け取ったメッセージIDを使用して、送信をキャンセルできます。<br>
メッセージ内のすべてのリクエストがキャンセルされます。<br>


**リクエスト**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageId | Path | String | O |  |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メッセージの送信キャンセル

POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/messages/${messageId}/do-cancel" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>

<span id="messageV1x0101MessageIdDoConfirm"></span>

<a id="confirm-message-delivery"></a>

## メッセージの送信確認

確認後送信をリクエストしたメッセージを確認します。<br>


**リクエスト**

```
POST /message/v1.0/messages/{messageId}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | 型 | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageId | Path | String | O |  |



**リクエストボディ**

<!--リクエストボディを必要としない場合は"このAPIはリクエストボディを必要としません"と入力します。-->

このAPIはリクエストボディを必要としません。



**レスポンスボディ**

<!--レスポンスボディを返さない場合は"このAPIはレスポンスボディを返しません"と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!--レスポンスボディのフィールドを説明します。-->

| パス | 型 | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値：true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値：0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値：SUCCESS |



**リクエストの例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メッセージの送信確認

POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/messages/${messageId}/do-confirm" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}"
```

</details>
