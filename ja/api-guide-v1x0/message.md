<!-- 新しいフォームのために追加されたstyleです。 -->
<style>
    .page__rnb .lst_rnb_item .rnb_item:first-of-type a {
        display: inline !important;
    }
</style>

<!-- 新しいフォームのためにタイトルを<h1>に変更しました。 -->
<h1>メッセージ</h1>

**Notification > Notification Hub > API v1.0 使用ガイド > メッセージ**



<span id="messageV1x0001SmsFreeFormMessages"></span>

## 自由形式メッセージ送信リクエスト - SMS

SMSに対する自由形式メッセージの送信をリクエストします。メッセージ内容をリクエストボディに入力した後、送信をリクエストします。

各メッセージチャネルにメッセージを送信するには、各メッセージチャネルの送信元情報が登録されている必要があります。送信元情報の登録は**Notification Hubコンソール** > **送信元情報タブ**で進行できます。メッセージチャネルの送信元情報の詳細については、**Notification** > **Notification Hub** > **利用ポリシー及び事前設定のご案内**で確認できます。


**リクエスト**

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |


**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| sender | Object | N |  |
| sender.senderPhoneNumber | String | Y | 送信元番号 |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| content | Object | N |  |
| content.messageType | String | Y | 送信メッセージタイプ(SMS、LMS、MMS)<br>[SMS, LMS, MMS] |
| content.title | String | N | メッセージタイトル |
| content.body | String | Y | メッセージ本文 |
| content.attachmentIds | Array | N | 添付ファイルID 最大3個 |

* メッセージチャネルによって**sender**、**content**フィールドは異なる形式を持ちます。
* メッセージチャネルによって**recipients[].contact.contactType**、**recipients[].contact.contact**フィールドに入力できる値が異なります。
* 予約送信の場合は**scheduledDateTime**を設定します。送信が開始される前の予約送信はリクエストのキャンセルが可能です。リクエストキャンセルAPIを呼び出すか、**Notification Hubコンソール** > **送信照会**でキャンセルできます。
* 承認後送信の場合は**confirmBeforeSend**を**true**に設定します。承認後送信のメッセージは、**Notification Hubコンソール** > **送信照会**で承認を行うと送信が進行されます。
* 予約送信と承認後送信は同時に設定できません。

### メッセージチャネル別のsenderフィールド

| メッセージチャネル | フィールド | 説明 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 送信元番号 |
| RCS | sender.brandId | ブランドID |
| RCS | sender.chatbotId | トークルームID |
| EMAIL | sender.senderMailAddress | 送信元メールアドレス |
| ALIMTALK | sender.senderKey | 送信元キー |
| ALIMTALK | sender.senderProfileType | 送信プロフィールタイプ<br>GROUP、NORMAL |

* お知らせトーク(ALIMTALK)は、送信元キー(senderKey)と送信プロフィールタイプ(senderProfileType)を必須で入力する必要があります。
* お知らせトーク(ALIMTALK)は、送信時にテンプレートが必ず必要です。自由形式メッセージの送信はサポートしていません。
* 送信プロフィールタイプには**GROUP(グループ)**と**NORMAL(一般)**があります。**GROUP**はグループ送信元プロフィール、**NORMAL**は一般送信元プロフィールです。


**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |


**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージ送信リクエスト - SMS

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
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/SMS/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0003EmailFreeFormMessages"></span>

## 自由形式メッセージ送信リクエスト - メール(EMAIL)

メール(EMAIL)に対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| sender | Object | N |  |
| sender.senderMailAddress | String | Y | 送信元メールアドレス |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| content | Object | N |  |
| content.title | String | Y | テンプレートメールタイトル |
| content.body | String | Y | テンプレートメール本文 |
| content.attachmentIds | Array | N | テンプレート添付ファイルID |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージ送信リクエスト - メール(EMAIL)

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
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/EMAIL/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>
<span id="messageV1x0004RcsFreeFormMessages"></span>

## 自由形式メッセージ送信リクエスト - RCS

RCSに対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ご来店ください^^",
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
                "title" : "予定タイトル",
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
              "title" : "予定タイトル",
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

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| sender | Object | N |  |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | トークルーム(チャットボット)ID |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| content | Object | N |  |
| content.messageType | String | N | RCS送信メッセージタイプ<br>[SMS, LMS, MMS, RBC_TEMPLATE] |
| content.title | String | N | (Deprecated、content.cards[].title を使用) メッセージタイトル |
| content.body | String | N | (Deprecated、content.cards[].description を使用) メッセージ本文 |
| content.smsType | String | N | SMSタイプ<br>[STANDALONE, UNIFIED_STANDALONE] |
| content.lmsType | String | N | LMSタイプ<br>[STANDALONE, FORMAT_BASIC, FORMAT_TITLE_HIGHLIGHT, FORMAT_PARAGRAPH, UNIFIED_STANDALONE] |
| content.mmsType | String | N | MMSタイプ(MMS送信の場合は必須)<br>[HORIZONTAL, VERTICAL, CAROUSEL_MEDIUM, CAROUSEL_SMALL, UNIFIED_HORIZONTAL, UNIFIED_VERTICAL] |
| content.messagebaseId | String | N | RCS Biz CenterテンプレートID |
| content.unsubscribePhoneNumber | String | N | 受信拒否番号(広告送信の場合は必須) |
| content.cards | Array | N | RCSカード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | N | 本文 |
| content.cards[].attachmentId | String | N | 添付ファイルID<br>※ 統合MMSカードでGIF画像を添付すると、iOSデバイスでは受信できません。 |
| content.cards[].mTitle | String | N | メインタイトル |
| content.cards[].mTitleMedia | String | N | メインタイトルロゴファイルID |
| content.cards[].title1 | String | N | タイトル 1 |
| content.cards[].title2 | String | N | タイトル 2 |
| content.cards[].title3 | String | N | タイトル 3 |
| content.cards[].description1 | String | N | 本文 1 |
| content.cards[].description2 | String | N | 本文 2 |
| content.cards[].description3 | String | N | 本文 3 |
| content.cards[].buttons | Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | N | ボタンタイプ<br>COMPOSE(トークルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(地図を表示する)、MAP_QUERY(地図を検索する)、MAP_SHARE(現在位置を共有する)、URL(URLを開く)、CALENDAR(予定を登録する)<br><br>※ 統合メッセージタイプにCLIPBOARD(コピーする)ボタンを使用すると、iOSデバイスでは受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | N | ボタンJSON、ボタンタイプに合ったフォーマットを確認 |
| content.buttons | Array | N | (Deprecated、content.cards[].buttons を使用) RCSボタン一覧 |
| content.buttons[].buttonType | String | N | buttonType値と同じ名前を持つActionオブジェクトがbuttonJsonとして含まれます。<br>ボタンタイプ トークルームを開く(COMPOSE)、コピーする(CLIPBOARD)、電話をかける(DIALER)、地図を表示する(MAP_SHOW)、地図を検索する(MAP_QUERY)、現在位置を共有する(MAP_SHARE)、URLを開く(URL)、予定を登録する(CALENDAR)<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | N |  |
| content.buttons[].buttonJson.action | Object | N | ボタンアクション |
| options | Object | N |  |
| options.expiryOption | Integer | N | キャリアからデバイスへの送信を試みる時間(1: 1日、2: 40秒、3: 3分、4: 1時間)<br>デフォルト値: 1 |
| options.groupId | String | N | RCS Biz Centerの統計連携のためのgroup ID [ガイド](../console-guide/send-a-message/#RCS) (最大20 Byte) |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージ送信リクエスト - RCS

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
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ご来店ください^^",
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
                "title" : "予定タイトル",
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
              "title" : "予定タイトル",
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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ご来店ください^^",
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
                "title" : "予定タイトル",
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
              "title" : "予定タイトル",
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

## 自由形式メッセージ送信リクエスト - PUSH

PUSHに対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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
        "link" : "ボタンを押した時にリンクされるリンク",
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
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
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

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| content | Object | N | プッシュメッセージの内容 |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 自由形式メッセージ送信リクエスト - PUSH

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
        "link" : "ボタンを押した時にリンクされるリンク",
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
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
        "link" : "ボタンを押した時にリンクされるリンク",
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
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Androidでのみサポート",
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

## テンプレートメッセージ送信リクエスト

登録したテンプレートを使用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
<br>
予約送信の場合は「scheduledDateTime」を設定します。<br>
確認後送信の場合は「confirmBeforeSend」をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messageChannel | Path  | String | Y | メッセージチャネルです。<br>[SMS, RCS, ALIMTALK, EMAIL, PUSH] |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| templateId | String | N | テンプレートID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートメッセージ送信リクエスト

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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

## お知らせトークテンプレートメッセージ送信

登録したテンプレートを使用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
<br>
予約送信の場合は「scheduledDateTime」を設定します。<br>
確認後送信の場合は「confirmBeforeSend」をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/ALIMTALK/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| sender | Object | N |  |
| sender.senderKey | String | Y | 送信プロフィール送信元キー |
| templateId | String | N | テンプレートID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### お知らせトークテンプレートメッセージ送信

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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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
<span id="messageV1x0008RcsTemplateMessages"></span>

## RCSテンプレートメッセージ送信

登録したテンプレートを使用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
<br>
予約送信の場合は「scheduledDateTime」を設定します。<br>
確認後送信の場合は「confirmBeforeSend」をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| sender | Object | N |  |
| sender.chatbotId | String | N | トークルーム(チャットボット)ID |
| content | Object | N |  |
| content.unsubscribePhoneNumber | String | N | 受信拒否電話番号 |
| templateId | String | N | テンプレートID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| options | Object | N |  |
| options.expiryOption | Integer | N | キャリアからデバイスへの送信を試みる時間(1: 1日、2: 40秒、3: 3分、4: 1時間)<br>デフォルト値: 1 |
| options.groupId | String | N | RCS Biz Centerの統計連携のためのgroup ID [ガイド](../console-guide/send-a-message/#RCS) (最大20 Byte) |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCSテンプレートメッセージ送信

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

## SMSテンプレートメッセージ送信

登録したテンプレートを使用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
  <br>
  予約送信の場合は「scheduledDateTime」を設定します。<br>
  確認後送信の場合は「confirmBeforeSend」をtrueに設定します。<br>

画像レイアウトが連携されたMMSテンプレート送信時に、以下の事項に注意する必要があります。
* **必須テンプレートパラメータ**: `cardNumber`、`scratchNumber`を必ず含める必要があります。
    * `cardNumber`: バーコード生成に使用され、必ず16桁の数字で構成される必要があります。
    * `scratchNumber`: 別途の制約条件はありません。
* **画像レイアウトOverride**: リクエストボディに`content.imageLayoutId`または`content.imageLayoutName`を含めて、テンプレートに設定された画像レイアウトを変更できます。
    * `content.imageLayoutId`と`content.imageLayoutName`のいずれか1つのみを使用する必要があります。
    * 両方のフィールドが含まれていない場合は、テンプレート作成時に連携したデフォルトの画像レイアウトが使用されます。


**リクエスト**

```
POST /message/v1.0/SMS/template-messages/{messagePurpose}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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
  "id" : "alpha123",
}
```

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| templateId | String | N | テンプレートID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| content | Object | N |  |
| content.imageLayoutId | String | N | 画像レイアウトID |
| content.imageLayoutName | String | N | 画像レイアウト名 |
| recipients | Array | N |  |
| recipients[].contacts | Array | Y |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| dryRun | Boolean | N | 送信をシミュレーションモードで実行します。実際の送信は行いません。<br>連絡先別の受信結果状態は送信失敗(SEND_FAILED)に設定されます。<br><br>デフォルト値: false |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMSテンプレートメッセージ送信

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
  "id" : "alpha123",
}'
```

</details>
<span id="messageV1x0009FlowMessages"></span>

## フローメッセージ送信

登録したフローを使用してメッセージを送信します。<br>
フローを登録していない場合は、フローを登録して送信する必要があります。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
<br>
予約送信の場合は「scheduledDateTime」を設定します。<br>
確認後送信の場合は「confirmBeforeSend」をtrueに設定します。<br>


**リクエスト**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| flowId | String | N | フローID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| recipients | Array | N |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| id | String | N | 大量受信者一覧及びファイルアップロード成功時に作成されるID |
| flow | Object | N |  |
| flow.steps | Array | Y |  |
| flow.steps[].messageChannel | String | Y | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| flow.steps[].sender | Object | N | 送信元情報です。送信元情報はメッセージチャネルによって異なるように構成される場合があります。<br> |
| flow.steps[].content | Object | N | メッセージ内容です。メッセージ内容はメッセージチャネルによって異なるように構成される場合があります。<br> |
| flow.steps[].options | Object | N | 送信オプションです。送信オプションはメッセージチャネルによって異なるように構成される場合があります。<br> |
| flow.steps[].nextSteps | Array | N | 次のステップです。次のステップがない場合、メッセージ送信が終了します。<br> |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローメッセージ送信

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
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}"  \ 
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

## インスタントフローメッセージ送信

メッセージ送信リクエスト時にフローを定義してメッセージの送信をリクエストします。<br>
<br>
インスタントフロー入力時にテンプレートを使用して送信リクエストするか、直接送信元情報、内容を入力して送信リクエストできます。


**リクエスト**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path  | String | Y | メッセージの目的です。<br>[AD, AUTH, NORMAL] |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->


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
      "templateId" : "テンプレート_ID",
      "nextSteps" : [ ]
    } ]
  }
}
```

<!-- リクエストボディのフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | N | 統計キーID |
| scheduledDateTime | String | N | 予約送信時間 |
| confirmBeforeSend | Boolean | N | 確認後送信の有無 |
| templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| recipients | Array | Y |  |
| recipients[].contacts | Array | N |  |
| recipients[].templateParameters | Object | N | テンプレートパラメータです。キー(Key、テンプレート変数)と値(Value)のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメータを指定できません。<br><br>受信者に設定されるテンプレートパラメータは、メッセージのテンプレートパラメータより優先されます。<br><br> |
| instantFlow | Object | Y |  |
| instantFlow.steps | Array | Y |  |
| instantFlow.steps[].messageChannel | String | Y | メッセージチャネル<br>[SMS, ALIMTALK, EMAIL, RCS, PUSH] |
| instantFlow.steps[].sender | Object | N | 送信元情報です。送信元情報はメッセージチャネルによって異なるように構成される場合があります。<br> |
| instantFlow.steps[].content | Object | N | メッセージ内容です。メッセージ内容はメッセージチャネルによって異なるように構成される場合があります。<br> |
| instantFlow.steps[].options | Object | N | 送信オプションです。送信オプションはメッセージチャネルによって異なるように構成される場合があります。<br> |
| instantFlow.steps[].templateId | String | N | テンプレートIDです。テンプレートIDを設定した場合、リクエスト時に送信元情報(sender)とメッセージ内容(content)が適用されません。<br>インスタントフローメッセージでテンプレートIDを設定しない場合、送信元情報(sender)とメッセージ内容(content)が必ず必要です。<br> |
| instantFlow.steps[].nextSteps | Array | N | 次のステップです。次のステップがない場合、メッセージ送信が終了します。 |



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

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

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | メッセージIDです。メッセージ送信リクエストを受け取ると作成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### インスタントフローメッセージ送信

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
      "templateId" : "テンプレート_ID",
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
      "templateId" : "テンプレート_ID",
      "nextSteps" : [ ]
    } ]
  }
}'
```

</details>
<span id="messageV1x0100MessageIdDoCancel"></span>

## メッセージ送信キャンセル

送信をキャンセルするメッセージIDを入力して送信をキャンセルします。<br>
メッセージ送信時にレスポンスとして受け取ったメッセージIDを使用して送信をキャンセルできます。<br>
メッセージ内の全てのリクエストがキャンセルされます。<br>


**リクエスト**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messageId | Path  | String | Y | null |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メッセージ送信キャンセル

POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/messages/${messageId}/do-cancel" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
<span id="messageV1x0101MessageIdDoConfirm"></span>

## メッセージ送信確認

確認後送信リクエストしたメッセージを確認します。<br>


**リクエスト**

```
POST /message/v1.0/messages/{messageId}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header  | String | Y | Appkey |
| X-NHN-Authorization | Header  | String | Y | アクセストークン |
| messageId | Path  | String | Y | null |



**リクエストボディ**

<!-- リクエストボディを要求しない場合は「このAPIはリクエストボディを要求しません」と入力します。-->

このAPIはリクエストボディを要求しません。



**レスポンスボディ**

<!-- レスポンスボディを返却しない場合は「このAPIはレスポンスボディを返却しません」と入力します。-->

```
{
  "header" : {
    "isSuccessful" : true,
    "resultCode" : 0,
    "resultMessage" : "SUCCESS"
  }
}
```

<!-- レスポンスボディのフィールドを説明します。-->

| パス | タイプ | 説明 |
| - | - | - |
| header | Object |  |
| header.isSuccessful | Boolean | リクエストの成否を示します。<br>デフォルト値: true |
| header.resultCode | Integer | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メッセージ送信確認

POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-confirm
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}


```

</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/messages/${messageId}/do-confirm" \
-H "X-NC-APP-KEY: {appKey}"  \ 
-H "X-NHN-Authorization: Bearer {accessToken}" 
```

</details>
