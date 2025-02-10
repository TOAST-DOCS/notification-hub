<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>メッセージ</h1>

**Notification > Notification Hub > API v1.0使用ガイド > メッセージ**

<span id="free-form-message-sending-request"></span>

## 自由形式のメッセージ送信リクエスト

リクエスト本文にメッセージ内容を入力し、メッセージを送信リクエストします。

各メッセージチャンネルにメッセージを送信するためには、各メッセージチャンネルの送信情報が登録されている必要があります。送信情報の登録は、**Notification Hubコンソール** > **送信情報**タブで行うことができます。メッセージチャンネルの発信情報の詳細な説明は、**Notification** > **Notification Hub** > **利用ポリシー及び事前設定案内**で確認できます。

<!-- !!! tip 「知っておくべきこと」-->
<!-- APIを使用する際、ユーザーが知っておくと良い注意事項や追加情報を提供する際に使用します。 -->

<!-- !!! warning 「注意」-->
<!--APIを使用する際、従わない場合、サービスの異常または非効率的な動作が発生する可能性がある注意事項を表記する際に使用します。 -->

**リクエスト**

```
POST /message/v1.0/{messageChannel}/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | メッセージ目的<br>NORMAL, AD, AUTH |

**共通リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

メッセージチャンネルによるリクエスト本文の詳細は、下記の**メッセージチャンネル別詳細リクエスト本文**をご確認ください。

```json
{
  "statsKeyId": "統計_ID",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "...": "メッセージ_チャンネルに_よって_異なる_形式"
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
    "...": "メッセージ_チャンネルに_よって_異なる_形式"
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ | 必須 | 説明 |
| --- | --- |-----| --- |
| statsKeyId | String | N   | 統計キーID |
| scheduledDateTime | DateTime(ISO 8601) | N   | 予約送信日時(例：2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean | N   | 送信前に確認するかどうか(デフォルト値false) |
| sender | Object | Y/N | 発信者、プッシュ以外のメッセージチャンネルは必須 |
| recipients | Object Array | Y   | 受信者配列 |
| recipients[].contacts | Object Array | Y   | 受信者の連絡先配列 |
| recipients[].contacts[].contactType | String | Y   | 連絡先タイプ |
| recipients[].contacts[].contact | String | Y   | 連絡先 |
| content | Object | Y   | メッセージ内容 |

* メッセージチャンネルによって**sender**, **content**フィールドは異なる形式を持ちます。
* メッセージチャンネルによって **recipients[].contacts.contactType**, **recipients[].contacts.contact**フィールドに入力できる値が異なります。
* 予約送信の場合、**scheduledDateTime**を設定します。送信開始前の予約送信は、リクエストのキャンセルが可能です。リクエストキャンセルAPIを呼び出すか、**Notification Hubコンソール** > **送信照会**でキャンセルできます。
* 承認後送信の場合、**confirmBeforeSend**を**true**に設定します。承認後送信のメッセージは**Notification Hubコンソール** > **送信照会**で承認すると送信が行われます。
* 予約送信と承認後送信は同時に設定できません。

### メッセージチャンネル別senderフィールド

| メッセージチャンネル | フィールド | 説明 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 発信者番号 |
| RCS | sender.brandId | ブランドID |
| RCS | sender.chatbotId | チャットルームID |
| EMAIL | sender.senderMailAddress | 発信者メールアドレス |
| ALIMTALK, FRIENDTALK | sender.senderKey | 発信キー |
| ALIMTALK | sender.senderProfileType | 発信プロフィールタイプ<br>GROUP, NORMAL |

* お知らせトーク(ALIMTALK)は発信キー(senderKey)と発信プロフィールタイプ(senderProfileType)を必ず入力する必要があります。
* カカともへのメッセージ(FRIENDTALK)はNORMAL(一般)発信プロフィールタイプのみ使用できます。 GROUP(グループ)発信プロフィールタイプの発信キーを使用すると送信に失敗します。
* 発信者プロフィールタイプは**GROUP(グループ)**と **NORMAL(一般)**があります。**GROUP**はグループ発信者プロフィール、 **NORMAL**は一般発信者プロフィールです。

**レスポンス本文**

<!--レスポンス本文を返さない場合は、「このAPIは応答本文を返しません」と入力します。 -->

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "メッセージ_ID"
}
```

<!--レスポンス本文のフィールドを説明します。-->

| 名前 | タイプ | 説明 |
| --- | --- | --- |
| header.isSuccessful | Boolean | APIリクエスト成否 |
| header.resultCode | Integer | 結果コード |
| header.resultMessage | String | 結果メッセージ |
| messageId | String | リクエスト成功したメッセージID |

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### 専門メッセージ送信
POST {{endpoint}}/message/v1.0/PUSH/free-form-messages/{messagePurpose}
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
curl -X POST "${ENDPOINT}/message/v1.0/PUSH/free-form-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
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
    }'
```

</details>

<span id="free-form-message-request-body"></span>

## メッセージチャンネル別詳細リクエスト本文例

<span id="free-form-message-request-body-sms"></span>

### SMS

```json
{
  "statsKeyId": "統計_キー_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
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
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| sender | Object | Y | 発信者、プッシュ以外のメッセージチャンネルは必須 |
| sender.senderPhoneNumber | String | N | 発信者番号 |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | メッセージタイプ<br>SMS(短文), LMS(長文), MMS(メディア長文) |
| content.title | String | Y | タイトル |
| content.body | String | Y | 内容 |
| content.attachmentIds | String Array | N | 添付ファイルID |


<span id="free-form-message-request-body-rcs"></span>

### RCS

```json
{
  "statsKeyId": "統計_キー_ID",
  "scheduledDateTime": "2024-10-24T06:29:00+09:00",
  "confirmBeforeSend": false,
  "sender": {
    "brandId": "ブランド_ID",
    "chatbotId": "チャットルーム_ID"
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
    "unsubscribePhoneNumber": "08012341234",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "mmsType": "HORIZONTAL",
    "messagebaseId": "44o4SUjpqnjDuUcH+uHvPg==",
    "cards": [
        {
          "title":"testTitle",
          "description":"testBody",
          "media":"fileId",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"Webサイトへ移動\"}}"
            },
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"Webサイトへ移動\"}}"
            }
          ]
        }
    ],
    "buttons": [
        {
            "buttonType": "URL",
            "buttonJson": "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"Webサイトへ移動\"}}"
        }
    ]
  }
}
```


| 名前 | タイプ | 必須 | 説明                                                                                                                                                     |
| --- | --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------| 
| sender | Object | Y | 発信者                                                                                                                                                    |
| sender.brandId | Object | N | ブランドID                                                                                                                                                  |
| sender.chatbotId | Object | N | チャットルームID                                                                                                                                                  |
| content | Object | Y | メッセージ内容                                                                                                                                                 |
| content.messageType | String | Y | RCS内のメッセージタイプ、 SMS, LMS, MMS, RCS_TEMPLATE                                                                                                                |
| content.unsubscribePhoneNumber | String | Y | 080受信拒否番号、送信目的が広告の場合は必須                                                                                                                         |
| content.title | Object | Y | タイトル                                                                                                                                                     |
| content.Object | Y | 内容 |
| content.mmsType | Object | N | MMSタイプ、メッセージタイプがMMSの場合必須、 HORIZONTAL(水平), VERTICAL(垂直), CAROUSEL_MEDIUM(カルーセル中央), CAROUSEL_SMALL(カルーセル小さく)                                                |
| content.messagebaseId | Object | N | メッセージタイプがRCS_TEMPLATEの場合必須、 RCS Biz Centerに登録されたテンプレートID                                                                                                 |
| content.cards | Object Array | Y | カード                                                                                                                                                     |
| content.cards[].title | String | Y | タイトル                                                                                                                                                     |
| content.cards[].description | String | Y | 内容                                                                                                                                                     |
| content.cards[].media | String | Y | 添付ファイルID                                                                                                                                                  |
| content.cards[].buttons | Object Array | Y | ボタン                                                                                                                                                     |
| content.cards[].button.buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(マップを表示する), MAP_QUERY(マップを検索する), MAP_SHARE(現在地を共有する), URL(URL接続する), CALENDAR(予定を登録する) |
| content.cards[].button.buttonJson | String | Y | ボタンJson,ボタンタイプに合ったフォーマット確認                                                                                                                              |
| content.buttons | Object Array | Y | ボタン |
| content.buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く), CLIPBOARD(コピーする), DIALER(電話をかける), MAP_SHOW(マップを表示する), MAP_QUERY(マップを検索する), MAP_SHARE(現在地を共有する), URL(URL接続する), CALENDAR(予定を登録する) |
| content.buttons[].buttonJson | String | Y | ボタンJSON形式の文字列                                                                                                                                        |
| content.attachmentIds | String Array | N | 添付ファイルID配列                                                                                                                                           |


<span id="free-form-message-request-body-friendtalk-text"></span>

### カカともへのメッセージ - テキスト型

* お知らせトークは、テンプレート登録後、承認された状態で送信可能なため、テンプレート、フローメッセージの送信のみ可能です。
* お知らせトークの**sender**, **content**フィールドは**テンプレートメッセージ送信**の**リクエスト本文**をご確認ください。
* カカともへのメッセージ(FRIENDTALK)はNORMAL(一般)発信プロフィールタイプのみ使用できます。GROUP(グループ)発信プロフィールタイプの発信キーを使用すると送信に失敗します。

```json
{
    "statsKeyId": "統計_キー_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "発信プロフィール_発信キー"
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
      "messageType": "TEXT",
      "content": "送信_内容",
      "buttons": [
        {
          "type": "WL",
          "name": "ボタン_名前",
          "linkMo": "モバイル_リンク",
          "linkPc": "PC_リンク",
          "schemeIos": "iOS_アプリ_リンク",
          "schemeAndroid": "Android_アプリ_リンク",
          "bizFormKey": "ビズフォーム_キー"
        }
      ],
      "coupon": {
        "title": "クーポン_タイトル",
        "description": "クーポン_詳細_説明",
        "linkMo": "モバイル_リンク",
        "linkPc": "PC_リンク",
        "schemeIos": "iOS_アプリ_リンク",
        "schemeAndroid": "Android_アプリ_リンク"
      }
    }
}
```


| 名前 | タイプ | 必須 | 説明                                                          |
| --- | --- |----|---------------------------------------------------------------|
| sender | Object | Y  | 発信者                                                         |
| sender.senderKey | Object | Y  | 発信プロフィール_発信キー                                                    |
| content | Object | Y  | メッセージ内容                                                      |
| content.messageType | String | Y  | メッセージタイプ                                                      |
| content.content | String | Y  | 内容                                                          |
| content.buttons                   | Object Array  | N  | ボタン                                                                                                                                                      |
| content.buttons[].type            | String | Y  | ボタンタイプ<br>WL(Webリンク), AL(アプリリンク), BK(Botキーワード), MD(メッセージ伝達), BF(ビジネスフォーム)                                                                                             |
| content.buttons[].name            | String | Y  | ボタン名                                                                                                                                                   |
| content.buttons[].linkMo          | String | N  | リンクモバイル、ボタンタイプがWLの場合は必須                                                                                                                                  |
| content.buttons[].linkPc          | String | N  | リンクPC                                                                                                                                                     |
| content.buttons[].schemeIos       | String | N  | iOSアプリリンク                                                                                                                                                |
| content.buttons[].schemeAndroid   | String | N  | Androidアプリリンク                                                                                                                                            |
| content.buttons[].bizFormKey      | String | N  | ビズフォームキー、ボタンタイプがBFの場合は必須                                                                                                                                   |
| content.coupon | Object | N  | クーポン                                                          |
| content.coupon.title | String | Y  | タイトル、場合5つの形式に制限<br>"${数字}KRW割引クーポン"数字は1以上99,999,999以下<br>"${数字}%割引クーポン"数字は1以上100以下<br>"送料割引クーポン"<br><br>"${7文字以内}無料クーポン"<br>"${7文字以内} UPクーポン"                                                          |
| content.coupon.description | String | Y  | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字) |
| content.coupon.linkMo | String | N  | リンクモバイル                                                      |
| content.coupon.linkPc | String | N  | リンクPC                                                         |
| content.coupon.schemeIos | String | N  | iOSアプリリンク                                          |
| content.coupon.schemeAndroid | String | N  | Androidアプリリンク                       |

<span id="free-form-message-request-body-friendtalk-image"></span>

### カカともへのメッセージ - 画像型 / ワイド画像型

* カカともへのメッセージ(FRIENDTALK)はNORMAL(一般)発信プロフィールタイプのみ使用できます。 GROUP(グループ)発信プロフィールタイプの発信キーを使用すると送信に失敗します。

```json
{
    "statsKeyId": "統計_キー_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "発信プロフィール_発信キー"
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
      "messageType": "WIDE_IMAGE",
      "content": "送信_内容",
      "attachmentId": "添付_ファイル_ID",
      "imageLink": "画像_リンク_URL",
      "buttons": [
        {
          "type": "WL",
          "name": "ボタン_名前",
          "linkMo": "モバイル_リンク",
          "linkPc": "PC_リンク",
          "schemeIos": "iOS_アプリ_リンク",
          "schemeAndroid": "Android_アプリ_リンク",
          "bizFormKey": "ビズフォーム_キー"
        }
      ],
      "coupon": {
        "title": "クーポン_タイトル",
        "description": "クーポン_詳細_説明",
        "linkMo": "モバイル_リンク",
        "linkPc": "PC_リンク",
        "schemeIos": "iOS_アプリ_リンク",
        "schemeAndroid": "Android_アプリ_リンク"
      }
    }
}
```

| 名前 | タイプ          | 必須 | 説明                                                          |
| --- |---------------|----|---------------------------------------------------------------|
| sender | Object        | Y  | 発信者                                                         |
| sender.senderKey | Object        | Y  | 発信プロフィール_発信キー                                                    |
| content | Object        | Y  | メッセージ内容                                                      |
| content.messageType | String        | Y  | メッセージタイプ                                                      |
| content.content | String        | Y  | 内容                                                          |
| content.attachmentId | String        | Y  | 添付ファイルID |
| content.imageLink | String        | N  | 画像リンク |
| content.buttons                   | Object Array | N  | ボタン                                                                                                                                                      |
| content.buttons[].type            | String        | Y  | ボタンタイプ<br>WL(Webリンク), AL(アプリリンク), BK(Botキーワード), MD(メッセージ伝達), BF(ビジネスフォーム)                                                                                             |
| content.buttons[].name            | String        | Y  | ボタン名                                                                                                                                                   |
| content.buttons[].linkMo          | String        | N  | リンクモバイル、ボタンタイプがWLの場合は必須                                                                                                                                  |
| content.buttons[].linkPc          | String        | N  | リンクPC                                                                                                                                                     |
| content.buttons[].schemeIos       | String        | N  | iOSアプリリンク                                                                                                                                                |
| content.buttons[].schemeAndroid   | String        | N  | Androidアプリリンク                                                                                                                                            |
| content.buttons[].bizFormKey      | String        | N  | ビズフォームキー、ボタンタイプがBFの場合必須                                                                                                                                   |
| content.coupon | Object        | N  | クーポン                                                          |
| content.coupon.title | String        | Y  | タイトル、場合5つの形式に制限<br>"${数字}KRW割引クーポン"数字は1以上99,999,999以下<br>"${数字}%割引クーポン"数字は1以上100以下<br>"送料割引クーポン"<br><br>"${7文字以内}無料クーポン"<br>"${7文字以内} UPクーポン"                                                          |
| content.coupon.description | String        | Y  | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字) |
| content.coupon.linkMo | String        | N  | リンクモバイル                                                      |
| content.coupon.linkPc | String        | N  | リンクPC                                                         |
| content.coupon.schemeIos | String        | N  | iOSアプリリンク                                          |
| content.coupon.schemeAndroid | String        | N  | Androidアプリリンク                       |

<span id="free-form-message-request-body-friendtalk-wide-itemlist"></span>

### カカともへのメッセージ - ワイドアイテムリスト型

* カカともへのメッセージ(FRIENDTALK)はNORMAL(一般)発信プロフィールタイプのみ使用できます。 GROUP(グループ)発信プロフィールタイプの発信キーを使用すると送信に失敗します。

```json
{
    "statsKeyId": "統計_キー_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "発信プロフィール_発信キー"
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
      "messageType": "WIDE_ITEMLIST",
      "buttons": [
        {
          "type": "WL",
          "name": "ボタン_名前",
          "linkMo": "モバイル_リンク",
          "linkPc": "PC_リンク",
          "schemeIos": "iOS_アプリ_リンク",
          "schemeAndroid": "Android_アプリ_リンク",
          "bizFormKey": "ビズフォーム_キー"
        }
      ],
      "header": "ヘッダ",
      "item": {
          "list": [{
            "title": "アイテム_タイトル",
            "attachmentId": "添付_ファイル_ID",
            "linkMo": "モバイル_リンク",
            "linkPc": "PC_リンク",
            "schemeIos": "iOS_アプリ_リンク",
            "schemeAndroid": "Android_アプリ_リンク"
          },
          {
            "title": "アイテム_タイトル",
            "attachmentId": "添付_ファイル_ID",
            "linkMo": "モバイル_リンク",
            "linkPc": "PC_リンク",
            "schemeIos": "iOS_アプリ_リンク",
            "schemeAndroid": "Android_アプリ_リンク"
          },
          {
          "title": "アイテム_タイトル",
          "attachmentId": "添付_ファイル_ID",
          "linkMo": "モバイル_リンク",
          "linkPc": "PC_リンク",
          "schemeIos": "iOS_アプリ_リンク",
          "schemeAndroid": "Android_アプリ_リンク"
          }
        ]
      },
      "coupon": {
        "title": "クーポン_タイトル",
        "description": "クーポン_詳細_説明",
        "linkMo": "モバイル_リンク",
        "linkPc": "PC_リンク",
        "schemeIos": "iOS_アプリ_リンク",
        "schemeAndroid": "Android_アプリ_リンク"
      }
    }
}
```

| 名前                              | タイプ          | 必須 | 説明                                                                                                                                                      |
|-----------------------------------|---------------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                            | Object        | Y  | 発信者                                                                                                                                                     |
| sender.senderKey                  | Object        | Y  | 発信プロフィール_発信キー                                                                                                                                                |
| content                           | Object        | Y  | メッセージ内容                                                                                                                                                  |
| content.messageType               | String        | Y  | メッセージタイプ                                                                                                                                                  |
| content.buttons                   | Object Array | N  | ボタン                                                                                                                                                      |
| content.buttons[].type            | String        | Y  | ボタンタイプ<br>WL(Webリンク), AL(アプリリンク), BK(Botキーワード), MD(メッセージ伝達), BF(ビジネスフォーム)                                                                                             |
| content.buttons[].name            | String        | Y  | ボタン名                                                                                                                                                   |
| content.buttons[].linkMo          | String        | N  | リンクモバイル、ボタンタイプがWLの場合は必須                                                                                                                                  |
| content.buttons[].linkPc          | String        | N  | リンクPC                                                                                                                                                     |
| content.buttons[].schemeIos       | String        | N  | iOSアプリリンク                                                                                                                                                |
| content.buttons[].schemeAndroid   | String        | N  | Androidアプリリンク                                                                                                                                            |
| content.buttons[].bizFormKey      | String        | N  | ビズフォームキー、ボタンタイプがBFの場合必須                                                                                                                                   |
| content.header                    | String        | Y  | ヘッダ                                                                                                                                                      |
| content.item                      | Object        | Y  | ワイドアイテム                                                                                                                                                 |
| content.item.list                 | Object Array | Y  | ワイドアイテムリスト(最小3個、最大4個)                                                                                                                                 |
| content.item.list[].title         | String        | Y  | アイテムタイトル(最初のアイテムの場合は最大25文字、 2～4番目のアイテムの場合は最大30文字)                                                                                                         |
| content.item.list[].attachmentId  | String        | Y  | 添付ファイルID                                                                                                                                                 |
| content.item.list[].linkMo        | String        | Y  | モバイルWebリンク                                                                                                                                                |
| content.item.list[].linkPc        | String        | Y  | PC Webリンク                                                                                                                                                 |
| content.item.list[].schemeIos     | String        | Y  | iOSアプリリンク                                                                                                                                                |
| content.item.list[].schemeAndroid | String        | Y  | Androidアプリリンク                                                                                                                                               |
| content.coupon                    | Object        | N  | クーポン                                                                                                                                                      |
| content.coupon.title              | String        | Y  | タイトル、場合5つの形式に制限<br>"${数字}KRW割引クーポン"数字は1以上99,999,999以下<br>"${数字}%割引クーポン"数字は1以上100以下<br>"送料割引クーポン"<br><br>"${7文字以内}無料クーポン"<br>"${7文字以内} UPクーポン" |
| content.coupon.description        | String        | Y  | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字)                                                                                   |
| content.coupon.linkMo             | String        | N  | リンクモバイル                                                                                                                                                  |
| content.coupon.linkPc             | String        | N  | リンクPC                                                                                                                                                     |
| content.coupon.schemeIos          | String        | N  | iOSアプリリンク                                                                                                                                                |
| content.coupon.schemeAndroid      | String        | N  | Androidアプリリンク                                                                                                                                            |

<span id="free-form-message-request-body-friendtalk-carousel"></span>

### カカともへのメッセージ - カルーセルフィード型

* カカともへのメッセージ(FRIENDTALK)はNORMAL(一般)発信プロフィールタイプのみ使用できます。 GROUP(グループ)発信プロフィールタイプの発信キーを使用すると送信に失敗します。

```json
{
    "statsKeyId": "統計_キー_ID",
    "scheduledDateTime": "2024-10-24T06:29:00+09:00",
    "confirmBeforeSend": false,
    "sender": {
        "senderKey": "発信プロフィール_発信キー"
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
      "messageType": "CAROUSEL_FEED",
      "carousel": {
        "list": [
          {
            "header": "カルーセル_アイテム_タイトル",
            "message": "カルーセル_アイテム_メッセージ",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "ボタン_名前",
                  "linkMo": "モバイル_リンク",
                  "linkPc": "PC_リンク",
                  "schemeIos": "iOS_アプリ_リンク",
                  "schemeAndroid": "Android_アプリ_リンク"
                }
              ],
              "image": {
                "attachmentId": "添付_ファイル_ID",
                "imageLink": "画像_リンク_URL"
              },
              "coupon": {
                "title": "クーポン_タイトル",
                "description": "クーポン_詳細_説明",
                "linkMo": "モバイル_リンク",
                "linkPc": "PC_リンク",
                "schemeIos": "iOS_アプリ_リンク",
                "schemeAndroid": "Android_アプリ_リンク"
              }
            }
          },
          {
            "header": "カルーセル_アイテム_タイトル",
            "message": "カルーセル_アイテム_メッセージ",
            "attachment": {
              "buttons": [
                {
                  "type": "WL",
                  "name": "ボタン_名前",
                  "linkMo": "モバイル_リンク",
                  "linkPc": "PC_リンク",
                  "schemeIos": "iOS_アプリ_リンク",
                  "schemeAndroid": "Android_アプリ_リンク"
                }
              ],
              "image": {
                "attachmentId": "添付_ファイル_ID",
                "imageLink": "画像_リンク_URL"
              },
              "coupon": {
                "title": "クーポン_タイトル",
                "description": "クーポン_詳細_説明",
                "linkMo": "モバイル_リンク",
                "linkPc": "PC_リンク",
                "schemeIos": "iOS_アプリ_リンク",
                "schemeAndroid": "Android_アプリ_リンク"
              }
            }
          }
        ],
        "tail": {
          "linkMo": "モバイル_リンク",
          "linkPc": "PC_リンク",
          "schemeAndroid": "Android_アプリ_リンク",
          "schemeIos": "iOS_アプリ_リンク"
        }
      }
    }
}
```

| 名前                                                       | タイプ          | 必須 | 説明                                                                                                                                                     |
|------------------------------------------------------------|---------------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender                                                     | Object        | Y  | 発信者                                                                                                                                                    |
| sender.senderKey                                           | Object        | Y  | 発信プロフィール_発信キー                                                                                                                                               |
| content                                                    | Object        | Y  | メッセージ内容                                                                                                                                                 |
| content.messageType                                        | String        | Y  | メッセージタイプ                                                                                                                                                 |
| content.carousel                                           | Object        | Y  | カルーセル                                                                                                                                                    |
| content.carousel.list                                      | Object Array | Y  | カルーセルリスト(最小2個、最大10個)                                                                                                                                   |
| content.carousel.list[].header                             | String        | Y  | カルーセルアイテムタイトル(最大20文字)、カルーセルフィード型でのみ使用可能                                                                                                                   |
| content.carousel.list[].message                            | String        | Y  | カルーセルアイテムメッセージ(最大180文字)、カルーセルフィード型でのみ使用可能                                                                                                                 |
| content.carousel.list[].attachment                         | Object        | N  | カルーセルアイテム画像、ボタン情報                                                                                                                                     |
| content.carousel.list[].attachment.buttons                 | Object Array | N  | ボタンリスト(最大2個)                                                                                                                                           |
| content.carousel.list[].attachment.buttons[].type          | String        | Y  | ボタンタイプ<br>WL(Webリンク), AL(アプリリンク), BK(Botキーワード), MD(メッセージ伝達), BF(ビジネスフォーム)                                                                                            |
| content.carousel.list[].attachment.buttons[].name          | String        | Y  | ボタン名                                                                                                                                                  |
| content.carousel.list[].attachment.buttons[].linkMo        | String        | N  | リンクモバイル、ボタンタイプがWLの場合は必須                                                                                                                                 |
| content.carousel.list[].attachment.buttons[].linkPc        | String        | N  | リンクPC                                                                                                                                                    |
| content.carousel.list[].attachment.buttons[].schemeIos     | String        | N  | iOSアプリリンク                                                                                                                                               |
| content.carousel.list[].attachment.buttons[].schemeAndroid | String        | N  | Androidアプリリンク                                                                                                                                           |
| content.carousel.list[].attachment.image                   | Object        | Y  | カルーセル画像                                                                                                                                                |
| content.carousel.list[].attachment.image.attachmentId      | String        | Y  | 添付ファイルid                                                                                                                                                 |
| content.carousel.list[].attachment.image.imageLink         | String        | N  | 画像リンクURL                                                                                                                                               |
| content.carousel.list[].attachment.coupon                  | Object        | N  | クーポン                                                                                                                                                     |
| content.carousel.list[].attachment.coupon.title            | String        | Y  | タイトル、場合5つの形式に制限<br>"${数字}KRW割引クーポン"数字は1以上99,999,999以下<br>"${数字}%割引クーポン"数字は1以上100以下<br>"送料割引クーポン"<br><br>"${7文字以内}無料クーポン"<br>"${7文字以内} UPクーポン" |
| content.carousel.list[].attachment.coupon.description      | String        | Y  | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字)                                                                                  |
| content.carousel.list[].attachment.coupon.linkMo           | String        | N  | リンクモバイル                                                                                                                                                 |
| content.carousel.list[].attachment.coupon.linkPc           | String        | N  | リンクPC                                                                                                                                                    |
| content.carousel.list[].attachment.coupon.schemeIos        | String        | N  | iOSアプリリンク                                                                                                                                               |
| content.carousel.list[].attachment.coupon.schemeAndroid    | String        | N  | Androidアプリリンク                                                                                                                                           |
| content.carousel.tail                                      | Object        | N  | カルーセル詳細表示ボタン情報                                                                                                                                         |
| content.carousel.tail.linkMo                               | String        | Y  | モバイルWebリンク                                                                                                                                         |
| content.carousel.tail.linkPc                               | String        | N  | モバイルWebリンク                                                                                                                                         |
| content.carousel.tail.schemeIos                            | String        | N  | モバイルWebリンク                                                                                                                                         |
| content.carousel.tail.schemeAndroid                        | String        | N  | モバイルWebリンク                                                                                                                                         |

<span id="free-form-message-request-body-email"></span>

### Email

```json
{
  "sender": {
    "senderMailAddress": "sender@example.com"
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
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。 NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

| 名前 | タイプ          | 必須 | 説明 |
| --- |---------------|----| --- |
| sender | Object        | N  | 発信者、プッシュ以外のメッセージチャンネルは必須 |
| sender.senderMailAddress | Object        | N  | 発信者メールアドレス |
| content | Object        | Y  | メッセージ内容 |
| content.title | Object        | Y  | タイトル |
| content.Object | Y             | 内容 |
| content.attachmentIds | String Array | N  | 添付ファイルID |

* 発信者メールアドレスのドメインは所有認証が完了している必要があります。
* 添付ファイルは**最大10個**までアップロード可能で、**30MB以下のファイル**のみ可能です。
* 添付ファイルの**合計は30MB**を超えることはできません。
* 最大**30MB**まで添付可能ですが、受信するメールシステム(gmail.com, naver.comなど)の添付ファイル制限ポリシーにより、**制限超過**で拒否されたり、スパム判定率が高くなる可能性があるため、**10MB以内で添付することを推奨します。

<span id="free-form-message-request-body-push"></span>

### Push

```json
{
  "statsId": "統計_ID",
  "scheduledDateTime": "2024-10-29T06:29:00+09:00",
  "confirmBeforeSend": false,
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "トークン"
        }
      ]
    }
  ],
  "content": {
    "unsubscribePhoneNumber": "1234-1234",
    "unsubscribeGuide": "設定 > メニュー",
    "style": {
      "useHtmlStyle": true
    },
    "title" : "<b>NHN Cloud </b> Notification",
    "body" : "<b>リリースイベント</b> <i>告知事項確認</i>",
    "richMessage" : {
      "buttons" : [{
        "name" : "ボタン名",
        "submitName": "送信ボタン名",
        "buttonType" : "REPLY",
        "link" : "myapp://product_detail?product_id=1234",
        "hint" : "ボタンに関するヒント"
      }
      ],
      "media" : {
        "source" : "URL",
        "mediaType" : "IMAGE",
        "expandable" : true
      },
      "androidMedia": {
        "source" : "URL",
        "mediaType" : "IMAGE",
        "expandable" : true
      },
      "iosMedia": {
        "source" : "URL",
        "mediaType" : "IMAGE",
        "expandable" : true
      },
      "largeIcon" : {
        "source" : "URL"
      },
      "group" : {
        "key" : "グループのキー",
        "description" : "グループについての説明"
      }
    },
    "customKey" : "customValue"
  }
}
```

| 名前 | タイプ                  | 必須 | 説明 |
| --- |-----------------------| --- | --- |
| content | Object                | Y | メッセージ内容 |
| content.unsubscribePhoneNumber | String                | プッシュメッセージ受信拒否のための代表番号 |
| content.unsubscribeGuide | String                | プッシュメッセージ受信拒否のための案内 |
| content.title | String                | Y | タイトル |
| content.String | Y                     | 内容 |
| content.style.useHtmlStyle | Boolean               | Y | HTMLスタイル使用(Androidでのみ可能) |
| content.richMessage | Object                | リッチメッセージ |
| content.richMessage | Object                | N | リッチメッセージ使用時に必要 |
| content.richMessage.buttons | Object Array         | N | リッチメッセージに追加されるボタン、最大3個まで可能 |
| content.richMessage.button.name | String                | ボタン名 |
| content.richMessage.button.buttonType | String                | ボタンタイプ、 REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.button.link | String                | ボタンを押した時に接続されるリンク |
| content.richMessage.button.hint | String                | ボタンについてのヒント |
| content.richMessage.media | Object                | N | リッチメッセージに追加されるメディア |
| content.richMessage.media.source | String                | メディアの位置のアドレス、 URL, LOCAL_RESOURCE可能 |
| content.richMessage.media.mediaType | String                | N | メディアのタイプ、 IMAGE, GIF, VEDIO, AUDIO. AndroidでのみIMAGEのみサポート |
| content.richMessage.media.expandable | Boolean               | N | Androidでメディアをクリックした時に展開機能を使用するかどうか |
| content.richMessage.androidMedia | Object                | N |  Android端末で使用されるメディア。形式はmediaと同じ。 |
| content.richMessage.iosMedia | Object                | N |  iOS端末使用されるメディア。形式はmediaと同じ。 |
| content.richMessage.largeIcon | Object                | N | リッチメッセージに追加される大きなアイコン、 Androidでのみサポート |
| content.richMessage.largeIcon.source | String                | Y | メディアの位置のアドレス |
| content.richMessage.group | Object                | N | 複数のメッセージをグループ単位でまとめる機能、Androidのみサポート |
| content.richMessage.group.key | String                | Y | グループのキー |
| content.richMessage.group.description | String                | Y | グループについての説明 |
| content.customKey | Object Array or String Array | N | ユーザー定義キーと値 |

* プッシュは**sender**フィールドが必要ありません。
* プッシュはユーザーが定義したキーと値を追加して**content**フィールドを作成できます。


<span id="template-message-sending-request"></span>

## テンプレートメッセージ送信リクエスト

**リクエスト**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageChannel | Path | String | Y | メッセージチャンネル<br>SMS, RCS, ALIMTALK, FRIENDTALK, EMAIL, PUSH |
| messagePurpose | Path | String | Y | メッセージ目的<br>NORMAL, AD, AUTH |

**リクエスト本文**

```json
{
  "statsKeyId": "統計_ID",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "テンプレート_ID",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ]
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前 | タイプ               | 必須 | 説明 |
| --- |--------------------| --- | --- |
| statsKeyId | String             | N | 統計キーID |
| scheduledDateTime | DateTime(ISO 8601) | N | 予約送信日時(例：2024-10-29T06:29:00+09:00) |
| confirmBeforeSend | Boolean            | N | 送信前確認を行うかどうか(デフォルト値false) |
| templateId | String             | Y | テンプレートID |
| templateParameters | Object             | N | テンプレートパラメータ |
| recipients | Object Array      | Y | 受信者配列 |
| recipients[].contacts | Object Array              | Y | 受信者の連絡先配列 |
| recipients[].contacts[].contactType | String             | Y | 連絡先タイプ |
| recipients[].contacts[].contact | String             | Y | 連絡先 |
| recipients[].templateParameters | Object             | N | テンプレートパラメータ |

* テンプレートパラメータはテンプレートに定義されたパラメータと一致する必要があります。
* テンプレートパラメータは共通テンプレートパラメータ、受信者テンプレートパラメータに区分されます。
* 共通テンプレートパラメータは、すべての受信者に同じように適用されるパラメータです。受信者テンプレートパラメータは、受信者ごとに異なるパラメータを適用する際に使用します。
* 受信者テンプレートパラメータがない場合は、共通テンプレートパラメータのみ適用されます。共通テンプレートパラメータと受信者テンプレートパラメータが重複する場合、受信者テンプレートパラメータが優先的に適用されます。
* テンプレートパラメータの値のタイプは、文字列または配列、オブジェクトのいずれかを指定できます。配列やオブジェクトタイプはFREE_MARKERテンプレートで使用できます。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "メッセージ_ID"
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### テンプレートメッセージ送信
POST {{endpoint}}/message/v1.0/SMS/template-messages/NORMAL
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "statsKeyId": "統計_ID",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "templateId": "テンプレート_ID",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345678"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ]
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/SMS/template-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
        "statsKeyId": "統計_ID",
        "scheduledDateTime": "2024-10-29T00:06:29+09:00",
        "confirmBeforeSend": false,
        "templateId": "テンプレート_ID",
        "templateParameters": {
            "key1": "value1",
            "key2": "value2",
            "key3": {
                "key4": "value4",
                "key5": "value5"
            }
        },
        "recipients": [
            {
            "contacts": [
                {
                "contactType": "PHONE_NUMBER",
                "contact": "01012345678"
                }
            ],
            "templateParameters": {
                "key3": {
                "key4": "value4",
                "key5": "value5"
                },
                "key6": "value6"
            }
            }
        ]
    }'
```

</details>

<span id="flow-message-sending-request"></span>

## フローメッセージ送信リクエスト

**リクエスト**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messagePurpose | Path | String | Y | メッセージ目的<br>NORMAL, AD, AUTH |

**リクエスト本文**


```json
{
  "statsKeyId": "統計_ID",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "テンプレート_ID",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "token"
        },
        {
          "contactType": "EMAIL_ADDRESS",
          "contact": "recipient@example.com"
        },
        {
          "contactType": "PHONE_NUMBER",
          "contact": "01012345679"
        }
      ],
      "templateParameters": {
        "key3": {
          "key4": "value4",
          "key5": "value5"
        },
        "key6": "value6"
      }
    }
  ]
}
```

<!--リクエスト本文のフィールドを説明します。-->

| 名前               | タイプ           | 必須 | 説明                                   |
|--------------------| ----------------| --- |----------------------------------------|
| statsKeyId         | String         | N | 統計キーID                               |
| scheduledDateTime  | DateTime(ISO 8601) | N | 予約送信日時(例：2024-10-29T06:29:00+09:00) |
| confirmBeforeSend  | Boolean        | N | 送信前確認を行うかどうか(デフォルト値false)                  |
| flowId             | String         | Y | テンプレートID                                |
| templateParameters | Object         | N | メッセージ共通テンプレートパラメータ                      |
| recipients         | Object Array          | Y | 受信者配列                               |
| recipients[].contacts | Object Array          | Y | 受信者の連絡先配列                          |
| recipients[].contacts[].contactType | String         | Y | 連絡先タイプ                               |
| recipients[].contacts[].contact | String         | Y | 連絡先                                  |
| recipients[].templateParameters | Object         | N | 受信者別テンプレートパラメータ                       |

* フローメッセージ送信もテンプレートメッセージ送信と同じようにテンプレートパラメータを使用します。
* 受信者の連絡先はフローで使用するメッセージチャンネルに必要な連絡先が全て含まれている必要があります。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "messageId": "メッセージ_ID"
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フローメッセージ送信
POST {{endpoint}}/message/v1.0/flow-messages/{{messagePurpose}}
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{authorizationToken}}

{
  "statsKeyId": "統計_ID",
  "scheduledDateTime": "2024-10-29T00:06:29+09:00",
  "confirmBeforeSend": false,
  "flowId": "テンプレート_ID",
  "templateParameters": {
    "key1": "value1",
    "key2": "value2",
    "key3": {
        "key4": "value4",
        "key5": "value5"
    }
  },
  "recipients": [
    {
      "contacts": [
        {
          "contactType": "TOKEN_FCM",
          "contact": "token"
        },
        {
          "contactType": "EMAIL_ADDRESS",
          "contact": "recipient@example.com"
        }
      ],
        "templateParameters": {
          "key3": {
            "key4": "value4",
            "key5": "value5"
          },
          "key6": "value6"
        }
      }
    ]
}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/flow-messages/${MESSAGE_PURPOSE}" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}" \
     -d '{
       "statsKeyId": "統計_ID",
       "scheduledDateTime": "2024-10-29T00:06:29+09:00",
       "confirmBeforeSend": false,
       "flowId": "テンプレート_ID",
       "templateParameters": {
         "key1": "value1",
         "key2": "value2",
         "key3": {
           "key4": "value4",
           "key5": "value5"
         }
       },
       "recipients": [
         {
           "contacts": [
             {
               "contactType": "TOKEN_FCM",
               "contact": "token"
             },
             {
               "contactType": "EMAIL_ADDRESS",
               "contact": "recipient@example.com"
             }
           ],
           "templateParameters": {
             "key3": {
               "key4": "value4",
               "key5": "value5"
             },
             "key6": "value6"
           }
         }
       ]
     }'
```

</details>


<span id="cancel-message-sending-request"></span>

## メッセージリクエストキャンセル

送信前の予約メッセージ、承認後の送信メッセージの送信要求をキャンセルします。リクエストキャンセルされたメッセージは、連絡先別受信結果照会で照会できます。

**リクエスト**

```
POST /message/v1.0/messages/{messageId}/do-cancel
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメータ**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | --- |
| appKey | Header | String | Y | アプリキー |
| accessToken | Header | String | Y | 認証トークン |
| messageId | Path | String | Y | メッセージID |


**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。 -->

このAPIはリクエスト本文を要求しません。

**レスポンス本文**

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

<!--レスポンス本文のフィールドを説明します。-->

**リクエスト例**

<details>
  <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メッセージリクエストキャンセル
POST {{endpoint}}/message/v1.0/messages/{{messageId}}/do-cancel
Content-Type: application/json
X-NC-APP-KEY: {{appKey}}
X-NHN-Authorization: {{accessToken}}
```

</details>

<details>
  <summary><strong>cURL</strong></summary>

```curl
curl -X POST "${ENDPOINT}/message/v1.0/messages/${MESSAGE_ID}/do-cancel" \
     -H "Content-Type: application/json" \
     -H "X-NC-APP-KEY: ${APP_KEY}" \
     -H "X-NHN-Authorization: ${ACCESS_TOKEN}"
```

</details>
