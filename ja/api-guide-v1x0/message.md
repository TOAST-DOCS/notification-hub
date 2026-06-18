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

## 自由形式メッセージ送信リクエスト - SMS

SMSに対する自由形式メッセージの送信をリクエストします。メッセージ内容をリクエスト本文に入力して送信をリクエストします。

各メッセージチャンネルでメッセージを送信するには、各メッセージチャンネルの発信情報が登録されている必要があります。発信情報の登録は **Notification Hub コンソール** > **発信情報タブ**で行えます。メッセージチャンネルの発信情報についての詳細は **Notification** > **Notification Hub** > **利用ポリシーおよび事前設定ガイド**で確認できます。


**リクエスト**

```
POST /message/v1.0/SMS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「このAPIはリクエスト本文を必要としません」と入力します。-->


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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信するかどうか |
| sender | Object | X |  |
| sender.senderPhoneNumber | String | O | 発信番号 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| content | Object | X |  |
| content.messageType | String | O | 送信メッセージタイプ（SMS、LMS、MMS）<br>[SMS（ショートメッセージ）、LMS（長文メッセージ）、MMS（マルチメディアメッセージ）] |
| content.title | String | X | メッセージタイトル |
| content.body | String | O | メッセージ本文 |
| content.attachmentIds | Array | X | 添付ファイル ID（最大 3 件） |

* メッセージチャンネルによって、**sender**、**content** フィールドは異なる形式を持ちます。
* メッセージチャンネルによって、**recipients[].contact.contactType**、**recipients[].contact.contact** フィールドに入力できる値が異なります。
* 予約送信の場合は **scheduledDateTime** を設定します。送信が開始される前の予約送信はリクエストのキャンセルが可能です。リクエストキャンセル API を呼び出すか、**Notification Hub コンソール** > **送信照会**でキャンセルできます。
* 承認後送信の場合は **confirmBeforeSend** を **true** に設定します。承認後送信のメッセージは、**Notification Hub コンソール** > **送信照会**で承認すると送信が進みます。
* 予約送信と承認後送信は同時に設定できません。

<a id="sender-fields-by-message-channel"></a>

### メッセージチャンネル別 sender フィールド

| メッセージチャンネル | フィールド | 説明 |
| --- | --- | --- |
| SMS | sender.senderPhoneNumber | 発信者番号 |
| RCS | sender.brandId | ブランド ID |
| RCS | sender.chatbotId | チャットルーム ID |
| EMAIL | sender.senderMailAddress | 発信者メールアドレス |
| ALIMTALK | sender.senderKey | 発信キー |
| ALIMTALK | sender.senderProfileType | 発信プロフィールタイプ<br>GROUP, NORMAL |

* お知らせトーク（ALIMTALK）は発信キー（senderKey）と発信プロフィールタイプ（senderProfileType）を必須で入力する必要があります。
* お知らせトーク（ALIMTALK）は送信時にテンプレートが必須です。自由形式メッセージ送信はサポートしていません。
* 発信プロフィールタイプは **GROUP（グループ）** と **NORMAL（一般）** があります。**GROUP** はグループ発信プロフィール、**NORMAL** は一般発信プロフィールです。


**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けると生成される値です。 |



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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0002BrandmessageFreeFormMessages"></span>

## 自由形式メッセージ送信リクエスト - ブランドメッセージ (BRANDMESSAGE)

ブランドメッセージ (BRANDMESSAGE) に対する自由形式メッセージ送信をリクエストします。

ブランドメッセージは KakaoTalk Bizmessage の友だちトークのアップグレード商品で、従来の友だちトークよりも多様なメッセージタイプをサポートします。
- TEXT: テキスト型
- IMAGE: イメージ型
- WIDE_IMAGE: ワイドイメージ型
- WIDE_ITEM_LIST: ワイドアイテムリスト型
- CAROUSEL_FEED: カルーセルフィード型
- CAROUSEL_COMMERCE: カルーセルコマース型
- COMMERCE: コマース型
- PREMIUM_VIDEO: プレミアムビデオ型

**リクエスト**

```
POST /message/v1.0/BRANDMESSAGE/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |

**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->

```
{
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
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
    "chatBubbleType" : "TEXT",
    "adult" : false,
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "buttons" : [ {
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "ヘッダー",
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "buttons" : [ {
          "type" : "WL",
          "name" : "ボタン名",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormKey" : "bizFormKey123",
          "chatExtra" : "extra_info",
          "chatEvent" : "event_name"
        } ],
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様限定",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様限定",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "価格情報"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| sender | Object | X |  |
| sender.senderKey | String | O | 発信キー（40文字）。グループ発信キーは使用不可 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに設定できるユーザー定義フィールドです |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定することはできません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成されるID |
| content | Object | X |  |
| content.chatBubbleType | String | X | メッセージ吹き出しタイプ。TEXT: テキスト型、IMAGE: イメージ型、WIDE: ワイドイメージ型、WIDE_ITEM_LIST: ワイドアイテムリスト型、CAROUSEL_FEED: カルーセルフィード型、CAROUSEL_COMMERCE: カルーセルコマース型、COMMERCE: コマース型、PREMIUM_VIDEO: プレミアムビデオ型<br>[TEXT, IMAGE, WIDE, WIDE_ITEM_LIST, CAROUSEL_FEED, CAROUSEL_COMMERCE, COMMERCE, PREMIUM_VIDEO] |
| content.adult | Boolean | X | 成人向けメッセージかどうか（default: false）。成人向け設定時は成人認証を完了した受信者にのみ表示<br>デフォルト値: false |
| content.content | String | X | メッセージ本文。TEXT: 必須（最大 1,300 文字、改行最大 99 個）、IMAGE: 必須（最大 1,300 文字）、WIDE: 必須（最大 76 文字、改行最大 5 個）、PREMIUM_VIDEO: 選択（最大 76 文字、改行最大 5 個）。WIDE_ITEM_LIST/CAROUSEL_FEED/CAROUSEL_COMMERCE: 使用不可。URL 入力可能 |
| content.attachmentId | String | X | 添付ファイルID。IMAGE/WIDE: attachmentId または image.imageUrl のいずれか必須 |
| content.image | Object | X |  |
| content.image.attachmentId | String | X | 添付ファイルID。imageUrl とどちらか一方を選択 |
| content.image.imageUrl | String | X | イメージ URL。attachmentId とどちらか一方を選択 |
| content.image.imageLink | String | X | イメージクリック時の遷移先 URL（http/https）。選択。未設定時は KakaoTalk イメージビューアーを使用 |
| content.video | Object | X |  |
| content.video.videoUrl | String | O | カカオTV 動画 URL（https://tv.kakao.com/ で始まる）。PREMIUM_VIDEO タイプ必須 |
| content.video.thumbnailAttachmentId | String | X | サムネイルイメージ添付ファイルID。thumbnailUrl とどちらか一方を選択。通常のイメージアップロード API で登録したイメージのみ使用可能 |
| content.video.thumbnailUrl | String | X | 動画サムネイルイメージ URL。thumbnailAttachmentId とどちらか一方を選択。通常のイメージアップロード API で登録したイメージのみ使用可能。未設定時はカカオTV デフォルトサムネイルを使用 |
| content.buttons | Array | X | メッセージボタンリスト。TEXT/IMAGE: 最大 5 個（クーポン適用時は最大 4 個）、WIDE/WIDE_ITEM_LIST: 最大 2 個、PREMIUM_VIDEO: 最大 1 個、COMMERCE: 必須（最小 1 個、最大 2 個）。CAROUSEL_FEED/CAROUSEL_COMMERCE: カルーセルアイテム内の attachment.buttons を使用 |
| content.buttons[].type | String | O | ボタンタイプ。WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク転換、BT: チャットボット転換、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, BK, MD, BC, BT, BF, AC] |
| content.buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大 14 文字、その他: 最大 8 文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申し込む」「応募する」のいずれかを選択 |
| content.buttons[].linkMo | String | X | モバイル Web リンク（http/https）。WL タイプ必須、AL タイプ選択（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| content.buttons[].linkPc | String | X | PC Web リンク（http/https）。WL/AL タイプ選択 |
| content.buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.buttons[].bizFormKey | String | X | ビジネスフォームキー。BF タイプ必須 |
| content.buttons[].chatExtra | String | X | BC（相談トーク転換）、BT（チャットボット転換）タイプボタンのメタ情報 |
| content.buttons[].chatEvent | String | X | BT（チャットボット転換）タイプボタンのボットイベント名 |
| content.header | String | X | メッセージタイトル。WIDE_ITEM_LIST: 必須（最大 20 文字）、PREMIUM_VIDEO: 選択（最大 20 文字）。その他のタイプ: 使用不可 |
| content.item | Object | X |  |
| content.item.list | Array | O | アイテムリスト。最小 3 個、最大 4 個 |
| content.item.list[].title | String | X | アイテムタイトル（改行最大 1 個）。1 番目のアイテム: 選択（最大 25 文字）、2〜4 番目のアイテム: 必須（最大 30 文字） |
| content.item.list[].image | Object | O |  |
| content.item.list[].image.attachmentId | String | X | 添付ファイルID。imageUrl とどちらか一方を選択 |
| content.item.list[].image.imageUrl | String | X | イメージ URL。attachmentId とどちらか一方を選択 |
| content.item.list[].linkMo | String | O | アイテムクリック時の遷移先モバイル Web リンク（http/https）。必須 |
| content.item.list[].linkPc | String | X | アイテムクリック時の遷移先 PC Web リンク（http/https）。選択 |
| content.item.list[].schemeIos | String | X | アイテムクリック時に起動する iOS アプリリンク。選択 |
| content.item.list[].schemeAndroid | String | X | アイテムクリック時に起動する Android アプリリンク。選択 |
| content.carousel | Object | X |  |
| content.carousel.head | Object | X |  |
| content.carousel.head.header | String | O | イントロヘッダー。head 使用時必須（最大 20 文字） |
| content.carousel.head.content | String | O | イントロ内容。head 使用時必須（最大 50 文字） |
| content.carousel.head.image | Object | O |  |
| content.carousel.head.image.attachmentId | String | X | 添付ファイルID。imageUrl とどちらか一方を選択 |
| content.carousel.head.image.imageUrl | String | X | イメージ URL。attachmentId とどちらか一方を選択 |
| content.carousel.head.linkMo | String | X | イントロクリック時の遷移先モバイル Web リンク。他のリンク（linkPc/schemeIos/schemeAndroid）を入力する場合は必須 |
| content.carousel.head.linkPc | String | X | イントロクリック時の遷移先 PC Web リンク。選択 |
| content.carousel.head.schemeIos | String | X | イントロクリック時に起動する iOS アプリリンク。選択 |
| content.carousel.head.schemeAndroid | String | X | イントロクリック時に起動する Android アプリリンク。選択 |
| content.carousel.list | Array | O | カルーセルアイテムリスト。head 使用時は 1〜5 個、未使用時は 2〜6 個 |
| content.carousel.list[].header | String | X | カルーセルアイテムタイトル。CAROUSEL_FEED: 必須（最大 20 文字）。CAROUSEL_COMMERCE: 使用不可 |
| content.carousel.list[].message | String | X | カルーセルアイテムメッセージ。CAROUSEL_FEED: 必須（最大 180 文字）。CAROUSEL_COMMERCE: 使用不可 |
| content.carousel.list[].additionalContent | String | X | 追加コンテンツ。CAROUSEL_COMMERCE: 選択（最大 34 文字）。CAROUSEL_FEED: 使用不可 |
| content.carousel.list[].buttons | Array | O | カルーセルアイテムボタン。最小 1 個、最大 2 個必須。AC ボタンは最後の位置 |
| content.carousel.list[].buttons[].type | String | O | ボタンタイプ。WL: Webリンク、AL: アプリリンク、BK: ボットキーワード、MD: メッセージ転送、BC: 相談トーク転換、BT: チャットボット転換、BF: ビジネスフォーム、AC: チャンネル追加<br>[WL, AL, BK, MD, BC, BT, BF, AC] |
| content.carousel.list[].buttons[].name | String | X | ボタン名。TEXT/IMAGE: 最大 14 文字、その他: 最大 8 文字。AC タイプ: 値なしで送信。BF タイプ: 「アンケートに参加する」「申し込む」「応募する」のいずれかを選択 |
| content.carousel.list[].buttons[].linkMo | String | X | モバイル Web リンク（http/https）。WL タイプ必須、AL タイプ選択（schemeIos/schemeAndroid のいずれかと併せて入力する場合に必要） |
| content.carousel.list[].buttons[].linkPc | String | X | PC Web リンク（http/https）。WL/AL タイプ選択 |
| content.carousel.list[].buttons[].schemeIos | String | X | iOS アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.carousel.list[].buttons[].schemeAndroid | String | X | Android アプリリンク。AL タイプ: linkMo、schemeAndroid、schemeIos のうち 2 つ以上必須 |
| content.carousel.list[].buttons[].bizFormKey | String | X | ビジネスフォームキー。BF タイプ必須 |
| content.carousel.list[].buttons[].chatExtra | String | X | BC（相談トーク転換）、BT（チャットボット転換）タイプボタンのメタ情報 |
| content.carousel.list[].buttons[].chatEvent | String | X | BT（チャットボット転換）タイプボタンのボットイベント名 |
| content.carousel.list[].image | Object | O |  |
| content.carousel.list[].image.attachmentId | String | X | 添付ファイルID。imageUrl とどちらか一方を選択 |
| content.carousel.list[].image.imageUrl | String | X | イメージ URL。attachmentId とどちらか一方を選択 |
| content.carousel.list[].image.imageLink | String | X | イメージクリック時の遷移先 URL（http/https）。選択。未設定時は KakaoTalk イメージビューアーを使用 |
| content.carousel.list[].commerce | Object | X |  |
| content.carousel.list[].commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| content.carousel.list[].commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| content.carousel.list[].commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。選択。使用時は discountRate または discountFixed のいずれか必須 |
| content.carousel.list[].commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice 存在時は discountFixed とどちらか一方を選択 |
| content.carousel.list[].commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice 存在時は discountRate とどちらか一方を選択 |
| content.carousel.list[].coupon | Object | X |  |
| content.carousel.list[].coupon.title | String | O | クーポンタイトル。必須。形式: 「{N}円割引クーポン」（N: 1〜99,999,999）、「{N}%割引クーポン」（N: 1〜100）、「送料割引クーポン」、「{商品名}無料クーポン」（商品名最大 7 文字）、「{商品名} UP クーポン」（商品名最大 7 文字）のいずれかを選択 |
| content.carousel.list[].coupon.description | String | O | クーポン詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大 12 文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大 18 文字 |
| content.carousel.list[].coupon.linkMo | String | X | クーポンクリック時の遷移先モバイル Web リンク（http/https）。チャンネルクーポン URL 以外の場合は必須 |
| content.carousel.list[].coupon.linkPc | String | X | クーポンクリック時の遷移先 PC Web リンク。選択 |
| content.carousel.list[].coupon.schemeIos | String | X | クーポンクリック時に起動する iOS アプリリンク。チャンネルクーポン URL（alimtalk=coupon://）使用時は schemeAndroid と合わせて 1 つ以上必須 |
| content.carousel.list[].coupon.schemeAndroid | String | X | クーポンクリック時に起動する Android アプリリンク。チャンネルクーポン URL（alimtalk=coupon://）使用時は schemeIos と合わせて 1 つ以上必須 |
| content.carousel.tail | Object | X |  |
| content.carousel.tail.linkMo | String | O | 「もっと見る」ボタンクリック時の遷移先モバイル Web リンク（http/https）。tail 使用時必須 |
| content.carousel.tail.linkPc | String | X | 「もっと見る」ボタンクリック時の遷移先 PC Web リンク。選択 |
| content.carousel.tail.schemeIos | String | X | 「もっと見る」ボタンクリック時に起動する iOS アプリリンク。選択 |
| content.carousel.tail.schemeAndroid | String | X | 「もっと見る」ボタンクリック時に起動する Android アプリリンク。選択 |
| content.commerce | Object | X |  |
| content.commerce.title | String | O | 商品タイトル（最大 30 文字）。必須 |
| content.commerce.regularPrice | Integer | O | 通常価格（0〜99,999,999）。必須 |
| content.commerce.discountPrice | Integer | X | 割引後価格（0〜99,999,999）。選択。使用時は discountRate または discountFixed のいずれか必須 |
| content.commerce.discountRate | Integer | X | 割引率（0〜100）。discountPrice 存在時は discountFixed とどちらか一方を選択 |
| content.commerce.discountFixed | Integer | X | 定額割引価格（0〜999,999）。discountPrice 存在時は discountRate とどちらか一方を選択 |
| content.coupon | Object | X |  |
| content.coupon.title | String | O | クーポンタイトル。必須。形式: 「{N}円割引クーポン」（N: 1〜99,999,999）、「{N}%割引クーポン」（N: 1〜100）、「送料割引クーポン」、「{商品名}無料クーポン」（商品名最大 7 文字）、「{商品名} UP クーポン」（商品名最大 7 文字）のいずれかを選択 |
| content.coupon.description | String | O | クーポン詳細説明。必須。TEXT/IMAGE/COMMERCE: 最大 12 文字、WIDE/WIDE_ITEM_LIST/PREMIUM_VIDEO: 最大 18 文字 |
| content.coupon.linkMo | String | X | クーポンクリック時の遷移先モバイル Web リンク（http/https）。チャンネルクーポン URL 以外の場合は必須 |
| content.coupon.linkPc | String | X | クーポンクリック時の遷移先 PC Web リンク。選択 |
| content.coupon.schemeIos | String | X | クーポンクリック時に実行する iOS アプリリンク。チャンネルクーポン URL（alimtalk=coupon://）使用時は schemeAndroid とともに 1 つ以上必須 |
| content.coupon.schemeAndroid | String | X | クーポンクリック時に実行する Android アプリリンク。チャンネルクーポン URL（alimtalk=coupon://）使用時は schemeIos とともに 1 つ以上必須 |
| content.additionalContent | String | X | 追加コンテンツ。COMMERCE タイプでのみ使用可（任意、最大 34 文字）。CAROUSEL_COMMERCE はカルーセルアイテム内の additionalContent を使用 |
| options | Object | X |  |
| options.audienceType | String | X | 送信対象タイプ。CUSTOMER: 顧客、FRIEND: 友だち<br>[CUSTOMER, FRIEND] |
| options.targeting | String | X | メッセージ対象タイプ。M: マーケティング受信同意ユーザー、N: 友だちでないマーケティング受信同意ユーザー、O: 友だちであるユーザー。M/N 使用時は発信プロフィールにマーケティング受信同意の有効化および 080 受信拒否番号が必要<br>[M, N, O] |
| options.pushAlarm | Boolean | X | メッセージプッシュ通知の送信有無（デフォルト: true）<br>デフォルト値: true |
| options.unsubscribePhoneNumber | String | X | 080 無料受信拒否電話番号。targeting が M/N の場合に必要。形式: 080-XXX-XXXX、080-XXXX-XXXX、080XXXXXXX、080XXXXXXXX。省略時は発信プロフィールに登録された値が自動適用 |
| options.unsubscribeAuthNumber | String | X | 受信拒否認証番号（数字、最大 9 文字）。必須ではありません。unsubscribePhoneNumber なしでの単独入力は不可。省略時は発信プロフィールに登録された値が自動適用 |
| statsKeyId | String | X | 統計キー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |

**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドについて説明します。-->

| 経路 | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け付けると生成される値です。 |

**リクエスト例**

<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http

### 自由形式メッセージ送信リクエスト - ブランドメッセージ(BRANDMESSAGE)

POST {{endpoint}}/message/v1.0/BRANDMESSAGE/free-form-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
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
    "chatBubbleType" : "TEXT",
    "adult" : false,
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "buttons" : [ {
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "ヘッダー",
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "buttons" : [ {
          "type" : "WL",
          "name" : "ボタン名",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormKey" : "bizFormKey123",
          "chatExtra" : "extra_info",
          "chatEvent" : "event_name"
        } ],
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様専用",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様専用",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "価格情報"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/BRANDMESSAGE/free-form-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
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
    "chatBubbleType" : "TEXT",
    "adult" : false,
    "content" : null,
    "attachmentId" : "20230131070811m2fDe1rXx80",
    "image" : {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    },
    "video" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    },
    "buttons" : [ {
      "type" : "WL",
      "name" : "ボタン名",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android",
      "bizFormKey" : "bizFormKey123",
      "chatExtra" : "extra_info",
      "chatEvent" : "event_name"
    } ],
    "header" : "ヘッダー",
    "item" : {
      "list" : [ {
        "title" : "アイテムタイトル",
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      } ]
    },
    "carousel" : {
      "head" : {
        "header" : "イントロヘッダー",
        "content" : null,
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg"
        },
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      },
      "list" : [ {
        "header" : "Carousel Header",
        "message" : "Carousel Message",
        "additionalContent" : "価格情報",
        "buttons" : [ {
          "type" : "WL",
          "name" : "ボタン名",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android",
          "bizFormKey" : "bizFormKey123",
          "chatExtra" : "extra_info",
          "chatEvent" : "event_name"
        } ],
        "image" : {
          "attachmentId" : "20230131070811m2fDe1rXx80",
          "imageUrl" : "https://example.com/image.jpg",
          "imageLink" : "https://www.example.com"
        },
        "commerce" : {
          "title" : "商品タイトル",
          "regularPrice" : 50000,
          "discountPrice" : 45000,
          "discountRate" : 10,
          "discountFixed" : 5000
        },
        "coupon" : {
          "title" : "5000円割引クーポン",
          "description" : "初回購入のお客様専用",
          "linkMo" : "https://m.example.com",
          "linkPc" : "https://www.example.com",
          "schemeIos" : "example://ios",
          "schemeAndroid" : "example://android"
        }
      } ],
      "tail" : {
        "linkMo" : "https://m.example.com",
        "linkPc" : "https://www.example.com",
        "schemeIos" : "example://ios",
        "schemeAndroid" : "example://android"
      }
    },
    "commerce" : {
      "title" : "商品タイトル",
      "regularPrice" : 50000,
      "discountPrice" : 45000,
      "discountRate" : 10,
      "discountFixed" : 5000
    },
    "coupon" : {
      "title" : "5000円割引クーポン",
      "description" : "初回購入のお客様専用",
      "linkMo" : "https://m.example.com",
      "linkPc" : "https://www.example.com",
      "schemeIos" : "example://ios",
      "schemeAndroid" : "example://android"
    },
    "additionalContent" : "価格情報"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}'
```

</details>

<span id="messageV1x0003EmailFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---email"></a>

## 自由形式メッセージ送信リクエスト - メール(EMAIL)

メール(EMAIL)に対する自由形式メッセージ送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/EMAIL/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "body" : "こんにちは。本日、お客様の商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信するかどうか |
| sender | Object | X |  |
| sender.senderMailAddress | String | O | 送信元メールアドレス |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| content | Object | X |  |
| content.title | String | O | テンプレートメールの件名 |
| content.body | String | O | テンプレートメールの本文 |
| content.attachmentIds | Array | X | テンプレート添付ファイル ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けると生成される値です。 |



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
    "body" : "こんにちは。本日、お客様の商品が入荷いたしました。",
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
    "title" : "[NHN Cloud Email][##env##] モニタリング通知",
    "body" : "こんにちは。本日、お客様の商品が入荷いたしました。",
    "attachmentIds" : [ "YaX2DA4Weab2", "YaX2DA4Weab1" ]
  }
}'
```

</details>

<span id="messageV1x0004RcsFreeFormMessages"></span>

<a id="request-to-send-a-free-form-message---rcs"></a>

## 自由形式メッセージ送信リクエスト - RCS

RCS に対する自由形式メッセージの送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/RCS/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様のご注文商品が入荷しました。ぜひご来店ください^^",
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
            "displayText" : "スケジュールを登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "スケジュールのタイトル",
                "description" : "スケジュールの説明"
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
          "displayText" : "スケジュールを登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "スケジュールのタイトル",
              "description" : "スケジュールの説明"
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

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信するかどうか |
| sender | Object | O |  |
| sender.brandId | String | O | ブランド ID |
| sender.chatbotId | String | O | トークルーム（チャットボット） ID |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに設定できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定することはできません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| content | Object | X |  |
| content.messageType | String | X | RCS 送信メッセージタイプ<br>[SMS（短文メッセージ）、LMS（長文メッセージ）、MMS（マルチメディアメッセージ）、RBC_TEMPLATE（RCS Biz Center テンプレート）] |
| content.title | String | X | （Deprecated、content.cards[].title を使用）メッセージタイトル |
| content.body | String | X | （Deprecated、content.cards[].description を使用）メッセージ本文 |
| content.smsType | String | X | SMS タイプ<br>[STANDALONE（独立型）、UNIFIED_STANDALONE（統合独立型）] |
| content.lmsType | String | X | LMS タイプ<br>[STANDALONE（独立型）、FORMAT_BASIC（基本形式）、FORMAT_TITLE_HIGHLIGHT（タイトル強調形式）、FORMAT_PARAGRAPH（段落形式）、UNIFIED_STANDALONE（統合独立型）] |
| content.mmsType | String | X | MMS タイプ（MMS 送信時は必須）<br>[HORIZONTAL（横型）、VERTICAL（縦型）、CAROUSEL_MEDIUM（カルーセル中型）、CAROUSEL_SMALL（カルーセル小型）、UNIFIED_HORIZONTAL（統合横型）、UNIFIED_VERTICAL（統合縦型）] |
| content.messagebaseId | String | X | RCS Biz Center テンプレート ID |
| content.unsubscribePhoneNumber | String | X | 受信拒否番号（広告送信時は必須） |
| content.cards | Array | X | RCS カード |
| content.cards[].title | String | X | タイトル |
| content.cards[].description | String | X | 本文 |
| content.cards[].attachmentId | String | X | 添付ファイル ID<br>※ 統合 MMS カードに GIF 画像を添付した場合、iOS 端末では受信できません。 |
| content.cards[].mTitle | String | X | メインタイトル |
| content.cards[].mTitleMedia | String | X | メインタイトルロゴファイル ID |
| content.cards[].title1 | String | X | タイトル 1 |
| content.cards[].title2 | String | X | タイトル 2 |
| content.cards[].title3 | String | X | タイトル 3 |
| content.cards[].description1 | String | X | 本文 1 |
| content.cards[].description2 | String | X | 本文 2 |
| content.cards[].description3 | String | X | 本文 3 |
| content.cards[].buttons | Array | X | RCS ボタンリスト |
| content.cards[].buttons[].buttonType | String | X | COMPOSE（トークルームを開く）、CLIPBOARD（コピーする）、DIALER（電話をかける）、MAP_SHOW（地図を表示する）、MAP_QUERY（地図を検索する）、MAP_SHARE（現在地を共有する）、URL（URL を開く）、CALENDAR（スケジュールを登録する）<br>※ 統合メッセージタイプに CLIPBOARD（コピーする）ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.cards[].buttons[].buttonJson | Object | X |  |
| content.cards[].buttons[].buttonJson.action | Object | X | ボタンアクション |
| content.buttons | Array | X | （Deprecated、content.cards[].buttons を使用）RCS ボタンリスト |
| content.buttons[].buttonType | String | X | COMPOSE（トークルームを開く）、CLIPBOARD（コピーする）、DIALER（電話をかける）、MAP_SHOW（地図を表示する）、MAP_QUERY（地図を検索する）、MAP_SHARE（現在地を共有する）、URL（URL を開く）、CALENDAR（スケジュールを登録する）<br>※ 統合メッセージタイプに CLIPBOARD（コピーする）ボタンを使用すると、iOS 端末では受信できません。<br><br>[COMPOSE, CLIPBOARD, DIALER, MAP_SHOW, MAP_QUERY, MAP_SHARE, URL, CALENDAR] |
| content.buttons[].buttonJson | Object | X |  |
| content.buttons[].buttonJson.action | Object | X | ボタンアクション |
| options | Object | X |  |
| options.expiryOption | Integer | X | 通信会社からデバイスへの送信試行時間（1: 1日、2: 40秒、3: 3分、4: 1時間）<br>デフォルト値: 1 |
| options.groupId | String | X | RCS Biz Center 統計連携のための group ID [ガイド](../console-guide/send-a-message/#RCS)（最大 20 Byte） |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
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
            "displayText" : "スケジュールを登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "スケジュールのタイトル",
                "description" : "スケジュールの説明"
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
          "displayText" : "スケジュールを登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "スケジュールのタイトル",
              "description" : "スケジュールの説明"
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
    "title" : "祝日営業時間のお知らせ",
    "body" : "こんにちは。本日、お客様の商品が入荷しました。ぜひご来店ください^^",
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
            "displayText" : "スケジュールを登録する",
            "calendarAction" : {
              "createCalendarEvent" : {
                "startTime" : "2024-01-01T00:00:00.000+09:00",
                "endTime" : "2024-01-01T00:00:00.000+09:00",
                "title" : "スケジュールのタイトル",
                "description" : "スケジュールの説明"
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
          "displayText" : "スケジュールを登録する",
          "calendarAction" : {
            "createCalendarEvent" : {
              "startTime" : "2024-01-01T00:00:00.000+09:00",
              "endTime" : "2024-01-01T00:00:00.000+09:00",
              "title" : "スケジュールのタイトル",
              "description" : "スケジュールの説明"
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

## 自由形式メッセージ送信リクエスト - PUSH

PUSH に対する自由形式メッセージ送信をリクエストします。


**リクエスト**

```
POST /message/v1.0/PUSH/free-form-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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
        "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Android でのみサポート",
        "description" : "グループに関する説明"
      }
    },
    "style" : {
      "useHtmlStyle" : true
    },
    "customKey" : "customValue"
  }
}
```

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信するかどうか |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| content | Object | X | プッシュメッセージの内容 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



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
        "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Android でのみサポート",
        "description" : "グループに関する説明"
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
        "buttonType" : "ボタンタイプ, REPLY, DEEP_LINK, OPEN_APP, OPEN_URL, DISMISS",
        "link" : "ボタンを押したときに遷移するリンク",
        "hint" : "ボタンに関するヒント"
      } ],
      "media" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "androidMedia" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "iosMedia" : {
        "sourceType" : "メディアの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE",
        "mediaType" : "メディアのタイプ, IMAGE, GIF, VEDIO, AUDIO。Android では IMAGE のみサポート",
        "extension" : "メディアファイルの拡張子, jpg, png",
        "expandable" : true
      },
      "largeIcon" : {
        "sourceType" : "大きいアイコンの場所, REMOTE, LOCAL",
        "source" : "メディアの場所のアドレス, URL, LOCAL_RESOURCE"
      },
      "group" : {
        "key" : "グループのキー、複数のメッセージをグループ単位でまとめる機能、Android でのみサポート",
        "description" : "グループに関する説明"
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

## テンプレートメッセージ送信リクエスト

登録したテンプレートを使用してメッセージを送信します。<br>
登録したテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
  <br>
  予約送信の場合は `scheduledDateTime` を設定します。<br>
  確認後発送の場合は `confirmBeforeSend` を true に設定します。<br>


**リクエスト**

```
POST /message/v1.0/{messageChannel}/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messageChannel | Path | Enum | O | メッセージチャンネルです。 |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| templateId | String | X | テンプレート ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信かどうか |
| templateParameters | Object | X | テンプレートパラメーターです。キー (Key、置換子) と値 (Value) のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー (Key、置換子) と値 (Value) のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けると生成される値です。 |



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

## お知らせトークテンプレートメッセージ送信

登録済みのテンプレートを使用してメッセージを送信します。<br>
登録済みのテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者（recipient）<br>
* 大量/グループ受信者（id）<br>
  <br>
  予約送信の場合は `scheduledDateTime` を設定します。<br>
  確認後送信の場合は `confirmBeforeSend` を true に設定します。<br>


**リクエスト**

```
POST /message/v1.0/ALIMTALK/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| sender | Object | X |  |
| sender.senderKey | String | O | 発信プロフィール発信キー |
| templateId | String | O | テンプレート ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信かどうか |
| templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されたテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



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

<span id="messageV1x0007BrandmessageTemplateMessages"></span>

## ブランドメッセージ テンプレートメッセージ送信

登録済みのテンプレートを使用してブランドメッセージを送信します。<br>
登録済みのテンプレートがない場合は、先にテンプレートを登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者（recipient）<br>
* 大量/グループ受信者（id）<br>
  <br>
  予約送信の場合は `scheduledDateTime` を設定します。<br>
  確認後送信の場合は `confirmBeforeSend` を true に設定します。<br>


**リクエスト**

```
POST /message/v1.0/BRANDMESSAGE/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


```
{
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
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
    },
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    }
  } ],
  "id" : "alpha123",
  "templateId" : "aA123456",
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| sender | Object | X |  |
| sender.senderKey | String | O | 発信キー（40文字）。グループ発信キーは使用不可 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| recipients[].imageParameters | Array | X | 受信者別の画像パラメーター。メッセージレベルの画像パラメーターをオーバーライドします。 |
| recipients[].imageParameters[].attachmentId | String | X | 添付ファイル ID。imageUrl とどちらか一方を選択 |
| recipients[].imageParameters[].imageUrl | String | X | 画像 URL。attachmentId とどちらか一方を選択 |
| recipients[].imageParameters[].imageLink | String | X | 画像クリック時に遷移する URL（http/https）。任意。未設定時は KakaoTalk 画像ビューアーを使用 |
| recipients[].videoParameter | Object | X |  |
| recipients[].videoParameter.videoUrl | String | O | カカオ TV 動画 URL（https://tv.kakao.com/ で始まる）。PREMIUM_VIDEO タイプで必須 |
| recipients[].videoParameter.thumbnailAttachmentId | String | X | サムネイル画像の添付ファイル ID。thumbnailUrl とどちらか一方を選択。通常の画像アップロード API で登録した画像のみ使用可能 |
| recipients[].videoParameter.thumbnailUrl | String | X | 動画サムネイル画像の URL。thumbnailAttachmentId とどちらか一方を選択。通常の画像アップロード API で登録した画像のみ使用可能。未設定時はカカオ TV のデフォルトサムネイルを使用 |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| templateId | String | X | テンプレート ID |
| templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では受信者別のテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| options | Object | X |  |
| options.audienceType | String | X | 送信対象タイプ。CUSTOMER: 顧客、FRIEND: 友だち<br>[CUSTOMER, FRIEND] |
| options.targeting | String | X | メッセージ対象タイプ。M: マーケティング受信同意ユーザー、N: 友だちでないマーケティング受信同意ユーザー、O: 友だちであるユーザー。M/N 使用時は発信プロフィールにマーケティング受信同意の有効化と 080 受信拒否番号が必要<br>[M, N, O] |
| options.pushAlarm | Boolean | X | メッセージプッシュ通知の送信有無（デフォルト: true）<br>デフォルト値: true |
| options.unsubscribePhoneNumber | String | X | 080 無料受信拒否電話番号。targeting が M/N の場合に必要。形式: 080-XXX-XXXX、080-XXXX-XXXX、080XXXXXXX、080XXXXXXXX。省略時は発信プロフィールに登録された値が自動適用 |
| options.unsubscribeAuthNumber | String | X | 受信拒否認証番号（数字、最大 9 文字）。必須ではありません。unsubscribePhoneNumber なしで単独入力不可。省略時は発信プロフィールに登録された値が自動適用 |
| statsKeyId | String | X | 統計キー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### ブランドメッセージ テンプレートメッセージ送信

POST {{endpoint}}/message/v1.0/BRANDMESSAGE/template-messages/{{messagePurpose}}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
{
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
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
    },
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    }
  } ],
  "id" : "alpha123",
  "templateId" : "aA123456",
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}
```
</details>

<details>
    <summary><strong>cURL</strong></summary>

```http
curl -X POST "${endpoint}/message/v1.0/BRANDMESSAGE/template-messages/${messagePurpose}" \
-H "X-NC-APP-KEY: {appKey}" \
-H "X-NHN-Authorization: Bearer {accessToken}" \
-d '{
  "sender" : {
    "senderKey" : "3f8a6b1c5d9e2f7a0b4c8d3e6f1a9b2c5d7e0f4a8b3c"
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
    },
    "imageParameters" : [ {
      "attachmentId" : "20230131070811m2fDe1rXx80",
      "imageUrl" : "https://example.com/image.jpg",
      "imageLink" : "https://www.example.com"
    } ],
    "videoParameter" : {
      "videoUrl" : "https://tv.kakao.com/v/123456789",
      "thumbnailAttachmentId" : "20230131070811m2fDe1rXx80",
      "thumbnailUrl" : "https://www.example.com/thumbnail.jpg"
    }
  } ],
  "id" : "alpha123",
  "templateId" : "aA123456",
  "templateParameters" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "options" : {
    "audienceType" : "CUSTOMER",
    "targeting" : "M",
    "pushAlarm" : true,
    "unsubscribePhoneNumber" : "0801111234",
    "unsubscribeAuthNumber" : "1234"
  },
  "statsKeyId" : "aA123456",
  "scheduledDateTime" : "2024-10-29T06:00:01.000+09:00",
  "confirmBeforeSend" : false
}'
```

</details>

<span id="messageV1x0008EmailTemplateMessages"></span>

<a id="send-email-template-message"></a>

## メールテンプレートメッセージ送信

登録済みのテンプレートを使用してメッセージを送信します。<br>
登録済みのテンプレートがない場合は、テンプレートを先に登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
  <br>
  予約送信の場合は `scheduledDateTime` を設定します。<br>
  確認後発送の場合は `confirmBeforeSend` を true に設定します。<br>


**リクエスト**

```
POST /message/v1.0/EMAIL/template-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「この API はリクエスト本文を要求しません」と入力します。-->


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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| templateId | String | X | テンプレート ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後発送かどうか |
| templateParameters | Object | X | テンプレートパラメーターです。キー (Key、置換子) と値 (Value) のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せず、連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー (Key、置換子) と値 (Value) のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### メールテンプレートメッセージ送信

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

## RCS テンプレートメッセージ送信

登録済みのテンプレートを使用してメッセージを送信します。<br>
登録済みのテンプレートがない場合は、先にテンプレートを登録してから送信します。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者（recipient）<br>
* 大量/グループ受信者（id）<br>
  <br>
  予約送信の場合は `scheduledDateTime` を設定します。<br>
  確認後発送の場合は `confirmBeforeSend` を true に設定します。<br>


**リクエスト**

```
POST /message/v1.0/RCS/template-messages/{messagePurpose}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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

<!--リクエスト本文のフィールドについて説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| sender | Object | X |  |
| sender.chatbotId | String | X | チャットルーム（チャットボット）ID |
| content | Object | X |  |
| content.unsubscribePhoneNumber | String | X | 受信拒否電話番号 |
| templateId | String | X | テンプレート ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信の有無 |
| templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| options | Object | X |  |
| options.expiryOption | Integer | X | 通信会社からデバイスへの送信を試みる時間（1: 1日、2: 40秒、3: 3分、4: 1時間）<br>デフォルト値: 1 |
| options.groupId | String | X | RCS Biz Center 統計連携用の group ID [ガイド](../console-guide/send-a-message/#RCS)（最大 20 Byte） |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドについて説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### RCS テンプレートメッセージ送信

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

## SMS テンプレート送信

登録済みのテンプレートを使用してメッセージを送信します。
登録済みのテンプレートがない場合は、先にテンプレートを登録してから送信します。

受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。
* 単件受信者(recipient)
* 大量/グループ受信者(id)

予約送信の場合は `scheduledDateTime` を設定します。
確認後発送の場合は `confirmBeforeSend` を true に設定します。

イメージレイアウトと連動した MMS テンプレートを送信する際は、次の点に注意してください。
* **必須テンプレートパラメーター**: cardNumber、scratchNumber を必ず含める必要があります。
  * cardNumber: バーコード生成に使用されます。必ず 16 桁の数字で構成する必要があります。
  * scratchNumber: 特別な制約条件はありません。
* **イメージレイアウト Override**: リクエスト本文に content.imageLayoutId または content.imageLayoutName を含めることで、テンプレートに設定されたイメージレイアウトを変更できます。
  * content.imageLayoutId と content.imageLayoutName はどちらか一方のみ使用する必要があります。
  * 両フィールドが含まれていない場合は、テンプレート作成時に連動したデフォルトのイメージレイアウトが使用されます。


**リクエスト**

```
POST /message/v1.0/SMS/template-messages/{messagePurpose}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を必要としない場合は「この API はリクエスト本文を必要としません」と入力します。-->


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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| templateId | String | X | テンプレート ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後発送かどうか |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| content | Object | X |  |
| content.imageLayoutId | String | X | イメージレイアウト ID |
| content.imageLayoutName | String | X | イメージレイアウト名 |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージのテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「この API はレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### SMS テンプレート送信

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

## フロー送信

登録したフローを使用してメッセージを送信します。<br>
フローを登録していない場合は、フローを登録してから送信する必要があります。<br>
<br>
受信対象の設定は、単件受信者、大量受信者、グループクエリのいずれかを選択して設定する必要があります。<br>
* 単件受信者(recipient)<br>
* 大量/グループ受信者(id)<br>
  <br>
  予約送信の場合は 'scheduledDateTime' を設定します。<br>
  確認後発送の場合は 'confirmBeforeSend' を true に設定します。<br>


**リクエスト**

```
POST /message/v1.0/flow-messages/{messagePurpose}
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {accessToken}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| X-NC-APP-KEY | Header | String | O | アプリキー |
| X-NHN-Authorization | Header | String | O | アクセストークン |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キー ID |
| flowId | String | X | フロー ID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後発送するかどうか |
| templateParameters | Object | X | テンプレートパラメーターです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | X |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー(Key、置換子)と値(Value)のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| id | String | X | 大量受信者リストおよびファイルアップロード成功時に生成される ID |
| flow | Object | X |  |
| flow.steps | Array | O |  |
| flow.steps[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| flow.steps[].sender | Object | X | 発信者情報です。発信者情報はメッセージチャンネルによって異なる構成になる場合があります。<br> |
| flow.steps[].content | Object | X | メッセージ内容です。メッセージ内容はメッセージチャンネルによって異なる構成になる場合があります。<br> |
| flow.steps[].options | Object | X | 送信オプションです。送信オプションはメッセージチャンネルによって異なる構成になる場合があります。<br> |
| flow.steps[].nextSteps | Array | X | 次のステップです。次のステップがない場合、メッセージ送信が終了します。<br> |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージ ID です。メッセージ送信リクエストを受け付けた際に生成される値です。 |



**リクエスト例**


<details>
    <summary><strong>IntelliJ HTTP</strong></summary>

```http
### フロー送信

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

## インスタントフローメッセージ送信

メッセージ送信リクエスト時にフローを定義してメッセージを送信リクエストします。<br>
<br>
インスタントフロー入力時は、テンプレートを利用して送信リクエストするか、直接発信者情報・内容を入力して送信リクエストできます。


**リクエスト**

```
POST /message/v1.0/instant-flow-messages/{messagePurpose}
```

**リクエストパラメーター**

| 名前 | 区分 | タイプ | 必須 | 説明 |
| - | - | - | - | - |
| messagePurpose | Path | Enum | O | メッセージ目的です。 |



**リクエスト本文**

<!--リクエスト本文を要求しない場合は「このAPIはリクエスト本文を要求しません」と入力します。-->


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

<!--リクエスト本文のフィールドを説明します。-->

| パス | タイプ | 必須 | 説明 |
| - | - | - | - |
| statsKeyId | String | X | 統計キーID |
| scheduledDateTime | String | X | 予約送信日時 |
| confirmBeforeSend | Boolean | X | 確認後送信するかどうか |
| templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| recipients | Array | O |  |
| recipients[].contacts | Array | O |  |
| recipients[].contacts[].contactType | String | O | 連絡先タイプ<br>[PHONE_NUMBER, EMAIL_ADDRESS, TOKEN_ADM, TOKEN_FCM, TOKEN_APNS, TOKEN_APNS_SANDBOX, TOKEN_APNS_SANDBOX_VOIP, TOKEN_APNS_VOIP] |
| recipients[].contacts[].contact | String | O | 連絡先です。受信者を指定せずに連絡先を直接入力してメッセージを送信できます。 |
| recipients[].contacts[].clientReference | String | X | 受信者ごとに付与できるユーザー定義フィールドです。 |
| recipients[].templateParameters | Object | X | テンプレートパラメーターです。キー（Key、置換子）と値（Value）のペアで構成されています。<br><br>グループ送信では、受信者ごとのテンプレートパラメーターを指定できません。<br><br>受信者に設定されるテンプレートパラメーターは、メッセージテンプレートパラメーターより優先されます。<br><br> |
| instantFlow | Object | O |  |
| instantFlow.steps | Array | O |  |
| instantFlow.steps[].messageChannel | String | O | メッセージチャンネル<br>[SMS(SMS), ALIMTALK(お知らせトーク), EMAIL(メール), RCS(RCS), PUSH(プッシュ)] |
| instantFlow.steps[].sender | Object | X | 発信者情報です。発信者情報はメッセージチャンネルによって異なる構成になる場合があります。<br> |
| instantFlow.steps[].content | Object | X | メッセージ内容です。メッセージ内容はメッセージチャンネルによって異なる構成になる場合があります。<br> |
| instantFlow.steps[].options | Object | X | 送信オプションです。送信オプションはメッセージチャンネルによって異なる構成になる場合があります。<br> |
| instantFlow.steps[].templateId | String | X | テンプレートIDです。テンプレートIDを設定した場合、リクエスト時に発信者情報（sender）とメッセージ内容（content）は適用されません。<br>インスタントフローメッセージでテンプレートIDを設定しない場合、発信者情報（sender）とメッセージ内容（content）が必須です。<br> |
| instantFlow.steps[].nextSteps | Array | X | 次のステップです。次のステップがない場合、メッセージ送信が終了します。<br> |



**レスポンス本文**

<!--レスポンス本文を返さない場合は「このAPIはレスポンス本文を返しません」と入力します。-->

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

<!--レスポンス本文のフィールドを説明します。-->

| パス | タイプ | Not Null | 説明 |
| - | - | - | - |
| header | Object | O |  |
| header.isSuccessful | Boolean | O | リクエストが成功したかどうかを示します。<br>デフォルト値: true |
| header.resultCode | Integer | O | リクエストの結果コードです。<br>デフォルト値: 0 |
| header.resultMessage | String | O | リクエストの結果メッセージです。<br>デフォルト値: SUCCESS |
| messageId | String | O | メッセージIDです。メッセージ送信リクエストを受け付けると生成される値です。 |



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
