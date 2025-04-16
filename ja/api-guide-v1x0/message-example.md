<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>メッセージ - 送信リクエスト本文例</h1>

**Notification > Notification Hub > API v1.0使用ガイド > メッセージ - 送信リクエスト本文例**


<span id="sms"></span>

## SMS

<span id="sms-sms"></span>

### SMS(短文)

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "body": "こんにちは。NHN Cloud Notification Hubです。",
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| sender | Object | Y | 発信者 |
| sender.senderPhoneNumber | String | Y | 発信者番号 |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | SMS |
| content.body | String | Y | 内容 |

### LMS(長文)

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。NHN Cloud Notification Hubです。"
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| sender | Object | Y | 発信者 |
| sender.senderPhoneNumber | String | Y | 発信者番号 |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | LMS |
| content.title | String | Y | タイトル |
| content.body | String | Y | 内容 |

### MMS(メディア長文)

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "MMS",
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| sender | Object | Y | 発信者 |
| sender.senderPhoneNumber | String | Y | 発信者番号 |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | MMS |
| content.body | String | Y | 内容 |
| content.attachmentIds | String Array | Y | 添付ファイルID<br>添付画像の制限事項。<br>サポートコーデック: .jpg, .jpeg<br>添付画像数: 3個以下。<br>添付画像サイズ: 1枚あたり300KB以下。ただし、添付した画像の数が3枚の場合、合計800KB以下。<br>添付画像解像度: 1000*1000以下。 |


<span id="rcs"></span>

## RCS

<span id="rcs-sms"></span>

### SMS

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "SMS",
    "unsubscribePhoneNumber": "08012341234",
    "smsType": "STANDALONE",
    "cards": [
        {
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```


| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | 
| sender | Object | Y | 発信者 |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | チャットルームID |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | RCS内のメッセージタイプ、SMS、LMS、MMS、RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080受信拒否番号、送信目的が広告の場合は必須 |
| content.smsType | String | Y | SMSタイプ、メッセージタイプがSMSの場合必須、STANDALONE(スタンダード) |
| content.cards | Object Array | Y | カード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | Y | 内容 |
| content.cards[].buttons | Object Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(マップを表示する)、MAP_QUERY(マップを検索する)、MAP_SHARE(現在地を共有する)、URL(URをL接続する)、CALENDAR(予定を登録する) |
| content.cards[].buttons[].buttonJson | Object | Y | ボタンJson、ボタンタイプに合ったフォーマットを確認 |
| options | Object | N | 送信オプション |
| options.expiryOption | Integer | N | RCSメッセージ受信待機有効期限設定値(1: 1日、2: 40秒、3: 3分、4: 1時間) |
| options.groupId | String | N | RCS BizCenter統計連動のためのグループID |

<span id="free-form-message-request-body-rcs-lms-standalone"></span>

### LMSスタンダード

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "unsubscribePhoneNumber": "08012341234",
    "lmsType": "STANDALONE",
    "cards": [
        {
          "title":"[NHN Cloud]告知事項",
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| sender | Object | Y | 発信者 |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | チャットルームID |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | RCS内のメッセージタイプ、SMS、LMS、MMS、RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080受信拒否番号、送信目的が広告の場合は必須 |
| content.lmsType | String | Y | LMSタイプ、メッセージタイプがLMSの場合必須、STANDALONE(スタンダード)、FORMAT_BASIC(フォーマット基本型)、FORMAT_TITLE_HIGHLIGHT(フォーマットタイトル強調型)、FORMAT_PARAGRAPH(フォーマット段落型) |
| content.cards | Object Array | Y | カード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | Y | 内容 |
| content.cards[].buttons | Object Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(マップを表示する)、MAP_QUERY(マップを検索する)、MAP_SHARE(現在地を共有する)、URL(URをL接続する)、CALENDAR(予定を登録する) |
| content.cards[].buttons[].buttonJson | Object | Y | ボタンJson、ボタンタイプに合ったフォーマットを確認 |
| options | Object | N | 送信オプション |
| options.expiryOption | Integer | N | RCSメッセージ受信待機有効期限設定値(1: 1日、2: 40秒、3: 3分、4: 1時間) |
| options.groupId | String | N | RCS BizCenter統計連動のためのグループID |

<span id="free-form-message-request-body-rcs-lms-format-basic"></span>

### LMSフォーマット基本型及びフォーマットタイトル強調型
* mTitleMediaアイコンファイルIDリスト
  * プロモーション: LT-messagebase.common-jFBCKu
  * クーポン: LT-messagebase.common-LbshOv
  * イベント: LT-messagebase.common-aWdsJX
  * 予約: LT-messagebase.common-5eFcIF
  * 領収書: LT-messagebase.common-rJQ22U
  * 通知: LT-messagebase.common-j11Gtf

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "unsubscribePhoneNumber": "08012341234",
    "lmsType": "FORMAT_BASIC",
    "cards": [
        {
          "mTitle":"[NHN Cloud]告知事項",
          "mTitleMedia":"LT-messagebase.common-DdWk6s",
          "title":"告知1",
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | 
| sender | Object | Y | 発信者 |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | チャットルームID |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | RCS内のメッセージタイプ、SMS、LMS、MMS、RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080受信拒否番号、送信目的が広告の場合は必須 |
| content.lmsType | String | Y | LMSタイプ、メッセージタイプがLMSの場合必須、STANDALONE(スタンダード)、FORMAT_BASIC(フォーマット基本型)、FORMAT_TITLE_HIGHLIGHT(フォーマットタイトル強調型)、FORMAT_PARAGRAPH(フォーマット段落型) |
| content.cards | Object Array | Y | カード |
| content.cards[].mTitle | String | Y | メインタイトル |
| content.cards[].mTitleMedia | String | N | メインタイトルアイコン |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | Y | 内容 |
| content.cards[].buttons | Object Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(マップを表示する)、MAP_QUERY(マップを検索する)、MAP_SHARE(現在地を共有する)、URL(URをL接続する)、CALENDAR(予定を登録する) |
| content.cards[].buttons[].buttonJson | Object | Y | ボタンJson、ボタンタイプに合ったフォーマットを確認 |
| options | Object | N | 送信オプション |
| options.expiryOption | Integer | N | RCSメッセージ受信待機有効期限設定値(1: 1日、2: 40秒、3: 3分、4: 1時間) |
| options.groupId | String | N | RCS BizCenter統計連動のためのグループID |

### LMSフォーマット段落型タイプ
* mTitleMediaアイコンファイルIDリスト
  * プロモーション: LT-messagebase.common-jFBCKu
  * クーポン: LT-messagebase.common-LbshOv
  * イベント: LT-messagebase.common-aWdsJX
  * 予約: LT-messagebase.common-5eFcIF
  * 領収書: LT-messagebase.common-rJQ22U
  * 通知: LT-messagebase.common-j11Gtf

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "LMS",
    "unsubscribePhoneNumber": "08012341234",
    "lmsType": "FORMAT_PARAGRAPH",
    "cards": [
        {
          "mTitle":"[NHN Cloud]告知事項",
          "mTitleMedia":"LT-messagebase.common-DdWk6s",
          "title1":"告知1",
          "description1":"こんにちは。NHN Cloud Notification Hubです。",
          "title2":"告知2",
          "description2":"こんにちは。NHN Cloud Notification Hubです。",
          "title3":"告知3",
          "description3":"こんにちは。NHN Cloud Notification Hubです。",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "告知1ボタン"
                }
              }
            },
            {},
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "告知2ボタン"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "告知2ボタン"
                }
              }
            },
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "告知3ボタン"
                }
              }
            },
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | 
| sender | Object | Y | 発信者 |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | チャットルームID |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | RCS内のメッセージタイプ、SMS、LMS、MMS、RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080受信拒否番号、送信目的が広告の場合は必須 |
| content.lmsType | String | Y | LMSタイプ、メッセージタイプがLMSの場合必須、STANDALONE(スタンダード)、FORMAT_BASIC(フォーマット基本型)、FORMAT_TITLE_HIGHLIGHT(フォーマットタイトル強調型)、FORMAT_PARAGRAPH(フォーマット段落型) |
| content.cards | Object Array | Y | カード |
| content.cards[].mTitle | String | Y | メインタイトル |
| content.cards[].mTitleMedia | String | N | メインタイトルアイコン |
| content.cards[].title1 | String | N | タイトル(段落1) |
| content.cards[].description1 | String | Y | 内容(段落1) |
| content.cards[].title2 | String | N | タイトル(段落2) |
| content.cards[].description2 | String | Y | 内容(段落2) |
| content.cards[].title3 | String | N | タイトル(段落3) |
| content.cards[].description3 | String | Y | 内容(段落3) |
| content.cards[].buttons | Object Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(マップを表示する)、MAP_QUERY(マップを検索する)、MAP_SHARE(現在地を共有する)、URL(URをL接続する)、CALENDAR(予定を登録する) |
| content.cards[].buttons[].buttonJson | Object | Y | ボタンJson、ボタンタイプに合ったフォーマットを確認 |
| options | Object | N | 送信オプション |
| options.expiryOption | Integer | N | RCSメッセージ受信待機有効期限設定値(1: 1日、2: 40秒、3: 3分、4: 1時間) |
| options.groupId | String | N | RCS BizCenter統計連動のためのグループID |



### MMS横型、縦型

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "MMS",
    "unsubscribePhoneNumber": "08012341234",
    "mmsType": "HORIZONTAL",
    "cards": [
        {
          "title":"[NHN Cloud]告知事項",
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "attachmentId":"添付ファイルID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```


| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | 
| sender | Object | Y | 発信者 |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | チャットルームID |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | RCS内のメッセージタイプ、SMS、LMS、MMS、RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080受信拒否番号、送信目的が広告の場合は必須 |
| content.mmsType | String | Y | MMSタイプ、メッセージタイプがMMSの場合必須、HORIZONTAL(横型)、VERTICAL(縦型)、CAROUSEL_MEDIUM(カルーセル中)、CAROUSEL_SMALL(カルーセル小) |
| content.cards | Object Array | Y | カード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | Y | 内容 |
| content.cards[].attachmentId | String | Y | 添付ファイルID |
| content.cards[].buttons | Object Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(マップを表示する)、MAP_QUERY(マップを検索する)、MAP_SHARE(現在地を共有する)、URL(URをL接続する)、CALENDAR(予定を登録する) |
| content.cards[].buttons[].buttonJson | Object | Y | ボタンJson、ボタンタイプに合ったフォーマットを確認 |
| options | Object | N | 送信オプション |
| options.expiryOption | Integer | N | RCSメッセージ受信待機有効期限設定値(1: 1日、2: 40秒、3: 3分、4: 1時間) |
| options.groupId | String | N | RCS BizCenter統計連動のためのグループID |

### MMSカルーセル

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
          "contact": "01012345678",
          "clientReference": "クライアント_リファレンス"
        }
      ]
    }
  ],
  "content": {
    "messageType": "MMS",
    "unsubscribePhoneNumber": "08012341234",
    "mmsType": "CAROUSEL_MEDIUM",
    "cards": [
        {
          "title":"[NHN Cloud]告知事項",
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "attachmentId":"添付ファイルID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        },
        {
          "title":"[NHN Cloud]告知事項",
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "attachmentId":"添付ファイルID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        },
        {
          "title":"[NHN Cloud]告知事項",
          "description":"こんにちは。NHN Cloud Notification Hubです。",
          "attachmentId":"添付ファイルID",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : {
                "action": {
                  "urlAction": { "openUrl": { "url": "http://www.test.com" } },
                  "displayText": "Webサイトへ移動"
                }
              }
            }
          ]
        }
    ]
  },
  "options": {
    "expiryOption": 1,
    "groupId":"groupId"
  }
}
```


| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- | 
| sender | Object | Y | 発信者 |
| sender.brandId | String | Y | ブランドID |
| sender.chatbotId | String | Y | チャットルームID |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | RCS内のメッセージタイプ、SMS、LMS、MMS、RBC_TEMPLATE |
| content.unsubscribePhoneNumber | String | N | 080受信拒否番号、送信目的が広告の場合は必須 |
| content.mmsType | String | Y | MMSタイプ、メッセージタイプがMMSの場合必須、HORIZONTAL(横型)、VERTICAL(縦型)、CAROUSEL_MEDIUM(カルーセル中)、CAROUSEL_SMALL(カルーセル小) |
| content.cards | Object Array | Y | カード |
| content.cards[].title | String | N | タイトル |
| content.cards[].description | String | Y | 内容 |
| content.cards[].attachmentId | String | Y | 添付ファイルID |
| content.cards[].buttons | Object Array | N | ボタン |
| content.cards[].buttons[].buttonType | String | Y | ボタンタイプ<br>COMPOSE(チャットルームを開く)、CLIPBOARD(コピーする)、DIALER(電話をかける)、MAP_SHOW(マップを表示する)、MAP_QUERY(マップを検索する)、MAP_SHARE(現在地を共有する)、URL(URをL接続する)、CALENDAR(予定を登録する) |
| content.cards[].buttons[].buttonJson | Object | Y | ボタンJson、ボタンタイプに合ったフォーマットを確認 |
| options | Object | N | 送信オプション |
| options.expiryOption | Integer | N | RCSメッセージ受信待機有効期限設定値(1: 1日、2: 40秒、3: 3分、4: 1時間) |
| options.groupId | String | N | RCS BizCenter統計連動のためのグループID |


<span id="free-form-message-request-body-friendtalk-text"></span>

## カカともへのメッセージ

### テキスト型

* お知らせトークはテンプレート登録後、承認を受けた状態で送信できるため、テンプレート、フローメッセージの送信のみ可能です。
* お知らせトークの**sender**, **content**フィールドは **テンプレートメッセージ送信**の**リクエスト本文**をご確認ください。
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


| 名前 | タイプ | 必須 | 説明 |
| --- | --- |----|---------------------------------------------------------------|
| sender | Object | Y | 発信者 |
| sender.senderKey | Object | Y | 発信プロフィール_発信キー |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | メッセージタイプ |
| content.content | String | Y | 内容 |
| content.buttons | Object Array | N | ボタン |
| content.buttons[].type | String | Y | ボタンタイプ<br>WL(Webリンク)、AL(アプリリンク)、BK(Botキーワード)、MD(メッセージ伝達)、BF(ビジネスフォーム) |
| content.buttons[].name | String | Y | ボタン名 |
| content.buttons[].linkMo | String | N | リンクモバイル、ボタンタイプがWLの場合は必須 |
| content.buttons[].linkPc | String | N | リンクPC |
| content.buttons[].schemeIos | String | N | iOSアプリリンク |
| content.buttons[].schemeAndroid | String | N | Androidアプリリンク |
| content.buttons[].bizFormKey | String | N | ビズフォームキー、ボタンタイプがBFの場合は必須 |
| content.coupon | Object | N | クーポン |
| content.coupon.title | String | Y | タイトル。5つの形式に制限される<br>「${数字}KRW割引クーポン」数字は1以上99,999,999以下<br>「${数字}%割引クーポン」数字は1以上100以下<br>「送料割引クーポン」<br><br>「${7文字以内}無料クーポン」<br>「${7文字以内} UPクーポン」 |
| content.coupon.description | String | Y | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字) |
| content.coupon.linkMo | String | N | リンクモバイル |
| content.coupon.linkPc | String | N | リンクPC |
| content.coupon.schemeIos | String | N | iOSアプリリンク |
| content.coupon.schemeAndroid | String | N | Androidアプリリンク |

<span id="free-form-message-request-body-friendtalk-image"></span>

### 画像型 / ワイド画像型

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

| 名前 | タイプ | 必須 | 説明 |
| --- |---------------|----|---------------------------------------------------------------|
| sender | Object | Y | 発信者 |
| sender.senderKey | Object | Y | 発信プロフィール_発信キー |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | メッセージタイプ |
| content.content | String | Y | 内容 |
| content.attachmentId | String | Y | 添付ファイルID |
| content.imageLink | String | N | 画像リンク |
| content.buttons | Object Array | N | ボタン |
| content.buttons[].type | String | Y | ボタンタイプ<br>WL(Webリンク)、AL(アプリリンク)、BK(Botキーワード)、MD(メッセージ伝達)、BF(ビジネスフォーム) |
| content.buttons[].name | String | Y | ボタン名 |
| content.buttons[].linkMo | String | N | リンクモバイル、ボタンタイプがWLの場合は必須 |
| content.buttons[].linkPc | String | N | リンクPC |
| content.buttons[].schemeIos | String | N | iOSアプリリンク |
| content.buttons[].schemeAndroid | String | N | Androidアプリリンク |
| content.buttons[].bizFormKey | String | N | ビズフォームキー、ボタンタイプがBFの場合は必須 |
| content.coupon | Object | N | クーポン |
| content.coupon.title | String | Y | タイトル。5つの形式に制限される<br>「${数字}KRW割引クーポン」数字は1以上99,999,999以下<br>「${数字}%割引クーポン」数字は1以上100以下<br>「送料割引クーポン」<br><br>「${7文字以内}無料クーポン」<br>「${7文字以内} UPクーポン」 |
| content.coupon.description | String | Y | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字) |
| content.coupon.linkMo | String | N | リンクモバイル |
| content.coupon.linkPc | String | N | リンクPC |
| content.coupon.schemeIos | String | N | iOSアプリリンク |
| content.coupon.schemeAndroid | String | N | Androidアプリリンク |

<span id="free-form-message-request-body-friendtalk-wide-itemlist"></span>

### ワイドアイテムリスト型

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

| 名前 | タイプ | 必須 | 説明 |
|-----------------------------------|---------------|----|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | 発信者 |
| sender.senderKey | Object | Y | 発信プロフィール_発信キー |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | メッセージタイプ |
| content.buttons | Object Array | N | ボタン |
| content.buttons[].type | String | Y | ボタンタイプ<br>WL(Webリンク)、AL(アプリリンク)、BK(Botキーワード)、MD(メッセージ伝達)、BF(ビジネスフォーム) |
| content.buttons[].name | String | Y | ボタン名 |
| content.buttons[].linkMo | String | N | リンクモバイル、ボタンタイプがWLの場合は必須 |
| content.buttons[].linkPc | String | N | リンクPC |
| content.buttons[].schemeIos | String | N | iOSアプリリンク |
| content.buttons[].schemeAndroid | String | N | Androidアプリリンク |
| content.buttons[].bizFormKey | String | N | ビズフォームキー、ボタンタイプがBFの場合は必須 |
| content.header | String | Y | ヘッダ |
| content.item | Object | Y | ワイドアイテム |
| content.item.list | Object Array | Y | ワイドアイテムリスト(最小3個、最大4個) |
| content.item.list[].title | String | Y | アイテムタイトル(最初のアイテムの場合は最大25文字、2～4番目のアイテムの場合は最大30文字) |
| content.item.list[].attachmentId | String | Y | 添付ファイルID |
| content.item.list[].linkMo | String | Y | モバイルWebリンク |
| content.item.list[].linkPc | String | Y | PC Webリンク |
| content.item.list[].schemeIos | String | Y | iOSアプリリンク |
| content.item.list[].schemeAndroid | String | Y | Androidアプリリンク |
| content.coupon | Object | N | クーポン |
| content.coupon.title | String | Y | タイトル。5つの形式に制限される<br>「${数字}KRW割引クーポン」数字は1以上99,999,999以下<br>「${数字}%割引クーポン」数字は1以上100以下<br>「送料割引クーポン」<br><br>「${7文字以内}無料クーポン」<br>「${7文字以内} UPクーポン」 |
| content.coupon.description | String | Y | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字) |
| content.coupon.linkMo | String | N | リンクモバイル |
| content.coupon.linkPc | String | N | リンクPC |
| content.coupon.schemeIos | String | N | iOSアプリリンク |
| content.coupon.schemeAndroid | String | N | Androidアプリリンク |

<span id="free-form-message-request-body-friendtalk-carousel"></span>

### カルーセルフィード型

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

| 名前 | タイプ | 必須 | 説明 |
|------------------------------------------------------------|---------------|----|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| sender | Object | Y | 発信者 |
| sender.senderKey | Object | Y | 発信プロフィール_発信キー |
| content | Object | Y | メッセージ内容 |
| content.messageType | String | Y | メッセージタイプ |
| content.carousel | Object | Y | カルーセル |
| content.carousel.list | Object Array | Y | カルーセルリスト(最小2個、最大10個) |
| content.carousel.list[].header | String | Y | カルーセルアイテムタイトル(最大20文字)、カルーセルフィード型でのみ使用可能 |
| content.carousel.list[].message | String | Y | カルーセルアイテムメッセージ(最大180文字)、カルーセルフィード型でのみ使用可能 |
| content.carousel.list[].attachment | Object | N | カルーセルアイテム画像、ボタン情報 |
| content.carousel.list[].attachment.buttons | Object Array | N | ボタンリスト(最大2個) |
| content.carousel.list[].attachment.buttons[].type | String | Y | ボタンタイプ<br>WL(Webリンク)、AL(アプリリンク)、BK(Botキーワード)、MD(メッセージ伝達)、BF(ビジネスフォーム) |
| content.carousel.list[].attachment.buttons[].name | String | Y | ボタン名 |
| content.carousel.list[].attachment.buttons[].linkMo | String | N | リンクモバイル、ボタンタイプがWLの場合は必須 |
| content.carousel.list[].attachment.buttons[].linkPc | String | N | リンクPC |
| content.carousel.list[].attachment.buttons[].schemeIos | String | N | iOSアプリリンク |
| content.carousel.list[].attachment.buttons[].schemeAndroid | String | N | Androidアプリリンク |
| content.carousel.list[].attachment.image | Object | Y | カルーセル画像 |
| content.carousel.list[].attachment.image.attachmentId | String | Y | 添付ファイルid |
| content.carousel.list[].attachment.image.imageLink | String | N | 画像リンクURL |
| content.carousel.list[].attachment.coupon | Object | N | クーポン |
| content.carousel.list[].attachment.coupon.title | String | Y | タイトル。5つの形式に制限される<br>「${数字}KRW割引クーポン」数字は1以上99,999,999以下<br>「${数字}%割引クーポン」数字は1以上100以下<br>「送料割引クーポン」<br><br>「${7文字以内}無料クーポン」<br>「${7文字以内} UPクーポン」 |
| content.carousel.list[].attachment.coupon.description | String | Y | クーポン詳細説明(一般テキスト、画像型、カルーセルフィード型最大12文字 / ワイド画像型、ワイドアイテムリスト型最大18文字) |
| content.carousel.list[].attachment.coupon.linkMo | String | N | リンクモバイル |
| content.carousel.list[].attachment.coupon.linkPc | String | N | リンクPC |
| content.carousel.list[].attachment.coupon.schemeIos | String | N | iOSアプリリンク |
| content.carousel.list[].attachment.coupon.schemeAndroid | String | N | Androidアプリリンク |
| content.carousel.tail | Object | N | カルーセルさらに表示ボタン情報 |
| content.carousel.tail.linkMo | String | Y | モバイルWebリンク |
| content.carousel.tail.linkPc | String | N | モバイルWebリンク |
| content.carousel.tail.schemeIos | String | N | モバイルWebリンク |
| content.carousel.tail.schemeAndroid | String | N | モバイルWebリンク |

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
          "contactType": "EMAIL_ADDRESS",
          "contact": "recipient@example.com"
        }
      ]
    }
  ],
  "content": {
    "title": "[NHN Cloud Notification Hub]告知事項",
    "body": "こんにちは。NHN Cloud Notification Hubです。",
    "attachmentIds": [
      "添付_ファイル_ID"
    ]
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- |---------------| --- | --- |
| sender | Object | N | 発信者、プッシュ以外のメッセージチャンネルは必須 |
| sender.senderMailAddress | Object | N | 発信者メールアドレス |
| content | Object | Y | メッセージ内容 |
| content.title | Object | Y | タイトル |
| content.Object | Y | 内容 |
| content.attachmentIds | String Array | N | 添付ファイルID |

* 発信者メールアドレスのドメインは所有認証が完了している必要があります。
* 添付ファイルは30MB以下で最大10個までアップロードできます。
* 添付ファイルの合計が最大30MBを超えることはできません。
* 最大30MBまで添付可能ですが、受信するメールシステム(gmail.com, naver.comなど)の添付ファイル制限ポリシーにより、**制限超過**として拒否されたり、スパム判定率が高くなる可能性があるため、10MB以内で添付することを推奨します。
* **recipients[].contacts[].contactType**フィールドには**EMAIL_ADDRESS**のみ使用可能です。
* **recipients[].contacts[].contact** フィールドには受信者メールアドレスを入力します。

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
        "description" : "グループの説明"
      }
    },
    "customKey" : "customValue"
  }
}
```

| 名前 | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| content | Object | Y | メッセージ内容 |
| content.unsubscribePhoneNumber | String | N | プッシュメッセージ受信拒否のための代表番号 |
| content.unsubscribeGuide | String | N | プッシュメッセージ受信拒否のための案内 |
| content.title | String | Y | タイトル |
| content.body | String | Y | 内容 |
| content.style.useHtmlStyle | Boolean | Y | HTMLスタイル使用(Androidのみ可能) |
| content.richMessage | Object | N | リッチメッセージ使用時必要 |
| content.richMessage.buttons | Object Array | N | リッチメッセージに追加されるボタン。最大3個まで可能 |
| content.richMessage.buttons.name | String | N | ボタン名 |
| content.richMessage.buttons.buttonType | String | N | ボタンタイプ: REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS |
| content.richMessage.buttons.link | String | N | ボタンを押した時に接続されるリンク |
| content.richMessage.buttons.hint | String | N | ボタンに関するヒント |
| content.richMessage.media | Object | N | リッチメッセージに追加されるメディア |
| content.richMessage.media.source | String | N | メディアのアドレス(URL, LOCAL_RESOURCE可能) |
| content.richMessage.media.mediaType | String | N | メディアタイプ: IMAGE、GIF、VIDEO、AUDIO。AndroidはIMAGEのみサポート |
| content.richMessage.media.expandable | Boolean | N | Androidでメディアをクリックしたときに展開機能を使用するかどうか |
| content.richMessage.androidMedia | Object | N | Android端末専用メディア。media形式と同じ |
| content.richMessage.iosMedia | Object | N | iOS端末専用メディア。media形式と同じ |
| content.richMessage.largeIcon | Object | N | リッチメッセージに追加される大きなアイコン。Androidのみサポート |
| content.richMessage.largeIcon.source | String | Y | アイコンのアドレス |
| content.richMessage.group | Object | N | 複数のメッセージをグループ化する機能。Androidのみサポート |
| content.richMessage.group.key | String | Y | グループキー |
| content.richMessage.group.description | String | Y | グループの説明 |
| content.customKey | Object Array or String Array | N | ユーザー定義キーと値 |

* プッシュは**sender**フィールドが必要ありません。
* プッシュはユーザーが定義したキーと値を追加して**content**フィールドを作成できます。
* **recipients[].contacts[].contactType**フィールドは**TOKEN_FCM**, **TOKEN_APNS**, **TOKEN_ADM**, **TOKEN_APNS_SANDBOX**, **TOKEN_APNS_VOIP**, **TOKEN_APNS_VOIP_SANDBOX**のいずれかでなければなりません。
* **recipients[].contacts[].contact**フィールドには**プッシュトークン**を入力します。
